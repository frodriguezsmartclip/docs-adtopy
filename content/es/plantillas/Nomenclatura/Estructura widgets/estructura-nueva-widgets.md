+++
title = "Estructura nueva de Widgets"
linkTitle = "Estructura nueva de Widgets"
description = "Estructura nueva de Widgets de la ruta output/html/"
weight = 5
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

```bash
├── BEHAVIOR
│   └── BEHAVIOR/MODAL
│       ├── BEHAVIOR/MODAL/MODAL.wid
│       └── BEHAVIOR/MODAL/VENTANA_MODAL.wid
├── BEHAVIOR/CARD.wid
└── BEHAVIOR/COLLAPSE.wid
```

### ELEMENT

```bash
├── ELEMENT
│   └── BUTTON
│       ├── BUTTON/ACCEPT.wid
│       ├── BUTTON/ADD.wid
│       ├── BUTTON/BUTTON.wid
│       ├── BUTTON/CANCEL.wid
│       ├── BUTTON/DELETE.wid
│       └── BUTTON/SEND.wid
│
│   └── CONTENT
│       ├── CONTENT/BLOCKQUOTE.wid
│       ├── CONTENT/CITE.wid
│       ├── CONTENT/CODE.wid
│       └── CONTENT/PARRAFO.wid
│
│   └── FORM
│   └── FORM/BUTTONS
│       └── FORM/BUTTONS/BUTTON_HORIZONTAL.wid
│   └── FORM/GROUPS
│       ├── FORM/GROUPS/HORIZONTAL.wid
│       └── FORM/GROUPS/VERTICAL.wid
│   └── FORM/INPUTCONTAINER
│       ├── FORM/INPUTCONTAINER/HORIZONTAL_ICONS.wid
│       ├── FORM/INPUTCONTAINER/HORIZONTAL.wid
│       └── FORM/INPUTCONTAINER/VERTICAL.wid
│   └── FORM/INPUTS
│       ├── FORM/INPUTS/CHECKBOX.wid
│       ├── FORM/INPUTS/DATASOURCEDINPUT.wid
│       ├── FORM/INPUTS/FILE.wid
│       ├── FORM/INPUTS/RADIO.wid
│       ├── FORM/INPUTS/SELECT.wid
│       ├── FORM/INPUTS/SELECTMULTIPLE.wid
│       ├── FORM/INPUTS/SUBMIT.wid
│       ├── FORM/INPUTS/TEXTAREA.wid
│       └── FORM/INPUTS/TEXTFIELD.wid
│   └── FORM/FORM.wid
│
│   └── MEDIA
│       ├── MEDIA/ICON.wid
│       ├── MEDIA/IFRAME.wid
│       ├── MEDIA/IMAGE.wid
│       ├── MEDIA/SVG.wid
│       └── MEDIA/VIDEO.wid
│
│   └── TEXT
│       ├── TEXT/ITALIC.wid
│       ├── TEXT/LINK.wid
│       └── TEXT/STRONG.wid
│   └── TITLE
│       ├── TITLE/H1.wid
│       ├── TITLE/H2.wid
│       ├── TITLE/H3.wid
│       ├── TITLE/H4.wid
│       └── TITLE/H5.wid
│
│   └── TYPES
│       └── TYPES/INPUTS
│           ├── TYPES/INPUTS/_STRING.wid
│           ├── TYPES/INPUTS/ADD_RELATION_MxN.wid
│           ├── TYPES/INPUTS/BOOLEAN.wid
│           ├── TYPES/INPUTS/DATETIME.wid
│           ├── TYPES/INPUTS/DECIMAL.wid
│           ├── TYPES/INPUTS/EMAIL.wid
│           ├── TYPES/INPUTS/ENUM.wid
│           ├── TYPES/INPUTS/FILE.wid
│           ├── TYPES/INPUTS/IMAGE.wid
│           ├── TYPES/INPUTS/INTEGER.wid
│           ├── TYPES/INPUTS/IP.wid
│           ├── TYPES/INPUTS/LABEL.wid
│           ├── TYPES/INPUTS/LOGIN.wid
│           ├── TYPES/INPUTS/NAME.wid
│           ├── TYPES/INPUTS/PASSWORD.wid
│           ├── TYPES/INPUTS/RELATION_1xN.wid
│           ├── TYPES/INPUTS/RELATION_MxN.wid
│           ├── TYPES/INPUTS/STATE.wid
│           ├── TYPES/INPUTS/TEXTAREA.wid
│           └── TYPES/INPUTS/TIMESTAMP.wid
│   ├── TYPES/_STRING.wid
│   ├── TYPES/AUTOINCREMENT.wid
│   ├── TYPES/BOOLEAN.wid
│   ├── TYPES/DATETIME.wid
│   ├── TYPES/DECIMAL.wid
│   ├── TYPES/EMAIL.wid
│   ├── TYPES/ENUM.wid
│   ├── TYPES/IMAGE.wid
│   ├── TYPES/INTEGER.wid
│   ├── TYPES/IP.wid
│   ├── TYPES/LOGIN.wid
│   ├── TYPES/PASSWORD.wid
│   ├── TYPES/PO.wid
│   ├── TYPES/RELATIONSHIP.wid
│   ├── TYPES/STATE.wid
│   ├── TYPES/TEXT.wid
│   ├── TYPES/TIMESTAMP.wid
└───└── TYPES/USER_ID.wid
```

