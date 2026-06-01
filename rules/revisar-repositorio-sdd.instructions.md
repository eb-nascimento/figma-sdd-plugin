---
name: revisar-repositorio-sdd
description: Revisa a coerência entre SDD, agentes, prompts e skills deste repositório-base.
agent: ask
---

# Revisar Repositório SDD, Agentes, Prompts e Skills

Use este prompt para revisar se o repositório está coerente com boas práticas de SDD, agentes de IA, prompts reutilizáveis e skills.

## Objetivo

Avaliar a estrutura do repositório e identificar inconsistências entre documentação, agentes, prompts, skills e arquivos SDD.

## Instruções

- Verificar se existem exatamente dois arquivos SDD canônicos: `docs/SDD-origin.md` e `docs/SDD-dev.md`.
- Verificar se não existem arquivos `SDD-*.template.md`.
- Verificar se `SDD-origin.md` está separado de `SDD-dev.md`.
- Verificar se `SDD-origin.md` contém somente requisitos, regras e decisões validadas ou campos de preenchimento para novo projeto.
- Verificar se `SDD-dev.md` contém somente registro da implementação atual ou campos de preenchimento para novo projeto.
- Verificar se agentes referenciam corretamente o fluxo SDD.
- Verificar se prompts são objetivos, executáveis e reutilizáveis.
- Verificar se agents e prompts possuem frontmatter quando aplicável.
- Verificar se skills possuem frontmatter, objetivo, regras, checklist e formato de resposta.
- Identificar arquivos citados no SDD que não existem no repositório.
- Identificar nomes inconsistentes, como diferenças entre `AGENTS.md` e `agents.md`.
- Identificar links, caminhos ou referências quebradas.
- Propor alterações em bloco único/consolidado.

## Formato de Resposta Esperado

Responder com:

## Resumo

Qualidade geral do repositório.

## Pontos Positivos

Itens que já estão adequados.

## Problemas Encontrados

Para cada problema:

- Arquivo ou caminho.
- Problema.
- Impacto.
- Correção recomendada.

## Melhorias Prioritárias

Lista em ordem de prioridade.

## Próximos Passos

Ações objetivas para corrigir o repositório.
