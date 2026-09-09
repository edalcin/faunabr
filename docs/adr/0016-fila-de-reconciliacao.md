# Divergência como entidade com resolução registrada

Toda divergência entre o sistema e uma coleção é entidade de primeira classe, com ciclo de vida e autor. Três tipos, produzidos automaticamente:

| Tipo | Origem |
|---|---|
| Identificação superada por revisão | [ADR 0007](./0007-precedencia-da-revisao-taxonomica.md) |
| Espécie sem evidência vinculada (grau 6) | [ADR 0009](./0009-pertencimento-a-fauna-brasileira.md) |
| Registro ausente na última ingestão | [ADR 0014](./0014-licoes-do-pipeline-de-ingestao.md) |

Ciclo de vida: **aberta → em análise → resolvida**, sendo a resolução uma de três — *aceita*, *rejeitada* ou *reconhecida sem ação* — sempre com autor, data e justificativa. A resolução retorna ao sistema como **asserção assinada do Gestor de Coleção**, e entra no histórico do registro.

## Considered Options

- **Só leitura** (publicar a divergência via API e Darwin Core Archive): rejeitado — zero acoplamento, e na prática ninguém consome o que não sabe que existe.
- **Notificação ativa sem registro de resolução**: rejeitado — obriga o sistema a manter estado de entrega e silêncio, sem produzir o dado que interessa.

## Consequências

- **A resolução é dado científico, não notificação.** "Esta coleção examinou a divergência e a rejeitou, por este motivo" é informação que hoje não existe em lugar algum e que altera o peso da evidência de uma hipótese.
- Sem registro de resolução, a mesma divergência reapareceria a cada ingestão, treinando o gestor a ignorar a fila — o que mataria o mecanismo. A resolução é o que suprime a reapresentação.
- Exige identidade de Gestor de Coleção e autorização por coleção.
- **Não é motor de workflow.** É uma tabela com estado, autor, data e histórico no núcleo PostgreSQL ([ADR 0015](./0015-postgresql-unico-com-jsonb-e-postgis.md)) — não uma plataforma de tickets, sem regras configuráveis, sem escalonamento, sem SLA.
- Divergência rejeitada por uma coleção permanece visível como discordância declarada; não vira consenso nem desaparece.
