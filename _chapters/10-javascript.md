---
layout: chapter
title: Javascript
section: Extras
permalink: /capitulos/javascript/
description: Aprende cómo escribir CSS y Javascript mantenible al mismo tiempo.
---

Es posible que usemos Javascript para aplicar el mismo comportamiento a múltiples módulos o componentes.

Por ejemplo, podríamos usar un constructor `Plegar` (Collapser) que haga que un elemento sea visible o invisible.

Hay dos enfoques posibles, ambos complementarios a todo lo aplicable al CSS que hemos explicado en los capítulos anteriores.

## 1. Encapsular el estado en el módulo

Para ello, necesitamos aplicar una clase de estado específica para cada módulo al constructor:

	var modulo1Plegar = new Plegar(elemento1, {
	  cssClaseOculto: 'moduloA-estaOculto'
	});

	var modulo2Plegar = new Collapser(elemento2, {
	  cssClaseOculto: 'moduloB-estaOculto'
	});

Y luego reutilizar el CSS así:

	.moduloA-estaOculto,
	.moduloB-estaOculto {
      display: none;
	}

La contrapartida es que esta lista (o el "mixin") puede crecer rápidamente. Y cada vez que añadamos este comportamiento, tenemos que actualizar el CSS. Supondría un pequeño cambio, pero un cambio al fin y al cabo. Para este caso, podríamos considerar una clase de estado global.

## 2. Crear una clase de estado global

Si nos encontramos repitiendo exactamente el mismo conjunto de estilos para muchos módulos, quizás sea mejor usar una clase de estado global de la siguiente manera:

	.estadoGlobal-estaOculto {
      display: none;
	}

Este enfoque elimina las largas listas de selectores. Tampoco tenemos que especificar la clase del módulo cuando instanciamos, porque la clase global será referenciada desde dentro.

	var modulo1Plegar = new plegar(elemento1);
	var modulo2Plegar = new plegar(elemento2);

Sin embargo, esto no siempre tiene sentido. Podemos tener dos módulos distintos el mismo *comportamiento*, pero con distinta *apariencia*, algo de lo que ya hemos hablado en [Estados](/capitulos/estados/).

## 3. Lo mejor de ambos mundos

Podemos combinar los dos enfoques, usando por defecto la clase de estado global y solo cuando sea necesario, especificar una clase al instanciar como en el primer ejemplo.

## Conclusión

Cuando pensamos en estados, particularmente cuando tenemos Javascript en la cabeza, necesitamos considerar como afectan tanto al comportamiento como a la apariencia. Distintos componentes pueden compartir comportamiento, pero es posible que su apariencia sea bien distinta. Si lo consideramos cuidadosamente, podemos elegir la solución correcta al problema.
