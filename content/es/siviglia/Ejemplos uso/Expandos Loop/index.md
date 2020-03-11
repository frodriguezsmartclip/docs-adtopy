---
title: "Expandos Loop # Ejemplo Siviglia-js"
linkTitle: "Expandos Loop"
description: "Expandos Loop, ejemplo de uso con Siviglia-js"
weight: 6
---

El siguiente código veremos los **Loop Expandos**:

- Loop con Expandos.

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

        function callMe(node,params){
            console.dir(node);
            console.dir(params);
        }

        Siviglia.Utils.buildClass({
            "context": "Test",
            "classes":{
                "Test1":{
                    "inherits": "Siviglia.UI.Expando.View",
                    methods:{
                        preInitialize:function(params){
                            this.pepito2=params.uno;
                            this.pepito="HOLA";
                        },
                        initialize:function(params){},
                        initNode:function(node,params){
                            var name_widget = "Test.Test2";
                            if (params.curPais =="francia"){
                                name_widget = "Test.Test3";
                            }
                            var widget= new Test.Test2( // contiene 5 parámetros
                                name_widget,                // 1. nombre del widget
                                {country: params.curPais},  // 2. parametros
                                {},                         // 3. unsued
                                $('<div></div>'),           // 4. nodo
                                this.__context              // 5. contexto
                            );
                            widget.__build();               // Construcción del widget
                            node.append(widget.rootNode);   // append de ese nodo al rootnode
                        }
                    }
                },
                "Test2":{
                    "inherits": "Siviglia.UI.Expando.View",
                    methods:{
                        preInitialize:function(params){
                            this.country=params.country;
                        },
                        initialize:function(params){},
                    }
                }
            }
        })
</script>
</head>
<body>
<div style="display:none">
    <div data-sivWidget="Test.Test1" data-widgetCode="Test.Test1">
        <div data-sivValue="[%*pepito%]"></div> <!-- referencia  -->
        <div data-sivValue="[%*pepito2%]"></div> <!-- referencia  -->

        <div data-sivLoop="#paises" data-contextIndex="current">
            <a data-sivValue="Una ciudad de [%@current-index%] es [%#paises/{%@current-index%}/2%]::class|[%#clname%]::href|http://www.pepito.com/user?usreId=[%#myId%]"></a>
            <div data-sivEvent="click" data-sivCallback="callMe" data-sivParams='{"current":"@current-index"}'>click</div>
            <div data-sivCall="initNode" data-sivParams='{"curPais": "@current-index"}'></div>
        </div>
    </div>

    <div data-sivWidget="Test.Test2" data-widgetCode="Test.Test2">
        <div style="background-color: yellow" data-sivValue="/*country"></div>
    </div>

    <div data-sivWidget="Test.Test3" data-widgetCode="Test.Test2">
        <div style="background-color: blue" data-sivValue="/*country"></div>
    </div>
</div>


<div data-sivView="Test.Test1" data-sivParams='{"uno":1}'></div>
<div data-sivView="Test.Test1" data-sivParams='{"uno":2}'></div>
<div data-sivView="Test.Test1" data-sivParams='{"uno":3}'></div>
<div data-sivView="Test.Test1" data-sivParams='{"uno":4}'></div>


<script>
    var parser=new Siviglia.UI.HTMLParser();
    parser.addContext("#",obj);
    parser.addContext("!",obj2);
    parser.parse($(document.body));
</script>
</body>
</html>
```

En resumen, lo más importante de este ejemplo es quedarnos con la idea de que se pueden hacer *loop usando expandos*:

- **data-sivLoop**
- **data-contextIndex**
- **data-sivCall**
- **data-sivParams**
