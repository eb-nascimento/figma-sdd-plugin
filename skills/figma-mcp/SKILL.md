---
name: figma-mcp
description: Use esta skill para auditar arquivos Figma e orientar agentes de IA/Codex/VS Code/Cursor na geração de código com MCP, priorizando fidelidade visual, reutilização de componentes, tokens, acessibilidade, preservação de funcionalidades, controle de assets, confirmação de stack, estrutura escalável, QA visual bloqueante e atualização do SDD.
---

# Skill: Figma MCP

## Objetivo

Usar o Figma MCP como fonte estruturada para implementar, revisar ou auditar interfaces com fidelidade visual, segurança de arquitetura e controle de assets.

A skill deve orientar o agente a:

- interpretar frames, componentes, variantes, tokens, auto layout, estilos, espaçamentos, assets e fluxos;
- confirmar a stack antes de gerar ou alterar código;
- preservar funcionalidades existentes durante ajustes futuros;
- organizar o projeto em estrutura escalável;
- preservar logos, marcas, ícones oficiais e textos reais;
- tratar menus, carrosséis, sliders, galerias, hero slideshow e demais componentes interativos como comportamento real;
- baixar, renomear, separar e limpar assets com critério;
- executar QA visual real e validação técnica;
- atualizar SDD, README ou documentação aplicável quando houver decisão técnica, alteração estrutural, mudança de assets ou comportamento implementado.

Não usar esta skill para redesenhar por preferência própria. O Figma é a referência visual e estrutural, salvo decisão explícita do usuário.

## Quando usar

Use esta skill quando a tarefa envolver:

- implementar telas, seções ou componentes a partir de um link do Figma;
- auditar se um arquivo Figma está pronto para implementação com IA;
- converter layout Figma em frontend;
- comparar implementação existente com o design;
- ajustar código já gerado a partir do Figma;
- revisar fidelidade visual, responsividade, estados, assets e componentes;
- identificar e implementar menus, carrosséis, sliders, galerias, hero slideshow, abas, modais e dropdowns;
- definir quais assets devem ser baixados, renomeados, movidos ou excluídos;
- preservar logos, marcas, ícones sociais e identidade visual em toda a página;
- organizar estrutura de pastas de páginas, componentes, estilos, assets, serviços e utilitários;
- atualizar SDD, README ou documentação de handoff técnico.

## Regras obrigatórias

### Frames de especificação de componentes e estados

- Quando o link do Figma apontar para um trecho com botões, hovers, variações, cards isolados, inputs, ícones ou componentes soltos, o agente deve tratar o frame como especificação de componente, não como tela final.
- O agente não deve deduzir contexto, fluxo, texto final, posicionamento em página ou comportamento não mostrado no Figma.
- Antes de implementar, identificar se o node representa:
  - tela final;
  - seção de página;
  - componente isolado;
  - biblioteca de componentes;
  - variações/estados de componente;
  - documentação visual de design system.
- Se o frame representar botões e hovers, mapear todos os estados visuais antes de codificar:
  - default;
  - hover;
  - active/pressed;
  - focus;
  - disabled;
  - loading;
  - selected;
  - variações por cor, tamanho, ícone ou hierarquia.
- Estados mostrados visualmente no Figma devem virar estados reais no código, por exemplo `:hover`, `:focus`, `:disabled`, classes, props ou variantes do componente, conforme a stack.
- Não criar botões com estilos aproximados se o Figma mostra variações explícitas.
- Não inventar cor, borda, raio, sombra, tamanho, padding, fonte ou transição.
- Não transformar hovers em elementos estáticos duplicados na tela.
- Se o Figma mostra apenas a documentação do hover, implementar o hover como estado do componente, não como botão separado na interface final.
- Se houver dúvida se o frame é uma tela ou uma especificação de componente, perguntar antes de implementar.

### Stack e escopo

