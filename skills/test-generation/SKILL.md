---
name: test-generation
description: Use esta skill ao criar, revisar, refatorar ou ampliar testes automatizados, incluindo testes unitários, integração, componentes, APIs, fluxos críticos, mocks, casos de borda e prevenção de regressões.
---

# Test Generation

Use esta skill para orientar a criação e revisão de testes automatizados em projetos de software.

---

## Objetivo

Garantir que novas funcionalidades, correções e refatorações sejam acompanhadas por testes claros, úteis e sustentáveis, reduzindo regressões e aumentando a confiança nas alterações.

---

## Regras principais

- Priorizar testes que validem comportamento, não detalhes internos de implementação.
- Não criar testes frágeis dependentes de estrutura interna desnecessária.
- Não alterar regra de negócio apenas para facilitar teste.
- Não remover testes existentes sem justificativa.
- Não ignorar cenários de erro, borda ou permissão.
- Não adicionar dependências externas sem solicitação.
- Manter o padrão de testes já utilizado no projeto.
- Criar testes pequenos, legíveis e objetivos.
- Usar nomes descritivos para os cenários testados.
- Quando não for possível testar algo, explicar a limitação.
- Não editar linha por linha; aplicar alterações em bloco único/consolidado.

---

## Checklist de análise

### Entendimento do escopo

Antes de criar testes, identificar:

- qual comportamento precisa ser validado;
- qual alteração foi feita no código;
- quais fluxos podem quebrar;
- quais entradas e saídas são esperadas;
- quais regras de negócio estão envolvidas;
- quais dependências externas precisam ser simuladas;
- quais critérios de aceite estão definidos no SDD.

### Tipos de teste

Avaliar qual tipo de teste faz mais sentido:

- teste unitário para funções, métodos e regras isoladas;
- teste de componente para interface e comportamento visual/interativo;
- teste de integração para comunicação entre módulos;
- teste de API para contratos, status codes e payloads;
- teste end-to-end para fluxos críticos do usuário;
- teste de regressão para bugs corrigidos;
- teste de acessibilidade quando houver impacto em interface.

### Casos positivos

Verificar se os testes cobrem:

- fluxo principal esperado;
- entrada válida;
- resposta ou renderização correta;
- estado final esperado;
- chamadas corretas a funções, serviços ou APIs quando aplicável.

### Casos negativos

Verificar se os testes cobrem:

- entrada inválida;
- dados ausentes;
- erros de validação;
- falha de API ou serviço externo;
- permissão insuficiente;
- usuário não autenticado;
- estado vazio;
- timeout ou indisponibilidade quando aplicável.

### Casos de borda

Considerar:

- valores nulos ou indefinidos;
- lista vazia;
- lista com um item;
- lista com muitos itens;
- datas no limite;
- valores mínimos e máximos;
- strings vazias ou muito longas;
- caracteres especiais;
- diferenças de timezone;
- duplicidade de dados;
- estados concorrentes ou repetidos.

### Mocks e dependências

Ao usar mocks:

- simular apenas o necessário;
- evitar mocks excessivamente complexos;
- manter dados de teste claros e realistas;
- isolar chamadas externas como APIs, banco, autenticação, storage ou serviços de terceiros;
- garantir que mocks não escondam problemas reais de contrato.

---

## Processo recomendado

1. Ler o código alterado e entender o comportamento esperado.
2. Identificar critérios de aceite no SDD.
3. Identificar riscos de regressão.
4. Verificar padrões de teste existentes no projeto.
5. Criar casos positivos, negativos e de borda.
6. Usar mocks apenas quando necessário.
7. Rodar ou orientar a execução dos testes.
8. Ajustar testes frágeis ou redundantes.
9. Informar lacunas que ainda exigem validação manual.

---

## Formato de resposta esperado

## Resumo

O que foi testado.

## Testes criados ou sugeridos

Lista objetiva dos cenários cobertos.

## Casos considerados

Positivos, negativos e borda.

## Como executar

Comando ou orientação para rodar os testes.

## Riscos restantes

Pontos que ainda precisam de validação manual ou integração.
