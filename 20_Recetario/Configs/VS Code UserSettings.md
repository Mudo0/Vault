---
status: final
tags:
  - vscode
  - json
  - configuracion
created: 2025-12-10
---

### settings.json

```json
{
  "editor.wordWrap": "wordWrapColumn",
  "editor.wordWrapColumn": 69,
  "editor.fontSize": 14,

  

  "window.restoreWindows": "none",
  "security.workspace.trust.untrustedFiles": "open",
  "editor.detectIndentation": false,
  "editor.tabSize": 1,
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.renderWhitespace": "none",
  "terminal.integrated.defaultProfile.windows": "PowerShell",

  "emmet.includeLanguages": {

    "javascript": "html"

  },

  "liveServer.settings.donotVerifyTags": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "[csharp]": {

    "editor.maxTokenizationLineLength": 2500,
    "editor.inlineSuggest.suppressSuggestions": false,
    "editor.formatOnType": true

  },
  "editor.formatOnPaste": true,
  "editor.formatOnSave": true,
  "editor.formatOnType": true,
  "codeium.enableConfig": {
    "*": true,
    "markdown": true

  },

  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.maxTokenizationLineLength": 2500,
    "editor.formatOnPaste": true,
    "editor.formatOnSave": true,
    "editor.formatOnType": true
  },

  "[html]": {

    // "editor.defaultFormatter": "vscode.html-language-features"
    "editor.defaultFormatter": "esbenp.prettier-vscode"

  },

  //iconos
  "workbench.iconTheme": "material-icon-theme",
  "workbench.productIconTheme": "fluent-icons",

  

  // carpetas
  "material-icon-theme.folders.theme": "specific",
  "material-icon-theme.hidesExplorerArrows": true,
  "workbench.tree.enableStickyScroll": false,
  "workbench.tree.indent": 16,
  "workbench.tree.renderIndentGuides": "onHover",
  "explorer.compactFolders": false,
  "explorer.confirmDragAndDrop": false,

  //barra de navegacion lateral
  "workbench.sideBar.location": "right",


  "window.zoomLevel": 1.5,

  "window.titleBarStyle": "custom",

  "window.customTitleBarVisibility": "never",

  "window.title": "(. ❛ ᴗ ❛.) - Visual Studio Code",

  

  /////////////////////
  "apc.electron": {
    "frame": false,
    "titleBarStyle": "hidden",
    "titleBarOverlay": {
      "color": "#2f3241",
      "symbolColor": "#74b1be",
      "height": 60
    }
  },

  
  "apc.header": {
    "height": 37
  },
  "apc.sidebar.titlebar": {
    "height": 37
  },
  "apc.activityBar": {
    "size": 77,
    "itemSize": 48,
    "itemMargin": 0
  },

  "apc.stylesheet": {
    ".custom-sidebar-titlebar .sidebar .composite.title": "display: none;padding-left: 0;", // Don't indent the sidebar title. We want it horizontally aligned to the left so that it makes a nice vertical column with the controls in the sidebar.
    ".custom-sidebar-titlebar .sidebar .composite.title .inline-titlebar-placeholder": "padding-left: 0 !important;", // Don't indent the sidebar title. Part 2 to remove the empty space to the left of the sidebar title and complete the proper horizontal left alignment.
    ".monaco-workbench .part.statusbar>.items-container>.statusbar-item.left.first-visible-item": "padding-left: 0; display: none;" // Don't indent the statusbar items. This horizontally aligns the statusbar items with the "Problems" header in the panel, which looks nice.
  },

  /////////////////////

  "workbench.statusBar.visible": false,
  "custom-ui-style.electron": {
    "titleBarStyle": "hiddenInset"
  },

  

  //custom ui
  "custom-ui-style.stylesheet": {

    //desactiva la sombra del cuadro de notificaciones
    ".notification-toast": "box-shadow: none !important",

    //desactiva la sombra del command palette
    // ".quick-input-widget.show-file-icons": "box-shadow: none !important",

    //posicion del command palette
    ".quick-input-widget": "top: 25vh !important",

    //esconde el scrollbar de la command palette
    ".quick-input-list .scrollbar": "display: none ",

  

    ".quick-input-titlebar": "background: #161417 !important",
    //desactiva la sombra del ctrl+f
    "editor-widget.find-widget": "box-shadow: none; border-radius: 4px",
  

    //esconde el espacio vacio en el input de la command palette
    ".monaco-action-bar.quick-input-inline-action-bar": "display: none",
    ".title-actions:": "display: none !important",
    ".monaco-scrollable-element > .shadow.top": "display: none",
    ".sidebar .title-label": "padding: 0 !important",
    ".sidebar": "border: none !important",
    ".title.show-file-icons .label-container .monaco-icon-label.file-icon ": "justify-content: center; padding: 0 !important",

    ".monaco-workbench .monaco-list:not(.element-focused):focus:before": "outline: none !important",
    ".monaco-list-row.focused": "outline: none !important",
    ".title .monaco-icon-label:after": "margin-right: 0",

  

    //le da padding al titulo 60px a la derecha
    ".monaco-workbench .part.editor > .content .editor-group-container > .title > .label-container > .title-label": "padding-left: 60px"

  },

  

  //pestaña unica
  "workbench.editor.showTabs": "single",

  

  "workbench.layoutControl.enabled": false,
  
  //inicio de vscode
  "workbench.startupEditor": "none",
  "workbench.tips.enabled": false,
  "editor.minimap.autohide": "mouseover",
  "editor.guides.indentation": false,
  "indentRainbow.colorOnWhiteSpaceOnly": true,

  

  //colores
    "editor.tokenColorCustomizations": {
    "[*Light*]": {
      "textMateRules": [
        {
          "scope": "ref.matchtext",
          "settings": {
            "foreground": "#000"
          }
        }
      ]
    },

    "[*Dark*]": {
      "textMateRules": [
        {
          "scope": "ref.matchtext",
          "settings": {
            "foreground": "#fff"
          }
        }
      ]
    }
  },

  

  //editor de texto
  "editor.renderLineHighlight": "gutter",
  "editor.renderLineHighlightOnlyWhenFocus": false,
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 3000,
  "editor.cursorBlinking": "expand",
  "editor.cursorStyle": "line",
  "editor.cursorWidth": 2,
  "editor.linkedEditing": true,
  "workbench.editor.enablePreview": false,
  "editor.smoothScrolling": true,
  "editor.snippetSuggestions": "top",
  "breadcrumbs.enabled": false,
  "editor.lightbulb.enabled": "off",
  "editor.hover.enabled": false,
  "editor.stickyScroll.enabled": false,
  "editor.scrollbar.horizontal": "hidden",
  "editor.scrollbar.vertical": "hidden",
  "editor.overviewRulerBorder": false,
  "editor.hideCursorInOverviewRuler": true,
  "editor.cursorSmoothCaretAnimation": "on",
  "editor.fontLigatures": true,
  "editor.lineHeight": 1.5,

  
  "diffEditor.ignoreTrimWhitespace": true,
  "files.insertFinalNewline": true,

  

  "git.autofetch": true,
  "workbench.colorCustomizations": {
    "terminal.background": "#00000000"
  },

  "workbench.settings.applyToAllProfiles": ["workbench.colorCustomizations"],
  "glassit.alpha": 250,
  "terminal.integrated.env.windows": {},

  

  "errorLens.enabledDiagnosticLevels": ["error", "warning", "info"],
  "errorLens.messageEnabled": true,

  

  // Edita el estilo de las ventanas de vscode

  "vscode_custom_css.imports": [
    "file:///C:/Users/mateo/Documents/Facu/custom-vscode.css",
    "file:///C:/Users/mateo/Documents/Facu/custom-vscode.js"
  ],

  "workbench.colorTheme": "Next.js - Unified Glow",
  "workbench.activityBar.location": "hidden",
  "chat.commandCenter.enabled": false,
  "workbench.navigationControl.enabled": false,
  "window.commandCenter": false,
  "window.menuBarVisibility": "hidden",
  "extensions.ignoreRecommendations": true,
  "mssql.connectionGroups": [
    {

      "name": "ROOT",
      "id": "BF62E282-BC9C-4363-91E0-31DE68E4709C"

    }
  ],

  "mssql.connections": [],
  "security.allowedUNCHosts": [
   "wsl.localhost"
  ]
}

```