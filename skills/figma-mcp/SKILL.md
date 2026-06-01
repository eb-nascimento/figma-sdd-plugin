---
name: figma-mcp
description: Use esta skill para auditar arquivos Figma e orientar agentes de IA/Codex/VS Code/Cursor na geração de código com MCP, priorizando fidelidade visual, reutilização de componentes, tokens, acessibilidade, controle de assets, confirmação de linguagem/stack, organização de arquitetura, limpeza de assets e atualização do SDD.
---

# Skill: Figma MCP

## Objetivo

Ajudar o agente a usar o Figma MCP de forma controlada, verificável e aderente ao projeto, evitando geração de código baseada apenas em aparência visual e garantindo que o Figma seja tratado como fonte de contexto estruturado: componentes, variantes, tokens, auto layout, estilos, espaçamentos, assets e fluxos.

A skill também orienta o agente a não assumir automaticamente a linguagem, framework ou stack de implementação, exigindo confirmação prévia do usuário antes de gerar ou alterar código.

Além disso, define regras para organização da estrutura do projeto, controle, limpeza, exclusão e renomeação de assets gerados pelo Figma MCP, evitando que arquivos soltos, fundos, seções inteiras ou imagens desnecessárias sejam mantidos no projeto.

## Quando usar

Use esta skill quando a tarefa envolver:

- Implementar telas a partir de um link do Figma usando MCP.
- Auditar se um arquivo Figma está pronto para uso por agentes de IA.
- Converter layout Figma em código frontend.
- Comparar implementação existente com o design.
- Gerar ou atualizar componentes com base em design system.
- Avaliar consistência entre Figma, código e SDD.
- Criar prompts para Codex, Cursor, VS Code ou outro agente conectado ao Figma MCP.
- Definir quais assets devem ou não ser baixados a partir do Figma.
- Revisar, excluir ou renomear assets gerados automaticamente pelo Figma MCP.
- Organizar a implementação em uma estrutura escalável de páginas, componentes, estilos, assets, serviços e utilitários.

## Pré-requisitos

Antes de implementar qualquer tela, confirme:

- O MCP do Figma está configurado no cliente/agente utilizado.
- O link informado aponta para um frame, seção ou componente específico, não apenas para o arquivo geral.
- O usuário tem permissão adequada no Figma.
- O usuário informou a linguagem, framework ou stack desejada para a implementação.
- O repositório possui padrões de componentes, rotas, estilos, tokens e estrutura de pastas.
- O SDD ou documentação técnica do projeto está disponível ou deve ser atualizado durante a tarefa.


## Regra obrigatória — validação visual real, não apenas screenshot

Após implementar ou revisar uma tela, o agente não deve apenas gerar screenshots. Ele deve analisar os screenshots e o DOM/renderização para identificar problemas visuais objetivos.

São considerados erros bloqueantes:

- imagens sobrepostas indevidamente;
- textos cortados ou ilegíveis;
- botões desalinhados;
- elementos fora da tela;
- cards empilhados incorretamente;
- imagens duplicadas no mesmo espaço visual;
- ícones fora de posição;
- conteúdo oculto por z-index incorreto;
- containers com altura/largura incorreta;
- quebras visuais em responsividade;
- diferenças evidentes em relação ao Figma.

Se o agente gerar screenshots, ele deve revisar visualmente cada tela e declarar explicitamente:

- se há ou não sobreposição de elementos;
- se imagens, botões, textos e cards estão visíveis corretamente;
- se a tela está coerente com o Figma;
- se há divergências críticas, importantes ou cosméticas.

Não considerar a validação concluída apenas porque a página carregou ou porque o screenshot foi gerado.

## Regra obrigatória — detecção de sobreposição de elementos

Durante a revisão visual, o agente deve verificar se há elementos ocupando o mesmo espaço de forma indevida.

A validação deve considerar especialmente:

- imagens;
- logos;
- ilustrações;
- cards;
- botões;
- inputs;
- textos;
- menus;
- modais;
- elementos com `position: absolute`;
- elementos com `z-index`;
- elementos renderizados a partir de assets baixados do Figma MCP.

Quando houver três ou mais imagens, ícones ou elementos visuais próximos, o agente deve verificar se eles estão empilhados intencionalmente ou se houve erro de layout.

Se houver dúvida, tratar como possível erro visual e reportar antes de finalizar.

Sobreposição só deve ser aceita quando estiver claramente prevista no Figma, como em avatares agrupados, badges, overlays, sombras, fundos decorativos ou composições visuais intencionais.


## Regra obrigatória — confirmação da linguagem/stack

Antes de gerar, alterar ou sugerir código, o agente deve sempre perguntar em qual linguagem, framework ou stack o usuário deseja implementar.

O agente não deve assumir automaticamente React, Next.js, Vue, Angular, Flutter, HTML/CSS, Tailwind ou qualquer outra tecnologia apenas com base no Figma, no MCP, na aparência da tela ou em padrões visuais do layout.

A pergunta deve ser feita antes da implementação, mesmo que o projeto pareça indicar uma stack provável.

Exemplo de pergunta obrigatória:

