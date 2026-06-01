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
- preservar logos e marcas como assets;
- tratar componentes interativos como comportamento real, não como imagem estática;
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
- identificar e implementar componentes interativos, como carrosséis, sliders, galerias, abas, modais e menus;
- definir quais assets devem ser baixados, renomeados, movidos ou excluídos;
- preservar logos, marcas e identidade visual em toda a página;
- organizar estrutura de pastas de páginas, componentes, estilos, assets, serviços e utilitários;
- atualizar SDD, README ou documentação de handoff técnico.

## Regras obrigatórias

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
- Não editar linha por linha; aplicar alterações em bloco único/consolidado, preservando o comportamento existente e evitando reescritas desnecessárias.

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

### Fidelidade visual

- Preservar fidelidade visual ao Figma em textos, botões, logos, cores, espaçamentos, alinhamentos, bordas, sombras, ícones, imagens e hierarquia visual.
- Não inventar melhorias visuais, textos, botões, cores, ícones, espaçamentos, ordem dos elementos ou hierarquia visual.
- Não reinterpretar elementos visuais sem autorização explícita.
- Adaptar tecnicamente à stack escolhida sem alterar a intenção visual do layout.
- Quando não for possível reproduzir exatamente o Figma, registrar a limitação e propor a alternativa mais fiel.
- Classificar divergências como críticas, importantes ou cosméticas durante revisão.
- Corrigir apenas divergências objetivas em relação ao Figma, salvo pedido explícito de redesign.

### Logos e marcas

- Preservar logos, marcas, assinaturas visuais e elementos institucionais como assets ou componentes visuais, preferencialmente SVG.
- Aplicar essa regra à página inteira: header, footer, sidebar, menus, hero, cards, modais, estados vazios, telas de erro e demais seções.
- Não converter logos institucionais em texto HTML/CSS.
- Não substituir logo por fonte aproximada.
- Não alterar proporção, cor, espaçamento ou composição da marca.
- Reutilizar o mesmo asset quando a mesma marca aparece em mais de uma seção.
- Tratar como marca qualquer elemento visual institucional com dúvida razoável.
- Fazer inventário de logos antes de implementar ou revisar:
  - local da ocorrência;
  - nome visual/institucional;
  - formato esperado;
  - forma correta de implementação;
  - nome sugerido do asset;
  - dúvidas ou limitações.

### Componentes interativos

- Identificar componentes interativos antes de implementar.
- Tratar carrosséis, sliders e galerias como componentes interativos, não como blocos estáticos.
- Verificar também abas, accordions, menus dropdown, modais, cards clicáveis, paginações, steps, formulários multi-etapa e banners rotativos.
- Quando houver setas, dots, overflow horizontal, cards parcialmente visíveis ou sequência de imagens/cards, tratar como indício de carrossel/slider/galeria.
- Mapear itens, quantidade visível, controles, estados, responsividade, teclado e mobile antes de codificar.
- Perguntar o comportamento esperado quando carrossel, slider ou galeria não estiver claro no Figma.
- Não empilhar, duplicar ou sobrepor itens que deveriam navegar horizontalmente.
- Não adicionar autoplay, loop ou biblioteca externa sem confirmação ou padrão existente no projeto.

Pergunta recomendada quando o comportamento não estiver claro:

```text
Esse bloco deve funcionar como carrossel/slider? Se sim, deve ter setas, dots, autoplay, loop, swipe no mobile ou apenas rolagem horizontal?
```

### Assets

- Baixar assets apenas quando necessário: fotos, ilustrações, logos, ícones SVG, imagens institucionais ou visuais que não possam ser reproduzidos com código.
- Não baixar fundos, containers, cards, botões, inputs, sombras, bordas, gradientes simples, shapes simples ou seções inteiras como imagem quando puderem ser reproduzidos em código.
- Antes de baixar, listar os assets necessários e justificar cada um.
- Separar assets por tipo:
  - SVGs em `assets/svg/`;
  - PNG, JPG, JPEG, WEBP, GIF, AVIF e similares em `assets/img/`.
