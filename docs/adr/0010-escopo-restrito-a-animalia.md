# Escopo estritamente Animalia, com o ICZN embutido no núcleo

A arquitetura é desenhada para o reino Animalia. O *International Code of Zoological Nomenclature* não é isolado atrás de fronteira plugável: é premissa do núcleo, e o modelo pode assumi-lo em qualquer ponto — tipificação por espécime portador do nome, prioridade por data de publicação, homonímia, atos da Comissão.

## Considered Options

- **Núcleo agnóstico de reino, camada nomenclatural plugável** (com implementação ICZN única e espaço futuro para o ICN): rejeitado. O escopo declarado do projeto é a fauna brasileira, e desenhar a fronteira para um segundo Código que ninguém pediu é abstração especulativa — o custo aparece hoje, na indireção do modelo, e o benefício depende de um Catálogo da Vida do Brasil que não é interlocutor deste projeto.
- **Catálogo da Vida do Brasil completo** (fauna, flora e funga, microrganismos, fósseis): fora do escopo e sem interlocutor.

## Consequências

- O modelo pode usar vocabulário e regras zoológicas diretamente, sem camada de tradução: `nomenclaturalCode` é constante, não campo de decisão.
- **Generalizar para outros reinos exigirá refatoração do núcleo**, e isso é aceito. O Código botânico difere em pontos estruturais — tipificação, prioridade, nomes de híbridos, registro obrigatório — e essas diferenças não são acomodáveis por configuração.
- A integração com o futuro Catálogo da Vida do Brasil (BOEGER et al., 2024) seria por interoperabilidade entre catálogos, nunca por unificação de modelo.
