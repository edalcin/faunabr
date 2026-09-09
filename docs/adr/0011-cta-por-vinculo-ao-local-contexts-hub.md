# Conhecimento tradicional por vínculo ao Local Contexts Hub, sem modelagem própria

Esta arquitetura **não modela** conhecimento tradicional associado. Quando um registro tem CTA associado, ela guarda apenas o **vínculo**: o LC Project ID, resolvido contra a API do **Local Contexts Hub**, que é o registro canônico das Labels ([ADR 0006](./0006-fair-care-aberto-por-padrao.md)).

Nenhuma entidade de Relato, detentor individual ou consentimento é criada aqui. A autoridade cultural mora no Hub, com a Comunidade Detentora.

## A Arquitetura BioCultural fica fora do diagrama

A [Arquitetura BioCultural](https://github.com/edalcin/Arquitetura-BioCultural), do mesmo autor, modela CTA com profundidade — Regime Enunciativo, Fonte de Atribuição, Relato *versus* Evidência, contrato de harvest. Ela **não** entra como sistema externo desta arquitetura: acoplar dois protótipos de pesquisa cria dependência sem ganho, quando o Hub já é o registro canônico do que aqui interessa. O que se preserva é a **linguagem**: Comunidade Detentora, Label e Notice mantêm a definição do `CONTEXT.md` daquele repositório, para que os dois projetos não divirjam no vocabulário.

## Considered Options

- **Consumir Relatos da Arquitetura BioCultural pelo contrato de harvest**: rejeitado por criar dependência entre dois protótipos de pesquisa, sem que a fauna precise do conteúdo do Relato — precisa apenas saber que existe autoridade cultural sobre aquele registro, o que a Label já declara.
- **Esta arquitetura como Unidade Federada da BioCultural**: coerente, mas inverte a relação. O Comitê Federado daquela arquitetura existe para governar soberania de dados indígenas, e não tem por que decidir admissão de coleções zoológicas nem precedência de revisão taxonômica ([ADR 0007](./0007-precedencia-da-revisao-taxonomica.md), [ADR 0008](./0008-competencia-por-grupo-taxonomico.md)).
- **Modelar CTA aqui**: rejeitado — duplicaria o modelo, sem a autoridade para sustentá-lo.
- **Ignorar o tema**: rejeitado — o espécime coletado em território indígena existe, e omiti-lo não o torna neutro.

## Consequências

- Dependência externa única para CTA: o Local Contexts Hub. Indisponibilidade do Hub degrada a exibição da Label, e nunca a converte em ausência de restrição.
- O vocabulário de CTA desta arquitetura é **importado**, não autoral.
- Consentimento, revogação e ciclo de vida do CTA não são resolvidos aqui, e o sistema não finge resolvê-los.
