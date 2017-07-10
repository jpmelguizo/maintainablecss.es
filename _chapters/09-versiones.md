---
layout: chapter
title: Versiones
section: Extras
permalink: /capitulos/versiones/
description: Aprende como MaintainableCSS hace muy fácil actualizar módulos y realizar tests AB en sitios web en continuo crecimiento.
---

Podríamos, por ejemplo, querer hacer un test A/B sobre distintas versiones de un mismo módulo para ver cuál funciona mejor. Para hacerlo, necesitamos duplicar el módulo y darle un nombre único. Por ejemplo, si queremos probar distintos carritos, el CSS puede quedar así:

	/* módulo existente (variante A) */
	.carrito {}

	.carrito-titulo {}

	/* nueva versión (variante B) */
	.carrito2 {}

	.carrito2-titulo {}

De esta manera podemos mantener dos versiones mientras realizamos los tests y decidimos cual es el mejor. En cuanto lo decidamos, podemos descartar el módulo redundante, ya que no están entrelazados. Un buen código es un código fácil de borrar.
