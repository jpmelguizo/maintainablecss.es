---
layout: chapter
title: Modificadores
section: Core
permalink: /capitulos/modificadores/
description: Aprende a usar modificadores para cambiar la apariencia si existen ligeras diferencias.
---

Como los estados, los modificadores sobrescriben estilos. Son útiles cuando un módulo (o componente) tiene pequeñas diferencias fáciles de entender.

Imaginemos una tienda online donde cada categoría tiene una imagen de fondo distinta en la cabecera. Todas las cabeceras tienen el mismo `padding`, `margin`, etc. La única diferencia es la imagen de fondo.

La categoría "caballero" tendría un modificador, de esta manera:

	<div class="cabeceraCategoria cabeceraCategoria--caballero">

Y similarmente, la categoría "señora" tendría el modificador *senora*:

	<div class="cabeceraCategoria cabeceraCategoria--senora">

El CSS sería:

	.cabeceraCategoria {
	  padding-top: 50px;
	  padding-bottom: 50px;
	  /* etc */
	}

	.cabeceraCategoria--caballero {
	  background-image: url(/ruta/a/caballero.jpg);
	}

	.cabeceraCategoria--senora {
	  background-image: url(/ruta/a/señora.jpg);
	}

Como las diferencias son pequeñas y se entienden bien, este tipo de reutilización es más mantenible.

Podemos usar el mismo enfoque para botones. La mayoría de webs tienen estilos para botones primarios y secundarios. Si todo lo que cambian son un par de estilos, podemos usar un modificador para diferenciar primario de secundario de la siguiente forma:

	.boton {
	  padding: 20px;
	  border-radius: 3px;
	  /* etc */
	}

	.boton--primario {
	  background-color: green;
	}

	.boton--secundario {
	  background-color: #eee;
	}

De nuevo, esto funciona porque las diferencias están bien identificadas y se entienden.

## Conclusión

Los modificadores son una buena manera de reutilizar estilos en elementos bien definidos. El modificador en si debe considerarse como un ajuste. Si contiene muchas sobrescrituras, quizás sea la manera de proceder. En su lugar usa un [módulo](/capitulos/modulos/).
