---
title: "Sites + templating + widgets"
linkTitle: "Sites + templating + widgets"
description: "Explicación de uso para hacer testing directamente con templates (.wid), widgets y ficheros .php."
weight: 22
---

En esta sección de testing, veremos cómo abordar los tests para ver finalmente como los templates encagan y afectan directamente al diseño final de cada Site.

### 1. Ruta carpetas

Para ello, es importante tener en cuenta la siguiente ruta:

> /sites/nombreSite/widgets/ :file_folder:

* **nombreSite** pueden ser los siguientes valores:
  * adtopy
  * editor
  * reflection
  * cache (no aplicable)
  * statics (no aplicable)

Los últimos valores (cache y statics), no son aplicables para hacer testing ni nuevo módulos, templates asociado. Sólo sirven para la caché de ficheros y para los ficheros estáticos del proyecto.

### 2. Ruta de testing

> lib/tests/output/html/templating :file_folder:

Dentro de esta ruta, tenemos que fijarnos que hay **3 carpetas (layouts/  result/ widgets/)** y **1 fichero .php**. Para hacer un test tendremos que crearnos:

1. Fichero "Loquesea.php", para lanzar las funciones (Ejemplo: TemplateParse2Test.php)
2. La carpeta _layouts_, contiene las funciones que se quieren crear para el test.
3. La carpeta _widgets_, contiene un fichero "nombre_widget.wid" que contendrá una pequeña estructura de templating.
4. La carpeta, _results_, contiene la salida HTML que espera después de lanzar el fichero de prueba en el paso 1.

### 3. Salida de testing

Si todo hubiera salido bien, deberíamos depurar esas clases y ver que cada función devuelve como salida lo que se espera del templating.
