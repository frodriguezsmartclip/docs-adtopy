---
description: "Nomenclatura básica para entender el sistema de templating de Adtopy."
linkTitle: "Nomenclatura basica"
title: "Nomenclatura básica"
weight: 31
---

Para entender cómo funciona el sistema de templating de Adtopy, es importante conocer ciertas cosas básicas de la nomenclatura.

### Conceptos básicos

1. Hay WIDGETS.
2. Hay partes de un COMPONENTE que pertenece a un widget.
3. Cómo se accede al componente.
4. Nivel de anidamiento del widget.

Para ello, vamos a dividir dicha nomenclatura en los siguientes apartados:

### Parte de un Widget

#### 1- Nombre del widget

Está compuesto por la siguiente sintáxis:

```php
[*NOMBRE_WIDGET]componentes y contenido[#]
```

Para que un widget sea válido, tiene que estar contenido dentro de **corchetes** seguido de * **[*]**

Luego, para cerrar todos los widgets (o componentes) es necesario cerrarlo con **[#]**

Para poder usar un widget, tiene que estar creada es **fichero con extensión .wid**. Ejemplo: **NOMBRE_WIDGET.wid**

Veamos un ejemplo simple con una etiqueta de HTML `<strong>` (negrita), para enfazitar un texto. El código y widget de ejemplo sería el siguiente:

```php
1. 'STRONG.wid'

<strong>texto en negrita</strong>

2. 'Haciendo uso del widget STRONG.wid'

[*STRONG]texto en negrita[#]
```

El resultado sería el contenido enfatizado: **texto en negrita**.

#### 2- Atributos que tiene un widget.

#### 3- Acciones que se puede hacer en un widget.

#### 4- Contexto en el que se encuentra.

#### 5- Uso recursivo de componentes.
