---
title: "Nomenclatura"
linkTitle: "Nomenclatura"
description: "Nomenclatura de Siviglia-js en nuestro sistema de Adtopy."
weight: 3
---

A continuación podremos aprender la nomenclatura que se usa en Siviglia-js, y para que sirve.

{{% alert title="Nota" color="info" %}}

La nomenclatura de abajo se aplica cuando se usa **expandos**. Ver más en detalle aquí: [/siviglia/ejemplos-uso/expandos-loop/](/siviglia/ejemplos-uso/expandos-loop/)

{{% /alert %}}

## Declarar un widget

```html
<div data-sivWidget="nombreWidget"...></div>
```

Con **data-sivWidget**, se declara el widget, para posteriormente poder usarlo en *data-sivView*.

**data-sivWidget** es la llamada que se compone de: nombre del contexto + nombre clase (de *Siviglia.Utils.buildClass*)

## Usar un widget

```html
<div data-sivView="nombreWidget"...></div>
```

Sirve para poder usar un widget, a través del nombre del WIDGET (ojo, no de la CLASE (widgetCode) del widget). Luego, es importante saber que si hay 1 widget, **solo hay un sivWidget**, que se puede **usar N veces con sivView.**

Se compone con el nombre del contexto + nombre clase (de  Siviglia.Utils.buildClass)

Ejemplo uso:

```html
1. Si un widget se declara como <div data-sivWidget="A" data-widgetCode="B">

2. la vista se instancia como <div data-sivView="A">,  NO <div data-sivView="B">
```

## Usar parámetros

```html
<div data-sivParams='{"nombreParametro": "* o @ valorParametro"}'></div>
```

**data-sivParams** se utiliza para poder pasar parámetros en varios tipos como: *sivView, sivCall*...

## Recorrernos una estructura

```html
<div data-sivLoop="">...</div>
```

Con **data-sivLoop** sirve para poder recorrernos una estructura según:

- Un *contexto*.
- Un *data-contentIndex*.

Un *data-sivLoop* puede contener a otro *data-sivLoop*. Ejemplo:

```html
<div data-sivLoop="#pais" data-contextIndex="current">
    <h2 data-sivValue="Noticias de la seccion [%@current-index%]::class|[%#clname%]"></h2>
        <div data-sivLoop="/@current" data-contextIndex="currentNews">
            <p data-sivCall="initNode" data-sivParams='{"curSectionNews": "@currentNews"}'></p>
        </div>
    </div>
</div>
```

## Llamar a métodos

Con **data-sivCall** sirve para llamar a métodos de una clase creados.

## Notas varias

**preInitialize()**, se llama *antes* de procesar la plantilla del widget.y

**initialize()**, se llamada *después* de procesar la plantilla del widget.

Una variable usada en la plantilla, lo normal es que se inicialice antes, es decir, en el *preInitialize()*.

Además, de que las variables que se pongan dentro de del *methods->preInitialize()* se pueden usar en cualquier, sivValue o sivLoop, con /*nombre_variable o *nombre_variable.

{{% alert title="Importante" color="error" %}}

El ciclo de vida de un widget es: **preInitialize() -> render() -> initialize()**.

{{% /alert %}}
