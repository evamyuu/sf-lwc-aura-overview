# Aula 3: Aura x LWCs - O passado que assombra o futuro que encanta

> *"Entender o passado é como ter um mapa do tesouro: você sabe onde não pisar mais, mas ainda pode usar as pistas antigas pra chegar ao ouro novo."*

<img src="./banner.png" alt="Banner" style="width: 100%; display: block; margin: 0;">

---

## Sumário

- [O Passado: Entendendo Aura Components](#o-passado-entendendo-aura-components)
  - [O que são Aura Components?](#o-que-são-aura-components)
  - [Estrutura de um Bundle Aura](#estrutura-de-um-bundle-aura)
  - [Arquivos do Bundle](#arquivos-do-bundle)
    - [1. Component (.cmp) — Obrigatório](#1-component-cmp--obrigatório)
    - [2. Controller (.js) — Opcional mas Comum](#2-controller-js--opcional-mas-comum)
    - [3. Helper (.js) — Onde a Mágica Acontece](#3-helper-js--onde-a-mágica-acontece)
    - [4. Renderer (.js) — Customização de Renderização](#4-renderer-js--customização-de-renderização)
    - [5. Style (.css) — Estilos Encapsulados](#5-style-css--estilos-encapsulados)
    - [6. Design (.design) — Configuração para App Builder](#6-design-design--configuração-para-app-builder)
- [Aura vs LWC: A Grande Comparação](#aura-vs-lwc-a-grande-comparação)
  - [Filosofia e Arquitetura](#filosofia-e-arquitetura)
  - [Performance](#performance)
  - [Nomenclatura e Sintaxe](#nomenclatura-e-sintaxe)
  - [Estrutura de Arquivos](#estrutura-de-arquivos)
  - [Tratamento de Dados](#tratamento-de-dados)
  - [Comunicação entre Componentes](#comunicação-entre-componentes)
- [Quando Usar Cada Um?](#quando-usar-cada-um)
- [Convivência: Aura e LWC no mesmo App](#convivência-aura-e-lwc-no-mesmo-app)
- [Migrando de Aura para LWC](#migrando-de-aura-para-lwc)
- [Salesforce Lightning Design System (SLDS)](#salesforce-lightning-design-system-slds)
  - [O que é um Design System?](#o-que-é-um-design-system)
  - [O que é SLDS?](#o-que-é-slds)
  - [SLDS 1 vs SLDS 2](#slds-1-vs-slds-2)
  - [Elementos Fundamentais do SLDS](#elementos-fundamentais-do-slds)
    - [1. Design Tokens: Variáveis que falam a mesma língua](#1-design-tokens-variáveis-que-falam-a-mesma-língua)
    - [2. Utility Classes: Atalhos visuais prontos](#2-utility-classes-atalhos-visuais-prontos)
    - [3. Component Blueprints: Receitas visuais prontas](#3-component-blueprints-receitas-visuais-prontas)
    - [4. Guidelines: Padrões de UX](#4-guidelines-padrões-de-ux)
  - [SLDS 2: A Nova Geração](#slds-2-a-nova-geração)
    - [O que mudou no SLDS 2?](#o-que-mudou-no-slds-2)
    - [Styling Hooks: Customização sem medo](#styling-hooks-customização-sem-medo)
    - [Como ativar SLDS 2?](#como-ativar-slds-2)
    - [Benefícios do SLDS 2](#benefícios-do-slds-2)
    - [Principais Styling Hooks](#principais-styling-hooks)
  - [Quando usar SLDS 1 vs SLDS 2?](#quando-usar-slds-1-vs-slds-2)
  - [Usando SLDS em LWC](#usando-slds-em-lwc)
  - [Acessibilidade First: Design para Todos](#acessibilidade-first-design-para-todos)
    - [WCAG: O Guia da Acessibilidade](#wcag-o-guia-da-acessibilidade)
    - [Os 4 Princípios do WCAG (POUR)](#os-4-princípios-do-wcag-pour)
  - [Dicas](#dicas)
- [Troubleshooting: Quando as coisas dão errado](#troubleshooting-quando-as-coisas-dão-errado)
  - [Debug Mode](#debug-mode)
  - [Chrome DevTools: Seu melhor amigo](#chrome-devtools-seu-melhor-amigo)
  - [Breakpoints: Parando o Tempo](#breakpoints-parando-o-tempo)
    - [1. Line-of-code Breakpoint](#1-line-of-code-breakpoint)
    - [2. Conditional Breakpoint](#2-conditional-breakpoint)
    - [3. DOM Breakpoints](#3-dom-breakpoints)
- [Boas Práticas](#boas-práticas)
  - [Troubleshooting](#troubleshooting)
  - [Aura vs LWC](#aura-vs-lwc)
  - [SLDS](#slds)
  - [Performance](#performance-1)

---

## O Passado: Entendendo Aura Components

### O que são Aura Components?

Aura Components é o framework anterior de componentes Lightning da Salesforce, lançado em 2014. Foi revolucionário na época porque trouxe uma abordagem component-driven para o desenvolvimento Salesforce, permitindo criar aplicações web dinâmicas e responsivas.

**Por que Aura foi criado?**

Em 2014, os padrões web modernos ainda estavam em desenvolvimento. A Web não tinha Web Components nativos, módulos ES6, ou outras tecnologias que usamos hoje. Para criar aplicações enterprise robustas, a Salesforce precisou construir uma camada de abstração completa — e essa camada é o Aura Framework.

Pense assim: Aura é como construir uma casa com ferramentas customizadas que você mesmo fabricou. Funciona, mas exige que você aprenda o jeito específico de usar essas ferramentas.

**Razões para conhecer Aura:**
- **Legado vivo:** Milhares de componentes em produção
- **Manutenção:** Você precisará dar suporte a código existente
- **Migração:** Entender Aura facilita a transição para LWC
- **Interoperabilidade:** Aura e LWC podem trabalhar juntos
- **Contexto histórico:** Compreender a evolução tecnológica

💡 **Aura foi essencial para a evolução do Salesforce Lightning, mas hoje é considerado legado.**

**Documentação Oficial:** [Lightning Aura Components Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/intro_components.htm)

---

### Estrutura de um Bundle Aura

Um componente Aura é organizado em um **Component Bundle** — uma coleção de arquivos que trabalham juntos para definir o componente.

Estrutura típica:

```
meuComponente/
├── meuComponente.cmp              // Markup (obrigatório)
├── meuComponenteController.js     // Controller (opcional)
├── meuComponenteHelper.js         // Helper (opcional)
├── meuComponenteRenderer.js       // Renderer (opcional)
├── meuComponente.css              // Estilos (opcional)
├── meuComponente.design           // Design para App Builder (opcional)
├── meuComponente.svg              // Ícone (opcional)
└── meuComponente.auradoc          // Documentação (opcional)
```

---

### Arquivos do Bundle

#### 1. Component (.cmp) — Obrigatório

O arquivo `.cmp` é o coração do componente Aura. Ele define a estrutura visual usando uma sintaxe XML-like proprietária.

```xml
<aura:component implements="force:lightningQuickAction" access="global">
    <!-- Atributos (variáveis) -->
    <aura:attribute name="mensagem" type="String" default="Olá, Mundo!"/>
    
    <!-- Markup visual -->
    <div class="slds-box slds-theme_default">
        <p>{!v.mensagem}</p>
        <lightning:button label="Clique aqui" onclick="{!c.handleClick}"/>
    </div>
</aura:component>
```

**Características:**
- **`<aura:component>`**: Tag raiz que define o componente
- **`<aura:attribute>`**: Declara uma propriedade do componente (equivalente a variáveis públicas no LWC)
- **`implements`**: Define interfaces que o componente implementa (onde pode ser usado)
- **`access`**: Define visibilidade do componente (global, public, private)
- **Value Provider (`{!v.}`**: Sintaxe para acessar valores de atributos do componente
- **`{!c.methodName}`**: Referencia método do Controller

---

#### 2. Controller (.js) — Opcional mas Comum

O Controller é onde você define **métodos chamados diretamente pelo markup**. Ele age como intermediário entre a interface e a lógica de negócio.

```javascript
({
    handleClick : function(component, event, helper) {
        // Chama o helper para fazer o trabalho pesado
        helper.atualizarMensagem(component);
    }
})
```

**⚠️ IMPORTANTE:** O Controller tem limitações severas:
- **Métodos não podem chamar outros métodos do controller diretamente**
- Deve apenas receber eventos e delegar ao Helper
- Se você colocar lógica aqui, vai ter problemas de manutenção

**Características:**
- **`component`**: Objeto que representa a instância do componente
- **`component.get("v.attribute")`**: Lê valor de um atributo
- **`component.set("v.attribute", value)`**: Define valor de um atributo
- **`event`**: Objeto do evento que disparou a ação
- **`helper`**: Referência ao arquivo Helper do componente
  
**Pulo do Gato:**
- Pense no Controller como um **porteiro**: ele só recebe visitantes (eventos) e os direciona para o Helper
- Nunca coloque lógica complexa no Controller — sempre use o Helper

---

#### 3. Helper (.js) — Onde a Mágica Acontece

O Helper contém a **lógica de negócio real**. É aqui que você:
- Faz chamadas Apex
- Processa dados
- Executa validações
- Implementa transformações

```javascript
({
    atualizarMensagem : function(component) {
        const novaMsg = "Botão clicado! " + new Date().toLocaleTimeString();
        component.set("v.mensagem", novaMsg);
    },
    
    buscarDados : function(component) {
        const action = component.get("c.getDados");
        action.setCallback(this, function(response) {
            const state = response.getState();
            if (state === "SUCCESS") {
                component.set("v.dados", response.getReturnValue());
            }
        });
        $A.enqueueAction(action);
    }
})
```

**Características:**
- Helpers podem chamar outros métodos do Helper
- É reutilizável em múltiplos métodos do Controller
- Mantém código organizado e testável
- Helpers podem ser chamados de qualquer lugar do componente
- **`component.get("c.methodName")`**: Obtém método Apex do controller (c = controller Apex)
- **`action.setParams()`**: Define parâmetros da chamada Apex
- **`action.setCallback()`**: Define função a ser executada após resposta
- **`$A.enqueueAction()`**: Enfileira ação assíncrona para execução
- **`response.getState()`**: Retorna estado da resposta ("SUCCESS", "ERROR", "INCOMPLETE")
- **`response.getReturnValue()`**: Obtém valor retornado pelo método Apex

---

#### 4. Renderer (.js) — Customização de Renderização

Raramente usado, o Renderer permite controlar **como** o componente é renderizado no DOM. Útil para casos edge de manipulação direta do DOM.

---

#### 5. Style (.css) — Estilos Encapsulados

CSS específico do componente. Estilos aqui não vazam para outros componentes (encapsulamento).

```css
.THIS .slds-box {
    background-color: #f3f2f2;
    border-radius: 8px;
}
```

**Observação:** `.THIS` é um seletor especial do Aura que garante que os estilos só se apliquem ao componente atual.

---

#### 6. Design (.design) — Configuração para App Builder

Define quais atributos podem ser configurados visualmente no App Builder.

```xml
<design:component>
    <design:attribute name="mensagem" label="Mensagem Inicial" description="Texto exibido ao carregar"/>
</design:component>
```
---

### Handlers e Value Providers

**Handlers** são formas de escutar eventos e executar ações em resposta.

```html
<!-- Handler de inicialização -->
<aura:handler name="init" value="{!this}" action="{!c.doInit}"/>

<!-- Handler de evento customizado -->
<aura:handler name="notify" event="c:NotificationEvent" action="{!c.handleNotification}"/>

<!-- Handler de mudança de atributo -->
<aura:handler name="change" value="{!v.recordId}" action="{!c.onRecordChange}"/>

<!-- Handler de evento de aplicação -->
<aura:handler event="force:refreshView" action="{!c.handleRefresh}"/>
```

**Value Providers** são formas de acessar diferentes tipos de dados:

| Value Provider | Uso | Exemplo |
|----------------|-----|---------|
| **`{!v.}`** | Atributos do componente | `{!v.message}` |
| **`{!c.}`** | Métodos do Controller | `{!c.handleClick}` |
| **`{!m.}`** | Métodos do Helper | Raramente usado diretamente |
| **`{!$Label.}`** | Custom Labels | `{!$Label.c.HelloMessage}` |
| **`{!$Resource.}`** | Static Resources | `{!$Resource.MyLogo}` |

---

### O Ciclo de Vida do Aura

Aura possui eventos de ciclo de vida que disparam em momentos específicos. Compreender esses momentos é crucial para escrever lógica no timing correto.

| Evento | Quando Dispara | Uso Comum | Equivalente LWC |
|--------|----------------|-----------|-----------------|
| **init** | Componente carregado pela primeira vez | Buscar dados iniciais, setup inicial | `connectedCallback()` |
| **render** | Antes de renderizar no DOM | Customizar renderização (raro) | — |
| **afterRender** | Após renderizar no DOM | Inicializar bibliotecas JS externas | `renderedCallback()` |
| **rerender** | Componente re-renderiza | Atualizar estado visual | `renderedCallback()` |
| **unrender** | Antes de remover do DOM | Limpar timers, event listeners | `disconnectedCallback()` |

**Exemplo de uso:**
```html
<aura:component>
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:handler name="destroy" value="{!this}" action="{!c.cleanup}"/>
    
    <!-- Conteúdo -->
</aura:component>
```

```javascript
({
    doInit: function(component, event, helper) {
        // Setup inicial
        console.log('Componente inicializado');
        helper.loadInitialData(component);
    },
    
    cleanup: function(component, event, helper) {
        // Limpeza antes de destruir
        console.log('Componente sendo destruído');
        // Limpar timers, listeners, etc
    }
})
```

---

## Aura vs LWC: A Grande Comparação

### Filosofia e Arquitetura

| Aspecto | Aura Components | Lightning Web Components |
|---------|-----------------|--------------------------|
| **Base** | Framework proprietário da Salesforce | Padrões Web nativos (Web Components) |
| **Camada de Abstração** | Alta — Framework customizado | Baixa — JavaScript vanilla + Web APIs |
| **Sintaxe** | XML-like proprietária | HTML + JavaScript moderno |
| **Curva de Aprendizado** | Íngreme (sintaxe única) | Suave (padrões web conhecidos) |

---

### Nomenclatura e Sintaxe

#### Aura:
```xml
<!-- Uso de dois-pontos (:) -->
<c:meuComponente atributo="valor"/>

<!-- Acesso a atributos com v. -->
{!v.mensagem}

<!-- Acesso a métodos do controller com c. -->
{!c.handleClick}
```

#### LWC:
```html
<!-- Uso de hífen (kebab-case) -->
<c-meu-componente atributo="valor"></c-meu-componente>

<!-- Acesso direto a propriedades -->
{mensagem}

<!-- Eventos padrão do DOM -->
<button onclick={handleClick}>
```

**Observação:** Aura components seguem o formato namespace:componentName com dois-pontos, enquanto Lightning web components seguem o formato namespace-component-name com hífen.

---

### Estrutura de Arquivos

#### Aura Bundle:
```
meuComponente/
├── meuComponente.cmp           // Markup
├── meuComponenteController.js  // Controller (chamadas de eventos)
├── meuComponenteHelper.js      // Helper (lógica)
```

#### LWC Bundle:
```
meuComponente/
├── meuComponente.html          // Template
├── meuComponente.js            // Controller + Lógica (tudo em um)
├── meuComponente.css           // Estilos
```

**Vantagem LWC:** Os arquivos controller, helper e renderer do Aura são consolidados em um único arquivo JavaScript no LWC, simplificando a estrutura.

---

### Tratamento de Dados

#### Aura — Atributos e component.set/get:
```javascript
// Definir
component.set("v.nome", "Gabriel");

// Obter
const nome = component.get("v.nome");
```

#### LWC — Propriedades Reativas:
```javascript
// Definir
this.nome = "Gabriel";

// Obter
const nome = this.nome;
```

**Pulo do Gato:**
- Aura exige `component.set()` para tornar mudanças reativas
- LWC é automático — qualquer propriedade é reativa por padrão

---

### Comunicação entre Componentes

#### Aura — Component Events e Application Events:

**Component Event** (Pai ↔ Filho):
```xml
<!-- Filho dispara -->
<aura:registerEvent name="mensagemEvent" type="c:MensagemEvent"/>

<!-- Pai escuta -->
<c:filho mensagemEvent="{!c.handleMensagem}"/>
```

**Application Event** (broadcast global):
```javascript
// Disparar
const appEvent = $A.get("e.c:GlobalEvent");
appEvent.fire();

// Escutar
<aura:handler event="c:GlobalEvent" action="{!c.handleGlobal}"/>
```

#### LWC — DOM Events Nativos:

**Filho → Pai:**
```javascript
// Filho dispara
this.dispatchEvent(new CustomEvent('mensagem', { detail: dados }));
```

```html
<!-- Pai escuta -->
<c-filho onmensagem={handleMensagem}></c-filho>
```

**Sem Parentesco:** Use Lightning Message Service (LMS)

**Diferença Chave:**
- Aura tem eventos proprietários (Component/Application Events)
- LWC usa eventos DOM nativos (CustomEvent)

---

## Quando Usar Cada Um?

### Use **LWC** quando:
✅ Iniciar um novo projeto  
✅ Performance é crítica  
✅ Você quer seguir padrões web modernos  
✅ O time tem experiência com JavaScript moderno  

### Use **Aura** quando:
⚠️ Precisa manter/estender componentes legados  
⚠️ Funcionalidade específica ainda não existe em LWC  
⚠️ Integração profunda com Aura existente  

**Regra de Ouro:** Sempre escolha Lightning Web Components a menos que precise de uma funcionalidade não suportada.

---

## Convivência: Aura e LWC no mesmo App

**Boa notícia:** Aura components e Lightning web components trabalham bem juntos na mesma aplicação!

### Hierarquia Permitida:

✅ **Aura pode conter LWC** (Aura como wrapper)
```xml
<aura:component>
    <c:meuLwc></c:meuLwc>
</aura:component>
```

❌ **LWC NÃO pode conter Aura** (shadow DOM limitations)

**Estratégia Comum:**
Crie novos componentes em LWC e envolva-os em um componente Aura fino quando precisar usar features exclusivas do Aura (como Application Events ou certos tipos de Pages).

**Pulo do Gato:**
Pense no Aura como o "pai controlador" que orquestra componentes LWC mais modernos e eficientes.

---

## Migrando de Aura para LWC

### Processo de Migração

**1. Avalie a Complexidade**
- Componentes pequenos sem JavaScript → Migração rápida (troca sintaxe)
- Componentes grandes com lógica complexa → Redesenhe do zero

**2. Mapeie os Arquivos**

| Aura | LWC |
|------|-----|
| `.cmp` | `.html` + `.js` |
| `Controller.js` | `.js` (métodos da classe) |
| `Helper.js` | `.js` (métodos privados ou módulos separados) |
| `.css` | `.css` (sem mudanças) |

**3. Adapte a Sintaxe**

**Aura:**
```xml
<aura:attribute name="titulo" type="String"/>
<p>{!v.titulo}</p>
```

**LWC:**
```javascript
@api titulo;
```
```html
<p>{titulo}</p>
```

**4. Converta Eventos**

**Aura Component Event:**
```javascript
const event = component.getEvent("mensagemEvent");
event.fire();
```

**LWC CustomEvent:**
```javascript
this.dispatchEvent(new CustomEvent('mensagem'));
```

**Pulo do Gato:**
Migração não é conversão linha por linha — é uma oportunidade para simplificar, redesenhar e reorganizar. Aproveite para refatorar código antigo!

---

## Salesforce Lightning Design System (SLDS)

> "Design não é só como parece. Design é como funciona." - Steve Jobs

### O que é um Design System?

Um **Design System** (Sistema de Design) é uma coleção completa de padrões, componentes, guias e ferramentas reutilizáveis que garantem consistência visual e experiência unificada em toda uma plataforma.

Pense assim: se cada desenvolvedor criasse botões do seu jeito, teríamos centenas de estilos diferentes de botões no Salesforce. Um design system resolve isso criando "o botão oficial" que todos usam.

**Componentes de um Design System:**
- **Design Tokens**: Variáveis de design (cores, espaçamentos, fontes)
- **Component Library**: Componentes visuais prontos
- **Guidelines**: Regras de uso e boas práticas
- **Patterns**: Soluções comuns para problemas recorrentes
- **Accessibility Standards**: Padrões de acessibilidade

### O que é SLDS?

SLDS é um Design System que permite dividir a UI em partes reutilizáveis, organizadas, independentes e fáceis de manter. É o conjunto de diretrizes, componentes e tokens visuais que garantem consistência em toda a plataforma Salesforce.

**Por que usar SLDS?**
- ✅ **Consistência visual** com Lightning Experience
- ✅ **Acessibilidade nativa** (WCAG 2.1 compliant)
- ✅ **Responsividade automática**
- ✅ **Menos código CSS customizado**

---

### SLDS 1 vs SLDS 2

SLDS 2 foi introduzido na Spring '25 como a nova versão do design system, trazendo melhorias significativas.

| Recurso | SLDS 1 | SLDS 2 |
|---------|--------|--------|
| **CSS Framework** | CSS tradicional | Styling Hooks (CSS Custom Properties) |
| **Customização** | Limitada | Profunda (temas e tokens) |
| **Componentes** | Blueprints CSS | Base Lightning Components nativos |
| **Ativação** | Padrão | Opt-in via Salesforce Cosmos Theme |

💡 **Pulo do Gato**: SLDS 2 mantém **compatibilidade reversa** com SLDS 1, então seus componentes antigos continuam funcionando!

---

### Elementos Fundamentais do SLDS

SLDS é composto por quatro elementos fundamentais: **Design Tokens**, **Utility Classes**, **Component Blueprints** e **Guidelines**.

---

#### 1. Design Tokens: Variáveis que falam a mesma língua

**O que são**: Design Tokens são variáveis que armazenam valores de design como cores, espaçamentos, tamanhos de fonte e mais. Eles garantem consistência visual em toda a plataforma.

```css
/* Exemplo de Design Tokens */
--slds-c-button-brand-color-background: #0176D3;
--slds-c-button-spacing-block: 0.5rem;
--slds-c-card-spacing-padding: 1rem;
```

**Por que isso importa?**
- **Mudanças centralizadas**: alterar um token atualiza toda a interface
- **Tema consistente**: cores e espaçamentos padronizados
- **Manutenção facilitada**: menos código customizado para gerenciar

---

#### 2. Utility Classes: Atalhos visuais prontos

**O que são**: Utility classes são classes CSS prontas para aplicar espaçamentos, alinhamentos, cores e mais — sem escrever uma linha de CSS customizado.

```html
<!-- Sem SLDS: escrevendo CSS do zero -->
<div style="margin: 16px; padding: 24px; background-color: white; border-radius: 4px;">
    <h2 style="font-size: 1.25rem; font-weight: 700; margin-bottom: 8px;">Título</h2>
    <p style="color: #3e3e3c;">Descrição aqui</p>
</div>

<!-- Com SLDS: utility classes fazem tudo -->
<div class="slds-card slds-m-around_medium slds-p-around_large">
    <h2 class="slds-text-heading_medium slds-m-bottom_x-small">Título</h2>
    <p class="slds-text-color_default">Descrição aqui</p>
</div>
```

**Principais categorias de utility classes:**
- **Spacing**: `slds-m-top_small`, `slds-p-around_medium`
- **Typography**: `slds-text-heading_large`, `slds-text-body_regular`
- **Colors**: `slds-text-color_default`, `slds-theme_success`
- **Layout**: `slds-grid`, `slds-col`, `slds-size_1-of-2`
- **Alignment**: `slds-align_absolute-center`, `slds-text-align_center`

💡 **Pulo do Gato**: Abuse das utility classes. Elas economizam tempo, garantem consistência e reduzem a necessidade de CSS customizado.

**Documentação**: [SLDS Utilities](https://www.lightningdesignsystem.com/utilities/alignment/)

---

#### 3. Component Blueprints: Receitas visuais prontas

**O que são**: Blueprints são **estruturas de marcação HTML/CSS prontas** que você copia e cola. Eles **NÃO são componentes Lightning** (como `<lightning-card>`), mas sim o **código HTML puro** que define como algo deve parecer visualmente.

**Exemplo de Button Blueprint:**
```html
<button class="slds-button slds-button_brand">
    Botão Azul
</button>
```

**Diferença entre Blueprint e Componente Lightning:**

```html
<!-- Blueprint SLDS (HTML puro com classes) -->
<button class="slds-button slds-button_brand" onclick={handleClick}>
    Salvar
</button>

<!-- Componente Lightning (componente pronto) -->
<lightning-button variant="brand" label="Salvar" onclick={handleClick}>
</lightning-button>
```

💡 **Pulo do Gato**: Sempre que possível, use **Base Lightning Components** (`<lightning-button>`) em vez de criar do zero com blueprints. Eles já vêm com acessibilidade, responsividade e integração com SLDS 2.

**Documentação**: [SLDS Components](https://www.lightningdesignsystem.com/components/overview/)

---

#### 4. Guidelines: Padrões de UX

**O que são**: Diretrizes de experiência do usuário e padrões de interação que ensinam **quando** e **como** usar cada componente (modais, toasts, tabs, etc.).

**Exemplos de guidelines:**
- Quando usar um modal vs. uma página separada
- Como estruturar formulários acessíveis
- Padrões de navegação e hierarquia visual

**Referência**: [SLDS Guidelines](https://www.lightningdesignsystem.com/)

---

### SLDS 2: A Nova Geração

#### O que mudou no SLDS 2?

SLDS 2 introduz **Styling Hooks** — CSS Custom Properties que permitem customizar componentes Base Lightning sem quebrar o design system.

#### Styling Hooks: Customização sem medo

**O que são**: Variáveis CSS que você pode sobrescrever para personalizar a aparência dos componentes Base Lightning.

```css
/* nomeDoComponente.css */

/* Customizando um lightning-button */
lightning-button {
    --slds-c-button-brand-color-background: #FF6B35;
    --slds-c-button-brand-color-background-hover: #FF8555;
}

/* Customizando um lightning-card */
lightning-card {
    --slds-c-card-color-background: #F9F9F9;
    --slds-c-card-spacing-padding: 2rem;
}
```

**No componente:**
```html
<template>
    <lightning-card title="Card Customizado">
        <lightning-button 
            variant="brand" 
            label="Botão Laranja"
            class="custom-button">
        </lightning-button>
    </lightning-card>
</template>
```

#### Como ativar SLDS 2?

SLDS 2 está disponível através do **Salesforce Cosmos Theme**, que você ativa nas configurações da org:

1. **Setup** → **Themes and Branding** → **Themes**
2. Selecione **Salesforce Cosmos**
3. Ative para sua org

💡 **Pulo do Gato**: Componentes antigos continuam funcionando! SLDS 2 é **opt-in** e **retrocompatível**.

#### Benefícios do SLDS 2

**Antes (SLDS 1):**
```css
/* Difícil de customizar sem quebrar o design */
.slds-button {
    background-color: #FF6B35 !important; /* Hacky */
}
```

**Depois (SLDS 2):**
```css
/* Customização limpa e oficial */
lightning-button {
    --slds-c-button-brand-color-background: #FF6B35;
}
```

**Vantagens:**
- ✅ **Customização segura** — sem `!important` ou hacks
- ✅ **Temas consistentes** — crie paletas de cores personalizadas
- ✅ **Manutenibilidade** — mudanças localizadas e previsíveis
- ✅ **Performance** — menos CSS customizado para carregar

#### Principais Styling Hooks

```css
/* Cores */
--slds-c-button-brand-color-background
--slds-c-card-color-background
--slds-c-input-color-border

/* Espaçamentos */
--slds-c-button-spacing-block
--slds-c-card-spacing-padding
--slds-c-input-spacing-inline

/* Tipografia */
--slds-c-button-text-font-size
--slds-c-card-heading-text-font-weight
```

💡 **Pulo do Gato**: Use o **Lightning Inspector** para descobrir quais styling hooks estão disponíveis para cada componente. Eles aparecem na aba "Styles" do DevTools.

**Documentação completa**: [SLDS Styling Hooks](https://www.lightningdesignsystem.com/platforms/lightning/styling-hooks/)

---

### Quando usar SLDS 1 vs SLDS 2?

| Cenário | Recomendação |
|---------|--------------|
| **Componentes novos** | SLDS 2 com Styling Hooks |
| **Componentes legados** | Manter SLDS 1 (funcionará normalmente) |
| **Customização profunda** | SLDS 2 com Cosmos Theme |
| **Blueprints HTML puros** | SLDS 1 (ainda suportado) |
| **Base Lightning Components** | SLDS 2 (nativamente integrado) |

💡 **Pulo do Gato**: Comece novos projetos com SLDS 2 e Styling Hooks. Migre componentes antigos gradualmente conforme necessário.

### Usando SLDS em LWC

**Boas Práticas:**

1. **Prefira Base Lightning Components:**
```html
<!-- ✅ Recomendado -->
<lightning-button label="Salvar" variant="brand" onclick={handleSave}></lightning-button>

<!-- ⚠️ Evite criar do zero quando houver componente nativo -->
<button class="slds-button slds-button_brand" onclick={handleSave}>Salvar</button>
```

2. **Use Utility Classes para Layout:**
```html
<div class="slds-grid slds-wrap slds-gutters">
    <div class="slds-col slds-size_1-of-2">
        <p>Coluna 1</p>
    </div>
    <div class="slds-col slds-size_1-of-2">
        <p>Coluna 2</p>
    </div>
</div>
```

3. **Evite CSS Customizado Desnecessário:**

❌ **Ruim:**
```css
.meu-botao {
    background: #0070d2;
    color: white;
    border-radius: 4px;
    padding: 8px 16px;
}
```

✅ **Bom:**
```html
<lightning-button variant="brand"></lightning-button>
```

---

### Acessibilidade First: Design para Todos

O SLDS foi construído com acessibilidade como prioridade número um, não como "algo a ser adicionado depois". Todos os componentes seguem **WCAG 2.1 Level AA**.

**WCAG** (Web Content Accessibility Guidelines) é o padrão internacional para acessibilidade web, garantindo que pessoas com deficiências possam usar a web.

#### WCAG: O Guia da Acessibilidade

**WCAG (Web Content Accessibility Guidelines)** é o conjunto de diretrizes globais que definem como tornar conteúdo web acessível. Criado pelo W3C (World Wide Web Consortium), é seguido mundialmente.

---

#### Os 4 Princípios do WCAG (POUR)

**1. Perceptível (Perceivable)**
> *"Usuários devem poder perceber a informação apresentada"*

A informação não pode ser invisível para todos os sentidos do usuário.

**Exemplos práticos:**
- Adicionar texto alternativo em imagens
- Fornecer legendas em vídeos
- Usar cores com contraste adequado

**2. Operável (Operable)**
> *"Usuários devem poder operar a interface"*

A interface não pode exigir interação que o usuário não consegue realizar.

**Exemplos práticos:**
- Navegação por teclado (Tab, Enter, Arrow keys)
- Tempo suficiente para ler e completar tarefas
- Evitar conteúdo que pisca/pisca rapidamente (pode causar convulsões)

**3. Compreensível (Understandable)**
> *"Usuários devem entender a informação e como operar a interface"*

O conteúdo ou operação não pode estar além da compreensão do usuário.

**Exemplos práticos:**
- Linguagem clara e simples
- Comportamento previsível (navegação consistente)
- Mensagens de erro claras e úteis

**4. Robusto (Robust)**
> *"Usuários devem acessar o conteúdo usando diversos user agents, incluindo tecnologias assistivas"*

O conteúdo deve funcionar com tecnologias presentes e futuras.

---

**Princípios de acessibilidade no SLDS:**

**1. Labels sempre presentes:**
```html
<!-- ❌ Ruim - sem label -->
<input type="email" placeholder="Email"/>

<!-- ✅ Bom - com label -->
<label for="email-input">Email</label>
<input type="email" id="email-input"/>
```

**2. ARIA attributes quando necessário:**
```html
<!-- ARIA label quando não há label visual -->
<button aria-label="Fechar modal">
    <lightning-icon icon-name="utility:close"></lightning-icon>
</button>

<!-- ARIA describedby para ajuda contextual -->
<input 
    id="password" 
    type="password"
    aria-describedby="password-help"
/>
<div id="password-help">Mínimo 8 caracteres</div>

<!-- ARIA live para atualizações dinâmicas -->
<div aria-live="polite" aria-atomic="true">
    <p>5 novos itens adicionados</p>
</div>
```

**3. Estados visuais E semânticos:**
```html
<!-- Erro - visual + semântico -->
<div class="slds-form-element slds-has-error">
    <label for="input-error">Campo obrigatório</label>
    <input 
        id="input-error" 
        class="slds-input" 
        aria-describedby="error-message"
        aria-invalid="true"
    />
    <div id="error-message" class="slds-form-element__help">
        Este campo é obrigatório
    </div>
</div>

<!-- Loading - visual + semântico -->
<div role="status" aria-live="polite">
    <lightning-spinner></lightning-spinner>
    <span class="slds-assistive-text">Carregando dados...</span>
</div>
```

**4. Navegação por teclado:**
```html
<!-- Todos elementos interativos devem ser acessíveis por teclado -->
<button tabindex="0">Clicável</button>

<!-- Skip links para pular navegação -->
<a href="#main-content" class="slds-assistive-text slds-assistive-text_focus">
    Pular para conteúdo principal
</a>
```

**Termos importantes:**
- **ARIA** (Accessible Rich Internet Applications): Atributos HTML que fornecem informações adicionais para tecnologias assistivas
- **Screen Reader**: Software que lê conteúdo da tela em voz alta para pessoas com deficiência visual
- **WCAG**: Web Content Accessibility Guidelines - padrão de acessibilidade
- **`assistive-text`**: Classe SLDS que esconde texto visualmente mas mantém para leitores de tela

**Classe Especial - slds-assistive-text:**
```html
<button>
    <lightning-icon icon-name="utility:delete"></lightning-icon>
    <span class="slds-assistive-text">Deletar item</span>
</button>
```
Visualmente só mostra o ícone, mas screen readers leem "Deletar item".

**Referência:** [Accessibility](https://www.lightningdesignsystem.com/guidelines/accessibility/)

---

### Dicas

- 📚 **Marque como favorito:** [https://www.lightningdesignsystem.com](https://www.lightningdesignsystem.com)
- 🎨 **Use o SLDS Validator** no VS Code para garantir conformidade
- 🚫 **Evite CSS customizado** sempre que possível - use utility classes
- 🔍 **Explore os exemplos** de cada componente na documentação
- ⚡ **Abuse das utility classes** - elas são suas melhores amigas
- 📚 **Teste acessibilidade:** [https://webaim.org/resources/contrastchecker/](https://webaim.org/resources/contrastchecker/)

**Pulo do Gato:** Quando precisar estilizar algo, primeiro pergunte: "O SLDS já tem isso?" A resposta geralmente é sim!

---

## Troubleshooting: Quando as coisas dão errado

### Debug Mode

Ativar o Debug Mode na org torna o troubleshooting muito mais fácil. Com Debug Mode habilitado, os Lightning web components não são minificados, então os nomes das variáveis permanecem os mesmos e a estrutura geral do código permanece.

**Como Ativar:**
1. Setup → Quick Find: "Debug Mode"
2. Check na caixa ao lado do seu usuário
3. Click **Enable**

**Resultado:**
- Código legível no DevTools
- Variáveis com nomes originais
- Stack traces úteis

🚨 **Importante:** Debug Mode afeta performance — use apenas em desenvolvimento/sandbox!

---

### Chrome DevTools: Seu melhor amigo

O Chrome DevTools é sua ferramenta mais poderosa para debugar LWCs. Ele oferece tudo que você precisa para investigar problemas, inspecionar variáveis e entender o fluxo de execução.

**Atalhos essenciais:**
- `F12` - Abre/fecha DevTools
- `Ctrl+Shift+C` (Windows) / `Cmd+Shift+C` (Mac) - Inspect element
- `Ctrl+Shift+J` (Windows) / `Cmd+Option+J` (Mac) - Console

**Principais painéis:**

| Painel | Função | Atalho | Quando Usar |
|--------|--------|--------|-------------|
| **Elements** | Inspeciona DOM e CSS | `Cmd+Shift+C` | Debug de layout, estilos, HTML |
| **Console** | Logs e execução JavaScript | `Cmd+Option+J` | Ver erros, testar código |
| **Sources** | Debug JavaScript com breakpoints | — | Passo-a-passo no código |
| **Network** | Monitora requisições HTTP | — | Debug de chamadas Apex, APIs |
| **Application** | Storage, cache, PWA | — | Ver localStorage, sessionStorage |
| **Performance** | Perfil de performance | — | Identificar gargalos |
| **Memory** | Análise de memória | — | Debug de memory leaks |

**Documentação**: [Debug JavaScript](https://developer.chrome.com/docs/devtools/javascript)

---

**Console — Logs e Execução de Código:**
```javascript
// Teste expressões JavaScript
console.log(this.dados);
console.table(this.listaItens);
```

**Comandos Úteis:**
- `console.log()` — log simples
- `console.table()` — visualizar arrays/objetos em tabela
- `console.error()` — destacar erros
- `console.warn()` — avisos
- `JSON.stringify(objeto, null, 2)` — formatar JSON legível

---

**Sources — Navegação e Debug de Código:**

**Localizar Seu Componente:**
1. Abra o painel **Sources**
2. Navegue: `lightning/r/...` ou procure pelo nome do arquivo
3. No File Navigator, todos os arquivos solicitados do servidor são listados

**Estrutura:**
```
Sources
├── File Navigator (lista de arquivos)
├── Code Editor (código fonte)
└── Debugger (breakpoints, call stack)
```

---

### Breakpoints: Parando o Tempo

Breakpoints permitem pausar a execução do JavaScript. Enquanto pausado, você pode visualizar o estado das variáveis e as condições do seu código.

É como apertar "pause" em um filme para analisar cada frame.

**Tipos de Breakpoints:**

#### 1. Line-of-code Breakpoint
Pausa antes de uma linha específica executar.

**Como Adicionar:**
1. Abra o arquivo no Sources panel
2. Clique no número da linha (à esquerda do código)
3. Uma marcação azul aparece

**Uso:**
```javascript
handleIncrement(event) {
    // Adicione breakpoint AQUI ⬇️
    this.contador = this.contador + 1; // ← Clique no número da linha
    console.log('Novo valor:', this.contador);
}
```

**Controles de Execução:**
- ▶️ **Resume** — Continua até o próximo breakpoint
- ⤵️ **Step Over** — Executa linha atual e vai para a próxima
- ⤴️ **Step Into** — Entra na função sendo chamada
- ⤴️⤵️ **Step Out** — Sai da função atual

---

#### 2. Conditional Breakpoint
Pausa apenas quando uma condição é verdadeira.

**Como Adicionar:**
1. Clique com direito no número da linha
2. **Add conditional breakpoint**
3. Digite condição: `this.contador > 5`

**Exemplo:**
```javascript
handleClick() {
    this.contador++; // Pausa só quando contador > 5
    this.atualizarTela();
}
```

---

#### 3. DOM Breakpoints
Pausa quando o DOM muda (elemento modificado, filho adicionado/removido).

**Como Adicionar:**
1. Elements panel → Clique com direito no elemento
2. Break on → Subtree modifications

**Documentação**: [Pause your code with breakpoints](https://developer.chrome.com/docs/devtools/javascript/breakpoints)

---

## Boas Práticas

### Troubleshooting

1. **Sempre ative Debug Mode em desenvolvimento**
2. **Use breakpoints estratégicos** — não em cada linha!
3. **Valide dados em cada etapa** com `console.log()` ou `console.table()`
4. **Limpe logs antes de deploy para produção** 🚨

### Aura vs LWC

1. **Prefira LWC para novos desenvolvimentos**
2. **Mantenha Aura apenas onde necessário** (legado)
3. **Use Aura como wrapper quando precisar de features exclusivas**
4. **Não misture padrões** — seja consistente no estilo

### SLDS

1. **Use Base Lightning Components sempre que possível**
2. **Aplique utility classes antes de criar CSS customizado**
3. **Teste responsividade** em mobile, tablet e desktop
4. **Valide acessibilidade** (contraste, navegação por teclado)

### Performance

1. **Evite chamadas Apex desnecessárias** — use cache quando possível
2. **Implemente loading states** — sempre informe o usuário sobre operações em andamento
3. **Use @wire para leitura** e chamadas imperativas apenas quando necessário controle fino
4. **Otimize renderização** — minimize loops no template
5. **Lazy loading** — carregue componentes pesados sob demanda

---

Com muito carinho,

🌈 **Gabs Barboza** & 🌸 **Eve** agradecem a sua participação nesse treinamento! 

Que você domine tanto o passado (Aura) quanto o futuro (LWC) com maestria e confiança. Seguimos juntos construindo interfaces incríveis! 🚀

<img src="./footer.jpg" alt="footer" style="width: 100%; display: block; margin: 0;">

---
