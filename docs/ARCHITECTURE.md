# Arquitetura do Mercantarium

## Centro da arquitetura

O sistema é um fluxo de propostas e eventos. Agentes não possuem acesso direto a provedores. O control plane
recebe uma intenção tipada, consulta o policy engine, solicita aprovação quando necessário e delega a um
adaptador. O resultado retorna como evento e alimenta a projeção visual.

```text
observação -> tarefa -> proposta -> avaliação de política -> aprovação -> execução -> resultado -> aprendizado
```

## Componentes

- **Command Center:** projeção visual, fila, aprovações, métricas e controles.
- **Orchestrator:** escolhe o próximo trabalho sem confundir planejamento com autorização.
- **Agents:** funções especializadas com ferramentas mínimas e saída estruturada.
- **Policy Engine / WARDEN:** limites, autorização, orçamento, kill switch e separação de funções.
- **Ledger:** registro append-only dos fatos; projeções podem ser reconstruídas a partir dele.
- **Job Queue:** execução recuperável, retries classificados e chaves de idempotência.
- **Adapters:** fronteira explícita com serviços externos; inicialmente apenas simulação.

## Entidades iniciais

`Signal`, `ProductCandidate`, `SupplierQuote`, `Experiment`, `DraftAsset`, `ActionProposal`, `Approval`,
`Budget`, `Order`, `CustomerCase`, `PolicyDecision`, `ExecutionReceipt` e `LedgerEvent`.

Cada `ActionProposal` deve registrar: autor, objetivo, argumentos tipados, evidências, custo máximo, risco,
efeito esperado, prazo, chave de idempotência, política aplicável e forma de compensação.

## Estados de uma ação

```text
draft -> proposed -> allowed | approval_required | blocked
approval_required -> approved | rejected | expired
allowed/approved -> executing -> succeeded | failed | uncertain
```

`uncertain` é essencial: timeout não significa falha. Antes de repetir uma operação externa, o sistema deve
consultar o provedor usando a chave de idempotência ou um identificador estável.

## Métricas

As projeções devem separar, no mínimo: receita bruta, descontos, custo do produto, frete subsidiado, mídia,
taxas de pagamento, impostos estimados, reembolsos, chargebacks, margem de contribuição e caixa liquidado.
Valores simulados carregam a origem `simulation`; estimativas nunca aparecem como valores liquidados.

## Estratégia de integração

1. simulador determinístico;
2. sandbox oficial do provedor;
3. produção somente leitura;
4. escrita com aprovação em cada ação;
5. autonomia limitada para ações de baixo risco e baixo valor.

Cada provedor recebe seu próprio adaptador, escopo OAuth mínimo, rate limiting, circuit breaker e testes de
contrato. Nenhuma particularidade de fornecedor deve contaminar o domínio.

