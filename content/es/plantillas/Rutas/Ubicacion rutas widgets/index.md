---
title: "Ubicación rutas widgets"
linkTitle: "Ubicación rutas widgets"
description: "Ubicación y explicación de las rutas de los widgets que el Resolvedor hace para funcionar el sistema de plantillas."
weight: 12
---

### Ruta 1

{{% alert title="Ruta 1" color="exito" %}}
  $widgetPath[]=$this->id_site[0]->getRoot()."/widgets/"; :file_folder:
{{% /alert %}}

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

{{% alert title="Importante" color="error" %}}
  El fichero que toca el sistema de plantillas siempre es "Loquesea.php".  Los otros dos son para temas de configuraciones, funciones php, y extras que se hacen para cada página en concreto.
{{% /alert %}}

### Ruta 2

{{% alert title="Ruta 2" color="exito" %}}
  $widgetPath[]=PROJECTPATH."/output/html/Widgets";   :file_folder:
{{% /alert %}}

Buscará dentro del proyecto: **raíz/output/html/Widgets/nombreCarpeta/nombreComponente.wid** Donde:

* **nombreCarpeta** -> es la parte del widget a modelar

* **nombreComponente.wid** -> es la semántica que tiene un componente asociado a un widget.

### Ruta 3

{{% alert title="Ruta 3" color="exito" %}}
  $widgetPath[]=PROJECTPATH; :file_folder:
{{% /alert %}}

Esta ruta, usualmente estará en vistas asociado a los sites de los modelos. Ejemplo: **/model/web/objects/Site/html/views**
