---
title: "Widget Noticias # Ejemplo Siviglia-js"
linkTitle: "Widget Noticias"
description: "Widget Noticias, ejemplo de uso con Siviglia-js"
weight: 7
---

El siguiente código veremos un ejemplo donde usaremos:

- Loop con Expandos.
- 3 widgets separados
- Controlador, widget y vista
- 2 punteros data-contextIndex

```html
<html>
<head>
    <title>news siviglia</title>
    <script src="/node_modules/jquery/dist/jquery.js"></script>
    <script src="../../../Siviglia.js"></script>
    <script src="../../../SivigliaStore.js"></script>
    <script src="../../../Model.js"></script>
    <script src="../../../SivigliaTypes.js"></script>
    <style type="text/css">
        .contenedor1 {background-color: grey;}
        .titulo {background-color: green;}
        .titulo2 {color: red}
        .noticia {border: 1px solid #000;}
    </style>
    <script>

        Siviglia.Utils.buildClass({
            "context": "Widget",
            "classes":{
                "Card":{
                    "inherits": "Siviglia.UI.Expando.View",
                    methods:{

                        preInitialize:function(params){

                            this.controller=params.controller;
                            this.title=params.title;
                            this.controllerParam=params.controllerParam;
                        },
                        initialize:function(params){},

                        getTitle:function(){},
                        getContent:function(node){
                            var widget=this.controller.getContent(this.controllerParam);
                            node.append(widget.rootNode)
                        }

                    }
                },
                "Controller":{
                    "inherits": "Siviglia.UI.Expando.View",
                    methods: {

                        preInitialize: function (params) {
                            this.self = this;
                            this.contenedor_noticias = {
                                // widget contenedor de noticias
                                pais:
                                    {
                                        "espana": [
                                            {
                                                "Titulo": "el iphone vale más de 5000€",
                                                "Contenido": "Contenido 1. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "VR es la nueva forma de viajar",
                                                "Contenido": "Contenido 2. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "El cod vid 19 afecta a la comunidad de madrid",
                                                "Contenido": "Contenido 3. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "Cierran durante 15 dias los colegios",
                                                "Contenido": "Contenido 4. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                        ],
                                        "internacional": [
                                            {
                                                "Titulo": "Title international 1",
                                                "Contenido": "Contenido 5. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "Title international 2",
                                                "Contenido": "Contenido 6. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "Title international 3",
                                                "Contenido": "Contenido 7. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                            {
                                                "Titulo": "Title international 4",
                                                "Contenido": "Contenido 8. Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book."
                                            },
                                        ]
                                    },
                                clname: "contenedor1",
                                class_title: "titulo",
                                class_noticia: "noticia"
                            };


                        },
                        initialize: function (params) {
                        },
                        getTitle: function () {
                            return this.title;
                        },
                        getContent: function (section) {

                            var widget = new Widget.Content(
                                "Widget.Content",
                                {section: section},
                                {},
                                $('<div></div>'),
                                this.__context
                            );
                            widget.__build();
                            return widget;
                        }
                    }
                },

                "Content":{
                    "inherits": "Siviglia.UI.Expando.View",
                    methods:{
                        preInitialize:function(params)
                        {
                            this.section=params.section;
                        },
                        initialize:function(params)
                        {}
                    },
                }

            }
        })

        setTimeout(function(){
            contenedor_noticias.clname="titulo2";
        },5000);
</script>
</head>
<body>
<div style="display:none">


    <!-- Card pinta la tarjeta, llamando a getTitle y getContent cuando lo necesite -->
    <div data-sivWidget="Widget.Card" data-widgetCode="Widget.Card" style="border:2px solid green">
        <h1 data-sivValue="/*title"></h1>
        <div data-sivCall="getContent"></div>
    </div>

    <div data-sivWidget="Widget.Controller" data-widgetCode="Widget.Controller" style="border:2px solid yellow">
        <div data-sivLoop="/*contenedor_noticias/pais" data-contextIndex="currentSection">
            <div data-sivView="Widget.Card" data-sivParams='{"controller":"*self","title":"@currentSection-index","controllerParam":"@currentSection"}'>
            </div>
        </div>
    </div>

        <div data-sivWidget="Widget.Content" data-widgetCode="Widget.Content" style="border:2px solid red">
            <div data-sivLoop="*section" data-contextIndex="currentNews">
                <div style="border:2px solid blue">
                <h3 data-sivValue="/@currentNews/Titulo"></h3>
                <p data-sivValue="/@currentNews/Contenido"></p>
                </div>
            </div>
        </div>
</div>

    <!--La plantilla de Controller solo tiene una llamada a la data-sivView de Card,
    pasando self como parametro  -->
    <div data-sivView="Widget.Controller"></div>

    <script>
        var parser=new Siviglia.UI.HTMLParser();
        parser.parse($(document.body));
    </script>
</body>
</html>
```
