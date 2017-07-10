---
layout: chapter
title: Semántica
section: Background
permalink: /capitulos/semantica/
description: Aprende porqué nombrar algo basándose en lo que es, en lugar de en cómo se ve o lo que hace, es el fundamento del CSS mantenible y bien estructurado.
---

La semántica de HTML no trata solo de los elementos que usamos. Es bastante obvio que debemos usar `<a>` para enlaces, `<table>` para datos tabulares y `<p>` para párrafos. Lo que no es tan obvio es qué nombres darle a las clases.

Como dice Phil Karton, *solo hay dos cosas difícil en las Ciencias de la computación: la invalidación de caché y **nombrar cosas***.

Nombrar es, francamente, el aspecto más importante al escribir CSS mantenible. Hay dos enfoques: el semántico y el no semántico. Veamos de qué tratan.

## Semántico vs No semántico

Ejemplos de clases no semánticas:

	<div class="red pull-left pb3">
	<div class="grid row">
	<div class="col-xs-4">

Las clases no semánticas no reflejan lo que el elemento *representa*. Como mucho, nos dan una idea de su *apariencia*. Las clases atómicas, visuales, de comportamiento y utilitarias son ejemplos de clases no semánticas.

Ejemplos de clases semánticas:

	<div class="carrito">
	<div class="producto">
	<div class="resultadosBusqueda">

Las clases semánticas no reflejan los estilos. No pasa nada, para eso está CSS. Las clases semánticas significan algo para HTML, CSS, Javascript y test automatizados.

Hay muchas razones por las que usar clases semánticas puede resultar beneficioso:

## 1. Son legibles

El siguiente código es un ejemplo real de HTML con clases atómicas:

	<div class="pb3 pb4-ns pt4 pt5-ns mt4 black-70 fl-l w-50-l">
	  <h1 class="f4 fw6 f1-ns lh-title measure mt0">Heading</h1>
	  <p class="f5 f4-ns fw4 b measure dib-m lh-copy">Tagline</p>
	</div>

notas:

- Leer palabras completas es mucho más fácil que leer abreviaturas.
- Las abreviaturas tienen que desglosarse antes de poder obtener un modelo mental, asumiendo que entendamos lo que significan.
- Es muy difícil leer un grupo de clases juntas.
- Tenemos que ir tanteando muchas clases para saber de qué va la cosa, qué clases sobrescriben a otras, cuáles se aplican en puntos de ruptura (breakpoints), etc.
- Estas clases son ambiguas. Por ejemplo, ¿se refiere `black-70` a `color` o a `background`? Si necesitamos usar el inspector del navegador para enterarnos, está claro que esta clase no es legible.
- El contenido está ofuscado por el HTML que lo rodea.

Aquí tenemos el mismo ejemplo con clases semánticas:

	<div class="presentacion">
	  <h1 class="presentacion-titulo">Heading</h1>
	  <p class="presentacion-slogan">Tagline</p>
	</div>

Notas:

- Son fáciles de leer, no necesitamos ningún modelo mental.
- El contenido no está ofuscado.
- Sabemos donde empiezan y acaban los módulos.
- Tenemos la mitad de código HTML.
- El CSS es fácil de leer (en el inspector o en el archivo) porque usa un lenguaje dedicado, construido desde el propósito de cada elemento.

## 2. Es más fácil construir webs "responsive"

Imagina escribir una cuadrícula "responsive" a dos columnas donde:

* Cada columna tiene `padding: 20px` en pantallas pequeñas y `50px` en grandes.
* Cada columna tiene `font-size: 2em` en pantallas pequeñas y `3em` en grandes.
* Las columnas se apilan en pantallas pequeñas. Por tanto, *columna* sería un nombre de clase que lleva a confusión.

Esto es lo que habitualmente se hace con clases visuales y utilitarias:

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

Notas:

- Hay 7 clases, algunas sobrescribiendo a otras.
- Para hacer las columnas realmente "responsive" necesitaríamos una clase  `fs3large`, etc.
- En algunos puntos de ruptura las clases son confusas o redundantes. Por ejemplo `.clearfix` no hace nada en pantallas pequeñas.

