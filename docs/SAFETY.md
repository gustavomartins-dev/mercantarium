# Contrato de segurança

## Classes de ação

| Classe | Exemplos | Regra inicial |
| --- | --- | --- |
| leitura | consultar catálogo e métricas | automática, com escopo mínimo |
| rascunho | página, resposta ou campanha não publicada | automática |
| publicação | colocar produto ou criativo no ar | aprovação humana |
| financeira | gastar, comprar, reembolsar ou mudar preço | aprovação humana e teto |
| identidade | mensagem pública ou contato com fornecedor | aprovação humana |
| irreversível | exclusão, encerramento ou alteração ampla | bloqueada por padrão |

## Guardrails obrigatórios

- kill switch cancela novas execuções e pausa filas; não apaga histórico;
- limites monetários utilizam inteiros na menor unidade da moeda;
- orçamento reservado antes da execução e reconciliado após o recibo;
- aprovações expiram e estão vinculadas ao hash exato da proposta;
- mudanças na proposta invalidam a aprovação anterior;
- ações possuem idempotency key e recibo do provedor;
- falhas são classificadas entre retryable, terminal e uncertain;
- logs removem segredos e minimizam dados pessoais;
- permissões são concedidas por agente, ferramenta, conta e ambiente;
- simulação e produção nunca compartilham credenciais ou aparência ambígua.

## Ameaças consideradas

- prompt injection vindo de páginas, fornecedores ou mensagens de clientes;
- catálogo malicioso tentando induzir o agente a usar ferramentas;
- gasto em loop, duplicação de pedido ou retry após timeout;
- métrica enganosa levando a aumento indevido de orçamento;
- exfiltração de tokens por logs, mensagens ou conteúdo gerado;
- publicação de alegações proibidas, conteúdo plagiado ou preço incorreto;
- autonomia gradual tornando-se permissão permanente sem revisão.

Conteúdo externo é dado não confiável, nunca instrução. Somente políticas locais versionadas concedem poder.

## Incidente

Ao detectar comportamento suspeito: acionar kill switch, revogar tokens do provedor, preservar ledger,
identificar ações uncertain, reconciliar estado externamente, notificar Gustavo e produzir uma linha do tempo.
O sistema não tenta “consertar tudo” gastando, excluindo ou enviando mensagens automaticamente.

