---
title: "Expandos # Ejemplo Siviglia-js"
linkTitle: "Expandos"
description: "Expandos, ejemplo de uso con Siviglia-js"
weight: 5
---

El siguiente código veremos los **expandos**:

- Expandos.
- No hay contexto en el `<script>`
- HTMLParser, es el que busca expandos.

Los **expandos** sirven para expandir un contexto y aplicarlo a una entidad `<html>`.

```html
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script src="../../../Siviglia.js"></script>
    <script src="../../../SivigliaStore.js"></script>
    <script src="../../../Model.js"></script>
    <script src="../../../SivigliaTypes.js"></script>
<script>
        var contextStack = new Siviglia.Path.ContextStack();
        var obj = {
            paises: {"espana": ["Madrid","Sevilla","Barcelona"],
                    "francia": ["Paris","asdas","asdasdas"]
            }
        };
        var obj2 = {
            h:"espana"
        };

        // NO hay variables de contexto
        // var plainCtx = new Siviglia.Path.BaseObjectContext(obj, "#", contextStack);
        // var plainCtx2 = new Siviglia.Path.BaseObjectContext(obj2, "!", contextStack);

        setTimeout(function(){
            obj2.h="francia";
        },3000);

        setTimeout(function(){
            obj.clname="dos";
        },3000);

        setTimeout(function(){
            obj.myId=24;
        },3000);
</script>
</head>
<body>
<!-- expandiendo el ::class|[%#clname%] -->
<a data-sivValue="Una ciudad de [%!h%] es [%#paises/{%!h%}/2%]::class|[%#clname%]::href|http://www.pepito.com/user?usreId=[%#myId%]"></a>

<script>
    var parser=new Siviglia.UI.HTMLParser();
    parser.addContext("#",obj);
    parser.addContext("!",obj2);
    parser.parse($(document.body));
</script>
</body>
</html>
```

En resumen, lo más importante de este ejemplo es quedarnos con la idea de:

- **Siviglia.UI.HTMLParser, es el que busca expandos** y puede resolver contextos asociados a objetos.
