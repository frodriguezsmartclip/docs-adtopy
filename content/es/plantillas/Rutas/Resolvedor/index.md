---
title: "Resolvedor"
linkTitle: "Resolvedor"
description: "Explicación de la función que se encarga de resolver y buscar los widgets para las plantillas."
weight: 11
---

## Resolvedor de rutas

El archivo llamado `model/web/objetcs/Page/Page.php` es el encargado de resolver la ruta de cada widget, mirando en un Path u otro, dependiendo de si existe o no. :computer:

En concreto, en la función llamada **getWidgetPaths()** se encarga de resolver esto:

```php
// Path: model/web/objetcs/Page/Page.php -> getWidgetPaths()

    function getWidgetPaths($isWork=false)
    {
        $def=$this->getPageDefinition();
        $widgetPath=array();
        if(isset($def["WIDGETPATH"]))
        {
            $widgetPath=$def["WIDGETPATH"];
        }
        $widgetPath[]=$this->id_site[0]->getPagePath($this->path)."/widgets".($isWork===true?"_work":"")."/";
        // Se incluyen los paths del sitio actual 
        // (ojo, no el de la pagina, porque esta pagina podria ser llamada desde otros sites).
        $curSite=\Registry::getService("site");
        $sitePaths=$curSite->getExtraWidgetPath();
        $widgetPath=array_merge($widgetPath,$sitePaths);
        $widgetPath[]=$this->id_site[0]->getRoot()."/widgets/";
        $widgetPath[]=PROJECTPATH."/output/html/Widgets";
        $widgetPath[]=PROJECTPATH;
        return $widgetPath;
    }
```

Si nos fijamos en las últimas líneas de la función, nos dice las 3 rutas donde va a intentar resolver el sistema de plantillas para buscar los widgets:

* [Ubicación rutas widgets](/docs/rutas/ubicacion-rutas-widgets/ubicacion-widgets/): Ubicación rutas widgets.