# Próximos Passos — estado do projeto e pendências

> **Arquivo de referência único do projeto.** Registra onde o projeto está e o que falta fazer. É o ponto de entrada obrigatório de qualquer nova sessão de trabalho — humana ou assistida por IA — e a garantia de continuidade entre sessões: toda pendência aberta está aqui, com estado e bloqueio explícitos.
>
> **Duas frentes do FaunaBR:**
> - **Parte I — Projeto de pesquisa e fundamentação conceitual:** o problema científico (`docs/projetoPesquisa.md`), a formulação do conceito de espécie (`docs/specieConcept.md`), o glossário (`CONTEXT.md`) e as avaliações teóricas de literatura (`docs/referencias/`).
> - **Parte II — Arquitetura, modelagem de dados e governança:** o modelo C4 e persistência (`docs/arquitetura.md`), o conjunto de ADRs (`docs/adr/`), a matriz de governança (`docs/governanca.md`) e a engenharia reversa do CTFB (`dados/modeloERctf.md`).
>
> **Regras de manutenção:** ao final de cada sessão, atualizar (i) a data do estado, (ii) o estado do repositório, (iii) a síntese do que foi feito e (iv) a lista de próximas ações. Pendência resolvida não é apagada: é marcada como decidida, indicando onde e em qual commit foi consolidada. Caminhos citados são relativos à raiz do repositório.

**Estado em:** 2026-09-17 (Engenharia reversa do CTFB concluída; avaliação teórica de Wiley & Lieberman 2011 concluída e 10 ações propostas em aberto para discussão com Walter Boeger)

**Para quem retoma:** comece pela **§4 (Próximas Ações Imediatas)**. Para entender as pendências conceituais e de modelo, leia a **§2 (Pendências da avaliação teórica Wiley & Lieberman)** e o relatório em `docs/referencias/avaliacao-wiley-lieberman-2011.md`. Para o modelo físico atual do CTFB, consulte `dados/modeloERctf.md`.

**Estado do repositório:** `main`, sincronizado com `origin/main`. Último commit: `8682af2` (*docs: assess Wiley & Lieberman (2011) impact on specieConcept*).

---

# Parte I — Projeto de Pesquisa e Fundamentação Conceitual

## 1. Síntese do que foi feito até aqui

| Data | Commit | Onde | O que foi feito |
|---|---|---|---|
| 2026-09-09 | `bedf0c2` | `docs/` | Primeira versão completa da arquitetura FaunaBR, governança, conceito de espécie, 19 ADRs e glossário (`CONTEXT.md`). |
| 2026-09-09 | `ef74da2` | `README.md`, `docs/projetoPesquisa.md` | Registro formal dos responsáveis: Dr. Eduardo Dalcin (JBRJ) e Dr. Walter Boeger (Coordenador do CTFB). |
| 2026-09-09 | `0f0e750`, `89afab4` | `docs/projetoPesquisa.md` | Formalização do uso de IA agêntica e geração de código como parte integrante do objeto de pesquisa. |
| 2026-09-15 | `62d8212` | `docs/referencias/` | Adição do arquivo de referência Wiley & Lieberman (2011) — *Phylogenetics: Theory and Practice of Phylogenetic Systematics*, 2ª ed., Cap. 2 (*Species and Speciation*). |
| 2026-09-16 | `8682af2` | `docs/referencias/` | Avaliação de impacto de Wiley & Lieberman (2011) sobre `docs/specieConcept.md`, `CONTEXT.md` e ADR 0003 (`docs/referencias/avaliacao-wiley-lieberman-2011.md`). |

---

## 2. Pendências em aberto — Avaliação Wiley & Lieberman (2011)

A avaliação confirmou a decisão central da arquitetura: o FaunaBR trata espécie como linhagem que evolui separadamente, e hipóteses de espécie são enunciados singulares históricos testados por *weight of evidence* (fundamento ontológico do ADR 0003).

Contudo, foram identificadas 10 ações necessárias, divididas entre **ajustes conceituais/textuais** e **lacunas no modelo de dados**, que estão **suspensas aguardando discussão com Walter Boeger**:

