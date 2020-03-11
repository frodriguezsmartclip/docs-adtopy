---
title: "Widgets dinámicos"
linkTitle: "Widgets Dinámicos"
description: "Documentación acerca de qué son los widgets dinámicos en Adtopy"
weight: 43
---

En esta sección, veremos para qué se usan los **widgets dinámicos** en Adtopy.

Si se quiere mostrar información dinámica de una tabla de la base de datos (MySQL por ejemplo), habría que crear un widget dinámico para poder usarlo en el .wid que se quisiera mostrar.

Veamoslo mejor con un ejemplo :mag_right:

### Creación de la página dentro del site

Dentro de ese site, la vista nueva para una página (ejemplo JobDetail), hay que crear una página JobDetail con los siguientes 3 archivos:

```git
📦JobDetail
 ┣ 📜Definition.php
 ┣ 📜JobDetail.php      # Fichero importante 1
 ┗ 📜JobDetailPage.php  # Fichero importante 2
```

Si miramos el archivo **JobDetail.php**, podremos ver la llamada al **widget dinámico** `JobDetailWidget`

{{% alert title="Nota" color="nota" %}}
Si la función `getWidgetPath` no encuentra los .wid por defecto: *JOB_DEFAULT.wid o JOB_ESPECIAL.wid*, dará un error, ya que no encuentra el widget. No resuelve a un widget por defecto, ya que JM prefiere que de error.
{{% /alert %}}

### Cómo invocar a un widget dinámico

```php
<?php
$page=Registry::$registry["PAGE"];
$idJob=$page->job_id;
?>

[*PAGE/JOB]
    [_TITLE]Jobs: Backend - SmartClip v.1.0 beta[#]

    [_CONTENT]
        [*:BEHAVIOR/CARD]
            [_:TITLE]Detalle del trabajo: <?php echo $idJob; ?>[#]
            [_:CONTENT]
                [*::DATOS_RESUMEN_JOB({"datos_job":"$page"})][#]

                [*:[%JobDetailWidget%]][#]

                [*::WorkerFullList][#]
            [#]
        [#]
    [#]
[#]
```

La forma de llamar a un **widget dinámico** es:
`[*:[%nombre_widget_dinamico%]][#]`, puesto con `%` invocando al nombre del widget. A continuación se explica como se configura este nombre.

El encargado de asociar ese nombre del widget dinámico, es el fichero `**JobDetailPage.php**` (o cualquier _'NombrePaginaPage.php_):

```php
namespace sites\backend\pages\JobDetail;

use lib\model\ModelService;
use lib\model\ModelDescriptor;

include_once(PROJECTPATH."/model/web/objects/Jobs/objects/Worker/Definition.php");

class JobDetailPage extends  \model\web\Page
{
    protected $className = '\model\web\Jobs\Worker';

    function initializePage($params)
    {
        $s=\Registry::getService("model");
        $ins=$s->loadModel($this->className, ["job_id"=>$this->job_id]);
        $package = ModelService::getPackage($ins->worker_type);

        $md = new ModelDescriptor($ins->worker_type, "", $package);
        $resultJobWidget = $md->getWidgetPath(); // por defecto carga JOB_DEFAULT del worker
        //$resultJobWidget = $md->getWidgetPath("JOB_ESPECIAL"); // plantilla por nombre

        $this->setTemplateParams([
            "JobDetailWidget" => $resultJobWidget,
        ]);
    }

    function getFormModel($model,$form)
    {
        $s=\Registry::getService("model");
        $ins=$s->loadModel('\model\web\Job',["id_job"=>$this->id_job]);
        //$ins=$s->loadModel($this->className, ["job_id"=>$this->job_id]);
        return $ins;
    }
}
```

### Función que resuelve path del widget dinámico

La función `initializePage` es la encargada de resolver esto, busca en el *path de cada worker_type* que haya una carpeta *widgets*. Realmente, la funcion llamada `getWidgetPath`, es la que se encarga de resolver correctamente la carpeta de widgets para cada worker.

```php
    function getWidgetPath($widget="JOB_DEFAULT")
    {
        return "/model/" . $this->layer . "/objects/" . str_replace('\\', '/', $this->namespaceClassName) . "/" . $this->className . "/widgets/$widget";
    }
```

{{% alert title="Importante" color="error" %}}
Si la función `getWidgetPath` no encuentra los .wid por defecto: *JOB_DEFAULT.wid o JOB_ESPECIAL.wid*, dará un error, ya que no encuentra el widget. No resuelve a un widget por defecto, ya que JM prefiere que de error.
{{% /alert %}}

![error cargar widget dinamico](/img/uploads/error-cargar-widget-dinamico.png)

### Resultado final del widget dinámico

Una vez hayamos [invocado al wid dinámico](#cómo-invocar-a-un-widget-dinámico), si todo ha ido bien, podremos ver el contenido del mismo. :tada: :blush: Ejemplo de una posible salida:

![Ejemplo widget dinamico JobDetailWidget](/img/uploads/JobDetailWidget.png)