- Confirmar linguagem, framework ou stack antes de gerar ou alterar código.
- Não assumir React, Next.js, Vue, Angular, Flutter, HTML/CSS, Tailwind ou outra tecnologia apenas pelo Figma ou pelo repositório.
- Se o usuário já informou a stack na mesma solicitação ou no contexto direto da tarefa, seguir sem perguntar novamente.
- Trabalhar com o menor escopo possível: frame, seção, componente ou seleção específica.
- Não interpretar o arquivo Figma inteiro quando o pedido aponta para um frame ou nó específico.
- Validar que o link informado aponta para frame, seção ou componente rastreável.

Pergunta obrigatória quando a stack não estiver definida:

```text
Antes de implementar, em qual linguagem, framework ou stack você deseja escrever essa tela? Ex.: React, Next.js, Vue, Angular, Flutter, HTML/CSS, Tailwind ou outra.
```

### Preservação de funcionalidades existentes

- Preservar funcionalidades existentes em ajustes futuros.
- Não remover rotas, componentes, estados, validações, assets, estilos, integrações ou interações sem autorização explícita.
- Não substituir uma implementação funcional por uma versão mais simples que perca comportamento.
- Não alterar fluxos não relacionados ao pedido atual.
- Antes de alterar código existente, identificar comportamento atual, arquivos impactados, partes que devem ser preservadas e risco de regressão.
- Aplicar mudanças incrementais e controladas.
- Comparar comportamento anterior e posterior quando aplicável.
- Registrar no SDD remoções autorizadas, preservações relevantes e mudanças de comportamento.

### Estrutura do projeto

- Verificar a estrutura atual do repositório antes de criar arquivos.
- Não criar `index.html`, `style.css`, `script.js`, `main.js`, `app.js`, `styles.css` ou equivalentes soltos na raiz, salvo protótipo simples explicitamente solicitado.
- Organizar o projeto em estrutura escalável quando houver potencial de crescimento.
- Separar páginas, componentes, estilos, assets, serviços e utilitários.
- Seguir convenções da stack escolhida e padrões já existentes no repositório.
- Evitar concentrar toda a implementação em um único arquivo quando a tecnologia permite separação.
- Não criar arquitetura paralela sem justificar e documentar.

Estrutura de referência, adaptável à stack:

```text
src/
  pages/
  components/
  styles/
  services/
  utils/
assets/
  img/
  svg/
docs/
```

### Fidelidade visual e textos reais

- Preservar fidelidade visual ao Figma em textos, botões, logos, cores, espaçamentos, alinhamentos, bordas, sombras, ícones, imagens e hierarquia visual.
- Não inventar melhorias visuais, textos, botões, cores, ícones, espaçamentos, ordem dos elementos ou hierarquia visual.
- Textos visíveis no Figma devem ser implementados como texto real e visível no DOM, salvo quando forem parte inseparável de imagem institucional.
- Não criar textos invisíveis, fora da tela, com `opacity: 0`, `visibility: hidden`, `display: none`, `color: transparent`, `font-size: 0`, z-index incorreto ou posicionamento absoluto indevido para simular layout.
- Textos só podem ficar visualmente ocultos quando forem elementos de acessibilidade, como `sr-only`, e isso deve ser intencional.
- Se uma imagem/screenshot representar área com textos, menus ou links, sinalizar risco e preferir reconstrução com componentes reais.
- Quando não for possível reproduzir exatamente o Figma, registrar a limitação e propor a alternativa mais fiel.
- Classificar divergências como críticas, importantes ou cosméticas durante revisão.

### Menus, dropdowns e navegação

- Não implementar menus, dropdowns, listas ou blocos de navegação como screenshot/imagem quando textos e itens devem ser elementos reais de HTML/componente.
- Menus, dropdowns e navegações devem preservar comportamento, legibilidade, foco, hover, clique e acessibilidade por teclado quando aplicável.
- Links visíveis devem ser clicáveis ou ter limitação documentada.
- Não sobrepor textos invisíveis em cima de screenshot para simular navegação.
- Durante QA, verificar textos renderizados fora do container, invisíveis, cortados ou sobrepostos a screenshots/assets.