### 2.1 Lacunas estruturais no Modelo de Dados (candidatas a novos ADRs)

| ID | Área | Descrição da Lacuna / Proposta | Impacto no Modelo / ADR | Estado |
|---|---|---|---|---|
| **L1** | Modelo de Dados | **Especiação reticulada / Origem de linhagem:** o vocabulário atual de relações entre conceitos (`congruente`, `inclui`, `incluído em`, `sobrepõe`, `disjunto`) é de teoria dos conjuntos sobre circunscrições, não de descendência. Falta modelar relação de origem de linhagem admitindo **dois parentais** (hibridação/reticulação), comum na ictiofauna neotropical e répteis. | Candidato a ADR próprio. Afeta `HIPOTESE_ESPECIE` e relações no ER. | **Em aberto** (Aguardando Boeger) |
| **L2** | Hierarquia de Evidência | **Espécies ancestrais e parafilia sob PSC-I:** espécies ancestrais persistentes são necessariamente parafiléticas sob critérios cladísticos estritos. Monofilia não pode ser critério obrigatório nem ordenador de peso no `grauCorroboracao` (ADR 0003), para não penalizar linhagens ancestrais legítimas. | Candidato a revisão/ADR do ADR 0003 e §4.2 de `specieConcept.md`. | **Em aberto** (Aguardando Boeger) |
| **L3** | Persistência | **Intervalo de existência da linhagem:** como indivíduo histórico, a espécie tem origem e extinção. A entidade `HIPOTESE_ESPECIE` não possui intervalo temporal inferido (origem/fim), lacuna sensível para registros fósseis, espécies extintas e museômica histórica. | Afeta esquema relacional de `HIPOTESE_ESPECIE` (`arquitetura.md` e ADR 0015). | **Em aberto** (Aguardando Boeger) |

### 2.2 Ajustes conceituais e textuais em `docs/specieConcept.md` e `CONTEXT.md`

| ID | Onde | Descrição do Ajuste | Justificativa / Fonte | Estado |
|---|---|---|---|---|
| **A1** | `specieConcept.md` §1 | **Reatribuir o conceito de linhagem:** retificar a afirmativa de que o Conceito Unificado (De Queiroz 2007) é inovação que removeu o conflito. O conceito adotado é o de *espécie-como-linhagem* (Simpson 1961; Hennig 1966; Wiley 1978), na formulação unificada de De Queiroz (1998, 2007). Substituir "consenso" por "formulação dominante" e registrar a recusa do rótulo por Wiley & Lieberman. | Wiley & Lieberman (2011, p. 34) | **Em aberto** |
| **A2** | `specieConcept.md` §1, `CONTEXT.md` | **Sinonímia conceitual em `criteriosAplicados`:** explicitar equivalência ontológica: `ESC ≡ GLC ≡ Cohesion ≡ Cladistic ≡ Internodal ≡ Hennigian ≡ Population Lineages`. Impede que asserções da literatura zoológica que citam ESC sejam tratadas como concorrentes. | Evitar erro operacional no CTFB | **Em aberto** |
| **A3** | `specieConcept.md` §2 | **Camada ontológica formal:** explicitar a distinção entre *espécie-como-táxon* (indivíduo histórico) e *conceito de espécie* (*kind*). Registrar que caracteres e diagnoses entram como `EVIDENCIA` porque indivíduos são "diagnosticados, mas nunca definidos". | Ghiselin (1974); Wiley & Lieberman (2011, p. 23) | **Em aberto** |
| **A4** | `specieConcept.md` §2 | **Proibição da leitura extensional:** proibir explicitamente o erro de ver a espécie como o conjunto (*set*) de seus espécimes. A contagem de espécimes é evidência, não constituinte da espécie. | Hull (1981); Wiley & Lieberman (2011, p. 26) | **Em aberto** |
| **A5** | `specieConcept.md` §3.2 | **Generalização do viés de oversplitting:** registrar que superdivisão não é patologia restrita a métodos moleculares (MSC), mas decorre de qualquer critério operacional tomado como definição essencial (ocorre igualmente em clines morfológicos sob PSC-II). | Sukumaran & Knowles (2017); Wiley & Lieberman (2011, p. 28) | **Em aberto** |
| **A6** | `specieConcept.md` §3 | **Tabela de escopo de validade por critério:** incorporar matriz explicitando onde cada critério é válido e onde perde poder de teste (ex.: BSC inválido para alopatria/fósseis; PSC-I inválido para ancestrais). | Seção 3.2 de `avaliacao-wiley-lieberman-2011.md` | **Em aberto** |
| **A7** | `specieConcept.md` §7 | **Atualização bibliográfica:** adicionar citações completas de Wiley & Lieberman (2011) e Wiley & Mayden (2000a–c). | Completude das fontes teóricas | **Em aberto** |

