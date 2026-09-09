# Camada nomenclatural validada por regra, separada da camada taxonômica revisável

O sistema separa duas camadas com regimes de verdade distintos:

- **Camada nomenclatural** — fatos verificáveis contra o *International Code of Zoological Nomenclature*: data e forma de publicação, disponibilidade do nome, tipificação, homonímia, prioridade, grafias. É validada por **regras automatizadas**; um ato nomenclaturalmente inválido é rejeitado pelo motor, não submetido a juízo de especialista. Alterações aqui são correções de fato, não mudanças de opinião.
- **Camada taxonômica** — o que um nome abrange, segundo quem (`nome + secundum`). É o domínio do juízo científico revisável, sujeito ao fluxo de proposta e revisão do [ADR 0004](./0004-autoridade-de-assercao.md).

## Escape obrigatório: atos da Comissão

Decisões tomadas pela Comissão Internacional de Nomenclatura Zoológica sob *plenary power* — nomes conservados, `nomen protectum` sobre `nomen oblitum`, Listas Oficiais, supressão de nomes — **não são deriváveis por regra**. Entram como *override* explícito na camada nomenclatural, com citação obrigatória do ato da Comissão (Opinion / Declaration no *Bulletin of Zoological Nomenclature*). Sem esse escape, a validação automática falharia justamente nos casos mais visíveis da nomenclatura zoológica.

## Considered Options

- **Camada única, tudo revisável**: rejeitado por permitir o registro de estados nomenclaturalmente inválidos e por descartar a validação automática do Código.
- **Validação apenas advisória** (sinaliza, não bloqueia): rejeitado porque converte um fato derivável em opinião, e a deriva acumulada seria indistinguível de erro de curadoria.

## Consequências

- Prioridade e homonímia passam a ser **derivadas**, não digitadas — o principal ganho técnico do sistema sobre um catálogo de nomes convencional.
- Exige que dados de publicação e tipificação sejam completos o suficiente para alimentar as regras; registros incompletos ficam explicitamente marcados como não validáveis.
- Exige registro estruturado de atos da Comissão como fonte de *override*.