### HTML

```bash
├── HTML
│   └── HTML/CONTAINER
│       ├── HTML/CONTAINER/CONTAINER_SIMPLE.wid
│       └── HTML/CONTAINER/SUBCONTAINER.wid
│   └── HTML/METADATA
│       ├── HTML/METADATA/CSS.wid
│       ├── HTML/METADATA/META.wid
│       ├── HTML/METADATA/SCRIPT.wid
│       └── HTML/METADATA/STYLE.wid
└───└── HTML/HTMLPAGE.wid
```

### LAYOUT

```bash
├── LAYOUT
│   └── LAYOUT/FOOTER
│       ├── LAYOUT/FOOTER/FOOTER_FIXED.wid
│       ├── LAYOUT/FOOTER/FOOTER_STATIC.wid
│       └── LAYOUT/FOOTER/FOOTER.wid
│
│   └── LAYOUT/FORMS
│       ├── LAYOUT/FORMS/HORIZONTAL.wid
│       └── LAYOUT/FORMS/VERTICAL.wid
│
│   └── LAYOUT/NAVIGATION
│       └── LAYOUT/NAVIGATION/TOOLBAR
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_EXTRA_MENU.wid
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_HORIZONTAL.wid
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_USER_MENU.wid
│           └── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR.wid
│       ├── LAYOUT/NAVIGATION/BREADCRUMBS.wid
│       ├── LAYOUT/NAVIGATION/LINK_MENU.wid
│       ├── LAYOUT/NAVIGATION/LIST_DS_MENU.wid
│       ├── LAYOUT/NAVIGATION/MAIN_MENU_HORIZONTAL.wid
│       └── LAYOUT/NAVIGATION/MAIN_MENU.wid
│
│   └── LAYOUT/PAGE
│       ├── LAYOUT/PAGE/LAYOUT_HORIZONTAL.wid
│       ├── LAYOUT/PAGE/LAYOUT_VERTICAL_2COL_WHITE.wid
│       └── LAYOUT/PAGE/LAYOUT_VERTICAL.wid
└── LAYOUT/LAYOUT.wid
```

### ESTRUCTURA COMPLETA

