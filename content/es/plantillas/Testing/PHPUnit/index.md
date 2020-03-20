---
title: "PHPUnit"
linkTitle: "PHPUnit"
description: "Explicación de uso para hacer testing con PHPUnit para el framework."
weight: 21
---

### 1. Ruta de testing

{{% alert title="Ruta de testing" color="nota" %}}
  lib/tests/output/html/templating :file_folder:
{{% /alert %}}

Dentro de esta ruta, tenemos que fijarnos que hay **3 carpetas (layouts/  result/ widgets/)** y **1 fichero .php**. Para hacer un test tendremos que crearnos:

1. Fichero "Loquesea.php", para lanzar las funciones (Ejemplo: TemplateParse2Test.php)
2. La carpeta _layouts_, contiene las funciones que se quieren crear para el test.
3. La carpeta _widgets_, contiene un fichero "nombre_widget.wid" que contendrá una pequeña estructura de templating.
4. La carpeta, _results_, contiene la salida HTML que espera después de lanzar el fichero de prueba en el paso 1.

### 2. Salida de testing

Si todo hubiera salido bien, deberíamos depurar esas clases y ver que cada función devuelve como salida lo que se espera del templating.
