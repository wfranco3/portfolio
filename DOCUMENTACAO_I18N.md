# 📋 Documentação - Sistema Multi-idioma (PT/EN)

## ✅ O QUE FOI IMPLEMENTADO

### 1. **Sistema de Tradução (i18n)**
- Arquivo: `js/languages.js`
- Classe: `LanguageManager`
- Funcionalidade: Detecta idioma do navegador, persiste escolha em localStorage

### 2. **Recursos Implementados**

#### 🎯 Detecção Automática
- Detecta idioma do navegador (`navigator.language`)
- Se português (pt) ou inglês (en) → usa esse idioma
- Caso contrário, padrão é português

#### 💾 Persistência
- Salva a escolha do usuário em `localStorage` como `selectedLanguage`
- Próxima visita usa o idioma selecionado anteriormente

#### 🔘 Botões de Seleção
- Localização: Menu header (lado direito)
- Estilos: `css/styles.css` linhas ~3160-3200
- CSS:
  - Desativado: borda cinza fina (`1px solid #666666`)
  - Ativo: fundo branco, borda branca, texto preto
  - Altura reduzida: `padding: 0.25rem 0.6rem`

#### 📱 Tradução de Modais
- Quando um modal abre, o sistema:
  1. Aguarda 50ms para renderização
  2. Encontra o modal visível (`.basicLightbox--visible`)
  3. Traduz todos os `data-i18n` dentro do modal
  4. Aplica a tradução correta do idioma selecionado

---

## 🗂️ ESTRUTURA DE TRADUÇÃO

### HTML (index.html)
```html
<!-- Qualquer elemento com data-i18n será traduzido -->
<h2 data-i18n="about_title">Sou desenvolvedor...</h2>
<p data-i18n="services_desc">Meu objetivo é...</p>
```

### JavaScript (js/languages.js)
```javascript
const translations = {
    pt: {
        about_title: "Sou desenvolvedor Low-Code...",
        services_desc: "Meu objetivo é entregar...",
        // ... mais traduções
    },
    en: {
        about_title: "I'm a Low-Code developer...",
        services_desc: "My goal is to deliver...",
        // ... more translations
    }
};
```

---

## 📝 CHAVES DE TRADUÇÃO IMPLEMENTADAS (70+ chaves)

### Menu
- `menu_home`, `menu_about`, `menu_services`, `menu_folio`, `menu_contact`, `menu_toggle`

### Intro
- `intro_title_1`, `intro_title_2`, `intro_title_3`, `intro_btn`, `intro_scroll`

### About
- `about_pretitle`, `about_title`, `about_desc`
- `about_scope_title`, `about_scope_desc`
- `about_design_title`, `about_design_desc`
- `about_develop_title`, `about_develop_desc`
- `about_publish_title`, `about_publish_desc`

### Services
- `services_pretitle`, `services_title`, `services_desc`
- `service_objective_title`, `service_objective_desc`
- `service_1_title`, `service_1_desc`
- `service_2_title`, `service_2_desc`
- `service_3_title`, `service_3_desc`
- `service_4_title`, `service_4_desc`
- `service_extra_title`, `service_extra_desc`

### Portfolio
- `portfolio_pretitle`, `portfolio_title`, `portfolio_desc`

### Modais (6 projetos)
- `modal_01_title`, `modal_01_desc`
- `modal_02_title`, `modal_02_desc`
- `modal_03_title`, `modal_03_desc`
- `modal_04_title`, `modal_04_desc`
- `modal_05_title`, `modal_05_desc`
- `modal_06_title`, `modal_06_desc`

### Tecnologias
- `tech_title`

### Footer
- `footer_pretitle`, `footer_title`
- `footer_address_title`, `footer_address`
- `footer_phone_title`
- `footer_subscribe_title`, `footer_subscribe_placeholder`
- `cta_title`

---

## 🚀 COMO FUNCIONA

### Fluxo de Tradução

1. **Página Carrega**
   - `languages.js` detecta idioma do navegador
   - Chama `setLanguage()` com idioma detectado
   - Marca botão de idioma como `.active`
   - Chama `translatePage()` que traduz todos os elementos

2. **Usuário Clica em Botão de Idioma**
   - Clique dispara `setLanguage('en')` ou `setLanguage('pt')`
   - Salva em `localStorage`
   - Atualiza botões (adiciona/remove classe `.active`)
   - Chama `translatePage()` novamente

