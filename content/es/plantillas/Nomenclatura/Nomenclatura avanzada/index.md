---
description: "Nomenclatura avanzada para entender el sistema de templating de Adtopy."
linkTitle: "Nomenclatura avanzada"
title: "Nomenclatura avanzada"
weight: 32
---

Para entender cómo funciona el sistema de templating de Adtopy, es importante conocer ciertas cosas avanzadas de la nomenclatura.

### Conceptos avanzados

- [Conceptos avanzados](#conceptos-avanzados)
- [Variables dentro de cada componente](#variables-dentro-de-cada-componente)
- [Parametros por referencia y/o valor](#parametros-por-referencia-yo-valor)
- [Traducción para cadenas de texto](#traducci%c3%b3n-para-cadenas-de-texto)
- [Usar php dentro de una plantilla .wid](#usar-php-dentro-de-una-plantilla-wid)

Para ello, vamos a dividir dicha nomenclatura en los siguientes apartados:

### Variables dentro de cada componente

Está compuesto por la siguiente sintáxis:

```php
[*NOMBRE_WIDGET({"nombre_variable":"$variable_php"})]componentes y contenido[#]
```

Para que las variables se pasen entre widgets, para intercambio de información, recorrido de en estructuras de datos, etc., es importante que la **$variable_php** se haya calculado antes.

Para ello, el código tiene que ser generado antes de la llamada. Ejemplo:

```php
# Codigo ejemplo que guardamos en '$data' la $variable_php vista anteriormente

<?php
$job: new model\web\Jobs();
$job->job_id: $params->job_id;
$job->loadFromFields();
$data: json_decode($job->results, true);
?>
```

Y la llamada dentro del código .wid sería así:

```php
[*:/ELEMENT/TYPES/_ARRAY({"data":"$data"})][#]
```

Es importante ver, que las variables puede ser llamadas **por valor o por referencia**. Para más información, visitar [2--parametros-por-referencia-yo-valor](#2--parametros-por-referencia-yo-valor).

### Parametros por referencia y/o valor

Las variables (parámetros), pueden ser pasados entre widgets .wid por **por valor o por referencia**. La diferencia es que:

- Por **VALOR**:  Se crea cada widget que usa dicha variable, una copia local. Por lo que, el ámbito y uso queda relegado al contexto de sólo ese widget. `$variable_php`
- Por **REFERENCIA**:  La variable, se comparte entre widgets, de forma que el contexto y ámbito es global a cada widget que quiera usarlo. Uso común para iteradores. `&$variable_php`

Veamos un ejemplo de pasar un parámetro por referencia:

```php
# Parámetro por referencia
[*:/ELEMENT/TYPES/_ARRAY({"data":"$data","it":"&$iterator"})][#]

# Parámetro por valor
[*:/ELEMENT/TYPES/_ARRAY({"data":"$data","it":"$iterator"})][#]
```

En la variable `$it` estará almacenado el valor de la variable pasada por referencia `&$iterator`. Para así, en el contexto del widget deseado, poder usar `$it`.

### Traducción para cadenas de texto

Si se quiere usar traducciones dentro de los widgets, la nomenclatura para ello sería usar `[@L]` para crear una referencia en la base de datos, que ese cadena es "traducible".

```php
# Traducción para cadenas de texto
[_LABEL][@L]Aceptar[#][#]
```

### Usar php dentro de una plantilla .wid

Se puede **usar código php dentro de una plantilla .wid**, tan simple cómo incluir `<?php ?>` dentro de la plantilla .wid sería suficiente. Veamos un ejemplo de código mezclando todo lo anterior:

```php
# Código php dentro de una plantilla .wid

<?php
$serializer=\Registry::getService("storage")->getSerializerByName('web');
$currentPage=Registry::$registry["currentPage"];
$params=$currentPage->getPageParams();
?>
[*:JOB_LIST_DS_TABLE({"currentPage":"$currentPage","object":"/model/web/Jobs","dsName":"FullList","serializer":"$serializer","params":"$params","iterator":"&$iterator"})]
    [_:HEADER]
        [_:TITLE]Listado de trabajos[#]
        [_:DESCRIPTION]Tabla que muestra por fila los resultados de cada trabajo para la tarea ComScore.[#]
        [_:ICONO]statics[#]
    [#]
    [_:LISTING]
        [_:COLUMNHEADERS]
            [_:COLUMN][_:LABEL]ID[#][#]
            [_:COLUMN][_:LABEL]Trabajo[#][#]
            [_:COLUMN][_:LABEL]Tipo[#][#]
            [_:COLUMN][_:LABEL]Estado[#][#]
            [_:COLUMN][_:LABEL]Creado[#][#]
            [_:COLUMN][_:LABEL]Actualizado[#][#]
        [#]
        [_:ROWS]
            [_:ROW][_:VALUE][*::/ELEMENT/TYPES/AutoIncrement({"name":"id_job","model":"$iterator"})][#][#][#]
            [_:ROW][_:VALUE][*::/ELEMENT/TEXT/LINK][_::LINK_URL]/JobDetail/<?php echo $iterator->job_id;?>/view[#][_::LINK_TEXT]<?php echo $iterator->job_id;?>[#][#][#][#]
            [_:ROW][_:VALUE][*::/ELEMENT/TYPES/_String({"name":"name","model":"$iterator"})][#][#][#]
            [_:ROW][_:VALUE][*::/ELEMENT/TYPES/Integer_Job_Status({"name":"status","model":"$iterator"})][#][#][#]
            [_:ROW][_:VALUE][*::/ELEMENT/TYPES/DateTime({"name":"created_at","model":"$iterator"})][#][#][#]
            [_:ROW][_:VALUE][*::/ELEMENT/TYPES/DateTime({"name":"updated_at","model":"$iterator"})][#][#][#]
        [#]
    [#]
[#]
```
