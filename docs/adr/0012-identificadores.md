# Identificador interno próprio, com identificadores externos ancorados e resolvidos

O sistema emite **UUIDv7** para cada entidade que governa — Nome Científico, Conceito de Táxon, Hipótese de Espécie, Asserção, Evidência, Ocorrência — e mantém uma **tabela de resolução** de identificadores externos conhecidos apontando para ela. Nenhum vínculo interno depende de identificador emitido por terceiro.

## Reconciliação de espécimes

A chave **primária** de reconciliação não é o `occurrenceID`, e sim a tríplice `institutionCode` + `collectionCode` + `catalogNumber`: é o que os curadores usam e o que a literatura taxonômica cita desde o século XIX. O `occurrenceID` é chave **secundária** — na prática brasileira ele frequentemente não existe, é instável, ou é reemitido a cada republicação do IPT, e ancorar o vínculo nome→tipo nele significa vê-lo romper-se em silêncio na próxima sincronização ([ADR 0002](./0002-copia-materializada-de-ocorrencias.md)).

## Identificadores externos ancorados, nunca substituídos

| Identificador | Ancora |
|---|---|
| **ZooBank LSID** | Ato nomenclatural — é o registro oficial do ICZN |
| **DOI** | Publicação |
| **BIN / MOTU** | Agrupamento molecular ([ADR 0003](./0003-hierarquia-de-evidencia.md)) |
| **LC Project ID** | TK/BC Label ([ADR 0006](./0006-fair-care-aberto-por-padrao.md)) |
| **Chave GBIF** | Reconciliação de ocorrência |
| **`occurrenceID`** | Ocorrência (chave secundária) |

## Considered Options

- **Confiar no identificador da fonte**: rejeitado — quebra na primeira republicação do IPT.
- **Identificador derivado de conteúdo** (hash da tríplice): rejeitado — estável apenas enquanto o número de tombo não muda, e ele muda em fusões de coleção e recatalogação.

## Consequências

- A tabela de resolução é entidade de primeira classe, com proveniência: quando e por qual ingestão cada identificador externo passou a apontar para a entidade interna.
- Um espécime pode acumular vários identificadores externos ao longo do tempo sem perder identidade interna.
- Conflito de reconciliação — duas entidades internas reivindicando a mesma tríplice — é dado a resolver com o Gestor de Coleção, nunca fusão automática.
