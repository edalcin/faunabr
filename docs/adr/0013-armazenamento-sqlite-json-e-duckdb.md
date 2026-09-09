---
status: superado pelo ADR 0015
---

> **Superado pelo [ADR 0015](./0015-postgresql-unico-com-jsonb-e-postgis.md).** A escrita concorrente real — muitos taxonomistas editando o núcleo enquanto rodam lotes longos — inviabiliza o escritor único do SQLite. Mantido pelo registro das alternativas avaliadas.

# Armazenamento: SQLite com JSON1 no núcleo, DuckDB nas ocorrências

Duas engines embutidas, sem servidor de banco, cada uma no problema que resolve:

| Arquivo | Conteúdo | Perfil |
|---|---|---|
| **SQLite** (JSON1) | Núcleo nomenclatural e taxonômico: nomes, conceitos, hipóteses, asserções, proveniência, designações, tabela de resolução de identificadores | Dezenas a centenas de milhares de linhas; escrita transacional frequente; leitura relacional |
| **DuckDB** | Cópia materializada das ocorrências ([ADR 0002](./0002-copia-materializada-de-ocorrencias.md)) | Dezenas de milhões de linhas; escrita em lote entre ingestões; varredura analítica repetida |

O DuckDB lê arquivos SQLite nativamente, o que viabiliza a junção **na direção que importa**: analítica sobre ocorrências enriquecida pelo núcleo. O caminho inverso não é simétrico e é evitado por desenho.

## Estrutura JSON no núcleo

Os dados descritivos da espécie — distribuição, nomes vernaculares, perfil, referências, tipos e espécimes, atributos vindos de extensões Darwin Core — são armazenados como **documento JSON por táxon**, consultado via JSON1, e não normalizados em tabelas por extensão. O padrão é o mesmo validado no [Biodiversidade.Online](https://github.com/biopinda/Biodiversidade-Online): extensões DwC-A mescladas no documento do táxon, evitando junção em N tabelas para montar uma ficha.

O que **permanece relacional**, e nunca entra no JSON: nome, conceito, hipótese, asserção, proveniência, evidência e tabela de resolução de identificadores. São o que se consulta transversalmente, o que carrega integridade referencial e o que a governança versiona.

## Considered Options

- **SQLite único**: rejeitado — o escritor único serializa reprocessamentos que se quer paralelos, e a recomputação de grau de sustentação ([ADR 0009](./0009-pertencimento-a-fauna-brasileira.md)) é varredura completa linha-a-linha sobre dezenas de milhões de registros.
- **PostgreSQL + PostGIS**: resolve volume, geoespacial e concorrência, mas traz servidor, backup, tuning e imagem grande para um problema que dois arquivos embutidos resolvem. Contraria a diretriz de simplicidade e de imagem mínima.
- **SQLite particionado por papel** (núcleo + ocorrências, ambos SQLite): mantém uma só tecnologia, mas continua pagando varredura linha-a-linha a cada recomputação.

## Consequências

- **Duas tecnologias de armazenamento.** É o custo aceito, e a fronteira entre elas precisa ser explícita no modelo, não implícita no código.
- O dump do GBIF em Parquet é lido diretamente pelo DuckDB, sem etapa de conversão.
- Consulta descritiva sobre a ficha da espécie usa JSON1; consulta sobre autoridade, proveniência ou identidade usa SQL relacional. Misturar os dois regimes no mesmo campo é o erro a evitar.
- Backup são arquivos, não *dumps*: coerente com a diretriz de `DB_PATH` externo ao container.
