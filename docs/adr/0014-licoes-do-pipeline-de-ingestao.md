# Lições do pipeline de ingestão do Biodiversidade.Online — o que adotar e o que rejeitar

O [Biodiversidade.Online](https://github.com/biopinda/Biodiversidade-Online) (Dalcin & Pinheiro, [DOI 10.5281/zenodo.18668804](https://doi.org/10.5281/zenodo.18668804)) já opera em produção o problema que o [ADR 0002](./0002-copia-materializada-de-ocorrencias.md) cria aqui: ingestão de Darwin Core Archive do CTFB, da Flora e Funga e de mais de 505 IPTs de coleções, com auditoria. Seu pipeline é a referência de implementação — mas três de seus padrões são **incompatíveis** com decisões já tomadas nesta arquitetura, e precisam ser rejeitados explicitamente antes que reapareçam por inércia.

## Adotado

- **Parsing streaming de DwC-A** a partir de `meta.xml`, com leitura por índice de coluna e mapeamento para termo Darwin Core. Sem carregar o arquivo inteiro em memória.
- **Registro de execução de ingestão** (`ingest_runs`): contadores, duração, status, por fonte. Aqui vira a proveniência da ingestão exigida pelo [ADR 0012](./0012-identificadores.md) — quando e por qual execução cada identificador externo passou a apontar para a entidade interna.
- **Identificador de execução (UUIDv7) carimbado em todo registro tocado.** É o que torna a ingestão auditável e reversível registro a registro.
- **Comparação de `pubDate` e `dateStamp` do `eml.xml`** com a última execução bem-sucedida antes de reprocessar: evita reingestão silenciosa de dataset inalterado. Aqui é aviso ao operador, nunca bloqueio automático.
- **Campos computados para reconciliação difusa** — nome canônico (gênero + epíteto específico + infraespecífico) e nome científico achatado (minúsculas, apenas `[a-z0-9]`). São o que torna viável cruzar listas externas cujos nomes divergem em autoria, grafia e pontuação.
- **Documento JSON por táxon com extensões mescladas** (distribuição, nomes vernaculares, perfil, referências, tipos e espécimes, sinonímias). Formalizado no [ADR 0013](./0013-armazenamento-sqlite-json-e-duckdb.md).
- **Catálogo de fontes IPT como dado, não como código** — arquivo tabular com nome, repositório, reino, *tag* e URL por coleção. Ingerir 505 fontes exige que adicionar a 506ª não seja alteração de código.

## Rejeitado, com o motivo

- **`delete-not-seen`** — remover do banco todo registro da fonte ausente da última publicação. É correto para um espelho; é destrutivo aqui. Registro ausente de uma republicação **não** significa registro inexistente: pode ser falha de publicação, mudança de escopo do recurso IPT, ou o próprio Gestor de Coleção despublicando temporariamente. Nesta arquitetura o registro é **marcado como ausente na última ingestão**, com a data e a execução que o constataram, e permanece consultável. Apagar romperia a asserção que o cita e o vínculo nome→tipo do [ADR 0012](./0012-identificadores.md).
- **Identificador da fonte como chave primária** (`_id = taxonID`, `_id = occurrenceID`) — contraria frontalmente o ADR 0012. Aqui a identidade é interna (UUIDv7), e os identificadores da fonte vivem na tabela de resolução. O motivo é o mesmo que o próprio projeto contorna com cadeia de *fallbacks* (`taxonID` → `scientificNameID` → `scientificName + authorship`): identificador de terceiro não é estável o bastante para ser identidade.
- **Filtro que aceita apenas táxons-folha** (espécie, subespécie, variedade, forma), derivando os níveis superiores dos campos de classificação do próprio documento. Inaceitável nesta arquitetura: prioridade, homonímia e atos nomenclaturais incidem sobre nomes de **gênero e de família** tanto quanto sobre nomes de espécie ([ADR 0005](./0005-camadas-nomenclatural-e-taxonomica.md)). Descartar o nome supraespecífico como entidade impede validar o Código.

## Consequências

- O pipeline de ingestão desta arquitetura é reconhecidamente derivado do Biodiversidade.Online, e as divergências acima são deliberadas, não desconhecimento.
- "Ausente na última ingestão" é estado de primeira classe do registro de ocorrência, com data e execução — não é ausência de linha.
- O catálogo de fontes IPT é entidade governada: admitir uma coleção é decisão do Comitê, e se materializa como linha nesse catálogo.