### Logos, marcas e ícones oficiais

- Preservar logos, marcas, assinaturas visuais, ícones sociais e elementos institucionais como assets ou componentes visuais, preferencialmente SVG.
- Aplicar essa regra à página inteira: header, footer, sidebar, menus, hero, cards, modais, estados vazios, telas de erro e demais seções.
- Não converter logos institucionais em texto HTML/CSS.
- Não substituir logo ou ícone social por texto, emoji, fonte aproximada ou biblioteca visualmente diferente do Figma sem confirmação.
- Não alterar proporção, cor, espaçamento ou composição da marca.
- Reutilizar o mesmo asset quando a mesma marca aparece em mais de uma seção.
- Tratar como marca qualquer elemento visual institucional com dúvida razoável.
- Fazer inventário de logos antes de implementar ou revisar: local, nome, formato esperado, implementação correta, nome sugerido do asset e dúvidas.

### Botões com SVG e redes sociais

- Ícones de redes sociais devem ser tratados como assets de marca ou ícones oficiais, preferencialmente SVG.
- SVGs de redes sociais devem ficar centralizados dentro do botão/link.
- O botão/link deve usar alinhamento consistente, como `display: flex`, `align-items: center` e `justify-content: center`, ou equivalente na stack.
- Validar tamanho do botão, área clicável, `viewBox`, largura/altura do SVG, alinhamento vertical, foco, hover e cursor.
- Links/botões sociais devem ter `aria-label` ou alternativa acessível equivalente.
- Quando o ícone for clicável, deve haver `cursor: pointer` ou comportamento visual equivalente.
- Não deixar SVG deslocado, desalinhado, cortado ou com escala inconsistente dentro do botão.

### Componentes interativos

- Identificar componentes interativos antes de implementar.
- Tratar carrosséis, sliders, galerias, hero slideshow, menus, dropdowns, abas, accordions, modais, cards clicáveis, paginações, steps, formulários multi-etapa e banners rotativos como comportamento real.
- Quando houver setas, dots, overflow horizontal, cards parcialmente visíveis, sequência de imagens/cards ou frames similares, tratar como indício de carrossel/slider/slideshow.
- Mapear itens, quantidade visível, controles, estados, responsividade, teclado e mobile antes de codificar.
- Perguntar o comportamento esperado quando carrossel, slider, galeria ou slideshow não estiver claro no Figma.
- Não empilhar, duplicar ou sobrepor itens que deveriam navegar horizontalmente.
- Não adicionar autoplay, loop ou biblioteca externa sem confirmação ou padrão existente no projeto.

Pergunta recomendada quando o comportamento não estiver claro:

```text
Esse bloco deve funcionar como carrossel/slider/slideshow? Se sim, deve ter setas, dots, autoplay, loop, swipe no mobile ou apenas navegação manual?
```

### Carrossel, slider e estado ativo

- Carrosséis e sliders devem preservar estrutura e estilização completa dos estados.
- Se o item central/ativo aparece maior no Figma, a escala deve depender do estado ativo atual, não ficar fixa em um item específico.
- Ao navegar, o item que sai do centro deve voltar ao estilo inativo, e o novo item central deve receber o estilo ativo.
- Mapear e implementar estados ativo, inativo, anterior, próximo, hover, focus e disabled quando existirem ou forem necessários.
- Preservar transições, escala, opacidade, sombra, z-index, espaçamento, alinhamento, largura dos cards, overflow e responsividade conforme o Figma.
- Controles, cards clicáveis, setas e indicadores devem ter cursor/pointer quando forem interativos.
- Não implementar carrossel como lista estática, imagens sobrepostas ou cards empilhados.
- Não deixar todos os slides com estilo ativo ou tamanho grande.
- Não deixar o item ativo permanente após navegação.
- Validar o carrossel navegando para frente e para trás durante QA visual.
- Documentar no SDD item ativo, quantidade visível, navegação, responsividade e estados.

### Hero slideshow

