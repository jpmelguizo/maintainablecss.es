---
layout: chapter
title: Módulos
section: Core
permalink: /chapters/modulos/
description: Aprende la diferencia entre módulos y componentes y cómo identificarlos en un diseño. También crearemos algunos módulos de ejemplo.
---

## ¿Qué es un módulo?

Ún módulo es una unidad independiente y distintiva, que puede ser combinada con otros módulos para formar estructuras más complejas.

En una sala de estar, podríamos considera la televisión, el sofá o los cuadros de la pared como módulos. Todos se combinan para hacer una habitación usable.

Si quitámos alguno de esos módulos, los otros siguen funcionando. No necesitamos la tele para poder sentarnos en el sofá, etc.

En una web, su cabecera, formulario de registro, carrito de compra, navegación y promociones de la página de inicio pueden considerarse como módulos.

## ¿Qué es un componente?

Un módulo está hecho de componentes. Sin componentes, un módulo estaría incompleto o roto.

Por ejemplo, un sofa tiene una estructura, patas, acholchado del asiento, etc. todos ellos son componentes básicos para usar el diseño de la forma para la cual se diseño.

Un *módulo* logotipo puede consistir en un texto, una imágen y un enlace, cada uno es un componente. Sin la imagen el logotipo está roto y sin el enlace estaría incompleto.

## Módulos vs componentes

En ocasiones es difícil decidir si algo debería ser un componente o un módulo. Por ejemplo, pensemos en una cabecera que contiene un logotipo y un menú ¿Son módulos o componentes?

En un proyecto reciente, tenía sentido que el logo fuera un componente y el menú un módulo ¿Cómo queda la cabecera sin logo? El menú de navegación podría colocarse por debajo de la cabecera en algún momento.

Nadie entiende los tus requisitos tan bien como tu. A través de la experiencia obtendras un sentido especial para ello. Y si algo sale mal, es muy fácil cambiar de componente a módulo.

Suficiente teoría por hoy. Vamos a construir tres módulos distintos. Al hacerlo, espero que cubrir todas las cosas en las que solemos pensar al escribir CSS.

## 1. Creando un módulo de carrito de compra

Vamos a simplicar este carrito para ser más breves. Cada producto en el carrito mostrará su título y la posibilidad de eliminarlo.


La plantilla podría ser esta:

	<div class="carrito">
	  <h1 class="carrito-titulo">Tu carrito</h1>
	  <div class="carrito-elemento">
	      <h3 class="carrito-tituloProducto">Título del producto</h3>
          <form>
              <input type="submit" class="carrito-botonEliminar" value="Eliminar">
	      </form>
	  </div>
	</div>

Y su CSS:

	.carrito {}
	.carrito-titulo {}
	.carrito-elemento {}
	.carrito-tituloProducto {}
	.carrito-botonEliminar {}

## 2. Creando un módulo de resumen de pedido

El siguiente paso será construir un módulo resumen de pedido. Este módulo se muestra al final del proceso de compra y tiene cierta similitud con el carrito. Por ejemplo, tiene un título y muestra una lista de productos.

Sin embargo, tiene una estética diferente y no permite eliminar los productos, es decir, ya no hay botón de eliminar.

El primer asunto a resolver es la tentación de reusar la plantilla y el CSS del carrito. Si, son parecidos, pero no son lo mismo.

Si tratamos de combinar ambos, entrelazaríamos dos módulos sobreescribiendo plantillas y CSS. Algo que es complejo de por si y sería difícil de mantener. Es mejor evitarlo directamente.

En lugar de reutilizar o mezclar, debemos crear un nuevo módulo con la siguiente plantilla:

	<div class="resumenPedido">
	  <h2 class="resumenPedido-titulo">Order summary</h2>
	  <div class="resumenPedido-elemento">...</div>
	  <div class="resumenPedido">...</div>
	</div>

