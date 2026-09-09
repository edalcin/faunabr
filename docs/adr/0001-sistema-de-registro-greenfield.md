# Sistema de registro greenfield, não camada sobre o CTFB

O sistema é desenhado como **sistema de registro** (*system of record*) dos nomes e das hipóteses de espécie da fauna brasileira — a posição hoje ocupada pelo Catálogo Taxonômico da Fauna Brasileira (CTFB) — e não como uma camada de enriquecimento acoplada a ele.

A alternativa considerada e rejeitada foi tratar o CTFB como autoridade dos nomes e o novo sistema como camada de evidência. A rejeição é deliberada: **este é um projeto de pesquisa** (ver [`projetoPesquisa.md`](../projetoPesquisa.md)), cujo objeto é responder *"como seria o sistema ideal?"*. Ancorar o desenho no modelo de dados de um sistema em produção subordinaria a resposta às limitações que o exercício pretende examinar.

## Consequências

- **Nada aqui substitui sistema em produção.** Nenhum componente desta arquitetura é destinado a operar em produção ou a suceder o CTFB, o GBIF ou o SiBBr. Provas de conceito e MVPs derivados poderão ser planejados adiante, sempre como artefatos de pesquisa.
- O CTFB, o GBIF e o SiBBr aparecem na arquitetura como **sistemas externos de origem e destino de dados**, não como donos do modelo.
- A arquitetura tem liberdade para adotar `nome + secundum` (TCS 2) e hipóteses de espécie como entidades de primeira classe, sem retrocompatibilidade com esquemas legados.
