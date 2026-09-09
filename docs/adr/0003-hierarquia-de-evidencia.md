# Universo de evidência amplo, com peso evidencial explícito

O sistema ingere as três classes de evidência — material físico de coleção, observações (humanas e de máquina) e dados derivados de DNA (sequências, BINs/MOTUs, eDNA) — porém **nunca as trata como equivalentes**. Cada registro de evidência carrega um grau declarado, e nenhuma consulta agregada pode combinar classes sem explicitar o corte aplicado.

Hierarquia adotada, do maior para o menor peso:

1. **Espécime portador do nome** — holótipo, lectótipo, neótipo (ICZN Art. 72–75)
2. **Espécime preservado** — `PreservedSpecimen`, `FossilSpecimen`, `MaterialSample`
3. **Amostra com sequência** — material com DNA associado, incluindo museômica
4. **Observação verificada** — `HumanObservation` / `MachineObservation` com validação de especialista
5. **Observação não verificada** — inclui ciência cidadã sem revisão
6. **Unidade molecular sem material** — BIN, MOTU, eDNA sem espécime associado

## Considered Options

- **Somente material físico**: rejeitado por eliminar *dark taxa* e museômica, ambos pilares do [`specieConcept.md`](../specieConcept.md).
- **Todas as classes sem hierarquia**: rejeitado porque equipara uma fotografia não revisada a um holótipo — exatamente o defeito que o projeto se propõe a corrigir.

## Consequências

- O grau de corroboração de uma hipótese de espécie é computável a partir das classes de evidência que a sustentam, e não apenas do número de registros.
- Cobertura espaço-temporal muito maior que a das coleções isoladamente, sem diluir o rigor nomenclatural.
- Toda API e todo Darwin Core Archive publicado deve expor a classe de evidência de cada registro.