- Avaliar se o Hero inicial representa slideshow, carrossel de banners ou banner rotativo.
- Indícios incluem múltiplas imagens de hero, dots, setas, variações de banner, frames similares, estados de navegação, textos sobre imagens ou sequência horizontal/temporal.
- Não implementar o Hero automaticamente como bloco estático quando houver indícios de slideshow.
- Antes de implementar, mapear quantidade de slides, asset de cada slide, título, subtítulo, CTA, links, dots, setas, autoplay, duração, transição, loop, mobile e acessibilidade por teclado.
- Se o Figma indicar slideshow, implementar comportamento real, não apenas o primeiro slide estático.
- Validar o Hero navegando entre slides durante QA visual.
- Registrar o comportamento do Hero slideshow no SDD.

Pergunta recomendada quando o Hero não estiver claro:

```text
O Hero inicial deve funcionar como slideshow? Se sim, deve ter autoplay, dots, setas, loop, transição automática ou apenas navegação manual?
```

### Assets

- Baixar assets apenas quando necessário: fotos, ilustrações, logos, ícones SVG, imagens institucionais ou visuais que não possam ser reproduzidos com código.
- Não baixar fundos, containers, cards, botões, inputs, sombras, bordas, gradientes simples, shapes simples ou seções inteiras como imagem quando puderem ser reproduzidos em código.
- Antes de baixar, listar os assets necessários e justificar cada um.
- Separar assets por tipo: SVGs em `assets/svg/`; PNG, JPG, JPEG, WEBP, GIF, AVIF e similares em `assets/img/`.
- Não deixar assets soltos diretamente em `assets/`.
- Renomear assets com nomes semânticos, curtos e em kebab-case.
- Excluir somente assets claramente não utilizados.
- Não excluir assets com uso incerto.
- Não excluir logos, ícones institucionais, imagens públicas ou assets compartilhados sem confirmar uso.
- Atualizar imports, caminhos, CSS, JSON, componentes, páginas e documentação após mover ou renomear assets.
- Registrar no SDD assets baixados, renomeados, movidos, preservados ou excluídos.

### QA visual bloqueante

- Fazer QA visual real, não apenas gerar screenshot.
- Analisar screenshots e DOM/renderização.
- Validar desktop e mobile quando aplicável.
- Verificar textos invisíveis, fora do container, cortados, sobrepostos ou escondidos indevidamente.
- Verificar se menus/dropdowns/navegações não foram implementados como screenshot quando deveriam ser componentes.
- Verificar centralização de SVGs em botões sociais.
- Navegar carrosséis, sliders e slideshows para validar estados.
- Confirmar que o item ativo do carrossel muda corretamente.
- Confirmar que o Hero slideshow não ficou estático quando deveria ser interativo.
- Tratar como bloqueantes: sobreposição indevida, texto cortado, elemento oculto, botão desalinhado, item ativo incorreto, z-index incorreto, overflow indevido, logo como texto ou diferença evidente em relação ao Figma.
- Validar especialmente elementos com `position: absolute`, `z-index`, `overflow`, overlays e assets exportados pelo MCP.
- Não finalizar a tarefa se houver erro visual evidente.

### Documentação

- Atualizar SDD, README ou documentação aplicável quando houver decisão técnica, alteração de estrutura, alteração de assets, comportamento implementado, componente interativo definido ou divergência conhecida em relação ao Figma.
- Documentar limitações do Figma, suposições, assets não exportáveis e divergências aceitas.
- Documentar comportamento de carrosséis, sliders e Hero slideshow, incluindo item ativo, quantidade visível, navegação, responsividade e estados.
- Não tratar a tarefa como concluída se a documentação obrigatória ficou desatualizada.

## Fluxo obrigatório com Figma MCP

### 1. Entendimento do frame/seleção Figma

- Abrir o link via MCP.
- Confirmar que o escopo é específico e rastreável.
- Identificar frames, seções, componentes, textos, estilos, tokens, imagens, estados e fluxos.
- Preferir o menor nó possível para evitar contexto excessivo.

