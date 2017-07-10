---
layout: chapter
title: Reutilización
section: Background
permalink: /capitulos/reutilizacio/
description: Aprende porqué evitar la reutilización de elementos y aceptar la repetición hace que nuestro CSS sea más fácil de mantener.
---

Según Harry Roberts, *DRY (don't repeat yourself) es a menudo malinterpretado como la necesidad de nunca repetir lo mismo más de una vez. Esto no es práctico, es habitualmente contraproductivo y puede llevar a abstracciones forzadas y código enrevesado e innecesariamente complejo.*

Estas abstracciones forzadas y complejidad innecesaria resultan normalmente en clases visuales y atómicas. Ya las hemos repasado en el capítulo [semántica](/capitulos/semantica/) y sabemos lo inconvenientes que son. Los "mixins" también pueden crear problemas como veremos a continuación.

Aunque a veces tendemos a abstraer nuestro CSS demasiado, hay ocasiones en las que la reutilización tiene sentido. La pregunta que debemos hacernos es *¿cómo podemos reutilizar un estilo?*

## ¿Cómo podemos reutilizar un estilo?

Si queremos reutilizar un estilo, una opción sería delimitar con comas una lista de selectores en un archivo con nombre reconocible. Si sabes algo de SASS, esto es exactamente lo que los `@extends` hacen. Por ejemplo, si varios elementos necesitan un texto de color rojo, podemos hacer:

	.unaCosa,
	.otraCosa {
	  color: red;
	}

Este enfoque se debe usar cuando sea conveniente y no para mejorar el rendimiento. Si la abstracción solo tiene una regla, solo estamos cambiando una línea de código por otra.

Si algún selector se desvía de las reglas establecidas en la abstracción, debe ser eliminado de la lista. De otra manera, podría caer en regresión con otros selectores y crear problemas de sobrescritura de estilos.

Es importante resaltar que esta es solo una de varias técnicas a nuestra disposición. Cuando un *concepto* ha sido comprendido correctamente, podemos hacer uso de otras técnicas, que discutiremos en [Módulos](/capitulos/modulos/), [Estados](/capitulos/estados/) y [Modificadores](/capitulos/modificadores/).

## ¿Qué pasa con los "mixins"?

Los "mixins" nos dan lo mejor de ambos mundos. Al menos en teoría.

Al igual que las clases utilitarias, actualizar un "mixin" propaga los cambios a todas sus instancias. Si no controlamos qué está usando ese "mixin", aumentamos el riesgo de regresión. En lugar de actualizarlo podríamos crear uno nuevo, pero esto causaría redundancia.

Además, normalmente los "mixins" acaban teniendo muchas reglas, parámetros y condiciones. Algo que añade complejidad, y la complejidad es difícil de mantener.

Para mitigar esta complejidad, podemos crear "mixins" granulares, como el del ejemplo del texto rojo. En principio, parece buena idea. Pero, ¿no sería lo mismo declarar el "mixin" que, simplemente, añadir la regla `color: red`?

Si tenemos que actualizar la regla en varios sitios, buscar y reemplazar puede ser lo único que realmente necesites. Además, cuando el "mixin" *rojo* cambia a *naranja* vas a tener que actualizar su nombre de todas formas.

Aun con todo lo que hemos visto, los "mixins" pueden ser muy útiles. Podríamos, por ejemplo, querer aplicar *clearfix* en ciertos elementos, solo en determinados puntos de ruptura. Esto es algo que CSS "a secas" no puede hacer.

Como tales, los "mixins" no son *malos*, debemos usarlos, pero juiciosamente.

## ¿Qué pasa con el rendimiento?

Nos complicamos la vida innecesariamente cuando hablamos de rendimiento. Solemos obsesionarnos con los detalles más pequeños.

Incluso si el total del CSS es mayor de 100kb, probablemente no obtengamos mucha ganancia al intentar aplicar "DRY" sin control. Como vimos anteriormente, hacer CSS más pequeño puede resultar en un HTML más grande.

Comprimiendo una sola imagen de una web, obtenemos mejor retorno de nuestra inversión en rendimiento. Ya hemos hablado de que resolviendo problemas de redundancia mejoramos la mantenibilidad *y* el rendimiento.

## ¿Va esto en contra de los principios de DRY?

Intentar reutilizar, por ejemplo `float: left`, es parecido a intentar reutilizar variables en distintos objetos Javascript. Esto no va en contra de DRY.

## Conclusión

Sobreutilizar DRY conduce a código innecesariamente complejo y enrevesado. Haciendo esto, conseguimos una peor mantenibilidad. En lugar de obsesionarnos con los estilos, nos deberíamos enfocar en reutilizar módulos concretos. Algo que veremos en los siguientes capítulos.
