# Revisão taxonômica prevalece sobre a identificação de acervo na Visão Curada

Quando um Especialista de Grupo reidentifica lotes cuja identificação de acervo diverge, a **Visão Curada exibe a reidentificação**. A identificação de acervo permanece integralmente no histórico da ocorrência, com autor, data e proveniência, e continua exposta pela API como asserção concorrente — nunca é apagada nem sobrescrita.

A precedência é da **asserção mais recente de especialista competente no grupo**, não da instituição custodiante. Isso vale porque o sistema é sistema de registro de pesquisa ([ADR 0001](./0001-sistema-de-registro-greenfield.md)) e não canal de publicação das coleções: a coleção não depende dele para publicar seu próprio acervo no GBIF ou no SiBBr, e portanto a precedência aqui não retira dela nenhum canal.

## Considered Options

- **Prevalecer a identificação de acervo**: rejeitado por fazer a Visão Curada envelhecer — revisões taxonômicas levariam anos para se refletir no catálogo, que é exatamente o descolamento que este projeto examina.
- **Coexistência declarada, sem vencedor** (exibir ambas, nomeadas por `secundum`): rejeitado por não entregar resposta única a gestor público e cidadão, que é função do catálogo nacional ([ADR 0004](./0004-autoridade-de-assercao.md)).

## Consequências

- **O princípio de soberania da coleção fica estreitado**: a coleção é titular do **dado do espécime** — número de tombo, evento de coleta, localidade, mídia, correção e retirada da cópia materializada — e **não** da identificação exibida na Visão Curada.
- A divergência entre identificação de acervo e revisão continua sendo dado publicado e consultável, e alimenta uma fila de reconciliação devolvida à coleção. É um produto do sistema, não um erro a suprimir.
- Exige registro da competência do especialista por grupo taxonômico: sem isso, "especialista competente" é indeterminado e a precedência vira precedência de quem escreveu por último.
- Exige que a API distinga, sem ambiguidade, identificação de acervo de identificação por revisão — um consumidor que queira reproduzir o acervo original precisa conseguir fazê-lo.
