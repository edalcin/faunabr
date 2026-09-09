# IPT como sistema externo; o sistema expõe tabelas de publicação

O Integrated Publishing Toolkit (IPT) fica **fora** da fronteira da arquitetura. A responsabilidade do sistema termina em manter **tabelas de publicação** — Taxon core e extensões Darwin Core — em formato diretamente mapeável pelo IPT. Quem instala e opera o IPT é a instituição publicadora.

A geração e manutenção dessas tabelas é contêiner **interno**, e é o contrato verificável desta fronteira.

## Considered Options

- **IPT como contêiner interno**, empacotado e operado junto com o resto, entregando o Darwin Core Archive pronto: rejeitado por três razões — é produto de terceiro com ciclo de vida próprio (Java sobre Tomcat, imagem grande) e embuti-lo amarraria a arquitetura à evolução dele; a instituição publicadora tipicamente já opera um IPT com outros recursos, e impor um segundo é atrito puro; e a fronteira fica menos honesta, trocando um contrato verificável por uma dependência operacional.

## Consequências

- As tabelas de publicação são artefato de primeira classe, versionado e testável contra o `meta.xml` esperado pelo IPT.
- Mudança de versão do IPT não é mudança desta arquitetura, desde que o formato das tabelas permaneça válido.
- A publicação efetiva — periodicidade, licença declarada no EML, registro no GBIF — é decisão da instituição publicadora, não do sistema.
- Os termos de restrição exigidos pelo [ADR 0006](./0006-fair-care-aberto-por-padrao.md) (`informationWithheld`, `dataGeneralizations`, `accessRights`, LC Project ID em `rights`) precisam ser materializados **nas tabelas de publicação**, não aplicados depois pelo IPT.
