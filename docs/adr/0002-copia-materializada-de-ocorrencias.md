# Ocorrências ingeridas como cópia materializada

As ocorrências de espécimes (GBIF, SiBBr, coleções brasileiras) são **ingeridas e materializadas localmente**, versionadas e reprocessáveis, e não referenciadas por identificador em consulta remota.

## Considered Options

- **Índice de referências** (`occurrenceID` + instituição + vínculo, resto consultado em tempo real): rejeitado porque o IPT lê tabelas, não APIs de terceiros — sem materialização não há oferta de Darwin Core Archive; e a reinterpretação retroativa de ocorrências via mapeamento de conceitos de táxon ([`specieConcept.md`](../specieConcept.md), requisito 2) é inviável sobre dados remotos.
- **Híbrido por origem** (cópia para coleções brasileiras, índice para o restante): rejeitado por criar dois regimes de qualidade dentro da mesma entidade Ocorrência, inviabilizando análise agregada consistente.

## Consequências

- Exige pipeline permanente de sincronização e reconciliação com as fontes externas, com proveniência de cada ingestão.
- O sistema torna-se capaz de publicar seu próprio Darwin Core Archive enriquecido, com as asserções e vínculos que as fontes originais não possuem.
- O volume de dados passa a ser fator dimensionante da escolha de armazenamento.
