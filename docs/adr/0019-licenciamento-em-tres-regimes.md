# Licenciamento em três regimes

Código, documentação e dados recebem licenças distintas. Tratá-los sob uma só é o erro que produz tanto exposição jurídica quanto imobilismo.

| Camada | Licença | Razão |
|---|---|---|
| **Código** | **Apache-2.0** | Adoção sem atrito, com cláusula expressa de patentes — relevante num domínio com histórico documentado de apropriação de conhecimento associado à biodiversidade brasileira. Custo zero sobre a MIT |
| **Documentação e ADRs** | **CC BY 4.0** | Reuso e tradução livres, com atribuição |
| **Dados** | **CC BY 4.0**, exceto registros com TK/BC Label | Alinha com o CTFB (que é CC BY 4.0) e com o GBIF |
| **Dados com TK/BC Label** | **Fora de licença aberta** | Licença aberta é irrevogável e universal — o oposto do que a autoridade cultural exige |

## A exceção que importa

Registro com TK ou BC Label **não recebe licença aberta**. Não por menos compromisso com abertura, mas porque uma licença Creative Commons é juridicamente irrevogável, e o [ADR 0006](./0006-fair-care-aberto-por-padrao.md) dá à Comunidade Detentora autoridade final e revisável sobre suas Labels — inclusive para restringir depois de ter permitido. Um CC BY sobre esse registro anularia na prática essa autoridade.

Operacionalmente: no Darwin Core Archive publicado, esse registro sai com o **LC Project ID no campo `rights`**, e não com uma licença Creative Commons.

## Considered Options

- **Licença única CC BY 4.0 para tudo**, como o CTFB: rejeitado — licenciar código sob licença de conteúdo é juridicamente confuso, e a exceção de CTA não teria onde existir.

## Consequências

- O arquivo `LICENSE` do repositório passa a exigir declaração das três camadas, não uma linha só.
- Toda saída de dados — API e tabelas de publicação — precisa emitir a licença correta **por registro**, nunca uma licença global do conjunto.