Acabamos de empezar a analizarla y ya hemos encontrado bastantes problemas.

Lo mismo de antes, ahora usando clases semánticas:

	<div class="cosa">
	  <div class="cosa-cosaA"></div>
	  <div class="cosa-cosaB"></div>
	</div>

Notas:

- Estas clases están encapsuladas en el diseño y contenido del módulo en cuestión.
- Es fácil dar estilo a los elementos sin tener que escribir muchas clases ni cambiar el HTML de nuevo.
- Estas clases son significativas para pantallas pequeñas y grandes.
- Podemos usar un "media query" para aplicar el "clearfix" solo cuando hace falta.

> Pregunta: ¿Realmente son tan útiles los sistemas de cuadrículas (grid) preconfigurados? Un [diseño debe adaptarse al contenido](http://adamsilver.io/articles/stop-using-device-breakpoints/) y no al contrario.

## 3. Son más fáciles de encontrar

Buscar en el HTML cualquier clase no semántica puede dar multitud de resultados. Como las clases semánticas son únicas, solo dan un resultado, haciendo más fácil encontrar lo que se busca.

## 4. Eliminan el riesgo de regresión

Actualizar una clase visual puede causar regresión en muchos elementos. Actualizando una clase semántica solo aplicamos cambios en el módulo en cuestión, eliminando el riesgo de regresión totalmente.

## 5. Las clases visuales no merecen la pena

En algunos casos es incluso mejor usar estilos en línea (inline). Son más explícitos y reducen el CSS a cero. En todo caso, los estilos en línea son problemáticos, no podemos usar "media queries" por ejemplo. Añadir CSS en el HTML mezcla conceptos y elimina la posibilidad de usar caché.

> Pregunta: ¿No nos da `.red` exactamente la misma abstracción que se consigue en CSS con `color: red`?

## 6. Proporcionan "hooks" para tests funcionales automatizados

Los test funcionales automatizados funcionan buscando e interactuando con elementos, pudiendo incluir:

1. hacer click en un enlace,
2. encontrar una caja de texto,
3. teclear un texto,
4. enviar un formulario,
5. verificar algún criterio.

No podemos usar clases no semánticas para elegir elementos concretos. Añadir ganchos específicamente solo para realizar tests no es eficaz, el usuario tendría que descargar toda el código extra.

## 7. Proporcionan "hooks" para Javascript

Al igual que en el punto anterior, las clases no semánticas no sirven si queremos seleccionar elementos concretos para aplicar Javascript.

## 8. No necesitan mantenimiento

Si nombramos algo basándonos en lo que es, no tendremos que actualizar el HTML. Por ejemplo: una cabecera es siempre una cabecera, sea como sea su *apariencia*.

Con clases visuales, tanto el HTML como el CSS necesitan actualizarse (asumiendo que no haya otros selectores que puedan usarse).

## 9. Son mas fáciles de depurar

Inspeccionar un elemento con varias clases atómicas, significa tener que ir uno por uno por varios selectores. Con una clase semántica, solo hay una clase, es más fácil.

## 10. Está recomendado por los estándares

La especificación HTML en 3.2.5.7 dice sobre usar clases:

> "[...] se recomienda a los autores usar valores que describan la naturaleza del contenido, en lugar de la presentación deseada de este."

## 11. Aplicar estilos a estados es más fácil

Considera el siguiente HTML:

	<a class="padding-left-20 red" href="#"></a>

Cambiar el espaciado y el color al pasar el ratón por encima del elemento (hover) sería complicado. Es mejor evitar estas situaciones a tener que arreglar errores que hemos generado nosotros mismos.

## 12. Producen menos código HTML

Como hemos ido viendo, las clases atómicas inflan el HTML. Las clases semánticas producen un HTML más corto. Aunque el CSS puede incrementar en tamaño, se puede "cachear".

## Conclusión

Las clases semánticas son la piedra angular de *MaintainableCSS*. Sin ellas, lo demás no tiene mucho sentido. Así que empieza nombrando las cosas según lo que son y todo lo demás vendrá rodado.
