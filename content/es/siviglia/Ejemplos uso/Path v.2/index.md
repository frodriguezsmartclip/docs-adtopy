---
title: "Path v.2 # Ejemplo Siviglia-js"
linkTitle: "Path v.2"
description: "Path v.2, ejemplo de uso con Siviglia-js"
weight: 3
---

El siguiente código veremos los **path**:

- Paths.
- 2 Contextos de paths.
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
            paises: {"espana": ["Madrid","Sevilla","Barcelona"],
                    "francia": ["Paris","asdas","asdasdas"]
            }
        };
        var obj2 = {
            h:"espana"
        };

        // 2 variables de contexto, asociado # al obj1, y ! al obj2
        var plainCtx = new Siviglia.Path.BaseObjectContext(obj, "#", contextStack);
        var plainCtx2 = new Siviglia.Path.BaseObjectContext(obj2, "!", contextStack);


        // Una vez construido lo anterior, ya podemos preguntar por paths
        // BaseCursos -> un "iterador" de directorios, para saber como moverse entre directorios.
        // PathResolver, resuelve el path según dos contextos

        var pathResolver = new Siviglia.Path.PathResolver(contextStack,"#paises/{%!h%}");
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

- **pathResolver** puede resolver un path que está construido con *Parametrized String.*
