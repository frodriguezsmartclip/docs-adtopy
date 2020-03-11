---
title: "Parametrized string # Ejemplo Siviglia-js"
linkTitle: "Parametrized string"
description: "Parametrized string, ejemplo de uso con Siviglia-js"
weight: 4
---

El siguiente código veremos los **path**:

- Paths.
- Contextos de los paths.
- PathResolver (resolvedor de path).
- HTMLParse + contexto.

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
        // Como resuelve parametrized string el contexto [%nombre_objeto%]
        var ps = new Siviglia.Path.ParametrizableString("Una ciudad de [%!h%] es [%#paises/{%!h%}/2%]",contextStack);
        ps.addListener("CHANGE",null,function(evName,params){
            console.dir(params);
        });
        ps.parse();

        // A los 3 segundos, el contexto de h es francia, por lo que cambia parametrized string dinámicamente.
        setTimeout(function(){
            obj2.h="francia";
        },3000);
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

- **pathResolver** puede resolver parametrized string del contexto [%nombre_objeto%]
