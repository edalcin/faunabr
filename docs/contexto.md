# Proposta de arquitetura para um sistema de informações sobre a fauna brasileira

## Contexto

Estou querendo desenvolver aqui uma proposta de arquitetura para um sistema de informações sobre a fauna (reino Animalia) brasileira. Esta arquitetura deve ir além de um sistema taxonômico para listar nomes científicos para espécies, seus sinônimos e algumas características. Penso que o exercício acadêmico aqui é visualizar e propor uma arquitetura robusta, que envolva uma profunda integração entre os nomes das espécies e as evidências que suportam estes nomes, que são os exemplares (ocorrências) depositados em coleções científicas zoológicas e museus (veja as referências pertinentes sobre coleções científicas em @docs/). 

Hoje temos registros de exemplares em coleções disponíveis de forma aberta, tanto no https://www.gbif.org/ quanto no https://sibbr.gov.br/ porém estes registros não suportam diretamente o Catálogo Taxonômico da Fauna Brasileira (https://fauna.jbrj.gov.br/). Assim, esta arquitetura deve considerar que um sistema que suporta nomes científicos, regidos pelo "International Code of Zoological Nomenclature" (https://www.iczn.org/the-code/the-international-code-of-zoological-nomenclature/) deve ser baseado em evidências, que são os exemplares depositados em coleções científicas, seja como objetos físicos, seja como suas representações digitais ("digital life forms", em @"docs/referencias/Accelerating ocean species discovery and laying the foundations for the future of marine biodiversity research and monitoring.pdf").

Em essência, esta arquitetura deve propor um **sistema de informações baseado em evidências**, promovendo o avanço da ciência e do conhecimento sobre a fauna brasileira, provendo sua conservação e a conscientização do público em geral.

## Produtos esperados

Nesta fase, quero apenas visualizar a arquitetura de um sistema de informações robusto e completo sobre a fauna brasileira, para evoluir gradativamente. Esta visualização deve seguir os princípios da metodologia "C4 Model" (https://c4model.com/). Além dos diagramas, a documentação técnica descritiva deve ser gerada para que, futuramente, possa servir de subsídio para o desenvolvimento de ferramentas específicas que irão suportar a arquitetura.

No desenho da arquitetura, deve ser previsto a interação de diferentes atores, em seus diferentes contextos, como taxonomistas, gestores de coleções científicas e repositórios de dados, assim como gestores e formuladores de políticas públicas, e público em geral.

Gere um @README.md objetivo e didático (com diagramas básicos e de alto nível - contexto) voltado para taxonomistas e gestores de coleções. Toda a documentação mais técnica, para pessoal de sistemas, infraestrutura e TI, deve ficar em separado, mas linkado no @README.md.

Gere também um documento de **proposta de governança** (`docs/governanca.md`) cobrindo toda a arquitetura — não apenas o conhecimento tradicional associado. Taxonomistas e gestores de coleções científicas têm papel decisório tanto nas ferramentas associadas à arquitetura quanto na arquitetura em si, e esse papel precisa estar nomeado: quem decide o quê, com que processo, e o que acontece quando uma decisão muda.

## Diretrizes

Esta arquitetura deve prever contextos (C4 Model) onde taxonomistas irão interagir com os nomes das espécies, como no Catálogo Taxonômico da Fauna Brasileira, mas também, integrar profunda e robustamente estes nomes com as evidências de sua ocorrência no tempo e espaço, representados pelos registros de coleções. 

Como princípios, além de respeitar integralmente o "International Code of Zoological Nomenclature", deve respeitar também o padrão Darwin Core (https://github.com/tdwg/dwc) e os princípios F.A.I.R. e C.A.R.E..

A arquitetura deve prever o acesso amplo e irrestrito aos dados via API e tabelas específicas para serem mapeadas pelo IPT (https://github.com/gbif/ipt), para oferta de arquivos "Darwin Core Archive".

Fundamental que o desenho da arquitetura compreenda e represente o conceito de espécie biológica, definido em @docs/specieConcept.md 

### Governança

A governança desta arquitetura deve ser estruturada em **camadas com naturezas decisórias distintas**, seguindo o modelo já desenvolvido na [Arquitetura BioCultural](https://github.com/edalcin/Arquitetura-BioCultural) (`governanca/propostaGovernanca.md`), adaptado ao domínio faunístico:

- **Governança do conteúdo** — o que é nome válido, o que é hipótese de espécie sustentada, qual a identificação de um espécime, o que é conhecimento tradicional associado. Cada uma dessas quatro perguntas tem um titular **diferente**, e nenhum deles decide pelos outros.
- **Governança das ferramentas** — versão, implantação, disponibilidade, segurança de cada ferramenta que implementa a arquitetura. Decidida por quem opera a ferramenta.
- **Governança da arquitetura** — ADRs, modelo de dados, contratos de interoperabilidade, admissão de coleções e de repositórios. Decidida por corpo colegiado com representação de taxonomistas, gestores de coleções e repositórios de dados.

Princípios transversais às três camadas:

- **Soberania da coleção sobre o dado do espécime** — número de tombo, evento de coleta, localidade e mídia são da coleção que custodia o exemplar; a cópia materializada mantida pelo sistema é derivada, e corrigível ou retirável pela coleção de origem. A soberania **não** alcança a identificação exibida no catálogo: essa é da revisão taxonômica mais recente de especialista competente, com a identificação de acervo preservada como asserção concorrente.
- **Autoridade não uniforme** — parte do conteúdo não é decidida por ninguém: prioridade, homonímia e disponibilidade de nomes são **derivadas do Código**, não votadas. Governança que trate tudo como deliberação corrompe a nomenclatura.
- **Reversibilidade** — toda asserção é datada, assinada e reversível; nada é sobrescrito.
- **Habilitação, não subordinação** — a camada superior habilita a existência técnica da inferior, e nunca decide dentro dela.

A proposta de governança deve nomear explicitamente as lacunas em aberto, com responsável, em vez de descrever como existente o que ainda não existe.

Use neste projeto as skills:

- https://www.skills.sh/edalcin/biodiversitydataskills/darwin-core
- https://www.skills.sh/edalcin/biodiversitydataskills/iczn

Todos os documentos gerados devem ser em Markdown, com uso extensivo de diagramas em Mermaid.

Este documento será versionado e atualizado sempre que for necessário.
