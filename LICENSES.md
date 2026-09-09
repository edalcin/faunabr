# Licenciamento

Este repositório usa **três regimes distintos**, conforme o [ADR 0019](./docs/adr/0019-licenciamento-em-tres-regimes.md). Tratar código, documentação e dados sob uma licença única é o erro que produz, ao mesmo tempo, exposição jurídica e imobilismo.

| Camada | Licença | Onde se aplica |
|---|---|---|
| **Código** | [Apache License 2.0](./LICENSE) | Todo código-fonte deste repositório |
| **Documentação** | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) | `README.md`, `CONTEXT.md`, tudo em `docs/`, incluindo os ADRs |
| **Dados** | CC BY 4.0 | Dados publicados via API e via tabelas de publicação, alinhado ao CTFB e ao GBIF |
| **Dados com TK/BC Label** | **Fora de licença aberta** | Registros sob autoridade cultural de Comunidade Detentora |

## Por que Apache-2.0 no código

Cláusula expressa de concessão e retaliação de patentes, relevante em um domínio com histórico documentado de apropriação de conhecimento associado à biodiversidade brasileira. O custo sobre a MIT é zero.

## A exceção que importa

Registro com **TK ou BC Label** não recebe licença aberta. Uma licença Creative Commons é juridicamente **irrevogável**; o [ADR 0006](./docs/adr/0006-fair-care-aberto-por-padrao.md) dá à Comunidade Detentora autoridade final e **revisável** sobre suas Labels, inclusive para restringir depois de ter permitido. Um `CC BY` sobre esse registro anularia na prática essa autoridade.

Operacionalmente: no Darwin Core Archive publicado, esse registro sai com o **LC Project ID no campo `rights`**, e não com uma licença Creative Commons.

## Licença por registro, nunca por conjunto

Toda saída de dados — API e tabelas de publicação para o IPT — emite a licença aplicável **a cada registro**. Não existe licença global do conjunto.

## Referências das obras citadas

O conteúdo de terceiros referenciado em `docs/referencias/` mantém a licença de origem e não é redistribuído sob os regimes acima.