### 2. Confirmação da stack

- Confirmar linguagem, framework e estratégia de estilo antes de gerar ou alterar código.
- Se a stack já estiver definida no pedido/contexto, registrar a stack usada e seguir.

### 3. Auditoria do Figma

- Avaliar nomes, auto layout, componentes, variantes, tokens, responsividade, acessibilidade, interações e handoff.
- Classificar como pronto, parcialmente pronto ou risco alto.
- Sinalizar lacunas que impactam implementação.

### 4. Identificação de componentes interativos

- Mapear menus/dropdowns com textos reais, carrosséis, sliders, galerias, Hero slideshow, botões sociais com SVG centralizado, abas, modais, steps, filtros e formulários.
- Mapear carrossel com estado ativo dinâmico quando houver item central/destaque.
- Perguntar comportamento esperado quando o Figma não definir interação.
- Registrar estados e responsividade esperados.

### 5. Planejamento da estrutura do projeto

- Ler a estrutura atual do repositório.
- Reutilizar padrões, componentes, helpers e tokens existentes.
- Definir arquivos afetados, novos componentes, páginas, estilos e utilitários.
- Planejar mudanças incrementais preservando funcionalidades atuais.

### 6. Inventário de assets e logos

- Listar logos, marcas e ícones oficiais na página inteira.
- Listar fotos, ilustrações, ícones e demais assets realmente necessários.
- Definir nome semântico e pasta de destino para cada asset.
- Indicar assets que serão reproduzidos em código.

### 7. Implementação incremental

- Implementar respeitando a stack, arquitetura e fidelidade visual.
- Reutilizar componentes existentes antes de criar novos.
- Não remover funcionalidades fora do escopo.
- Evitar alterações globais sem justificar impacto.
- Registrar decisões no SDD conforme necessário.

### 8. Limpeza/organização de assets

- Separar SVGs em `assets/svg/` e imagens raster em `assets/img/`.
- Renomear assets usados em kebab-case.
- Atualizar imports e referências.
- Excluir apenas arquivos claramente não utilizados.
- Preservar assets com uso incerto.

### 9. QA visual bloqueante

- Gerar screenshots quando aplicável.
- Revisar visualmente os screenshots e a renderização.
- Verificar textos invisíveis, menus como screenshot, SVG social centralizado, carrossel ativo dinâmico, navegação de carrosséis/slideshows, overflow, z-index, responsividade, botões, cards, logos e assets.
- Comparar com o Figma e classificar divergências.
- Corrigir bloqueantes antes de finalizar.

### 10. Validação técnica e atualização do SDD

- Rodar validações disponíveis: build, lint, testes, typecheck ou checagem equivalente.
- Verificar console quando houver frontend renderizado.
- Atualizar SDD, README ou documentação aplicável.
- Reportar arquivos alterados, assets movidos/renomeados/excluídos, validações executadas e pendências.

## Prompts recomendados essenciais

### 1. Auditar Figma antes de implementar

```text
Use o Figma MCP para analisar este frame: <URL_DO_FRAME>.
Avalie se está pronto para implementação considerando escopo, nomes, auto layout, componentes, variantes, tokens, responsividade, acessibilidade, logos, assets, menus, textos reais e componentes interativos.
Classifique como pronto, parcialmente pronto ou risco alto.
Liste apenas lacunas que impactam implementação.
Não altere código ainda.
```

### 2. Implementar tela com controle de qualidade

```text
Use o Figma MCP para implementar este frame: <URL_DO_FRAME>.
Antes de alterar código, confirme a stack se ela ainda não estiver definida.
Preserve funcionalidades existentes, siga a estrutura do projeto, identifique componentes interativos, inventarie logos/assets e baixe apenas o necessário.
Implemente menus/dropdowns como componentes reais com textos visíveis no DOM, não como screenshots.
Trate carrosséis/sliders com estado ativo dinâmico e avalie Hero slideshow quando indicado pelo Figma.
Organize assets em assets/svg/ e assets/img/, com nomes semânticos em kebab-case; use SVGs centralizados para botões sociais.
Implemente de forma incremental, mantendo fidelidade visual ao Figma.
Execute QA visual real navegando carrosséis/slideshows, valide estados e atualize o SDD.
```

