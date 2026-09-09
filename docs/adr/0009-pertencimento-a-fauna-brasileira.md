# Pertencimento à fauna brasileira: declarado pelo especialista, sustentação computada ao lado

A presença de uma espécie na fauna brasileira permanece sendo **asserção do Especialista de Grupo**, como no CTFB. O sistema acrescenta, para cada espécie, um **grau de sustentação** computado a partir da evidência efetivamente vinculada:

| Grau | Sustentação da presença no país |
|---|---|
| 1 | Espécime portador do nome com localidade-tipo em território nacional |
| 2 | Espécime preservado em coleção, com ocorrência em território nacional |
| 3 | Amostra com sequência depositada, de origem nacional |
| 4 | Apenas literatura, sem ocorrência vinculada |
| 5 | Apenas observação |
| 6 | **Nenhuma evidência vinculada** |

O grau é derivado, nunca digitado, e é recomputado a cada ingestão. A hierarquia é a mesma do [ADR 0003](./0003-hierarquia-de-evidencia.md), aplicada à pergunta "por que esta espécie consta como brasileira?".

## Considered Options

- **Apenas declaração do especialista** (prática atual do CTFB): rejeitado por opacidade — não se sabe, para nenhuma das 125.138 espécies válidas, qual evidência sustenta a presença no país.
- **Pertencimento derivado exclusivamente da evidência**: rejeitado por rebaixar imediatamente milhares de espécies cuja evidência existe apenas em literatura não digitalizada ou em coleção não publicada, produzindo uma lista mais pobre que a atual sem que nada tenha mudado no conhecimento.

## Consequências

- **A cobertura evidencial do catálogo nacional torna-se mensurável.** Quantas espécies da fauna brasileira não têm um único espécime rastreável sustentando sua presença é pergunta hoje sem resposta; passa a ser consulta.
- O grau 6 é convertido em **pauta de trabalho** devolvida às coleções, não em marca de erro. É a "detecção automática de determinações desatualizadas em coleções" que BOEGER et al. (2024) anunciam como possibilidade ainda não realizada.
- **A métrica é politicamente sensível.** Publicar que *N* mil espécies do catálogo nacional não têm evidência vinculada é resultado de pesquisa legítimo e constrangimento institucional ao mesmo tempo. O `README.md` deve enquadrá-la pelo que ela mede — **lacuna de digitalização e de vinculação**, não erro de taxonomista. O custo é aceitável porque nada aqui substitui sistema em produção ([ADR 0001](./0001-sistema-de-registro-greenfield.md)).
- Exige que toda ingestão recompute o grau, e que a série histórica do grau seja preservada — a evolução da cobertura ao longo do tempo é o indicador, não o valor instantâneo.
