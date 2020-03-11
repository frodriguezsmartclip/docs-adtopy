---
title: "Estructura básica"
linkTitle: "Estructura básica"
description: "Estructura básica del framework Siviglia-js."
weight: 1
---

Consta de la siguiente estructura básica:

```html
<html>
    <head>
        <script src="/node_modules/jquery/dist/jquery.js"></script>
        <script src="../../Siviglia.js"></script>
        <script src="../../SivigliaPaths.js"></script>
        <script src="../../SivigliaStore.js"></script>
        <script src="../../Model.js"></script>
        <script src="../../SivigliaTypes.js"></script>
        <script><!-- contenido clases, etc de siviglia --></script>
    </head>
    <body>


    <script>
        var obj1={"uno":1};
        var parser=new Siviglia.UI.HTMLParser();
        parser.addContext("/",q);
        parser.parse($(document.body));
    </script>
    </body>
</html>
```

Veamos con más detalle qué es cada cosa:

### Scripts en el head

Veamos qué son cada fichero .js puesto en la cabecera `<head>`

```php
    // Jquery requerido
    <script src="/node_modules/jquery/dist/jquery.js"></script>  

    // Core del framework
    <script src="../../../Siviglia.js"></script>

    // Diferentes formas de obtener fuentes de datos, tipos, etc.. (ej: ajax, fuentes datos array, path...)
    <script src="../../../SivigliaStore.js"></script>

    // Librería que contiene todo lo referido a modelos (dame x modelo, carga tal model, dame el datasource de este...)
    // (capa de más alto nivel)
    <script src="../../../Model.js"></script>

    // Gestión de tipos por el lado del cliente (al igual que hay por el lado del servidor con el sistema de plantillas .wid)
    <script src="../../../SivigliaTypes.js"></script>
```

### Código script para Siviglia

En la sección siguiente, escribiremos el código javascript para que Siviglia lo interprete:

```php
<script>
    // Codigo javascript referido a Siviglia
</script>
</head>
```

### Body

Dentro del `<body>` pondremos la nomenclatura referida a Siviglia y el uso de parámetros.

La cosa importante a tener en cuenta, sería que siempre tiene que haber antes del cierre del `</body>` el siguiente código `<script>`:

```php
<script>
    var parser=new Siviglia.UI.HTMLParser();
    // Nota: NO es requerido añadir un contexto, es opcional.
    // Más adelante se explica en 
    //parser.addContext("/",objeto_con_contexto);
    parser.parse($(document.body));
</script>
```

Nota: NO es requerido añadir un contexto, es opcional.

Más adelante se explica en Expandos el uso de contextos (ver **[ejemplo uso/expandos](/siviglia/ejemplos-uso/expandos/)**)