### 3. Revisar fidelidade visual e QA bloqueante

```text
Compare a implementação atual com o frame Figma: <URL_DO_FRAME>.
Analise screenshots e DOM/renderização; não considere screenshot gerado como validação suficiente.
Verifique logos, textos visíveis, menus/dropdowns como componentes reais, botões, SVGs sociais centralizados, ícones, cores, espaçamentos, alinhamentos, imagens, cards, interações, z-index, overflow, position absolute e responsividade.
Navegue carrosséis/sliders/slideshows para validar item ativo dinâmico, estados, setas, dots, hover, focus e responsividade.
Classifique problemas em críticos, importantes e cosméticos.
Corrija apenas divergências objetivas em relação ao Figma e não finalize se houver erro visual evidente.
Atualize o SDD com correções, comportamento interativo, limitações e pendências.
```

### 4. Limpar, separar e renomear assets

```text
Revise os assets do projeto.
Identifique usados, não usados e incertos.
Mova SVGs para assets/svg/ e imagens raster para assets/img/.
Renomeie assets usados com nomes semânticos em kebab-case e atualize imports/referências.
Preserve logos, ícones sociais, marcas e arquivos com uso incerto; exclua somente assets claramente não utilizados.
Execute validações disponíveis e atualize o SDD com arquivos movidos, renomeados ou excluídos.
```

### 5. Ajustar sem remover funcionalidades existentes

```text
Ajuste a implementação atual conforme este pedido: <DESCREVER_PEDIDO>.
Antes de alterar, identifique comportamento existente, arquivos afetados, componentes, estados, rotas, validações, assets e interações que devem ser preservados.
Não remova nem simplifique funcionalidades sem autorização explícita.
Faça mudanças incrementais, valide regressões, execute QA visual quando houver UI e atualize o SDD com decisões e impactos.
```

## Critérios de aceite

A skill foi seguida corretamente quando:

- O escopo do Figma foi específico e rastreável.
- A stack foi confirmada ou já estava claramente definida.
- A estrutura do repositório foi analisada antes de criar ou mover arquivos.
- Arquivos soltos na raiz foram evitados, salvo protótipo simples solicitado.
- Funcionalidades existentes foram preservadas.
- Nenhuma rota, componente, estado, validação, asset ou interação foi removida sem autorização explícita.
- Componentes interativos foram identificados e tiveram comportamento definido ou confirmado.
- Menus, dropdowns e navegações com texto visível foram implementados como componentes reais, não como screenshots.
- Não existem textos invisíveis, deslocados ou escondidos indevidamente ao lado de imagens ou menus.
- Carrosséis possuem estado ativo dinâmico; o item central fica destacado apenas enquanto está ativo.
- A navegação do carrossel foi validada para frente e para trás.
- O Hero inicial foi avaliado como possível slideshow e implementado como slideshow quando indicado pelo Figma.
- Slideshow e carrosséis tiveram comportamento documentado no SDD.
- Logos e marcas da página inteira foram preservados como assets/componente visual.
- Nenhuma logo institucional foi recriada como texto HTML/CSS.
- Ícones SVG de redes sociais estão centralizados nos botões, com área clicável correta, cursor/pointer e acessibilidade.
- Assets foram baixados apenas quando necessários e separados em `assets/svg/` e `assets/img/`.
- Não restaram assets soltos diretamente em `assets/`.
- Assets usados foram renomeados em kebab-case e referências foram atualizadas.
- Apenas assets claramente não utilizados foram excluídos.
- QA visual real foi executado e analisado.
- Não há sobreposição indevida, texto cortado, elemento oculto, overflow, z-index incorreto ou erro visual evidente.
- Validações técnicas disponíveis foram executadas ou a impossibilidade foi reportada.
- SDD, README ou documentação aplicável foi atualizada.
- Divergências, limitações e suposições foram registradas.
- Frames de especificação de componentes foram tratados como componentes/estados, não como telas finais.
- Estados de botão exibidos no Figma foram implementados como estados reais no código.
- Hovers não foram implementados como elementos estáticos duplicados.
- Nenhum estilo de botão foi deduzido quando havia variação explícita no Figma.
- O agente tratou um frame de botões/hover como tela final.
- O hover foi implementado como outro botão estático.
- Estados de botão foram ignorados ou aproximados.
- O agente inventou estilos de botão não presentes no Figma.

