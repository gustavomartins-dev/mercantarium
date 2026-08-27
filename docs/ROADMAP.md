# Roadmap por portões de confiança

## P0 — Blueprint (estado atual)

- visão, linguagem, agentes, arquitetura e contrato de segurança;
- nenhuma aplicação ou integração implementada.

## P1 — Turno fantasma

- aplicação local com armazém operacional visual;
- jornada determinística, ledger, aprovações, orçamento e kill switch;
- testes das políticas e jornadas desktop/mobile.

**Portão:** toda ação reproduzível, estados honestos e zero dependência externa.

## P2 — Control plane local

- API, SQLite, fila persistente, replay e autenticação local;
- agentes substituíveis com provider simulado;
- observabilidade e recuperação após reinício.

**Portão:** idempotência, reconciliação e testes de falha demonstrados.

## P3 — Sandboxes

- primeiro adaptador oficial escolhido por necessidade real;
- credenciais em secret store, permissões mínimas e contrato testado;
- ações ainda exigem aprovação individual.

**Portão:** nenhum efeito real e trilha completa de chamadas.

## P4 — Produção em modo sombra

- leitura de dados reais sem escrever em provedores;
- propostas comparadas às decisões humanas;
- métricas de precisão, custo, latência e taxa de rejeição.

**Portão:** período de avaliação definido e critérios objetivos cumpridos.

## P5 — Escrita supervisionada

- rascunhos externos e ações reais sempre aprovadas;
- limites baixos, rollout por capacidade e plano de rollback;
- monitoramento de incidentes e reconciliação financeira.

**Portão:** histórico estável, auditoria e conformidade revisadas.

## P6 — Autonomia limitada

- apenas ações reversíveis, rotineiras, de baixo risco e valor pequeno;
- orçamento diário, janela operacional, circuit breakers e revisão frequente;
- expansão de autonomia exige nova decisão humana explícita.

O roadmap não contém “autonomia total”. O objetivo é uma operação eficiente e controlável, não ausência de
responsabilidade humana.