```text
Antes de implementar, em qual linguagem, framework ou stack você deseja escrever essa tela? Ex.: React, Next.js, Vue, Angular, Flutter, HTML/CSS, Tailwind ou outra.
```

Somente após a resposta do usuário o agente pode planejar ou gerar código.

Se o usuário já tiver informado a linguagem, framework ou stack na mesma solicitação, o agente pode seguir sem perguntar novamente.

## Regra obrigatória — organização da estrutura do projeto

Antes de criar arquivos, o agente deve verificar a estrutura atual do repositório e respeitar o padrão existente.

O agente não deve criar arquivos soltos diretamente na raiz do projeto, como:

- `index.html`
- `style.css`
- `script.js`
- `main.js`
- `app.js`
- `styles.css`

Essa abordagem só é permitida quando o usuário solicitar explicitamente um protótipo estático simples, de página única, sem intenção de evolução.

Quando o projeto puder ter mais de uma página, tela, rota ou módulo, o agente deve organizar a implementação em uma estrutura escalável, separando páginas, componentes, estilos, assets, serviços e utilitários.

Antes de implementar, o agente deve identificar ou propor uma estrutura de pastas adequada para a stack escolhida.

Exemplo genérico de estrutura recomendada:

```text
src/
  pages/
    Home/
      index.*
      styles.*
    Login/
      index.*
      styles.*
  components/
    Button/
      index.*
      styles.*
    Header/
      index.*
      styles.*
  assets/
    images/
    icons/
  styles/
    globals.*
    tokens.*
  services/
  utils/
```

Para projetos HTML/CSS/JS simples, evitar arquivos soltos na raiz e preferir uma organização como:

```text
public/
  index.html

src/
  pages/
    home.html
    login.html
  scripts/
    main.js
    navigation.js
  styles/
    globals.css
    pages/
      home.css
      login.css
  assets/
    images/
    icons/
```

Para React, Next.js, Vue, Angular, Flutter ou outra stack, o agente deve seguir a convenção própria da tecnologia escolhida e a estrutura já existente no repositório.

Se a estrutura do projeto ainda não existir, o agente deve propor a organização antes de criar arquivos.

Se o projeto já possuir uma arquitetura definida, o agente deve adaptar a implementação a ela, sem criar padrões paralelos.

O agente deve evitar concentrar toda a implementação em um único arquivo quando houver potencial de crescimento do projeto.

## Regra obrigatória — fidelidade visual e não invenção de layout

O agente deve preservar a maior fidelidade possível ao Figma, especialmente em elementos visuais, textos, botões, logos, espaçamentos, cores, bordas, ícones e hierarquia visual.

O agente não deve inventar melhorias, alterar estilos, trocar formatos, mudar textos, ajustar botões, substituir ícones ou reinterpretar elementos visuais sem autorização explícita do usuário.

É permitido adaptar tecnicamente o design para a linguagem/stack escolhida, mas sem alterar a intenção visual do layout.

Antes de modificar qualquer elemento em relação ao Figma, o agente deve sinalizar a divergência e pedir confirmação.

Não alterar automaticamente:

- textos de botões;
- tamanho, cor, borda ou raio de botões;
- ícones;
- logos;
- espaçamentos;
- alinhamentos;
- hierarquia visual;
- ordem dos elementos;
- estados visuais;
- cores de fundo;
- imagens e ilustrações.

Quando houver limitação técnica para reproduzir exatamente o Figma, o agente deve registrar a limitação e propor a alternativa mais fiel possível.

## Regra obrigatória — inventário de logos e marcas na página inteira

O agente deve identificar e validar todas as ocorrências de logos, marcas, assinaturas institucionais e elementos de identidade visual presentes no frame ou página do Figma.

A validação não deve se limitar ao header.

O agente deve verificar logos e marcas em:

- header;
- footer;
- sidebar;
- menu;
- hero/banner;
- cards;
- modais;
- telas de login;
- telas de erro;
- estados vazios;
- componentes institucionais;
- qualquer outra seção da página.

Logos e marcas devem ser preservados como assets, preferencialmente SVG, quando existirem no Figma.

O agente não deve recriar logos como texto HTML/CSS, mesmo quando a logo parecer apenas uma palavra digitada.

Antes de implementar, o agente deve montar um inventário de marcas contendo:

- local onde a logo aparece;
- nome visual ou institucional identificado;
- formato esperado, como SVG, imagem ou componente;
- forma correta de implementação;
- nome sugerido do asset;
- observação sobre eventuais dúvidas.

Exemplo de inventário:

```text
Local: Header
Elemento: Logo SESI
Implementação correta: SVG/asset
Nome sugerido: logo-sesi.svg

Local: Footer
Elemento: Logo SESI
Implementação correta: SVG/asset
Nome sugerido: logo-sesi.svg
Observação: reutilizar o mesmo asset se for a mesma marca.
```

Se a mesma logo aparecer em mais de uma área da página, o agente deve reutilizar o mesmo asset sempre que possível, evitando duplicidade.

Se houver dúvida se um elemento é texto comum ou marca institucional, tratar como logo/marca e pedir confirmação antes de converter para texto.

Ao revisar a implementação, o agente deve confirmar explicitamente que todas as logos da página foram preservadas como asset ou componente visual, incluindo as logos do footer.

