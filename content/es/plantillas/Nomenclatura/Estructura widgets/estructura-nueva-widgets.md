+++
title = "Estructura nueva de Widgets"
linkTitle = "Estructura nueva de Widgets"
description = "Estructura nueva de Widgets de la ruta output/html/"
weight = 9
+++

Como vimos anteriormente, los Widgets pueden tener [3 rutas de búsqueda](/plantillas/rutas/ubicacion-rutas-widgets/ubicacion-widgets/). La nueva estructura creada solo afecta a la ruta **/output/html/Widgets/** :file_folder:

### Estructura nueva Widgets (output/html/)

Ordenado por importancia los .wid:

1. [BEHAVIOR](#behavior)
2. [ELEMENT](#element)
3. [HTML](#html)
4. [LAYOUT](#layout)
5. [Toda la estructura completa](#estructura-completa)

### BEHAVIOR

```git
📦BEHAVIOR
 ┣  📂MODAL
 ┃      ┣ 📜MODAL.wid
 ┃      ┗ 📜VENTANA_MODAL.wid
 ┣  📜CARD.wid
 ┗  📜COLLAPSE.wid
```

### ELEMENT

```git
📦ELEMENT
 ┣   📂BUTTON
 ┃    ┣   📜ACCEPT.wid
 ┃    ┣   📜ADD.wid
 ┃    ┣   📜BUTTON.wid
 ┃    ┣   📜CANCEL.wid
 ┃    ┣   📜DELETE.wid
 ┃    ┗   📜SEND.wid
 ┃
 ┣    📂CONTENT
 ┃    ┣   📜BLOCKQUOTE.wid
 ┃    ┣   📜CITE.wid
 ┃    ┣   📜CODE.wid
 ┃    ┗   📜PARRAFO.wid
 ┃
 ┣    📂FORM
 ┃    ┣   📂BUTTONS
 ┃    ┃   ┗ 📜BUTTON_HORIZONTAL.wid
 ┃    ┣   📂GROUPS
 ┃    ┃   ┣ 📜HORIZONTAL.wid
 ┃    ┃   ┗ 📜VERTICAL.wid
 ┃    ┣   📂INPUTCONTAINER
 ┃    ┃   ┣ 📜HORIZONTAL.wid
 ┃    ┃   ┣ 📜HORIZONTAL_ICONS.wid
 ┃    ┃   ┗ 📜VERTICAL.wid
 ┃    ┣   📂INPUTS
 ┃    ┃   ┣ 📜CHECKBOX.wid
 ┃    ┃   ┣ 📜DATASOURCEDINPUT.wid
 ┃    ┃   ┣ 📜DATETIME.wid
 ┃    ┃   ┣ 📜FILE.wid
 ┃    ┃   ┣ 📜RADIO.wid
 ┃    ┃   ┣ 📜SELECT.wid
 ┃    ┃   ┣ 📜SELECTMULTIPLE.wid
 ┃    ┃   ┣ 📜SUBMIT.wid
 ┃    ┃   ┣ 📜TEXTAREA.wid
 ┃    ┃   ┗ 📜TEXTFIELD.wid
 ┃    ┗ 📜FORM.wid
 ┃
 ┣    📂MEDIA
 ┃    ┣   📜ICON.wid
 ┃    ┣   📜IFRAME.wid
 ┃    ┣   📜IMAGE.wid
 ┃    ┣   📜SVG.wid
 ┃    ┗   📜VIDEO.wid
 ┃
 ┣    📂TEXT
 ┃    ┣   📜ITALIC.wid
 ┃    ┣   📜LINK.wid
 ┃    ┗   📜STRONG.wid
 ┃
 ┣    📂TITLE
 ┃    ┣   📜H1.wid
 ┃    ┣   📜H2.wid
 ┃    ┣   📜H3.wid
 ┃    ┣   📜H4.wid
 ┃    ┗   📜H5.wid
 ┃
 ┗    📂TYPES
 ┃    ┣   📂INPUTS
 ┃    ┃   ┣ 📜ADD_RELATION_MxN.wid
 ┃    ┃   ┣ 📜BOOLEAN.wid
 ┃    ┃   ┣ 📜DATETIME.wid
 ┃    ┃   ┣ 📜DECIMAL.wid
 ┃    ┃   ┣ 📜EMAIL.wid
 ┃    ┃   ┣ 📜ENUM.wid
 ┃    ┃   ┣ 📜FILE.wid
 ┃    ┃   ┣ 📜IMAGE.wid
 ┃    ┃   ┣ 📜INTEGER.wid
 ┃    ┃   ┣ 📜IP.wid
 ┃    ┃   ┣ 📜LABEL.wid
 ┃    ┃   ┣ 📜LOGIN.wid
 ┃    ┃   ┣ 📜NAME.wid
 ┃    ┃   ┣ 📜PASSWORD.wid
 ┃    ┃   ┣ 📜RELATION_1xN.wid
 ┃    ┃   ┣ 📜RELATION_MxN.wid
 ┃    ┃   ┣ 📜STATE.wid
 ┃    ┃   ┣ 📜TEXTAREA.wid
 ┃    ┃   ┣ 📜TIMESTAMP.wid
 ┃    ┃   ┗ 📜_STRING.wid
 ┃    ┣   📜AUTOINCREMENT.wid
 ┃    ┣   📜BOOLEAN.wid
 ┃    ┣   📜DATETIME.wid
 ┃    ┣   📜DECIMAL.wid
 ┃    ┣   📜EMAIL.wid
 ┃    ┣   📜ENUM.wid
 ┃    ┣   📜IMAGE.wid
 ┃    ┣   📜INTEGER.wid
 ┃    ┣   📜IP.wid
 ┃    ┣   📜LOGIN.wid
 ┃    ┣   📜PASSWORD.wid
 ┃    ┣   📜PO.wid
 ┃    ┣   📜RELATIONSHIP.wid
 ┃    ┣   📜STATE.wid
 ┃    ┣   📜TEXT.wid
 ┃    ┣   📜TIMESTAMP.wid
 ┃    ┣   📜USER_ID.wid
 ┗    ┗   📜_STRING.wid
```

### HTML

```git
📦HTML
 ┣     📂CONTAINER
 ┃      ┣ 📜CONTAINER_SIMPLE.wid
 ┃      ┗ 📜SUBCONTAINER.wid
 ┣      📂METADATA
 ┃      ┣ 📜CSS.wid
 ┃      ┣ 📜META.wid
 ┃      ┣ 📜SCRIPT.wid
 ┃      ┗ 📜STYLE.wid
 ┗ 📜HTMLPAGE.wid
```

### LAYOUT

```git
📦LAYOUT
 ┣     📂FOOTER
 ┃      ┣ 📜FOOTER.wid
 ┃      ┣ 📜FOOTER_FIXED.wid
 ┃      ┗ 📜FOOTER_STATIC.wid
 ┃
 ┣      📂FORMS
 ┃      ┣ 📜HORIZONTAL.wid
 ┃      ┗ 📜VERTICAL.wid
 ┃
 ┣      📂NAVIGATION
 ┃      ┣   📂BREADCRUMBS
 ┃      ┃   ┣ 📜BREADCRUMBS.wid
 ┃      ┃   ┣ 📜LINK_BREADCRUMBS.wid
 ┃      ┃   ┗ 📜LIST_DS_BREADCRUMBS.wid
 ┃      ┣   📂TOOLBAR
 ┃      ┃   ┣ 📜TOOLBAR.wid
 ┃      ┃   ┣ 📜TOOLBAR_EXTRA_MENU.wid
 ┃      ┃   ┣ 📜TOOLBAR_HORIZONTAL.wid
 ┃      ┃   ┗ 📜TOOLBAR_USER_MENU.wid
 ┃      ┣ 📜LINK_MENU.wid
 ┃      ┣ 📜LIST_DS_MENU.wid
 ┃      ┣ 📜MAIN_MENU.wid
 ┃      ┗ 📜MAIN_MENU_HORIZONTAL.wid
 ┃
 ┣      📂PAGE
 ┃      ┣ 📜LAYOUT_HORIZONTAL.wid
 ┃      ┣ 📜LAYOUT_VERTICAL.wid
 ┃      ┗ 📜LAYOUT_VERTICAL_2COL_WHITE.wid
 ┗ 📜LAYOUT.wid
```

### ESTRUCTURA COMPLETA

```git
📦BEHAVIOR
 ┣   📂MODAL
 ┃      ┣ 📜MODAL.wid
 ┃      ┗ 📜VENTANA_MODAL.wid
 ┣  📜CARD.wid
 ┗  📜COLLAPSE.wid


📦ELEMENT
 ┣   📂BUTTON
 ┃    ┣   📜ACCEPT.wid
 ┃    ┣   📜ADD.wid
 ┃    ┣   📜BUTTON.wid
 ┃    ┣   📜CANCEL.wid
 ┃    ┣   📜DELETE.wid
 ┃    ┗   📜SEND.wid
 ┃
 ┣    📂CONTENT
 ┃    ┣   📜BLOCKQUOTE.wid
 ┃    ┣   📜CITE.wid
 ┃    ┣   📜CODE.wid
 ┃    ┗   📜PARRAFO.wid
 ┃
 ┣    📂FORM
 ┃    ┣   📂BUTTONS
 ┃    ┃   ┗ 📜BUTTON_HORIZONTAL.wid
 ┃    ┣   📂GROUPS
 ┃    ┃   ┣ 📜HORIZONTAL.wid
 ┃    ┃   ┗ 📜VERTICAL.wid
 ┃    ┣   📂INPUTCONTAINER
 ┃    ┃   ┣ 📜HORIZONTAL.wid
 ┃    ┃   ┣ 📜HORIZONTAL_ICONS.wid
 ┃    ┃   ┗ 📜VERTICAL.wid
 ┃    ┣   📂INPUTS
 ┃    ┃   ┣ 📜CHECKBOX.wid
 ┃    ┃   ┣ 📜DATASOURCEDINPUT.wid
 ┃    ┃   ┣ 📜DATETIME.wid
 ┃    ┃   ┣ 📜FILE.wid
 ┃    ┃   ┣ 📜RADIO.wid
 ┃    ┃   ┣ 📜SELECT.wid
 ┃    ┃   ┣ 📜SELECTMULTIPLE.wid
 ┃    ┃   ┣ 📜SUBMIT.wid
 ┃    ┃   ┣ 📜TEXTAREA.wid
 ┃    ┃   ┗ 📜TEXTFIELD.wid
 ┃    ┗ 📜FORM.wid
 ┃
 ┣    📂MEDIA
 ┃    ┣   📜ICON.wid
 ┃    ┣   📜IFRAME.wid
 ┃    ┣   📜IMAGE.wid
 ┃    ┣   📜SVG.wid
 ┃    ┗   📜VIDEO.wid
 ┃
 ┣    📂TEXT
 ┃    ┣   📜ITALIC.wid
 ┃    ┣   📜LINK.wid
 ┃    ┗   📜STRONG.wid
 ┃
 ┣    📂TITLE
 ┃    ┣   📜H1.wid
 ┃    ┣   📜H2.wid
 ┃    ┣   📜H3.wid
 ┃    ┣   📜H4.wid
 ┃    ┗   📜H5.wid
 ┃
 ┗    📂TYPES
 ┃    ┣   📂INPUTS
 ┃    ┃   ┣ 📜ADD_RELATION_MxN.wid
 ┃    ┃   ┣ 📜BOOLEAN.wid
 ┃    ┃   ┣ 📜DATETIME.wid
 ┃    ┃   ┣ 📜DECIMAL.wid
 ┃    ┃   ┣ 📜EMAIL.wid
 ┃    ┃   ┣ 📜ENUM.wid
 ┃    ┃   ┣ 📜FILE.wid
 ┃    ┃   ┣ 📜IMAGE.wid
 ┃    ┃   ┣ 📜INTEGER.wid
 ┃    ┃   ┣ 📜IP.wid
 ┃    ┃   ┣ 📜LABEL.wid
 ┃    ┃   ┣ 📜LOGIN.wid
 ┃    ┃   ┣ 📜NAME.wid
 ┃    ┃   ┣ 📜PASSWORD.wid
 ┃    ┃   ┣ 📜RELATION_1xN.wid
 ┃    ┃   ┣ 📜RELATION_MxN.wid
 ┃    ┃   ┣ 📜STATE.wid
 ┃    ┃   ┣ 📜TEXTAREA.wid
 ┃    ┃   ┣ 📜TIMESTAMP.wid
 ┃    ┃   ┗ 📜_STRING.wid
 ┃    ┣   📜AUTOINCREMENT.wid
 ┃    ┣   📜BOOLEAN.wid
 ┃    ┣   📜DATETIME.wid
 ┃    ┣   📜DECIMAL.wid
 ┃    ┣   📜EMAIL.wid
 ┃    ┣   📜ENUM.wid
 ┃    ┣   📜IMAGE.wid
 ┃    ┣   📜INTEGER.wid
 ┃    ┣   📜IP.wid
 ┃    ┣   📜LOGIN.wid
 ┃    ┣   📜PASSWORD.wid
 ┃    ┣   📜PO.wid
 ┃    ┣   📜RELATIONSHIP.wid
 ┃    ┣   📜STATE.wid
 ┃    ┣   📜TEXT.wid
 ┃    ┣   📜TIMESTAMP.wid
 ┃    ┣   📜USER_ID.wid
 ┗    ┗   📜_STRING.wid


📦HTML
 ┣     📂CONTAINER
 ┃      ┣ 📜CONTAINER_SIMPLE.wid
 ┃      ┗ 📜SUBCONTAINER.wid
 ┣      📂METADATA
 ┃      ┣ 📜CSS.wid
 ┃      ┣ 📜META.wid
 ┃      ┣ 📜SCRIPT.wid
 ┃      ┗ 📜STYLE.wid
 ┗ 📜HTMLPAGE.wid


📦LAYOUT
 ┣     📂FOOTER
 ┃      ┣ 📜FOOTER.wid
 ┃      ┣ 📜FOOTER_FIXED.wid
 ┃      ┗ 📜FOOTER_STATIC.wid
 ┃
 ┣      📂FORMS
 ┃      ┣ 📜HORIZONTAL.wid
 ┃      ┗ 📜VERTICAL.wid
 ┃
 ┣      📂NAVIGATION
 ┃      ┣   📂BREADCRUMBS
 ┃      ┃   ┣ 📜BREADCRUMBS.wid
 ┃      ┃   ┣ 📜LINK_BREADCRUMBS.wid
 ┃      ┃   ┗ 📜LIST_DS_BREADCRUMBS.wid
 ┃      ┣   📂TOOLBAR
 ┃      ┃   ┣ 📜TOOLBAR.wid
 ┃      ┃   ┣ 📜TOOLBAR_EXTRA_MENU.wid
 ┃      ┃   ┣ 📜TOOLBAR_HORIZONTAL.wid
 ┃      ┃   ┗ 📜TOOLBAR_USER_MENU.wid
 ┃      ┣ 📜LINK_MENU.wid
 ┃      ┣ 📜LIST_DS_MENU.wid
 ┃      ┣ 📜MAIN_MENU.wid
 ┃      ┗ 📜MAIN_MENU_HORIZONTAL.wid
 ┃
 ┣      📂PAGE
 ┃      ┣ 📜LAYOUT_HORIZONTAL.wid
 ┃      ┣ 📜LAYOUT_VERTICAL.wid
 ┃      ┗ 📜LAYOUT_VERTICAL_2COL_WHITE.wid
 ┗ 📜LAYOUT.wid
```
