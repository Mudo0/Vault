---
status: borrador
tags:
  - vscode
  - css
  - personalizacion
created: 2025-12-10
---

# 🎨 custom-vscode.css
Estilos personalizados para la interfaz de Visual Studio Code.

```css
/* Code canvas top shadow */
.monaco-editor .scroll-decoration {
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.75) !important;
  top: -6px !important;
}

/* Side bar */
.part.sidebar {
  box-shadow: 0px 0px 50px rgba(0, 0, 0, 0.25);
}

/* Sidebar top shadow */
/* .monaco-scrollable-element > .shadow.top {
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.75) !important;
  top: -3px !important;
} */

/* Command Palette */
/* .quick-input-widget {
  transform: translateY(-50%) !important;
  top: 50% !important;
  box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.45) !important;
  padding: 10px 10px 18px 10px !important;
  
  backdrop-filter: blur(3px) !important;
  
} */

/* Remove background for lists */
.monaco-list-rows {
  background: transparent !important;
}

/* Command palette text input */
/* .quick-input-filter .monaco-inputbox { */
/* border-radius: 12px !important; */
/* padding: 8px !important; */
/* border: none !important; */
/* background-color: rgba(34, 34, 34, 0.4) !important; */
/* font-size: 14px !important; */
/* margin-bottom: 16px !important; */
/* } */

/* #command-blur {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.15);
  top: 0;
  left: 0;
  backdrop-filter: blur(8px);
} */

/* Command palette's input box placeholder. */
/* .monaco-inputbox input::placeholder {
  color: rgba(255, 255, 255, 0.3) !important;
} */

/* Project title's style at the top. */
.monaco-workbench
  .part.titlebar
  > .titlebar-container
  > .titlebar-center
  > .window-title
  > .command-center
  .action-item.command-center-center {
  border: none !important;
  background: transparent !important;
  display: none;
}

/* esconde la barra de arriba */
/* .titlebar-container {
  display: none !important;
} */

/* Project Title */
.titlebar-left {
  display: none !important;
  justify-content: flex-end !important;
  flex-grow: 0 !important;
  /* width: 75px !important; */
}

/* Search Label */
.search-label {
  /* font-family: "Geist Mono" !important; */
  font-size: 14px !important;
  color: #fff;
  display: none;
}

/* Search icon */
.search-icon {
  display: none !important;
}

.codicon-search::before {
  display: none !important;
}

.codicon-arrow-right,
.codicon-arrow-left {
  display: none !important;
}

.titlebar-right > * {
  display: none !important;
}

.command-center-center {
  width: auto !important;
}

```