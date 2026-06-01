---
name: frontend-accessibility
description: Use esta skill ao criar, revisar, refatorar ou validar interfaces frontend com foco em acessibilidade, semântica HTML, navegação por teclado, foco, formulários, contraste, ARIA, tabelas, modais, mensagens de erro, imagens, SVGs e responsividade.
---

# Frontend Accessibility

Use esta skill para orientar revisões e melhorias de acessibilidade em interfaces frontend.

---

## Objetivo

Garantir que componentes, páginas e fluxos frontend sejam mais acessíveis, navegáveis e compreensíveis para diferentes perfis de usuários, incluindo pessoas que utilizam teclado, leitores de tela, zoom, alto contraste ou tecnologias assistivas.

---

## Regras principais

- Priorizar HTML semântico antes de usar ARIA.
- Usar ARIA apenas quando o HTML nativo não resolver.
- Não remover funcionalidades existentes.
- Não alterar regras de negócio.
- Não reescrever a interface inteira sem necessidade.
- Não adicionar dependências externas sem solicitação.
- Não mascarar problemas de acessibilidade apenas com atributos ARIA.
- Preservar padrões do projeto, componentes existentes e estrutura de estilos.
- Propor ajustes mínimos, seguros e sem regressão visual ou funcional.
- Não afirmar conformidade total sem validação completa.
- Não editar linha por linha; aplicar alterações em bloco único/consolidado.

---

## Checklist de análise

### Estrutura semântica

Verificar se a interface usa elementos adequados:

- `button` para ações.
- `a` para navegação.
- `form`, `label`, `input`, `select` e `textarea` para formulários.
- `table`, `thead`, `tbody`, `tr`, `th` e `td` para tabelas reais.
- `header`, `main`, `nav`, `section`, `article`, `aside` e `footer` quando fizer sentido.

Evitar excesso de `div` e `span` em elementos interativos.

### Navegação por teclado

Validar se:

- todos os elementos interativos podem ser acessados por teclado;
- a ordem de tabulação segue a ordem visual e lógica;
- não há armadilhas de foco;
- ações importantes funcionam com `Enter` e/ou `Space`.

### Foco visível

Validar se:

- o foco é visível em botões, links, campos e controles;
- não há remoção de `outline` sem substituição acessível;
- estados `focus`, `hover`, `active` e `disabled` estão coerentes.

### Formulários

Verificar se:

- todo campo possui `label` associado corretamente;
- placeholder não é usado como único rótulo;
- campos obrigatórios são identificados;
- mensagens de erro são claras;
- erros são associados aos campos quando possível;
- inputs usam tipos adequados;
- campos possuem `autocomplete` quando aplicável.

### Botões e links

Validar se:

- botões possuem texto acessível;
- ícones clicáveis possuem `aria-label` quando não há texto visível;
- links descrevem o destino ou ação;
- não há links genéricos sem contexto.

### Imagens, ícones e SVGs

Verificar se:

- imagens informativas possuem `alt` descritivo;
- imagens decorativas usam `alt=""`;
- SVGs decorativos usam `aria-hidden="true"`;
- SVGs funcionais possuem rótulo acessível.

### Cores e contraste

Validar se:

- texto e fundo possuem contraste adequado;
- informação não depende apenas de cor;
- estados de erro, sucesso ou alerta possuem texto, ícone ou reforço além da cor.

### Tabelas

Verificar se:

- tabelas reais usam estrutura de tabela;
- cabeçalhos usam `th`;
- cabeçalhos possuem `scope` quando aplicável;
- a leitura por tecnologia assistiva mantém sentido.

### Modais, menus e overlays

Validar se:

- foco é controlado ao abrir e fechar;
- é possível fechar com `Esc`, quando aplicável;
- há rótulo acessível;
- foco não vai para conteúdo atrás do modal;
- foco retorna ao elemento que abriu o modal.

### Movimento e animação

Verificar se:

- animações não prejudicam leitura ou navegação;
- transições intensas respeitam `prefers-reduced-motion`;
- não há autoplay intrusivo sem controle.

### Responsividade e zoom

Validar se:

- a interface continua utilizável com zoom;
- conteúdo não fica cortado sem alternativa;
- campos e botões continuam acessíveis em telas menores;
- textos não dependem de tamanho fixo que prejudique leitura.

---

## Processo recomendado

1. Identificar elementos interativos.
2. Verificar semântica HTML.
3. Validar navegação por teclado e foco.
4. Revisar formulários e mensagens de erro.
5. Revisar tabelas, modais, menus e componentes especiais.
6. Verificar contraste, texto alternativo e uso de ARIA.
7. Propor ajustes mínimos e seguros.
8. Informar riscos restantes.

---

## Formato de resposta esperado

## Resumo

O que foi analisado.

## Problemas encontrados

Lista objetiva dos pontos de acessibilidade.

## Correções sugeridas ou aplicadas

Ajustes realizados ou recomendados.

## Validações realizadas

Testes manuais ou automatizados executados.

## Riscos restantes

Pontos que ainda precisam de validação manual.