## Regra obrigatória — preservação de logos e marcas

Logos, marcas, assinaturas visuais e elementos institucionais devem ser preservados como assets, preferencialmente em SVG, quando existirem no Figma.

Essa regra vale para a página inteira, não apenas para o header.

O agente não deve converter uma logo em texto HTML/CSS, mesmo que visualmente pareça apenas texto, salvo se o usuário solicitar explicitamente.

Quando o Figma apresentar uma logo como vetor, SVG, imagem ou componente de marca, o agente deve tratá-la como asset institucional.

Regras:

- Usar SVG para logos sempre que disponível.
- Não recriar logo com texto digitado.
- Não substituir logo por fonte aproximada.
- Não alterar proporção, cor, espaçamento ou composição da marca.
- Não rasterizar SVG desnecessariamente.
- Não baixar versões duplicadas da mesma logo.
- Reutilizar o mesmo asset quando a mesma logo aparecer em header, footer ou outras seções.
- Nomear o asset de forma semântica, por exemplo: `logo-sesi.svg`, `logo-iel.svg`, `logo-fiergs.svg`.

Se houver dúvida se um elemento é logo ou texto comum, tratar como logo e pedir confirmação antes de converter para texto.

## Checklist de qualidade do Figma para MCP

Avalie o arquivo Figma antes de gerar código.

### 1. Estrutura do arquivo

O arquivo deve ter páginas e frames nomeados de forma clara, como:

- `Cover`
- `Design System`
- `Components`
- `Flows`
- `Desktop`
- `Mobile`
- `Homologação`
- `Dev Ready`

Evite nomes genéricos como `Frame 123`, `Group 8`, `Copy 2` ou `Untitled`.

### 2. Seleção correta do escopo

Sempre trabalhe com o menor escopo possível:

- Para uma tela, usar o link do frame da tela.
- Para um componente, usar o link do componente ou component set.
- Para um fluxo, usar uma seção com frames relacionados.
- Para ajustes pontuais, usar o link da seleção específica.

Não peça ao agente para interpretar o arquivo inteiro sem necessidade.

### 3. Auto layout

Verifique se os principais blocos usam auto layout:

- Containers principais.
- Cards.
- Headers.
- Menus laterais.
- Botões.
- Inputs.
- Modais.
- Listas e tabelas.

Caso o design esteja baseado em grupos soltos e posições absolutas, sinalize risco de baixa responsividade e maior retrabalho na implementação.

### 4. Componentes e variantes

Confirme se elementos recorrentes estão componentizados:

- Botões.
- Campos de formulário.
- Cards.
- Badges/status.
- Menus.
- Abas.
- Modais.
- Tabelas.
- Componentes de feedback, como alertas, empty states e loading.

Verifique se há variantes para estados como:

- Default.
- Hover.
- Focus.
- Disabled.
- Loading.
- Error.
- Success.
- Selected.

### 5. Tokens, estilos e variáveis

Priorize designs que usam:

- Variáveis de cor.
- Estilos de texto.
- Tokens de espaçamento.
- Tokens de borda.
- Tokens de raio.
- Tokens de sombra.
- Temas, quando aplicável.

Evite copiar valores brutos sem verificar se há token correspondente no projeto.

### 6. Responsividade

Verifique se há orientação para:

- Desktop.
- Tablet, se aplicável.
- Mobile.
- Breakpoints.
- Comportamento de menus, tabelas e cards em telas menores.

Quando o projeto for visual-first ou pixel-preview, tamanhos fixos podem ser aceitos temporariamente para acelerar a estilização, mas devem ser sinalizados como etapa intermediária, não como solução final responsiva.

### 7. Acessibilidade

Antes de implementar, validar:

- Hierarquia de títulos.
- Contraste de cores.
- Estados de foco.
- Labels de campos.
- Áreas clicáveis adequadas.
- Navegação por teclado.
- Textos alternativos para imagens relevantes.
- Feedbacks de erro compreensíveis.

### 8. Assets e ícones

Verifique se:

- Ícones fazem parte de uma biblioteca consistente.
- Imagens têm nome claro.
- Logos e imagens institucionais têm versão correta.
- Assets exportáveis estão marcados corretamente.
- SVGs não foram convertidos desnecessariamente em imagens rasterizadas.

## Regra para uso de assets via Figma MCP

Ao usar o Figma MCP, baixar assets somente quando forem imagens reais, logos, ilustrações, ícones SVG, fotografias ou elementos visuais que não possam ser reproduzidos com CSS, tokens, variáveis ou componentes do projeto.

Não baixar como imagem:

- fundos de tela com cor sólida;
- gradientes simples;
- cards;
- sombras;
- bordas;
- containers;
- botões;
- inputs;
- shapes decorativos simples;
- seções inteiras da tela;
- blocos que podem ser reproduzidos com CSS, Tailwind, tokens ou variáveis.

Sempre que possível, reproduzir fundos, espaçamentos, cores, bordas, sombras e estados usando CSS, Tailwind, tokens ou variáveis do projeto.

Antes de baixar assets, o agente deve listar quais arquivos serão gerados e justificar por que cada um precisa ser asset.

