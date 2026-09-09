# PostgreSQL único, com JSONB no núcleo e PostGIS nas ocorrências

Supersede o [ADR 0013](./0013-armazenamento-sqlite-json-e-duckdb.md).

Um único motor: **PostgreSQL**. O núcleo nomenclatural e taxonômico é relacional, com a ficha descritiva da espécie em **`JSONB`** indexado por GIN. As ocorrências ficam em tabela **particionada**, com **PostGIS** para toda consulta espacial.

## Por que se afasta da diretriz "priorizar SQLite"

O `AGENTS.md` do autor admite alternativa quando há "necessidade real de alta concorrência de escrita e acesso multi-processo". É exatamente o caso: em SQLite há **um escritor por vez** no arquivo, e esta arquitetura tem dois regimes de escrita disputando o mesmo recurso — edição curatorial interativa de muitos taxonomistas simultâneos, e escrita em lote longa (reidentificação em massa do [ADR 0007](./0007-precedencia-da-revisao-taxonomica.md), recomputação do [ADR 0009](./0009-pertencimento-a-fauna-brasileira.md), marcação de ausência do [ADR 0014](./0014-licoes-do-pipeline-de-ingestao.md)). Com escritor único, um lote de trinta minutos trava todo mundo. O MVCC do PostgreSQL elimina o bloqueio mútuo.

Somam-se três limites do SQLite alheios a desempenho: ausência de papéis e permissões no servidor, exigidos pelo modelo de autoridade dos ADRs [0004](./0004-autoridade-de-assercao.md) e [0008](./0008-competencia-por-grupo-taxonomico.md); ausência de replicação e *point-in-time recovery*; e fragilidade de acesso multiprocesso sobre sistema de arquivos de rede.

## Considered Options

- **SQLite (WAL) no núcleo + DuckDB nas ocorrências**: rejeitado pelo escritor único, insustentável com escrita em lote longa concorrente com edição interativa.
- **PostgreSQL no núcleo + DuckDB nas ocorrências**: tecnicamente forte — varredura colunar em segundos em vez de minutos, e leitura direta de Parquet do GBIF. Rejeitado por preferência declarada por **um motor só**, e porque o PostGIS é maduro de outra ordem que a extensão espacial do DuckDB, com consulta espacial sendo requisito central (generalização de coordenada do [ADR 0006](./0006-fair-care-aberto-por-padrao.md), cruzamento com unidades de conservação).

## Consequências

- **A recomputação do grau de sustentação (ADR 0009) precisa ser incremental desde o início**, restrita ao que a ingestão tocou. Varredura completa recorrente sobre dezenas de milhões de linhas em armazenamento por linha é da ordem de dezenas de segundos a minutos `[ESTIMATIVA]` — tolerável, mas caro o bastante para desestimular execução frequente, e recomputação que se evita é recomputação que fica errada. O custo desta decisão é mais código e mais superfície de erro nesse ponto específico.
- **Ingestão de Parquet do GBIF exige etapa de conversão**, que a leitura nativa do DuckDB dispensaria.
- Duas imagens no UNRAID: a aplicação e `postgres` (variante Alpine). O arquivo de dados fica em volume externo ao container, conforme a diretriz de `DB_PATH`.
- A ficha descritiva do táxon — distribuição, nomes vernaculares, perfil, referências, tipos e espécimes — vive em `JSONB` com índice GIN, e não em tabelas por extensão Darwin Core. Permanecem relacionais, e nunca entram no JSON: nome, conceito, hipótese, asserção, proveniência, evidência e tabela de resolução de identificadores.
- Ocorrências em tabela particionada; a chave de particionamento é decisão de implementação, não desta ADR.