- Não deixar assets soltos diretamente em `assets/`.
- Renomear assets com nomes semânticos, curtos e em kebab-case.
- Evitar nomes genéricos como `image-1`, `rectangle`, `frame`, `asset`, `vector`, `group`.
- Excluir somente assets claramente não utilizados.
- Não excluir assets com uso incerto.
- Não excluir logos, ícones institucionais, imagens públicas ou assets compartilhados sem confirmar uso.
- Atualizar imports, caminhos, CSS, JSON, componentes, páginas e documentação após mover ou renomear assets.
- Registrar no SDD assets baixados, renomeados, movidos, preservados ou excluídos.

### QA visual bloqueante

- Fazer QA visual real, não apenas gerar screenshot.
- Analisar screenshots e DOM/renderização.
- Validar desktop e mobile quando aplicável.
- Tratar como bloqueantes:
  - imagens sobrepostas indevidamente;
  - textos cortados, ilegíveis, ocultos ou fora do container;
  - botões desalinhados, cortados ou com texto incorreto;
  - elementos fora da tela;
  - cards empilhados incorretamente;
  - imagens duplicadas no mesmo espaço visual;
  - ícones fora de posição;
  - conteúdo oculto por z-index incorreto;
  - overflow indevido;
  - containers com altura/largura incorreta;
  - quebra visual evidente em responsividade;
  - logos recriadas como texto;
  - diferença evidente em relação ao Figma.
- Validar especialmente elementos com `position: absolute`, `z-index`, `overflow`, overlays e assets exportados pelo MCP.
- Não finalizar a tarefa se houver erro visual evidente.
- Declarar explicitamente se há ou não sobreposição, texto cortado, elementos ocultos e divergências críticas.

### Documentação

- Atualizar SDD, README ou documentação aplicável quando houver:
  - decisão técnica;
  - alteração de estrutura;
  - alteração de assets;
  - comportamento implementado;
  - componente interativo definido;
  - divergência conhecida em relação ao Figma;
  - remoção ou preservação relevante de funcionalidade.
- Documentar limitações do Figma, suposições, assets não exportáveis e divergências aceitas.
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

- Avaliar nomes de frames/camadas, auto layout, componentes, variantes, tokens, responsividade, acessibilidade e handoff.
- Classificar como pronto, parcialmente pronto ou risco alto.
- Sinalizar lacunas que impactam implementação.

### 4. Identificação de componentes interativos

- Mapear carrosséis, sliders, galerias, abas, modais, menus, steps, filtros e formulários.
- Perguntar comportamento esperado quando o Figma não definir interação.
- Registrar estados e responsividade esperados.

### 5. Planejamento da estrutura do projeto

- Ler a estrutura atual do repositório.
- Reutilizar padrões, componentes, helpers e tokens existentes.
- Definir arquivos afetados, novos componentes, páginas, estilos e utilitários.
- Planejar mudanças incrementais preservando funcionalidades atuais.

### 6. Inventário de assets e logos

