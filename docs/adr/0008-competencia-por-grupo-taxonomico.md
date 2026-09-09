# Competência designada por grupo, com evidência derivada como sinal e grupos órfãos declarados

A competência de um Especialista de Grupo é estabelecida por **designação** do Comitê, e não calculada. O sistema, porém, **deriva e exibe** a evidência de competência — autoria de atos nomenclaturais e de revisões no grupo, a partir de ZooBank e DOIs que ele já indexa — como insumo à designação e como alerta quando alguém sem produção no grupo assere sobre ele.

Grupos taxonômicos sem especialista designado são marcados explicitamente como **órfãos**. Neles, nenhuma asserção ganha precedência automática: voltam ao regime de coexistência declarada, com as identificações concorrentes exibidas lado a lado e nomeadas por `secundum`.

## Alinhamento com a prática existente

O modelo não é novo: o CTFB opera desde 2015 uma hierarquia de designação em três níveis — coordenador de grande grupo (Chordata; Invertebrados exceto Arthropoda; Hexapoda; Arthropoda exceto Hexapoda), subcoordenadores de táxons subordinados, e autores de táxons específicos — com mais de 800 especialistas, majoritariamente voluntários (BOEGER et al., 2024). A designação adotada aqui reproduz essa estrutura; a novidade é apenas tornar a **ausência** de designação um estado visível e mensurável.

## Considered Options

- **Competência derivada apenas do currículo publicado**: rejeitado por medir produção passada em vez de julgamento atual, excluir taxonomistas em início de carreira e favorecer volume de publicação.
- **Designação apenas, sem derivação nem marcação de órfãos**: rejeitado porque reproduz o gargalo do CTFB de forma invisível — grupo sem coordenador ficaria silenciosamente sob a regra de "quem asserou por último" ([ADR 0007](./0007-precedencia-da-revisao-taxonomica.md)).

## Consequências

- **A cobertura de especialistas passa a ser métrica publicada.** Quantos grupos da fauna brasileira não têm especialista ativo é pergunta hoje sem resposta; o sistema a responde como subproduto da governança. O impedimento taxonômico — perda de especialistas, reconhecido como risco central por BOEGER et al. (2024) — deixa de ser diagnóstico qualitativo e vira série temporal.
- Exige que o Comitê mantenha o registro de designação atualizado; designação vencida e não renovada converte o grupo em órfão, o que é o comportamento desejado.
- Exige indexação de ZooBank e DOIs por grupo taxonômico desde o início, não como recurso posterior.

## Referência

BOEGER, W. A. et al. Catálogo Taxonômico da Fauna do Brasil: Setting the baseline knowledge on the animal diversity in Brazil. **Zoologia**, v. 41, e24005, 2024. DOI: https://doi.org/10.1590/S1984-4689.v41.e24005
