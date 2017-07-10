---
layout: chapter
title: Organización
section: Extras
permalink: /capitulos/organizacion/
description: Aprende a organizar tus archivos CSS.
---

El buen código es fácil de encontrar, y esto significa estar bien organizado. Así es como queremos nuestro CSS. Generalmente hablando, hay dos enfoques para elegir, de los cuales hablaremos en este capítulo.

## 1. CSS en un solo directorio

Con este enfoque, todo el CSS va dentro del mismo directorio:

	/ruta/al/css
	  /vendor
        libreriasDeTerceros.css
        otraLibreriaDeTerceros.css
	  /miApp
	    algo.css
	    global.css
	    carrito.css

### Notas

* El código de terceros está en `/vendor`.
* El CSS de tu aplicación está en `/miApp`, donde *miApp* es el nombre de tu proyecto.
* Este enfoque simplifica el despliegue (deployment) porque al compilar el proyecto solo hay que especificar un directorio que empaquetar y comprimir.
* Esto sería lo más común, pero no por ello lo mejor.

## 2. CSS en directorios por módulo

Este enfoque usa directorios específicos para cada módulo:

	/global
	  /css
	    reset.css
	    global.css
        etc.css
	/carrito
      /controladoras
        ...
      /plantillas
        carrito.html
        carritoVacio.html
      /parciales
        cabeceraCarrito.html !!!
        resumenCarrito.html
      /js
        ...
      /css
        carrito.css
	/cabecera
	  ...

### Notas

* Nos orientamos en torno a características de la app (features) en lugar de su tecnología, haciendo que este enfoque sea robusto.
* El CSS global necesita un directorio por si solo, ya que sus estilos no pertenecen a ningún módulo.
* Este enfoque tiene más posibilidades de sufrir *el problema del límite de 31 archivos* que explicamos a continuación.

## El problema del límite de 31 archivos

Sea cual sea el camino que elijas, ten en cuenta que algunas versiones de Internet Explorer tienen un límite de 31 archivos CSS. Internet Explorer 9 por ejemplo, obvia del archivo CSS número 32 en adelante.

En producción no es un problema, ya que solemos empaquetar todo nuestro CSS para reducir peticiones HTTP. Pero en desarrollo local es mejor trabajar con los archivos fuente para depurar con facilidad, y es en navegadores antiguos (legacy) donde suelen salir errores.

**Si compilas tu CSS** desarrollando en local (como es normal al usar preprocesadores) no necesitas preocuparte. El preprocesador empaquetará los archivos por ti.

**Si no compilas tu CSSI** desarrollando en local (porque depurar es más fácil de esta manera) puedes remediar el problema mediante uno de estos dos enfoques:

### 1. Añade la opción de concatenar CSS localmente

Haciendo esto imitas al entorno de producción y puedes depurar como antes.

### 2. Usa menos de 32 archivos

Como probablemente tengas más de 31 módulos, no puedes usar una organización por módulo. En su lugar, puedes poner varios módulos en el mismo archivo CSS.

## Conclusión

En este capítulo hemos discutido sobre dos maneras de organizar CSS. Elijas la que elijas, ten en cuenta el problema de los 31 archivos, porque hace que la depuración sea mucho más complicada en los navegadores que causan más problemas.