Se houver dúvida se um elemento deve ser exportado como imagem ou reproduzido em código, priorizar reprodução em código e registrar a decisão.

## Regra obrigatória — separação da pasta assets por tipo

O agente deve organizar os assets do projeto separando imagens rasterizadas e arquivos SVG em pastas distintas.

A pasta de assets deve seguir, sempre que aplicável, uma estrutura como:

```text
assets/
  img/
  svg/
```

ou, conforme a stack do projeto:

```text
src/
  assets/
    img/
    svg/
```

ou:

```text
public/
  assets/
    img/
    svg/
```

Regras obrigatórias:

- Arquivos `.svg` devem ser salvos em `assets/svg/`.
- Logos, ícones, marcas e ilustrações vetoriais em SVG devem ficar em `assets/svg/`.
- Arquivos `.png`, `.jpg`, `.jpeg`, `.webp`, `.gif`, `.avif` e similares devem ficar em `assets/img/`.
- Não misturar SVGs e imagens rasterizadas na mesma pasta.
- Não salvar assets diretamente em `assets/` sem subpasta.
- Não criar nomes genéricos como `image-1`, `vector-2`, `asset-3`.
- Atualizar todos os imports e referências após mover arquivos.
- Se o projeto já tiver uma estrutura própria, adaptar a organização mantendo a separação entre `img` e `svg`.

Exemplos:

```text
src/assets/img/hero-login-background.png
src/assets/img/card-dashboard-illustration.webp
src/assets/svg/logo-sesi.svg
src/assets/svg/icon-arrow-right.svg
src/assets/svg/logo-fiergs.svg
```

Se houver dúvida sobre o tipo do asset, o agente deve verificar a extensão e o conteúdo antes de mover ou renomear.

## Regra para limpeza e renomeação de assets

Após usar o Figma MCP, o agente deve revisar os assets gerados e organizar os arquivos para evitar acúmulo de imagens desnecessárias no projeto.

O agente deve:

- Identificar assets utilizados no código.
- Identificar assets aparentemente não utilizados.
- Identificar assets com uso incerto.
- Excluir somente assets que não tenham nenhuma referência no projeto.
- Renomear assets utilizados com nomes semânticos, curtos e padronizados.
- Atualizar todas as referências aos assets renomeados.
- Manter o SDD atualizado com as alterações realizadas.
- Separar assets por tipo, mantendo SVGs em `assets/svg/` e imagens rasterizadas em `assets/img/`.

Antes de excluir ou renomear arquivos, o agente deve gerar um relatório com:

- assets utilizados;
- assets aparentemente não utilizados;
- assets com uso incerto;
- sugestão de novo nome para cada asset utilizado;
- justificativa para exclusão ou manutenção de cada arquivo analisado.

Regras obrigatórias:

- Não excluir arquivos com uso incerto.
- Não excluir logos, ícones institucionais, imagens públicas ou assets compartilhados sem confirmar uso.
- Não renomear assets externos, arquivos de biblioteca ou arquivos fora das pastas do projeto.
- Não editar linha por linha; aplicar alterações em bloco único/consolidado.
- Atualizar imports, caminhos, referências em CSS, componentes, páginas, JSON e documentação.
- Ao final, executar validações disponíveis no projeto, como lint, build ou testes.

Exceção importante: logos, marcas, assinaturas institucionais e ícones oficiais devem ser preservados como assets, preferencialmente SVG, mesmo quando pareçam reproduzíveis com texto ou CSS.

Padrão de nome sugerido:

- Usar letras minúsculas.
- Usar kebab-case.
- Evitar nomes genéricos como `image-1`, `rectangle`, `frame`, `asset`, `vector`, `group`.
- Usar nomes baseados na função visual do asset.

Exemplos:

- `image-12.png` → `hero-login-background.png`
- `vector-3.svg` → `icon-arrow-right.svg`
- `rectangle-45.png` → `dashboard-card-illustration.png`
- `logo-final-1.svg` → `logo-sesi.svg`

Pastas comuns a analisar:

- `public/`
- `src/assets/`
- `assets/`
- `app/assets/`
- `components/`
- `pages/`
- `styles/`
- qualquer pasta equivalente usada pelo projeto.

Se a estrutura do projeto não estiver clara, primeiro identifique onde os assets estão armazenados e onde são referenciados antes de alterar qualquer arquivo.

### 9. Dev Mode e handoff

Procure evidências de preparo para desenvolvimento:

- Frames finais marcados como prontos para desenvolvimento.
- Comentários resolvidos ou tratados.
- Regras de comportamento documentadas.
- Estados de tela disponíveis.
- Fluxos de navegação claros.
- Textos reais ou exemplos próximos do conteúdo final.

### 10. Code Connect e design system

Quando houver design system e repositório com componentes reais:

- Priorize reutilizar componentes existentes.
- Mapear componentes Figma para componentes do código.
- Evitar recriar componentes que já existem.
- Usar Code Connect quando disponível.
- Registrar divergências entre design e implementação.

## Fluxo recomendado de trabalho com MCP

### Etapa 1 — Entendimento

Antes de codificar, o agente deve:

