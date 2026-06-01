---
name: atualizar-sdd
description: Atualiza os dois arquivos SDD canônicos mantendo separação entre requisitos validados e registro da implementação atual.
agent: agent
---

# Atualizar SDD

Use este prompt quando uma tarefa exigir atualização do fluxo SDD do projeto.

## Objetivo

Atualizar `docs/SDD-origin.md` e/ou `docs/SDD-dev.md` de forma rastreável, mantendo separação entre requisitos validados e registro da implementação atual.

## Instruções

- Use o fluxo do agente `sdd-specialist`.
- Use somente os arquivos `docs/SDD-origin.md` e `docs/SDD-dev.md`.
- Não crie arquivos `SDD-*.template.md`; os dois SDDs ativos já são os modelos canônicos.
- Trate `docs/SDD-origin.md` como fonte de verdade de requisitos, regras, fluxos e decisões validadas.
- Trate `docs/SDD-dev.md` como registro da implementação atual.
- Não remover requisitos anteriores sem solicitação explícita.
- Não registrar comportamento que não foi implementado ou validado.
- Não antecipar requisitos futuros no `SDD-dev.md`.
- Não usar `SDD-origin.md` como changelog.
- Manter histórico funcional.
- Alterar apenas o necessário.
- Aplicar alterações em bloco único/consolidado.
- Preservar padrões arquiteturais e nomenclaturas do projeto.

## Quando Atualizar Cada Arquivo

### Atualizar `SDD-origin.md` quando:

- houver novo requisito validado;
- houver alteração validada de regra de negócio;
- houver novo fluxo, permissão, entidade, integração ou restrição oficial;
- uma decisão passar a valer para o sistema como um todo.

### Atualizar `SDD-dev.md` quando:

- houver implementação, correção, refatoração, validação ou decisão técnica referente à tarefa atual;
- for necessário registrar arquivos alterados, escopo tratado, premissas, riscos ou testes executados;
- houver validação pendente que não permita declarar a tarefa como totalmente validada.

## Formato de Resposta Esperado

Responder com:

- Resumo da atualização.
- Arquivos SDD alterados.
- Requisitos ou decisões incluídas.
- Escopo tratado.
- Validações realizadas.
- Validações pendentes.
- Riscos ou premissas registradas.