Y el CSS quedaría así:

	.resumenPedido {}
	.resumenPedido-titulo {}
	.resumenPedido-elemento {}

Aunque parezca contraintuituvo, duplicar es mejor a largo plazo. Y realmente, no estamos duplicando. Duplicar sería copiar la *misma* cosa. Estos dos módulos pueden parecer similares pero no son iguales.

Manteniendo las cosas separadas mantenemos la sencillez. La sencillez es el aspecto más importante a la hora de crear software seguro, escalable y mantenible.

## 3. Creando un módulo botón

Como nuestro carrito de compra solo aparece en la página "carrito", no consideramos la posibilidad de reusarlo en otros sitios. Además, no pensamos en el hecho de que el botón de eliminar es un componente del módulo carrito, haciendolo más difícil de reutilizar en otros módulos.

Los botones son un ejemplo de algo que podríamos reutilizar en muchos sitios y potencialmente *dentro* de distintos módulos. Un botón no es muy útil por si solo.

Una opción podría ser actualizar el botón de componente a módulo de la siguiente manera:

	<input class="boton" type="submit" value="{%raw%}{{texto}}{%endraw%}">

Y su CSS:

	.boton {}

El problema es que los botones tienen normalmente distinto posicionamiento, tamaño y espaciado dependiendo del contexto. Y por supuesto, hay que considerar las posibles "media queries".

Por ejemplo, dentro de un módulo, un botón puede flotar a la derecha junto a algún texto. En otro módulo, puede estar centrado con algún texto por debajo y un margen inferior.

Idealmente, deberíamos limar estas inconsistencias en el *diseño*, antes de que lleguen al código. Pero esto no es siempre posible y en este ejemplo, asumiremos que tenemos que solucionarlo nosotros.

Es por estas diferencias por lo que abstraer reglas comunes puede ser complicado, y no queremos lidiar con un lio de reglas que se sobreescriben unas a otras. O lo que es peor, acabar con miedo a actualizar alguna regla.

Para evitar estos problemas, podemos usar un "mixin" o una lista de reglas comunes que no estén afectadas por sus contextos. Por ejemplo:

	.carrito-botonEliminar,
	.otraCosa-botonLogin,
	.otraCosa-botonBorrar {
      background-color: green;
      padding: 10px;
      color: #fff;
	}

Observa que en este emplo, no especificamos `float`, `margin` o `width` etc. Esos estilos se aplican en el botón correspondiente:

	.carrito-botonEliminar {
	  float: right;
	}

	.otraCosa-botonBorrar {
	  margin-bottom: 10px;
	}

Lo que parece sensato, ya que podemos optar por añadir otros selectores a estos estilos comunes, lo contrario de tener que sobreescribir estilos. Pero nos queda otra opción.

Imagina un proceso de compra en el que cada página tiene un botón para continuar y un enlace para volver atrás. Podriamos reutilizarlo convirtiéndolo en un módulo:

	<div class="procesoCompra">
	  <input class="procesoCompra-continuar">
	  <a class="procesoCompra-atras"></a>
	</div>

Quedando así el CSS:

	.procesoCompra-continuar { }

	.procesoCompra-atras { }

Haciendo esto, abstraemos y aplicamos los estilos a `.procesoCompra`, un módulo fácil de entender a simple vista. Y lo hemos conseguido sin tener que afectar otros botones parecidos pero no idénticos.

Todavía no hemos hablado de tener más de un tipo de botón (primario, secundario, etc.). Para esto usaremos modificadores, de los que hablaremos más adelante.

## Conclusión

Un módulo, por definición, es un trozo de HTML y CSS reutilizable. Antes de que un conjunto de elementos pueda ser considerado como módulo, tenemos que entender cuáles son sus diferentes casos de uso.

Solo entonces, podremos diseñar la abstracción correcta. Al hacerlo evitamos añadir complejidad, el origen del CSS imposible de mantener.
