---
layout: chapter
title: Estados
section: Core
permalink: /chapters/estados/
description: Aprende a administrar los diferentes estilos de tus módulos y componentes basados en sus estados, como mostrado, escondido y cargando.
---

A menudo, y más aun con interfaces complejas, se debe aplicar estilo a los elementos en respuesta a sus cambios de estado. Por ejemplo, tenemos que dar estilos distintos a módulos (o componentes) si:

- Se muestran o esconden,
- están activos o inactivos,
- están habilitados o deshabilitados,
- están cargando o ya han cargado,
- tieneProductos o noTieneProductos,
- estaVacio o estaCompleto.

Para representar un estado, necesitamos añadir una clase adicional al módulo (o componente) al que pertenece el elemento. Por ejemplo, si nuestro módulo carrito de compra necesita un fondo gris cuando está vacío, el HTML debería ser:

	<div class="carrito carrito-estaVacio">

Y su CSS:

	.carrito-estaVacio {
      background-color: #eee;
	}

La clase tiene el nombre del módulo (o componente) como prefijo porque, aunque los estados puedan ser comunes, los estilos asociados no tienen porqué. Por ejemplo, un *carrito* vacío puede tener un fondo gris, mientras que unos resultados de búsqueda vacíos pueden tener una imágen posicionada de forma absoluta.

## ¿Qué pasa al reutilizar estados?

Algunas veces, quizás querramos reutilizar un estado en distintos módulos o componentes. Por ejemplo, hacer que un elemento sea visible o invisible. Esto se discute en más detalle en el capítulo [Javascript](/chapters/javascript/).


## ¿Qué pasa con los atributos ARIA?

No todos los estados visuales pueden ser representados con [atributos ARIA](https://www.w3.org/TR/wai-aria/states_and_properties#attrs_widgets). Por ejemplo, no hay atributo para representar `tieneProductos`. Por lo tanto, debemos usarlos solo cuando sean necesarios *adicionalmente* a las clases.

Además, usar un selector de atributo (en lugar de clase) tiene [menor soporte](https://www.impressivewebs.com/attribute-selectors/). Aunque algunos desarrolladores consideran estos navegadores anticuados, inseguros o irrelevantes, debemos evitar excluir usuarios.

## ¿Qué pasa si encadenamos clases?

Podríamos usar un selector encadenado para representar estados, por ejemplo:  `.modulo.estaDesactivado`. El problema es que este enfoque tiene menor soporte en navegadores. Hay que evitar patrones que excluyen usuarios innecesariamente, a no ser que tenamos una razón de peso para usarlos.

## Conclusión

Si un elemento necesita cambiar de estilo según su estado, debemos añadir una clase extra para aplicar las diferencias. Cuando sea necesario, usaremos atributos ARIA para las tecnologías asistivas, pero no para aplicar estilos. De esta manera, estamos empleando un enfoque consistente e inclusivo.
