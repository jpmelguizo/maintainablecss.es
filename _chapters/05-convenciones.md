---
layout: chapter
title: Convenciones
section: Core
permalink: /capitulos/convenciones/
description: Aprende las convenciones aplicadas en MaintainableCSS para escribir módulos, componentes y estados.
---

*MaintainableCSS* sigue la siguiente convención:

	.<modulo>[-<componente>][-<estado>] {}

Las llaves [] son opcionales dependiendo del módulo en cuestión. Algunos ejemplos:

	/* Módulo contenedor */
	.resultadosBusqueda {}

	/* Componente */
	.resultadosBusqueda-cabecera {}

	/* Estado */
	.resultadosBusqueda-estaCargando {}

Notas:

- Componente y estado están delimitados por un guión.
- Los nombres de los módulos se escriben con "[lowerCamelCase](https://es.wikipedia.org/wiki/CamelCase)".
- Los selectores tienen el nombre del módulo como prefijo.

## ¿Tengo que darle un nombre de clase a todos los elementos?

No. Puedes usar `.resultadosBusqueda p` si quieres. Tendrás que hacerlo así si usas "markdown" por ejemplo. Pero ten cuidado si vas a anidar otro módulo que contenga `p` porque heredará los estilos y necesitará que los sobreescribas.

## ¿Por qué hay que poner el nombre del módulo como prefijo?

Buena pregunta. Un ejeplo sin prefijos:

	<div class="carrito">
	  <div class="cabecera">

Y su CSS:

	/* módulo */
	.carrito {}

	/* componente cabecera del módulo carrito */
	.carrito .cabecera {}

Hay dos problemas:

1. Al leer el HTML, es difícil diferenciar entre módulo y componente.
2. El componente `.carrito .cabecera` hereda estilos del módulo `.cabecera`, lo que puede tener efectos indeseados.
