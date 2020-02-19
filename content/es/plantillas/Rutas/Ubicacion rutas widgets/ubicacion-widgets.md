---
title: "Ubicación rutas widgets"
linkTitle: "Ubicación rutas"
weight: 3
description: >
  Ubicación y explicación de las rutas de los widgets que el Resolvedor hace para funcionar el sistema de plantillas.
---


### Ruta 1

> 1. $widgetPath[]=$this->id_site[0]->getRoot()."/widgets/"; :file_folder:

Buscará dentro del proyecto: **/sites/nombre_site/widgets/nombre_carpeta/nombre_widget.wid**.  Donde:

* **nombre_site** -> pueden ser los valores:
    * adtopy
    * editor
    * reflection

* **nombre_carpeta** -> pueden ser los valores:
    * cache
    * html
    * pages
    * routes
    * widgets

* **nombre_widget.wid** -> puede ser los valores que se quieran, pero siempre tendrán la siguiente estructura:
    * Loquesea (primera en mayúscula), y dentro de ésta, estos 3 archivos siempre:
        * Definition.php
        * Loquesea.php
        * LoqueseaPage.php

{{< alert title="Importante" >}}El fichero que toca el sistema de plantillas siempre es "Loquesea.php".  Los otros dos son para temas de configuraciones, funciones php, y extras que se hacen para cada página en concreto.{{< /alert >}}


### Ruta 2

> 2. $widgetPath[]=PROJECTPATH."/output/html/Widgets";   :file_folder:

Buscará dentro del proyecto: **raíz/output/html/Widgets/nombreCarpeta/nombreComponente.wid** Donde:

* **nombreCarpeta** -> es la parte del widget a modelar

* **nombreComponente.wid** -> es la semántica que tiene un componente asociado a un widget.


### Ruta 3

> 3. $widgetPath[]=PROJECTPATH; :file_folder:

Esta ruta, usualmente estará en vistas asociado a los sites de los modelos. Ejemplo:

**/model/web/objects/Site/html/views**