3. **Modal Abre**
   - `basicLightbox` renderiza o modal no DOM
   - `onShow` detecta modal visível
   - Encontra todos os `[data-i18n]` dentro dele
   - Traduz cada elemento para o idioma atual

---

## 🎨 ESTILOS DOS BOTÕES

### Arquivo: `css/styles.css` (linhas ~3169-3197)

```css
.lang-btn {
    background: transparent;
    border: 1px solid #666666 !important;  /* Cinza fina quando desativado */
    color: white !important;
    padding: 0.25rem 0.6rem;              /* Altura reduzida */
    font-size: 0.7rem;
    font-weight: 700 !important;
    letter-spacing: 0.12em;
    cursor: pointer;
    transition: all 0.3s ease;
    border-radius: 2px;
    font-family: var(--font-1);
    text-transform: uppercase;
}

.lang-btn:hover {
    border-color: #888888 !important;
    background: rgba(255, 255, 255, 0.05) !important;
    color: white !important;
}

.lang-btn.active {
    background: white !important;        /* Fundo branco quando ativo */
    color: #1a1a1a !important;          /* Texto preto quando ativo */
    border-color: white !important;      /* Borda branca quando ativo */
    border: 1px solid white !important;
    font-weight: 700 !important;
}
```

---

## 📦 ARQUIVOS MODIFICADOS

### 1. `js/languages.js` (NOVO)
- 278 linhas
- Classe `LanguageManager`
- Objeto `translations` com 70+ chaves PT/EN
- Auto-inicialização ao carregar página

### 2. `js/main.js` (MODIFICADO)
- Linhas ~393-415: Adicionado `onShow` para traduzir modais
- Quando modal abre: busca elementos `data-i18n` e traduz

### 3. `css/styles.css` (MODIFICADO)
- Linhas ~3169-3197: Estilos dos botões de idioma
- Borda cinza → branca quando ativo
- Altura reduzida
- Transição suave

### 4. `index.html` (MODIFICADO)
- Linhas ~65-67: Botões PT/EN no header
- Adicionado `data-i18n="chave"` em 70+ elementos
- Referência ao `js/languages.js` (linha ~926)

---

## ✨ COMO USAR (Para Futuras Mudanças)

### Adicionar Novo Texto Traduzível

1. **No HTML:**
```html
<p data-i18n="nova_chave">Texto em português aqui</p>
```

2. **Em `js/languages.js`:**
```javascript
pt: {
    nova_chave: "Texto em português aqui"
}

en: {
    nova_chave: "Text in English here"
}
```

3. **Pronto!** O sistema traduz automaticamente

---

## 🔧 Requisitos para Funcionamento

- ✅ `js/languages.js` carregado ANTES de `js/main.js`
- ✅ Classe `.lang-btn` com `data-lang="pt"` ou `data-lang="en"`
- ✅ Todos os elementos traduzíveis com `data-i18n="chave"`
- ✅ localStorage disponível no navegador

---

## 🐛 Debugar Traduções

No console do navegador:

```javascript
// Ver idioma atual
window.languageManager.currentLang

// Forçar tradução manual
window.languageManager.translatePage()

// Ver todas as traduções
translations

// Mudar idioma
window.languageManager.setLanguage('en')
```

---

## 📊 Status Final

| Recurso | Status |
|---------|--------|
| Menu traduzido | ✅ Completo |
| Intro traduzido | ✅ Completo |
| About traduzido | ✅ Completo |
| Services traduzido | ✅ Completo |
| Portfolio traduzido | ✅ Completo |
| Modais traduzidos | ✅ Completo |
| Footer traduzido | ✅ Completo |
| Botões de idioma | ✅ Completo |
| Persistência localStorage | ✅ Completo |
| Auto-detecção idioma | ✅ Completo |
| Tradução de modais ao abrir | ✅ Completo |

---

## 📌 Notas Importantes

- Os nomes de tecnologias (Flutterflow, Supabase) não são traduzidos (padrão internacional)
- O email no footer aparece como texto puro (sem link) para permitir tradução
- Modais usam `basicLightbox` que clona elementos, por isso a tradução especial ao abrir
- Sistema é totalmente agnóstico - funciona com qualquer idioma adicionando novos objetos em `translations`

---

**Data de Implementação:** 31 de Dezembro de 2025  
**Sistema:** Multi-linguagem PT/EN  
**Versão:** 1.0 (Completo)
