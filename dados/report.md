# Relatório — extração do MER a partir do dump do Catálogo Taxonômico da Fauna

## Método

`pg_restore` não está disponível nesta máquina e o arquivo é um dump PostgreSQL em formato *custom* v1.16 (banco `fauna`, servidor 15.1, gerado por `pg_dump` 18.6). O DDL foi extraído diretamente do TOC do arquivo (primeiros 30 MB, onde as definições ficam em texto claro), parseando `CREATE TABLE` e `ALTER TABLE ... ADD CONSTRAINT`.

Fonte: `dados/backup_fauna_2026_09_09.dump` (907 MB, não versionado).

## Números extraídos

| Item | Quantidade |
|---|---|
| Tabelas | 94 |
| Colunas | 758 |
| Chaves estrangeiras | 98 |
| Chaves primárias | 65 |
| Restrições UNIQUE | 34 |
| Views e materialized views | 29 |
| Schemas | 5 (`public`, `carga`, `historico`, `postgrest`, `ipt_fauna`) |

## Conteúdo de `modeloERctf.md`

- Flowchart de visão geral dos domínios.
- 5 diagramas `erDiagram`: Núcleo taxonômico, Distribuição, Atributos biológicos/hospedeiros, Referências/vouchers/mídia, Usuários/editorial. Cada FK aparece em exatamente um diagrama (no domínio da tabela filha), com as tabelas-pai de outros domínios representadas como entidades vazias — cobertura verificada de 98/98 FKs, sem duplicação.
- Cardinalidade derivada do DDL: `NOT NULL` define o lado obrigatório; FK com restrição `UNIQUE` indica relação 1:1 (ex.: `figura ||--o| figura_lista`, `dados_lista_brasil |o--o| primario`).
- Schemas auxiliares (sem FK), lista de views/matviews e 45 domínios de valor extraídos das restrições `CHECK` (rank taxonômico, UF, bacias hidrográficas, regiões marinhas, formas de vida etc.).
- Dicionário de dados completo: as 94 tabelas com tipo, nulidade, valor padrão e referência por coluna.

## Verificação

Os 6 blocos Mermaid do documento passam em `mermaid.parse()` (mermaid 12.0.0, executado via Bun com jsdom): `6 blocos, 0 falhas`.

## Achados estruturais

- `taxon_base` é auto-relacionada duas vezes: `parent_fk` (hierarquia taxonômica) e `variante_ortografica_r_s_fk`.
- `lista ↔ taxonomic_tree` e `dados_lista_brasil ↔ distribuicao`/`grupo` formam pares de FK recíprocas — ciclos herdados do mapeamento Hibernate (toda tabela de entidade tem `id bigint` sintético e `hibernate_version`).
- 18 tabelas do schema `public` são associativas puras (N:N), sem PK declarada.
- Os schemas `carga` e `historico` não possuem nenhuma chave estrangeira: a ligação com `public` é feita em código de aplicação.

## Fora de escopo

- Contagem de linhas por tabela — exigiria restaurar os 907 MB de dados.
- Diagramas para `carga` e `historico` — sem FK, ficaram como listas de tabelas.
