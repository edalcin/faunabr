# Contribuição aberta com revisão por especialista, e visão curada como um conceito entre outros

Qualquer pesquisador identificado pode **propor** asserções taxonômicas e nomenclaturais; o especialista responsável pelo grupo taxonômico as **aprova, rejeita ou mantém pendentes**. Nada é descartado: propostas rejeitadas permanecem no histórico com proveniência completa (W3C PROV).

O sistema publica por padrão uma **visão curada** — o conjunto de asserções aprovadas, identificado como `secundum FaunaBR <data>` — que responde à pergunta "qual é o nome válido de X?". Essa visão é, no modelo de dados, **apenas um conceito de táxon entre outros**, sem privilégio ontológico. A API expõe simultaneamente todas as asserções concorrentes, permitindo a qualquer consumidor reconstruir visões alternativas.

## Considered Options

- **Curadoria fechada por grupo** (só credenciados escrevem, como no CTFB): rejeitado por congelar grupos sem especialista ativo e por não oferecer canal aos gestores de coleção, que são quem detecta divergências de identificação em massa.
- **Totalmente aberto, sem visão curada**: mais fiel à premissa de que espécie é hipótese e não há autoridade final, mas rejeitado por deixar gestor público e cidadão sem resposta a "qual o nome válido?" — o que anula o papel de catálogo nacional.

## Consequências

- Exige modelo de identidade de pesquisador e de atribuição de responsabilidade por grupo taxonômico.
- Exige fluxo de proposta/revisão como entidade de primeira classe, não como campo de status.
- A visão curada nunca pode ser materializada de forma que apague as asserções concorrentes.
