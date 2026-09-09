# FaunaBR — Linguagem do projeto

Glossário do projeto de pesquisa de arquitetura para um sistema de informações sobre a fauna brasileira. Apenas glossário: decisões e mecanismos ficam em [`docs/adr/`](./docs/adr/).

## Language

### Espécie, nome e conceito

**Espécie**:
Linhagem metapopulacional que evolui separadamente (De Queiroz, 2007). Entidade evolutiva real, nunca diretamente observada — sempre inferida.
_Avoid_: Táxon, Nome científico, Registro de espécie

**Nome Científico**:
Rótulo disponível segundo o *International Code of Zoological Nomenclature*. Governa-se por prioridade, não por juízo. Não delimita nada por si.
_Avoid_: Espécie, Nome válido (é um estado do nome, não o nome), Binômio

**Conceito de Táxon**:
A circunscrição de um táxon segundo um autor determinado — `nome + secundum`. Muda a cada revisão taxonômica; duas circunscrições sob o mesmo nome são conceitos distintos.
_Avoid_: Táxon, Nome aceito, Registro taxonômico

**Hipótese de Espécie**:
Circunscrição de uma linhagem acompanhada da evidência que a sustenta. É testável e refutável, e existe com ou sem nome disponível — um BIN ou MOTU é hipótese de espécie sem nome.
_Avoid_: Espécie candidata, Táxon provisório, Morfoespécie

**Critério Operacional**:
Linha de evidência de que uma linhagem evolui separadamente — isolamento reprodutivo, monofilia, diagnosticabilidade, divergência de nicho. Nunca é definição de espécie.
_Avoid_: Conceito de espécie, Método de delimitação

**Ato Nomenclatural**:
Ato regido pelo Código que altera o estado de um nome: descrição original, designação de tipo, sinonimização objetiva, homonímia, emenda. Seu efeito é derivável por regra, exceto quando decorre de ato da Comissão.
_Avoid_: Mudança taxonômica, Revisão, Decisão nomenclatural

**Camada Nomenclatural**:
O conjunto de fatos verificáveis contra o Código. Validada por regra automatizada; não se deliberam prioridade, disponibilidade nem homonímia.
_Avoid_: Nomenclatura (o campo do saber), Camada de nomes

**Camada Taxonômica**:
O conjunto de juízos revisáveis sobre o que cada nome abrange. É onde vive a deliberação de especialista.
_Avoid_: Taxonomia (o campo do saber), Camada de conceitos

### Evidência

**Evidência**:
Todo registro que sustenta uma hipótese de espécie, com peso declarado segundo uma hierarquia de seis níveis (ADR 0003). Não é sinônimo de espécime: uma sequência e uma observação verificada também são evidência, com peso menor.
_Avoid_: Dado, Registro, Prova

**Espécime**:
O objeto físico depositado em coleção científica, com sua representação digital associada.
_Avoid_: Exemplar (uso corrente, mas ambíguo com "cópia"), Amostra, Voucher

**Espécime Portador do Nome**:
O espécime a que um nome está permanentemente ancorado — holótipo, lectótipo, neótipo (ICZN Art. 72–75). É a única ponte objetiva entre um nome e o mundo real.
_Avoid_: Tipo (isolado, é ambíguo), Espécime-tipo (inclui parátipos, que não portam o nome)

**Ocorrência**:
O registro Darwin Core de um espécime ou observação em um lugar e tempo determinados. Responde onde e quando, nunca o que é.
_Avoid_: Registro de coleta, Ponto de ocorrência, Observação (é uma das classes)

**Identificação**:
A aplicação de um Conceito de Táxon a uma Ocorrência, por alguém, em uma data. Versionada: nunca sobrescreve a anterior.
_Avoid_: Determinação, Nome do espécime, Classificação

**Táxon Obscuro**:
Hipótese de espécie que existe apenas como unidade molecular — BIN, MOTU, eDNA — sem nome disponível segundo o Código. Não é promovível a nome sem publicação.
_Avoid_: Dark taxon (usar a forma portuguesa), Espécie não descrita, OTU

**Espécie Crítica**:
Linhagem separada cuja disparidade fenotípica é anomalamente baixa em relação à sua divergência genética e ao seu tempo de divergência (Struck et al., 2018). Não é espécie mal descrita.
_Avoid_: Espécie críptica (calco), Complexo de espécies

### Governança

**Asserção**:
Toda afirmação registrada no sistema com autor, data, fundamento e proveniência. A unidade de governança do conteúdo: nada entra como fato anônimo.
_Avoid_: Registro, Fato, Dado curado

**Visão Curada**:
O conjunto de asserções aprovadas que o sistema publica por padrão, identificado como um conceito entre outros (`secundum FaunaBR <data>`). Sem privilégio ontológico sobre as asserções concorrentes.
_Avoid_: Verdade, Nome válido do sistema, Backbone

**Especialista de Grupo**:
Quem detém autoridade designada de revisão sobre as asserções taxonômicas de um grupo taxonômico determinado. Sua asserção mais recente prevalece na Visão Curada; não decide nomenclatura, que é derivada do Código.
_Avoid_: Curador (é o da coleção), Revisor, Autoridade taxonômica

**Grupo Órfão**:
Grupo taxonômico sem Especialista de Grupo designado. Nele nenhuma asserção tem precedência, e as identificações concorrentes coexistem nomeadas por `secundum`. É estado declarado e mensurável, nunca silencioso.
_Avoid_: Grupo sem curador, Lacuna taxonômica, Grupo vago

**Gestor de Coleção**:
Quem responde pelo acervo de uma coleção científica e por seus registros de ocorrência. Titular do dado do espécime — tombo, evento, localidade, mídia — mas não da identificação exibida na Visão Curada.
_Avoid_: Curador de coleção (uso corrente, mas colide com Especialista de Grupo), Instituição

**Comunidade Detentora**:
Grupo humano culturalmente diferenciado, autoidentificado, titular coletivo do conhecimento tradicional associado a um táxon ou a um território. Autoridade final sobre suas TK/BC Labels, sem revisão por nenhuma outra instância.
_Avoid_: Comunidade local, População tradicional, Fonte

**Label**:
Rótulo de autoridade cultural aplicado **pela Comunidade Detentora** via Local Contexts Hub — TK ou BC. Expressa direito cultural, não direito autoral, e seu texto é customizável pela comunidade.
_Avoid_: Tag, Rótulo de acesso, Licença

**Notice**:
Declaração aplicada **pela instituição ou pesquisador** que reconhece a existência de direitos indígenas sobre um acervo ou registro — Engagement, Disclosure ou Collections Care. Funciona como marcador provisório até que a comunidade aplique sua Label.
_Avoid_: Aviso, Disclaimer, Label (são coisas distintas e não intercambiáveis)

## Referências

- [`docs/specieConcept.md`](./docs/specieConcept.md) — o conceito de espécie adotado e suas consequências para o modelo
- [`docs/adr/`](./docs/adr/) — decisões arquiteturais, com alternativas rejeitadas
- [`docs/contexto.md`](./docs/contexto.md) — requisitos e diretrizes do projeto de pesquisa