## Sinais de alerta

Interrompa, sinalize risco ou peça confirmação quando encontrar:

- Stack não informada.
- Link Figma genérico ou escopo amplo demais.
- Pedido que pode remover ou simplificar funcionalidade existente.
- Criação de `index.html`, `style.css`, `script.js` ou equivalentes soltos na raiz sem protótipo simples solicitado.
- Layout sendo alterado por preferência própria.
- Textos, botões, cores, ícones, espaçamentos ou hierarquia visual divergindo do Figma sem autorização.
- Menu ou dropdown implementado como screenshot/imagem.
- Textos invisíveis, fora da tela, com `opacity: 0`, `visibility: hidden`, `color: transparent` ou posicionamento indevido.
- Logo institucional implementada como texto ou fonte aproximada.
- Logo do footer, sidebar, card ou outra seção ignorada.
- Botões de redes sociais com SVG desalinhado, cortado ou fora do centro.
- Ícones sociais substituídos por biblioteca, fonte ou emoji visualmente diferente do Figma.
- Assets com uso incerto marcados para exclusão.
- SVGs e imagens raster misturados na mesma pasta.
- Assets soltos diretamente em `assets/`.
- Imports não atualizados após mover ou renomear assets.
- Seções inteiras, cards, sombras, botões ou fundos simples exportados como imagem sem necessidade.
- Carrossel, slider ou galeria implementado como bloco estático.
- Carrossel mantém sempre o mesmo item grande após navegação.
- Todos os cards do carrossel ficam grandes ou ativos ao mesmo tempo.
- Carrossel não possui cursor/pointer em elementos clicáveis.
- Setas, dots, cards parcialmente visíveis ou overflow horizontal ignorados.
- Autoplay, loop ou biblioteca externa adicionados sem confirmação ou padrão do projeto.
- Hero com indícios de slideshow implementado como imagem estática.
- Slideshow não validado navegando entre slides.
- Elementos com `position: absolute`, `z-index` ou `overflow` sem QA visual.
- Screenshot gerado, mas não analisado.
- Imagens, cards, textos ou botões ocupando o mesmo espaço indevidamente.
- Texto cortado, elemento oculto, botão desalinhado ou container com tamanho incorreto.
- Build, lint, teste ou validação aplicável não executado sem justificativa.
- SDD ou documentação aplicável desatualizada após mudança técnica.

## Resultado esperado

Ao final de uma tarefa usando esta skill, entregar de forma objetiva:

- stack utilizada ou confirmada;
- escopo Figma analisado;
- estrutura de pastas usada ou alterada;
- arquivos criados, alterados e removidos;
- funcionalidades preservadas e riscos de regressão verificados;
- componentes interativos identificados e comportamento definido;
- inventário de logos/marcas/ícones oficiais relevantes;
- assets baixados, movidos, renomeados, preservados ou excluídos;
- confirmação de separação `assets/svg/` e `assets/img/` quando houver assets;
- validação visual realizada, screenshots analisados e problemas encontrados;
- validação de menus/textos reais, SVGs sociais, carrosséis e Hero slideshow quando aplicável;
- validações técnicas executadas;
- divergências, limitações e suposições documentadas;
- SDD, README ou documentação aplicável atualizada;
- pendências ou próximos passos, se existirem.
