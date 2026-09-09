# Cinco contêineres; as demais responsabilidades são componentes

O sistema se implanta como **cinco contêineres**:

| Contêiner | Responsabilidade |
|---|---|
| **Núcleo** | Motor Nomenclatural ([ADR 0005](./0005-camadas-nomenclatural-e-taxonomica.md)), Núcleo Taxonômico ([ADR 0004](./0004-autoridade-de-assercao.md), [0007](./0007-precedencia-da-revisao-taxonomica.md), [0008](./0008-competencia-por-grupo-taxonomico.md)), Motor de Evidência ([ADR 0003](./0003-hierarquia-de-evidencia.md), [0009](./0009-pertencimento-a-fauna-brasileira.md), [0016](./0016-fila-de-reconciliacao.md)) e geração das tabelas de publicação ([ADR 0017](./0017-ipt-como-sistema-externo.md)) como trabalho agendado |
| **Pipeline de Ingestão** | Download e processamento de Darwin Core Archive, reconciliação de identificadores, marcação de ausência, registro de execução ([ADR 0002](./0002-copia-materializada-de-ocorrencias.md), [0012](./0012-identificadores.md), [0014](./0014-licoes-do-pipeline-de-ingestao.md)) |
| **API Pública** | Acesso amplo, com asserções concorrentes e proveniência |
| **Aplicação Web** | Interfaces do Especialista de Grupo, do Gestor de Coleção, do Comitê e do público |
| **Banco PostgreSQL** | Núcleo relacional, `JSONB` e PostGIS ([ADR 0015](./0015-postgresql-unico-com-jsonb-e-postgis.md)) |

As responsabilidades internas do Núcleo são **componentes** (C4 nível 3), não contêineres.

## Considered Options

- **Oito contêineres**, um por responsabilidade: rejeitado. Contêiner, no C4, é o que roda separadamente — não o que tem fronteira conceitual. Num sistema de um banco só e um operador só, oito imagens implicam oito ciclos de vida e comunicação em rede onde bastava chamada de função. É microsserviço sem motivo.

## Consequências

- **A única separação com motivo operacional é a ingestão**: roda em lote por horas e não pode competir por recursos com o atendimento interativo. Por isso é contêiner, e o resto não é.
- Extrair um componente para contêiner próprio depois — o Motor de Evidência, se precisar escalar sozinho — é trabalho pequeno, desde que a fronteira do componente permaneça limpa. Manter oito contêineres desde já custaria todo dia até lá.
- Implantação em servidor doméstico (UNRAID) fica com quatro imagens além do PostgreSQL, e não oito.
