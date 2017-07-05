---
layout: chapter
title: FAQs
section: Extras
permalink: /chapters/faqs/
description: Tus preguntas sobre MaintainableCSS y sus respuestas.
---

Si no puedes encontrar una respuesta, por favor [inicia una "issue" en Github](https://github.com/adamsilver/maintainablecss.com/issues/new). ¡Gracias!

## ¿Puedo traducir tu libro?

Si. Haz esto:

1. [Haz "fork" del repositorio](https://github.com/adamsilver/maintainablecss.com/).
2. Dirige la extensión de dominio de tu país hacia él.
3. Cita el original y hámelo saber :).

## ¿Qué pasa con la herencia para encabezados, etc?

Idealmente, nuestro HTML semántico refleja integralmente nuestro diseño visual. En el caso de que nuestros `h1`s sean idénticos, podemos declarar el siguiente CSS:

	h1 {
      /* etc */
	}

Sin embargo, rara vez se cumple esto en aplicaciones comerciales de gran escala. Para este caso debemos encapsular los estilos afectados en módulos:

	.modulo-encabezado {
	  font-size: ...;
	  color: ...;
	}
