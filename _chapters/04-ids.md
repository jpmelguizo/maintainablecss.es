---
layout: chapter
title: IDs
section: Background
permalink: /chapters/ids/
description: Aprende porqué usar IDs para aplicar estilos puede generar problemas y qué hacer en su lugar.
---
Semanticamente hablando, debemos usar un ID (identificador) cuando existe una sola instancia de algo y debemos usar clases cuando hay varias.

Sin embargo, [los ids tienen un rango mucho mayor ](http://www.w3.org/TR/css3-selectors/#specificity), lo que es un problema si queremos sobreescribir un estilo.

Para demostrar el problema, vamos a sobreescribir el color de un elemento de *rojo* a *azul* usando un ID.

Este es el HTML:

	<div id="modulo" class="modulo-sobreescrito">

Y este, el CSS:

	#modulo {
	  color: red;
	}

	.modulo-sobreescrito {
	  color: blue;
	}

El elemento será rojo aunque la clase `modulo-sobreescrito` lo declare como azul. Arreglémoslo cambiando el ID por una clase:


	<div class="modulo modulo-sobreescrito">

Y su CSS:

	.modulo {
	  color: red;
	}

	.modulo-sobreescrito {
	  color: blue;
	}

El elemento es azul ahora. Problema resuelto.

Aunque usar IDs sea problemático para dar estilo, se pueden seguir usando para otras cosas. Por ejemplo, los necesitamos para conectar:

- etiquetas a campos de formularios
- anclas dentro de una misma página
- atributos ARIA que ayuden a los usuarios de lectores de pantallas

## Conclusión

Usa IDs para habilitar funciones concretas de navegadores y tecnologías asistivas. Evita su uso al aplicar estilos.