---

# Parte II — Arquitetura, Engenharia Reversa e Persistência

## 3. Síntese do que foi feito

| Data | Commit | Onde | O que foi feito |
|---|---|---|---|
| 2026-09-10 | `eb92729` | `dados/modeloERctf.md`, `dados/report.md` | Engenharia reversa completa do banco de dados do Catálogo Taxonômico da Fauna (CTF): extração do DDL via parsing de TOC do dump de 907 MB (`backup_fauna_2026_09_09.dump`). Mapeamento de 94 tabelas, 758 colunas, 98 FKs e 5 diagramas Mermaid sem erros de validação sintática. |
| 2026-09-10 | `b04fc67` | `docs/contexto.md` | Normalização de quebras de linha e formatação do documento de requisitos. |

### 3.1 Próximos Desdobramentos da Engenharia Reversa do CTFB

1. **Mapeamento de De-Para (CTFB Legado → FaunaBR Greenfield):**
   - Cruzar as 94 tabelas do CTFB mapeadas em `dados/modeloERctf.md` com a proposta de persistência relacional do FaunaBR (`docs/arquitetura.md` e ADR 0015).
   - Identificar quais tabelas do schema `public` alimentam as entidades de Nomes e Sinônimos e como as 18 tabelas associativas sem PK migram para a camada de asserção e proveniência.
2. **Ciclos e integridade referencial herdados:**
   - Analisar o tratamento dos ciclos de FKs recíprocas herdadas do mapeamento Hibernate (`lista ↔ taxonomic_tree` e `dados_lista_brasil ↔ distribuicao/grupo`) na modelagem limpa do FaunaBR.
3. **Mapeamento das tabelas de `ipt_fauna` e `carga`:**
   - Formalizar o pipeline de ingestão e publicação conforme desenhado no ADR 0014, ADR 0016 e ADR 0017.

---

# 4. Próximas Ações Imediatas

- [ ] **Pauta com Dr. Walter Boeger:**
  - Apresentar o relatório `docs/referencias/avaliacao-wiley-lieberman-2011.md`.
  - Discutir as lacunas estruturais (**L1**: especiação reticulada/dois parentais; **L2**: espécies ancestrais e monofilia no `grauCorroboracao`; **L3**: intervalo temporal em hipótese de espécie).
  - Obter concordância sobre os ajustes textuais (**A1** a **A7**) em `docs/specieConcept.md` e `CONTEXT.md`.
- [ ] **Elaboração de novos ADRs:**
  - Redigir ADR sobre linhagens reticuladas e relações genealógicas vs. relações extensionais de circunscrição (caso aprovado na pauta).
  - Atualizar ADR 0003 (hierarquia de evidência) incorporando a fundamentação de enunciados singulares históricos e a ressalva de espécies ancestrais.
- [ ] **Aplicação dos ajustes em `docs/specieConcept.md` e `CONTEXT.md`:**
  - Executar as alterações aprovadas na reunião.
- [ ] **Início do Mapeamento De-Para (CTFB → FaunaBR):**
  - Elaborar documento de migração/interoperabilidade cruzando `dados/modeloERctf.md` com o esquema PostgreSQL/PostGIS de `docs/arquitetura.md`.