1. Ler o link do frame/seleção via MCP.
2. Perguntar em qual linguagem, framework ou stack o usuário deseja implementar, caso isso ainda não tenha sido informado.
3. Identificar layout, componentes, tokens, textos, estados e assets.
4. Verificar se existe componente equivalente no repositório.
5. Identificar dependências técnicas e padrões existentes.
6. Confirmar se a tela está pronta para implementação ou se há lacunas.

### Etapa 2 — Auditoria rápida do Figma

Classifique o design como:

- **Pronto para MCP**: componentes, auto layout, tokens, nomes claros e estados definidos.
- **Parcialmente pronto**: estrutura visual clara, mas com lacunas em responsividade, tokens ou estados.
- **Risco alto**: grupos soltos, nomes genéricos, sem componentes, sem estados e sem regras de comportamento.

Quando houver risco, informe antes de implementar.

### Etapa 3 — Planejamento da implementação

Antes de alterar código:

- Confirme a linguagem, framework ou stack desejada.
- Verifique se o projeto terá uma ou mais páginas, telas, rotas ou módulos.
- Analise a estrutura atual do repositório.
- Não crie arquivos soltos na raiz do projeto, salvo solicitação explícita para protótipo simples.
- Defina a estrutura de pastas adequada antes de implementar.
- Identifique arquivos afetados.
- Defina páginas, rotas ou módulos necessários.
- Defina componentes a reutilizar.
- Defina novos componentes necessários.
- Defina estilos/tokens a aplicar.
- Defina rotas, props, estados e integrações.
- Liste assets que realmente precisam ser baixados.
- Atualize o SDD com decisões relevantes.
- Defina a estrutura de assets separando `img/` e `svg/`.

### Etapa 4 — Implementação

Regras obrigatórias:

- Não editar linha por linha; aplicar alterações em bloco único/consolidado.
- Manter o SDD atualizado com alterações, adições e ajustes realizados.
- Usar componentes existentes antes de criar novos.
- Evitar hardcode quando houver tokens ou constantes do projeto.
- Separar layout, comportamento e dados quando a arquitetura do projeto permitir.
- Não implementar regras de negócio inexistentes no Figma sem sinalizar suposição.
- Não alterar padrões globais sem justificar impacto.
- Não baixar fundos, containers, cards ou seções inteiras como imagem quando puderem ser reproduzidos por código.
- Não trocar a linguagem/stack definida pelo usuário sem solicitar nova confirmação.
- Não criar arquivos soltos na raiz do projeto quando houver potencial de evolução para múltiplas páginas, telas, rotas ou módulos.
- Não concentrar toda a implementação em um único arquivo quando a stack permitir separação em páginas, componentes, estilos, serviços e utilitários.

### Etapa 5 — Limpeza de assets

Após implementar uma tela ou componente com Figma MCP, o agente deve:

- Revisar os assets baixados.
- Verificar quais assets estão referenciados no projeto.
- Listar assets não utilizados, utilizados e incertos.
- Excluir apenas arquivos claramente não utilizados.
- Renomear assets utilizados com nomes semânticos.
- Atualizar todos os imports e caminhos.
- Registrar as alterações no SDD.
- Mover SVGs para `assets/svg/` e imagens rasterizadas para `assets/img/`.

A limpeza não deve ser feita às cegas. O agente deve preservar qualquer arquivo cujo uso não esteja completamente claro.

### Etapa 6 — QA visual bloqueante e validação técnica

Após implementar e revisar assets:

- Comparar a tela com o frame Figma.
- Gerar screenshots quando aplicável e analisar visualmente cada tela.
- Validar se há imagens, cards, textos, botões, logos ou seções sobrepostos indevidamente.
- Verificar se há textos cortados, elementos ocultos, problemas de z-index, position absolute, overflow ou responsividade.
- Validar espaçamentos, tipografia, cores, estados e responsividade.
- Verificar se assets baixados são realmente necessários.
- Verificar se todas as logos da página foram preservadas como assets/SVG quando aplicável.
- Verificar se a estrutura de pastas está adequada para evolução do projeto.
- Verificar console, lint, build e testes disponíveis.
- Registrar divergências conhecidas.
- Atualizar SDD, README ou documentação aplicável.

A tarefa não deve ser considerada concluída se houver sobreposição indevida, elementos ocultos, textos cortados, logos recriadas como texto ou erro visual evidente.

## Prompts recomendados

### Auditar Figma antes de implementar

```text
Use o Figma MCP para analisar este frame: <URL_DO_FRAME>.
Avalie se ele está pronto para implementação com IA, considerando: nomes de camadas, auto layout, componentes, variantes, tokens, responsividade, acessibilidade, assets e clareza do fluxo.
Retorne uma classificação: Pronto para MCP, Parcialmente pronto ou Risco alto.
Liste apenas os pontos que impactam diretamente a implementação.
Não altere código ainda.
```

### Validar logos e marcas na página inteira

