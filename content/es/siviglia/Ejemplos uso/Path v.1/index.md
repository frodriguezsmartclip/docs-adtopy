---
title: "Path v.1 # Ejemplo Siviglia-js"
linkTitle: "Path v.1"
description: "Path v.1, ejemplo de uso con Siviglia-js"
weight: 2
---

El siguiente código veremos los **path**:

- Paths.
- 1 Contexto de path.
- PathResolver (resolvedor de path).

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
            a:{b:1,c:2}
        };
        // Contexto del path (ejemplo path valido -> #a)
        var plainCtx = new Siviglia.Path.BaseObjectContext(obj, "#", contextStack);

        // Una vez construido lo anterior, ya podemos preguntar por paths
        // BaseCursos -> un "iterador" de directorios, para saber como moverse entre directorios.
        // PathResolver, resuelve el path según un contexto.

        var pathResolver = new Siviglia.Path.PathResolver(contextStack,"#a/d"); //pathrresolver hereda de eventManager

        pathResolver.addListener("CHANGE",null,function(evName,params){
            console.dir(params);
        });
        pathResolver.getPath();

        // path NO es algo que exista, si no que pueda llegar a existir
        setTimeout(function(){
            obj.a.d=14;
        },3000);

        setTimeout(function(){
            //obj.a.d=27;
            delete obj.a.d;
        },4000);
</script>
</head>
<body>

<script>
    var parser=new Siviglia.UI.HTMLParser();
    parser.parse($(document.body));
</script>
</body>
</html>
```

En resumen, lo más importante de este ejemplo es quedarnos con la idea de:

- Dado un contexto de javascript, resolverlo como un sistema de directorio

**{z:{q:"c"}}   a/b/{%*z/q%}   --> a/b/c**

Para ello, `Siviglia.Path` es capaz de resolverlo, dado un contexto y objeto.