```bash
├── BEHAVIOR
├── BEHAVIOR/MODAL
│   ├── BEHAVIOR/MODAL/MODAL.wid
│   └── BEHAVIOR/MODAL/VENTANA_MODAL.wid
├── BEHAVIOR/CARD.wid
└── BEHAVIOR/COLLAPSE.wid


├── ELEMENT
│   └── BUTTON
│       ├── BUTTON/ACCEPT.wid
│       ├── BUTTON/ADD.wid
│       ├── BUTTON/BUTTON.wid
│       ├── BUTTON/CANCEL.wid
│       ├── BUTTON/DELETE.wid
│       └── BUTTON/SEND.wid
│
│   └── CONTENT
│       ├── CONTENT/BLOCKQUOTE.wid
│       ├── CONTENT/CITE.wid
│       ├── CONTENT/CODE.wid
│       └── CONTENT/PARRAFO.wid
│
│   └── FORM
│   └── FORM/BUTTONS
│       └── FORM/BUTTONS/BUTTON_HORIZONTAL.wid
│   └── FORM/GROUPS
│       ├── FORM/GROUPS/HORIZONTAL.wid
│       └── FORM/GROUPS/VERTICAL.wid
│   └── FORM/INPUTCONTAINER
│       ├── FORM/INPUTCONTAINER/HORIZONTAL_ICONS.wid
│       ├── FORM/INPUTCONTAINER/HORIZONTAL.wid
│       └── FORM/INPUTCONTAINER/VERTICAL.wid
│   └── FORM/INPUTS
│       ├── FORM/INPUTS/CHECKBOX.wid
│       ├── FORM/INPUTS/DATASOURCEDINPUT.wid
│       ├── FORM/INPUTS/FILE.wid
│       ├── FORM/INPUTS/RADIO.wid
│       ├── FORM/INPUTS/SELECT.wid
│       ├── FORM/INPUTS/SELECTMULTIPLE.wid
│       ├── FORM/INPUTS/SUBMIT.wid
│       ├── FORM/INPUTS/TEXTAREA.wid
│       └── FORM/INPUTS/TEXTFIELD.wid
│   └── FORM/FORM.wid    
│
│
│   └── MEDIA
│       ├── MEDIA/ICON.wid
│       ├── MEDIA/IFRAME.wid
│       ├── MEDIA/IMAGE.wid
│       ├── MEDIA/SVG.wid
│       └── MEDIA/VIDEO.wid
│
│   └── TEXT
│       ├── TEXT/ITALIC.wid
│       ├── TEXT/LINK.wid
│       └── TEXT/STRONG.wid
│   └── TITLE
│       ├── TITLE/H1.wid
│       ├── TITLE/H2.wid
│       ├── TITLE/H3.wid
│       ├── TITLE/H4.wid
│       └── TITLE/H5.wid
│
│
│   └── TYPES
│       └── TYPES/INPUTS
│           ├── TYPES/INPUTS/_STRING.wid
│           ├── TYPES/INPUTS/ADD_RELATION_MxN.wid
│           ├── TYPES/INPUTS/BOOLEAN.wid
│           ├── TYPES/INPUTS/DATETIME.wid
│           ├── TYPES/INPUTS/DECIMAL.wid
│           ├── TYPES/INPUTS/EMAIL.wid
│           ├── TYPES/INPUTS/ENUM.wid
│           ├── TYPES/INPUTS/FILE.wid
│           ├── TYPES/INPUTS/IMAGE.wid
│           ├── TYPES/INPUTS/INTEGER.wid
│           ├── TYPES/INPUTS/IP.wid
│           ├── TYPES/INPUTS/LABEL.wid
│           ├── TYPES/INPUTS/LOGIN.wid
│           ├── TYPES/INPUTS/NAME.wid
│           ├── TYPES/INPUTS/PASSWORD.wid
│           ├── TYPES/INPUTS/RELATION_1xN.wid
│           ├── TYPES/INPUTS/RELATION_MxN.wid
│           ├── TYPES/INPUTS/STATE.wid
│           ├── TYPES/INPUTS/TEXTAREA.wid
│           └── TYPES/INPUTS/TIMESTAMP.wid
│   ├── TYPES/_STRING.wid
│   ├── TYPES/AUTOINCREMENT.wid
│   ├── TYPES/BOOLEAN.wid
│   ├── TYPES/DATETIME.wid
│   ├── TYPES/DECIMAL.wid
│   ├── TYPES/EMAIL.wid
│   ├── TYPES/ENUM.wid
│   ├── TYPES/IMAGE.wid
│   ├── TYPES/INTEGER.wid
│   ├── TYPES/IP.wid
│   ├── TYPES/LOGIN.wid
│   ├── TYPES/PASSWORD.wid
│   ├── TYPES/PO.wid
│   ├── TYPES/RELATIONSHIP.wid
│   ├── TYPES/STATE.wid
│   ├── TYPES/TEXT.wid
│   ├── TYPES/TIMESTAMP.wid
│   └── TYPES/USER_ID.wid
│
│
├── HTML
│   └── HTML/CONTAINER
│       ├── HTML/CONTAINER/CONTAINER_SIMPLE.wid
│       └── HTML/CONTAINER/SUBCONTAINER.wid
│   └── HTML/METADATA
│       ├── HTML/METADATA/CSS.wid
│       ├── HTML/METADATA/META.wid
│       ├── HTML/METADATA/SCRIPT.wid
│       └── HTML/METADATA/STYLE.wid
│   ├── HTML/HTMLPAGE.wid
│
│
├── LAYOUT
│   └── LAYOUT/FOOTER
│       ├── LAYOUT/FOOTER/FOOTER_FIXED.wid
│       ├── LAYOUT/FOOTER/FOOTER_STATIC.wid
│       └── LAYOUT/FOOTER/FOOTER.wid
│
│   └── LAYOUT/FORMS
│       ├── LAYOUT/FORMS/HORIZONTAL.wid
│       └── LAYOUT/FORMS/VERTICAL.wid
│
│   └── LAYOUT/NAVIGATION
│       └── LAYOUT/NAVIGATION/TOOLBAR
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_EXTRA_MENU.wid
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_HORIZONTAL.wid
│           ├── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR_USER_MENU.wid
│           └── LAYOUT/NAVIGATION/TOOLBAR/TOOLBAR.wid
│       ├── LAYOUT/NAVIGATION/BREADCRUMBS.wid
│       ├── LAYOUT/NAVIGATION/LINK_MENU.wid
│       ├── LAYOUT/NAVIGATION/LIST_DS_MENU.wid
│       ├── LAYOUT/NAVIGATION/MAIN_MENU_HORIZONTAL.wid
│       └── LAYOUT/NAVIGATION/MAIN_MENU.wid
│
│  └── LAYOUT/PAGE
│       ├── LAYOUT/PAGE/LAYOUT_HORIZONTAL.wid
│       ├── LAYOUT/PAGE/LAYOUT_VERTICAL_2COL_WHITE.wid
│       └── LAYOUT/PAGE/LAYOUT_VERTICAL.wid
└── LAYOUT/LAYOUT.wid    


├── ADMINPAGE.wid
├── DATASOURCE.wid
├── LIST_DS_TABLE.wid
└── LIST_IT.wid
```