```text
Revise todas as logos, marcas e assinaturas institucionais presentes no frame Figma: <URL_DO_FRAME>.

Não limite a análise ao header.

Verifique obrigatoriamente:
- header;
- footer;
- sidebar;
- menus;
- hero/banner;
- cards;
- modais;
- estados vazios;
- telas de erro;
- qualquer outra seção da página.

Para cada logo encontrada, informe:
1. Onde ela aparece no Figma.
2. Como ela foi implementada no código.
3. Se está como SVG/asset/componente visual ou se foi recriada incorretamente como texto.
4. Qual asset deve ser usado.
5. Se há duplicidade desnecessária de arquivos.

Corrija logos recriadas como texto, inclusive no footer.

Preserve logos como SVG/assets sempre que possível.
Não substitua marca institucional por texto HTML/CSS.
Não altere proporção, cor, espaçamento ou composição da marca.
Atualize todas as referências no código.
Não editar linha por linha; aplicar alterações em bloco único/consolidado.
Manter o SDD atualizado com as correções realizadas.
```

### Organizar estrutura antes de implementar

```text
Antes de implementar o frame do Figma MCP, analise a estrutura atual do repositório.

Não crie index.html, style.css, script.js ou arquivos equivalentes diretamente na raiz do projeto, salvo se eu pedir explicitamente um protótipo estático simples de página única.

Se o projeto puder ter mais páginas, telas, rotas ou módulos, organize a implementação em estrutura escalável, separando páginas, componentes, estilos, assets, serviços e utilitários.

Primeiro proponha a estrutura de pastas adequada para a linguagem/stack escolhida.
Depois implemente respeitando essa estrutura.

Não editar linha por linha; aplicar alterações em bloco único/consolidado.
Manter o SDD atualizado com as alterações, adições e ajustes realizados.
```

### Implementar tela com controle de qualidade

```text
Use o Figma MCP para implementar este frame: <URL_DO_FRAME>.

Antes de implementar, pergunte em qual linguagem, framework ou stack devo escrever o código, caso isso ainda não tenha sido informado.

Não assuma React, Next.js, Vue, Angular, Flutter, HTML/CSS, Tailwind ou qualquer outra tecnologia automaticamente.

Antes de codificar:
1. Analise a estrutura atual do repositório.
2. Verifique se o projeto terá uma ou mais páginas, telas, rotas ou módulos.
3. Não crie index.html, style.css, script.js ou arquivos equivalentes diretamente na raiz do projeto, salvo solicitação explícita para protótipo simples.
4. Proponha ou siga uma estrutura escalável, separando páginas, componentes, estilos, assets, serviços e utilitários.
5. Identifique componentes existentes no repositório que devem ser reutilizados.
6. Liste os assets realmente necessários antes de baixá-los.

Implemente respeitando a arquitetura atual, tokens, padrões de estilo e estrutura de pastas.

Não editar linha por linha; aplicar alterações em bloco único/consolidado.

Atualize o SDD com as alterações, adições e decisões realizadas.

Ao final, reporte:
- arquivos criados;
- arquivos alterados;
- estrutura de pastas utilizada;
- assets baixados, renomeados ou excluídos;
- principais decisões;
- divergências em relação ao Figma.
```

### Controlar download de assets

```text
Use o Figma MCP para analisar este frame: <URL_DO_FRAME>.
Antes de baixar qualquer asset, liste quais imagens, ícones, logos ou ilustrações realmente precisam ser exportados.
Não exporte fundos, containers, cards, gradientes simples, sombras, bordas, inputs, botões, shapes decorativos simples ou seções inteiras da tela.
Sempre que possível, reproduza esses elementos com CSS, Tailwind, tokens ou variáveis do projeto.
Após listar e justificar os assets necessários, implemente usando apenas esses arquivos.
Não editar linha por linha; aplicar alterações em bloco único/consolidado.
Atualize o SDD com as decisões realizadas.
Organize os assets baixados separando arquivos SVG em assets/svg/ e imagens rasterizadas em assets/img/.
Não misture SVG, PNG, JPG, WEBP ou outros formatos na mesma pasta.
```

### Limpar e renomear assets após uso do Figma MCP

```text
Revise os assets gerados pelo Figma MCP neste projeto.

Objetivo:
1. Identificar assets não utilizados.
2. Excluir somente assets que não tenham nenhuma referência no código, estilos, configurações, rotas, componentes, HTML, CSS, TS/JS, JSX/TSX, JSON, Markdown ou arquivos de build relevantes.
3. Renomear os assets utilizados para nomes semânticos, curtos e padronizados.
4. Atualizar todas as referências aos assets renomeados.
5. Manter o SDD atualizado com as alterações realizadas.

Regras obrigatórias:
- Não excluir arquivos com uso incerto.
- Não excluir logos, ícones institucionais, imagens públicas ou assets compartilhados sem confirmar uso.
- Não renomear assets externos, arquivos de biblioteca ou arquivos fora das pastas do projeto.
- Não editar linha por linha; aplicar alterações em bloco único/consolidado.
- Antes de excluir ou renomear, gerar um relatório com:
  - assets utilizados;
  - assets aparentemente não utilizados;
  - assets com uso incerto;
  - sugestão de novo nome para cada asset utilizado.
- Após o relatório, aplicar as alterações somente nos assets claramente seguros.
- Atualizar imports, caminhos, referências em CSS, componentes, páginas, JSON e documentação.
- Ao final, executar validações disponíveis no projeto, como lint, build ou testes.
- Informar arquivos excluídos, arquivos renomeados e referências atualizadas.

Padrão de nome sugerido:
- Usar letras minúsculas.
- Usar kebab-case.
- Evitar nomes genéricos como image-1, rectangle, frame, asset, vector, group.
- Usar nomes baseados na função visual do asset.

Exemplos:
- image-12.png → hero-login-background.png
- vector-3.svg → icon-arrow-right.svg
- rectangle-45.png → dashboard-card-illustration.png
- logo-final-1.svg → logo-sesi.svg

Pastas a analisar:
- public/
- src/assets/
- assets/
- app/assets/
- components/
- pages/
- styles/
- ou qualquer pasta equivalente usada pelo projeto.

Além de limpar e renomear, reorganize os assets por tipo:
- SVGs em assets/svg/
- PNG, JPG, JPEG, WEBP, GIF, AVIF e similares em assets/img/

Atualize todos os imports e referências após mover os arquivos.

Se a estrutura do projeto não estiver clara, primeiro identifique onde os assets estão armazenados e onde são referenciados antes de alterar qualquer arquivo.
```