- Listar logos e marcas na página inteira.
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
- Verificar sobreposição, cortes, overflow, z-index, responsividade, botões, textos, cards, logos e assets.
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
Avalie se está pronto para implementação considerando escopo, nomes, auto layout, componentes, variantes, tokens, responsividade, acessibilidade, logos, assets e componentes interativos.
Classifique como pronto, parcialmente pronto ou risco alto.
Liste apenas lacunas que impactam implementação.
Não altere código ainda.
```

### 2. Implementar tela com controle de qualidade

```text
Use o Figma MCP para implementar este frame: <URL_DO_FRAME>.
Antes de alterar código, confirme a stack se ela ainda não estiver definida.
Preserve funcionalidades existentes, siga a estrutura do projeto, identifique componentes interativos, inventarie logos/assets e baixe apenas o necessário.
Organize assets em assets/svg/ e assets/img/, com nomes semânticos em kebab-case.
Implemente de forma incremental, mantendo fidelidade visual ao Figma.
Execute QA visual real, validações técnicas disponíveis e atualize o SDD.
```

### 3. Revisar fidelidade visual e QA bloqueante

```text
Compare a implementação atual com o frame Figma: <URL_DO_FRAME>.
Analise screenshots e DOM/renderização; não considere screenshot gerado como validação suficiente.
Verifique logos, textos, botões, ícones, cores, espaçamentos, alinhamentos, imagens, cards, interações, z-index, overflow, position absolute e responsividade.
Classifique problemas em críticos, importantes e cosméticos.
Corrija apenas divergências objetivas em relação ao Figma e não finalize se houver erro visual evidente.
Atualize o SDD com correções, limitações e pendências.
```

### 4. Limpar, separar e renomear assets

```text
Revise os assets do projeto.
Identifique usados, não usados e incertos.
Mova SVGs para assets/svg/ e imagens raster para assets/img/.
Renomeie assets usados com nomes semânticos em kebab-case e atualize imports/referências.
Exclua somente assets claramente não utilizados; preserve logos, marcas e arquivos com uso incerto.
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
- A implementação ficou organizada em páginas, componentes, estilos, assets, serviços e utilitários quando aplicável.
- Funcionalidades existentes foram preservadas.
- Nenhuma rota, componente, estado, validação, asset ou interação foi removida sem autorização explícita.
- Componentes interativos foram identificados e tiveram comportamento definido ou confirmado.
- Carrosséis, sliders e galerias não foram tratados como blocos estáticos.
- A fidelidade visual ao Figma foi priorizada sem inventar redesign.
- Logos e marcas da página inteira foram preservados como assets/componente visual.
- Nenhuma logo institucional foi recriada como texto HTML/CSS.
- Assets foram baixados apenas quando necessários.
- Fundos, containers, cards, botões, inputs, sombras, bordas e seções inteiras não foram exportados como imagem quando reproduzíveis em código.
- Assets ficaram separados em `assets/svg/` e `assets/img/`.
- Não restaram assets soltos diretamente em `assets/`.
- Assets usados foram renomeados em kebab-case e referências foram atualizadas.
- Apenas assets claramente não utilizados foram excluídos.
- QA visual real foi executado e analisado.
- Não há sobreposição indevida, texto cortado, elemento oculto, overflow, z-index incorreto ou erro visual evidente.
- Validações técnicas disponíveis foram executadas ou a impossibilidade foi reportada.
- SDD, README ou documentação aplicável foi atualizada.
- Divergências, limitações e suposições foram registradas.

## Sinais de alerta

Interrompa, sinalize risco ou peça confirmação quando encontrar:

- Stack não informada.
- Link Figma genérico ou escopo amplo demais.
- Frame com grupos soltos, nomes genéricos, sem tokens, sem estados ou sem responsividade clara.
- Pedido que pode remover ou simplificar funcionalidade existente.
- Necessidade de apagar rotas, componentes, estados, validações, assets ou interações.
- Criação de `index.html`, `style.css`, `script.js` ou equivalentes soltos na raiz sem protótipo simples solicitado.
- Implementação concentrada em arquivo único apesar de potencial de crescimento.
- Layout sendo alterado por preferência própria.
- Textos, botões, cores, ícones, espaçamentos ou hierarquia visual divergindo do Figma sem autorização.
- Logo institucional implementada como texto ou fonte aproximada.
- Logo do footer, sidebar, card ou outra seção ignorada.
- Assets com uso incerto marcados para exclusão.
- SVGs e imagens raster misturados na mesma pasta.
- Assets soltos diretamente em `assets/`.
- Imports não atualizados após mover ou renomear assets.
- Seções inteiras, cards, sombras, botões ou fundos simples exportados como imagem sem necessidade.
- Carrossel, slider ou galeria implementado como bloco estático.
- Setas, dots, cards parcialmente visíveis ou overflow horizontal ignorados.
- Autoplay, loop ou biblioteca externa adicionados sem confirmação ou padrão do projeto.
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
- inventário de logos/marcas relevantes;
- assets baixados, movidos, renomeados, preservados ou excluídos;
- confirmação de separação `assets/svg/` e `assets/img/` quando houver assets;
- validação visual realizada, screenshots analisados e problemas encontrados;
- validações técnicas executadas;
- divergências, limitações e suposições documentadas;
- SDD, README ou documentação aplicável atualizada;
- pendências ou próximos passos, se existirem.
