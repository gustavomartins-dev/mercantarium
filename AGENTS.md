# Instruções para agentes

O Mercantarium lida, no futuro, com dinheiro, contas externas e consumidores. Segurança e honestidade fazem
parte do produto, não são trabalho posterior.

## Ordem de leitura

Leia `README.md`, `docs/ARCHITECTURE.md`, `docs/SAFETY.md` e `docs/ROADMAP.md` antes de implementar.

## Princípios de trabalho

- Preserve o modo simulado como experiência completa e reproduzível.
- Não adicione integrações, dependências de nuvem ou serviços pagos sem pedido explícito.
- Faça mudanças pequenas, tipadas, testáveis e coerentes com o domínio.
- Mantenha uma única fonte de verdade; a UI deriva estado e envia intenções.
- Toda ação material deve nascer como proposta e passar pelo policy engine.
- Trate ações externas como idempotentes, auditáveis, limitadas e reversíveis quando possível.
- Nunca grave segredos, tokens, dados pessoais ou respostas sensíveis em fixtures, prompts ou logs.
- Não invente resultados, cobertura, screenshots, métricas ou integrações.
- Atualize documentação quando o estado real do produto mudar.

## Linguagem e identidade

Código, nomes técnicos e contratos podem usar inglês. A interface e a documentação voltadas a Gustavo usam
português brasileiro. A estética é um armazém digital noturno, funcional e autoral — não um template SaaS.

## Verificação esperada

Execute typecheck, testes e build. Para alterações visuais, valide desktop e mobile, console, overflow,
redução de movimento e navegação por teclado. Registre qualquer verificação que não puder ser executada.

