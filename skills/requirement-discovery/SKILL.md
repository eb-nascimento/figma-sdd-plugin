---
name: requirement-discovery
description: Use esta skill quando uma solicitação estiver vaga, incompleta ou ambígua e for necessário transformar a ideia em requisito, escopo, critérios de aceite, validações e pendências antes da implementação.
---

# Requirement Discovery

Use esta skill para aprofundar solicitações antes da implementação, especialmente quando houver risco de interpretar errado o requisito.

---

## Objetivo

Transformar uma solicitação inicial em um requisito claro, delimitado, testável e rastreável, sem inventar regra de negócio ou ampliar escopo sem confirmação.

---

## Quando usar

Use esta skill quando:

- a solicitação estiver vaga;
- houver mais de uma interpretação possível;
- faltarem critérios de aceite;
- a mudança afetar regra de negócio;
- a mudança afetar dados, permissões, integrações ou fluxo crítico;
- o pedido exigir decisão de produto ou usuário final;
- o agente precisar delimitar escopo antes de implementar;
- o SDD não tiver informação suficiente para orientar a tarefa.

---

## Regras principais

- Não transformar ideia vaga em requisito validado sem explicitar premissas.
- Não inventar comportamento esperado.
- Não ampliar escopo além do pedido original.
- Não alterar regra de negócio sem confirmação.
- Quando a dúvida for pequena e não alterar regra, contrato, dados ou escopo, registrar premissa conservadora e seguir.
- Quando a dúvida for relevante, parar e pedir confirmação.
- Não editar linha por linha; propor alterações em bloco único/consolidado.

---

## Checklist de descoberta

Antes de implementar, identificar:

- intenção principal do usuário;
- problema que precisa ser resolvido;
- usuário ou perfil impactado;
- fluxo atual;
- comportamento esperado;
- comportamento fora do escopo;
- regra de negócio envolvida;
- dados ou entidades impactadas;
- permissões envolvidas;
- integrações impactadas;
- estados de interface;
- mensagens de erro ou sucesso;
- critérios de aceite;
- validações esperadas;
- riscos e premissas.

---

## Perguntas úteis

Use apenas as perguntas necessárias. Não faça entrevista longa quando uma premissa conservadora resolver.

- Qual comportamento deve mudar?
- Qual comportamento deve permanecer igual?
- Em quais telas, fluxos ou perfis isso se aplica?
- Existe regra de negócio validada para esse caso?
- O que deve acontecer em erro, vazio, loading, sucesso ou permissão negada?
- Como saberemos que a tarefa foi concluída corretamente?
- Quais testes ou validações comprovam o aceite?

---

## Resultado esperado

Ao final da descoberta, produzir:

## Entendimento

Resumo da intenção principal.

## Escopo

Dentro e fora do escopo.

## Requisito proposto

Descrição clara do comportamento esperado.

## Critérios de aceite

Cenários verificáveis, preferencialmente no formato Dado / Quando / Então.

## Validações esperadas

Testes automatizados, revisão manual ou verificações técnicas.

## Premissas e riscos

Pontos assumidos ou dependentes de confirmação.

## Atualização SDD

O que deve entrar em `SDD-origin.md` e/ou `SDD-dev.md`.