### Comparar implementação com Figma

```text
Compare a implementação atual com este frame Figma: <URL_DO_FRAME>.

Verifique:
- fidelidade visual;
- espaçamentos;
- tipografia;
- cores;
- estados;
- responsividade;
- uso de componentes;
- uso adequado de assets;
- organização da estrutura de pastas.

Classifique divergências em:
- Impeditivas;
- Importantes;
- Cosméticas.

Não faça alterações sem listar primeiro o plano consolidado.
```

### Revisar fidelidade visual após implementação

```text
Compare a implementação atual com o frame Figma: <URL_DO_FRAME>.

Faça uma revisão rigorosa de fidelidade visual.

Faça uma busca no código por nomes de marcas, como SESI, SENAI, IEL, FIERGS ou outras identificadas no Figma, e confirme se essas ocorrências são conteúdo textual real ou se deveriam ser logos/assets.

Verifique especialmente:
- logos e marcas;
- textos;
- botões;
- ícones;
- cores;
- tipografia;
- espaçamentos;
- alinhamentos;
- bordas;
- sombras;
- imagens;
- hierarquia visual;
- estados visuais;
- sobreposição de elementos;
- z-index;
- position absolute;
- overflow;
- responsividade.

Não invente melhorias e não altere o layout com base em preferência própria.

Aponte diferenças entre Figma e código classificando em:
- Críticas: comprometem identidade visual, marca, entendimento da tela ou causam erro visual evidente.
- Importantes: alteram aparência, usabilidade ou consistência.
- Cosméticas: pequenas diferenças visuais aceitáveis para ajuste fino.

Para cada divergência, informe:
1. Como está no Figma.
2. Como ficou no código.
3. Correção recomendada.
4. Arquivos afetados.

Corrija apenas divergências objetivas em relação ao Figma.
Preserve logos como SVG/assets, não como texto.
Não finalize se houver imagens sobrepostas, elementos ocultos, textos cortados ou erro visual evidente.
Não editar linha por linha; aplicar alterações em bloco único/consolidado.
Atualize o SDD com as correções realizadas.
```

### Usar componentes do projeto

```text
Use o Figma MCP para obter o contexto deste componente: <URL_DO_COMPONENTE>.
Antes de gerar código, confirme a linguagem, framework ou stack desejada, caso ainda não tenha sido informada.
Procure no repositório o componente equivalente.
Se existir, reutilize e ajuste apenas props, composição ou estilos locais.
Se não existir, proponha um novo componente seguindo os padrões do projeto.
Atualize o SDD e evite duplicação de componentes.
```

### Revisar tela com validação visual rigorosa

```text
Revise a implementação atual comparando com o Figma: <URL_DO_FRAME>.

Não basta gerar screenshots. Analise visualmente os screenshots e a estrutura renderizada.

Verifique obrigatoriamente:
1. Se há imagens sobrepostas indevidamente.
2. Se há textos cortados, ocultos ou fora do container.
3. Se botões mantêm posição, tamanho, cor, borda, raio e texto conforme o Figma.
4. Se logos foram preservados como assets/SVG e não recriados como texto.
5. Se ícones, imagens e ilustrações estão na posição correta.
6. Se cards, seções e containers não estão empilhados incorretamente.
7. Se há elementos duplicados ocupando o mesmo espaço.
8. Se há problemas de z-index, position absolute, overflow ou responsividade.
9. Se a tela continua fiel ao Figma em desktop e, quando aplicável, mobile.

Classifique cada problema encontrado em:
- Crítico: erro visual evidente ou elemento sobreposto/cortado.
- Importante: diferença perceptível em relação ao Figma.
- Cosmético: ajuste fino de espaçamento, alinhamento ou proporção.

Antes de concluir, informe explicitamente:
- telas revisadas;
- screenshots gerados;
- problemas encontrados;
- correções aplicadas;
- problemas ainda pendentes.

Não finalize a tarefa se houver imagens sobrepostas, elementos ocultos ou erro visual evidente.
Não editar linha por linha; aplicar alterações em bloco único/consolidado.
Manter o SDD atualizado com as correções realizadas.
```

### Preparar handoff para desenvolvimento

