---
title: "Eventos # Ejemplo Siviglia-js"
linkTitle: "Eventos"
description: "Eventos, ejemplo de uso con Siviglia-js"
weight: 1
---

El siguiente código veremos los **eventos**:

- Funciones predefinidas.
- Llamar a métodos dentro de una clase.
- addListener()
- fireEvent()
- destruct()

```html
<html>
<head>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script src="../../../Siviglia.js"></script>
    <script src="../../../SivigliaStore.js"></script>
    <script src="../../../Model.js"></script>
    <script src="../../../SivigliaTypes.js"></script>
<script>
        Siviglia.Utils.buildClass({
            context: "Test",
            classes:{
                "Test":{
                    // Funciones predefinidas: constructor, destructor y metodos
                    construct:function(){ console.log("construct Test")},
                    destruct:function(){console.log("destruct Test")},
                    methods:{
                        metodo1:function(){console.log("metodo1 Test")},
                        metodo2:function(){console.log("metodo2 Test")},
                    }
                },
                "Test2":{
                    inherits:"Test",  // Test2 hereda todo lo de la clase "Test"
                    // Si no se pone punto, significa que está en el mismo contexto
                    // Test.Test  es = a poner solo Test1
                    //inherits: "Clase1, clase2, etc" por comas se pueden heredar más clases
                    construct:function(){
                        console.log("construct Test2");
                        this.Test();
                    },
                    destruct:function(){console.log("destruct Test2")},
                    methods:{
                        metodo1:function(){
                            this.Test$metodo1();
                            console.log("metodo1 Test2");
                        },
                        metodo3:function(){console.log("metodo3 Test2")}
                    }
                },
            }
        });

        // instancia de Test
        var s=new Test.Test();  
        s.metodo1();
        s.destruct();

        //instancia de textos
        var s2=new Test.Test2();
        // desde s2, queremos llamar al constructor del padre con this.Test();

        // llamar a un metodo NO sobreescrito
        s2.metodo3();
        //llamar a un metodo SI sobrerescrito this.Test$metodo1();
        s2.metodo1();

        // destructor al s2
        s2.destruct();  // los destructores llaman a todos los padres y siempre llaman en cascada

        var evento=new Siviglia.Dom.EventManger();

        evento.addListener("CHANGE",null,function(evName,params){
            console.log(evName);
            console.log(params);
        },"ESTE SE VA A QUEDAR COLGADO");

        evento.fireEvent("CHANGE",{p:12});
        evento.destruct();
        // importante, si se lanza un fireEvent, siempre hay que destruirlo
        // llamada global Siviglia.Dom.existingListeners
</script>
</head>
<body>

<script>
    //NO es necesario, ya que no se está parseando HTML para encontrar Expandos, etc... 
    //Solo se está usando Siviglia para crear clases.

    /*
    var obj1={"uno": 1};
    var parser=new Siviglia.UI.HTMLParser();
    parser.addContext("/",obj1);
    parser.parse($(document.body));
    */
</script>
</body>
</html>
```