```text
Analise este arquivo ou seção do Figma com MCP: <URL>.
Gere um checklist de handoff para desenvolvimento contendo: telas, componentes, estados ausentes, tokens, assets, fluxos, regras de comportamento, linguagem/stack a confirmar, estrutura de pastas sugerida e dúvidas pendentes.
Organize o resultado de forma objetiva para validação com UX, PO e desenvolvimento.
Não altere código.
```

## Critérios de aceite da skill

A skill foi usada corretamente quando:

- O agente não implementa baseado apenas em imagem ou screenshot.
- O escopo do Figma é específico e rastreável por URL.
- A linguagem, framework ou stack foi confirmada antes da geração ou alteração de código.
- A estrutura atual do repositório foi analisada antes da criação de arquivos.
- Arquivos soltos na raiz foram evitados, salvo solicitação explícita para protótipo simples.
- A implementação foi organizada em páginas, componentes, estilos, assets, serviços e utilitários quando aplicável.
- Componentes existentes são priorizados.
- Tokens e variáveis são respeitados.
- Lacunas do design são sinalizadas antes de virar código.
- Assets são baixados apenas quando realmente necessários.
- Fundos, containers, cards, sombras, bordas e formas simples são reproduzidos em código quando possível.
- Assets não utilizados são removidos apenas quando não há referência no projeto.
- Assets utilizados são renomeados com nomes semânticos e referências atualizadas.
- O SDD é atualizado.
- Alterações são aplicadas de forma consolidada.
- O resultado final é comparado com o Figma.
- Logos e marcas foram preservados como assets, preferencialmente SVG.
- O agente não converteu logos institucionais em texto HTML/CSS.
- Botões, textos, ícones, cores e espaçamentos não foram alterados por interpretação própria.
- Divergências em relação ao Figma foram tratadas como ajustes de fidelidade, não como redesign.
- Screenshots não foram apenas gerados; foram analisados visualmente.
- Não existem imagens, cards, textos, botões ou seções sobrepostos indevidamente.
- Problemas de z-index, position absolute, overflow e responsividade foram verificados.
- Erros visuais evidentes foram tratados como bloqueantes antes da conclusão.
- Todas as logos da página foram identificadas, não apenas a do header.
- Logos presentes no footer, sidebar, cards ou outras seções foram preservadas como assets/componentes visuais.
- Nenhuma logo institucional foi recriada como texto HTML/CSS sem autorização explícita.
- O mesmo asset de logo foi reutilizado quando a mesma marca apareceu em mais de uma seção.
- A revisão final confirmou explicitamente header, footer e demais áreas com presença de marca.

## Sinais de alerta

Interrompa ou sinalize risco quando encontrar:

- Linguagem, framework ou stack não informada pelo usuário.
- Criação de `index.html`, `style.css`, `script.js` ou arquivos equivalentes diretamente na raiz sem solicitação explícita.
- Implementação concentrada em um único arquivo quando há potencial de crescimento.
- Estrutura paralela criada sem respeitar a arquitetura existente.
- Frame sem nome claro.
- Layout baseado em grupos soltos sem auto layout.
- Vários componentes visualmente iguais, mas não componentizados.
- Estados de erro, loading ou vazio ausentes.
- Ausência de regras de responsividade.
- Cores e fontes fora dos tokens do projeto.
- Assets não exportáveis.
- Fundos, cards ou seções inteiras sendo exportados como imagem sem necessidade.
- Assets com uso incerto marcados para exclusão.
- Renomeação de assets sem atualização das referências.
- Figma divergente da arquitetura real do produto.
- Solicitação para copiar visualmente sem respeitar componentes existentes.
- O agente afirma que revisou a tela apenas porque gerou screenshots.
- Há imagens, textos, cards ou botões ocupando o mesmo espaço visual.
- Existem elementos com `position: absolute` ou `z-index` sem validação visual.
- O screenshot mostra erro evidente, mas o agente conclui a tarefa como finalizada.
- O agente revisou apenas a logo do header e ignorou marcas no footer ou em outras seções.
- Uma logo institucional foi implementada como texto digitado.
- A mesma logo foi baixada várias vezes com nomes diferentes.
- A logo do footer ficou visualmente diferente da logo do Figma.
- O agente assumiu que uma marca “parecida com texto” poderia ser implementada como texto comum.
- SVGs e imagens rasterizadas foram salvos na mesma pasta.
- Assets foram mantidos soltos diretamente em `assets/`.
- Imports não foram atualizados após mover arquivos entre `img/` e `svg/`.

## Resultado esperado

Ao final de uma tarefa usando esta skill, o agente deve entregar:

- Implementação aderente ao Figma e ao projeto.
- Confirmação da linguagem, framework ou stack utilizada.
- Estrutura de pastas utilizada ou proposta.
- Lista objetiva de arquivos criados.
- Lista objetiva de arquivos alterados.
- Lista de assets baixados, quando houver, com justificativa.
- Lista de assets excluídos, quando houver.
- Lista de assets renomeados, quando houver.
- Referências atualizadas no código e na documentação.
- Decisões técnicas registradas.
- Divergências ou suposições documentadas.
- SDD atualizado.
- Orientação clara para validação funcional e visual.
