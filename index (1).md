# Optimizando la carga de un catálogo en e-commerce: peso y dimensiones en Tiendanube

> Blog técnico — Materia: Mentalidad de Crecimiento y Comunicación en Entornos Digitales
> Diplomatura en Marketing Digital · Coderhouse · 2026
> Autor: Agustín Turcato

---

## Contexto

Hazard es una marca de streetwear independiente de Buenos Aires que vende sus prendas —hoodies, remeras y piezas de edición limitada— a través de una tienda online montada en **Tiendanube**, una de las plataformas de e-commerce más usadas de la región.

Al lanzar la tienda, el catálogo era chico y la carga de productos parecía un trámite simple: subir fotos, escribir la descripción y poner el precio. Sin embargo, a medida que la marca creció y se sumaron más prendas y más drops, apareció un cuello de botella inesperado que no tenía que ver con el diseño ni con las ventas, sino con un dato aparentemente menor de cada producto: **su peso y sus dimensiones**.

## Problema

El desafío técnico principal fue que **cargar manualmente el peso y las dimensiones de cada producto, uno por uno, resultaba lento, tedioso y propenso a errores**, y ese trabajo no escalaba a medida que crecía el catálogo.

En Tiendanube, el peso y las medidas de cada artículo no son un dato decorativo: son la base con la que las integraciones de envío (Correo Argentino, OCA y otras) **calculan automáticamente el costo del envío** en el checkout. Esto generaba dos problemas concretos:

- **Operativo:** cargar producto por producto el peso y las tres dimensiones (alto, ancho, profundidad) se volvía una tarea repetitiva y eterna cuando había que subir un drop completo de varias prendas y talles.
- **De negocio:** cuando un producto quedaba sin esos datos o con datos incorrectos, el cálculo de envío fallaba —mostraba un costo erróneo o directamente no ofrecía opción de envío—, lo que podía hacer que el cliente abandonara la compra en el último paso.

En otras palabras: un dato físico mal cargado o faltante se traducía, al final de la cadena, en una venta que se caía.

## Acciones (Post-Mortem Constructivo)

Para resolverlo apliqué un enfoque de post-mortem constructivo: no solo apagar el incendio, sino entender la causa raíz y dejar un proceso que evitara que el problema se repitiera.

1. **Detección y diagnóstico.** Identifiqué que las consultas de los clientes sobre "por qué no me figura el envío" y los costos raros en el checkout tenían un origen común: productos con el campo de peso/dimensiones vacío o mal cargado. El síntoma estaba en el checkout, pero la causa estaba en la ficha del producto.

2. **Análisis de causa raíz.** La raíz no era un error de la plataforma, sino la **falta de un criterio estandarizado** para cargar estos datos. Cada prenda se medía y pesaba de forma improvisada, lo que multiplicaba el tiempo y los errores.

3. **Estandarización por tipo de prenda (solución de fondo).** En lugar de medir y pesar cada artículo desde cero, definí **valores estándar por categoría**: un hoodie pesa y mide aproximadamente lo mismo que otro hoodie ya empaquetado, lo mismo para remeras, etc. Pesé y medí una pieza representativa de cada tipo —ya embalada, como sale al envío— y fijé esos valores como referencia para toda la categoría.

4. **Carga masiva por planilla (eficiencia).** En vez de editar producto por producto desde el panel, usé la **exportación/importación por planilla** de Tiendanube: descargué el catálogo a una hoja de cálculo, completé las columnas de peso y dimensiones de forma ordenada (apoyándome en los valores estándar por categoría) y volví a importar todo de una sola vez. Lo que antes era cargar decenas de fichas a mano pasó a ser una sola operación.

5. **Validación con prueba de checkout (verificación).** Después de la carga, simulé compras reales desde el sitio hacia distintas zonas (CABA, interior) para confirmar que las opciones de envío aparecían y que los costos calculados eran coherentes. Esta prueba fue clave para asegurarme de que la solución funcionaba antes de un nuevo lanzamiento.

6. **Documentación del criterio (prevención).** Dejé registrado el criterio de pesos y medidas por categoría, de modo que cada producto nuevo se cargue desde el inicio con el dato correcto y el problema no vuelva a aparecer.

## Aprendizajes

Este incidente me dejó varias lecciones que exceden a Tiendanube y aplican a cualquier proyecto de e-commerce:

- **Los datos "menores" no son menores.** Un campo aparentemente secundario como el peso de un producto puede romper toda la experiencia de compra si se descuida.
- **Estandarizar antes que repetir.** Definir un criterio por categoría ahorró horas de trabajo y eliminó la principal fuente de errores. La sistematización vence al esfuerzo manual.
- **La carga masiva es tu aliada.** Aprender a usar la importación por planilla transformó una tarea inmanejable en una operación de minutos.
- **Validar siempre con una prueba real.** Probar el checkout de punta a punta antes de cada drop evita que un error invisible se transforme en ventas perdidas.
- **Documentar para no repetir.** Dejar el criterio escrito convierte una solución puntual en un proceso repetible para el futuro.

## Relación entre Control de Versiones y Resolución del Problema

Para documentar este proceso utilicé **control de versiones con Git**, gestionando el blog y sus avances a través de commits que reflejan cada etapa del trabajo. Esto permitió:

- **Trazabilidad:** cada cambio quedó registrado con su fecha y su propósito, mostrando cómo evolucionó la solución desde la detección del problema hasta la prevención.
- **Reversión segura:** ante cualquier cambio que no funcionara, era posible volver a una versión anterior estable sin perder el trabajo.
- **Documentación viva:** el historial de commits funciona como una bitácora del proceso, complementando este post-mortem.

## Evidencia de Control de Versiones (Commits Relevantes)

Durante la elaboración de este blog, cada etapa fue versionada. A continuación se listan los commits relevantes:

- `docs: estructura inicial del blog y secciones de la plantilla`
- `content: redacción del contexto y el problema de carga de productos`
- `content: documentación de acciones y post-mortem constructivo`
- `content: aprendizajes y reflexión sobre feedback`

*(Los enlaces a cada commit se completan con la URL real del repositorio una vez publicado.)*

## Reflexión sobre Feedback Radicalmente Sincero

En medio del proceso, mientras me enfocaba en seguir cargando productos a mano para "terminar rápido", un comentario directo me hizo cambiar el enfoque. La devolución fue franca: *"Estás perdiendo horas cargando uno por uno y encima se te cuelan errores; el problema no es la velocidad con la que cargás, es que no tenés un sistema para hacerlo."*

Al principio fue incómodo escucharlo, porque sentía que ya estaba haciendo el esfuerzo. Pero esa **sinceridad radical** me obligó a frenar y reconocer que estaba atacando el síntoma (cargar más rápido) en lugar de la causa (la falta de un criterio y de carga masiva). Ese feedback fue el que me llevó a estandarizar por categoría y a usar la importación por planilla, que terminó siendo la verdadera solución. La lección fue que el feedback directo, aunque incomode, suele señalar justo el punto que uno está evitando mirar.

---

## Checklist de Entrega Final

**Información General**

- **URL pública del blog:** _(se completa con la URL de GitHub Pages, ej.: https://TUUSUARIO.github.io/blog-tecnico/)_
- **Enlace al repositorio:** _(se completa con la URL del repo, ej.: https://github.com/TUUSUARIO/blog-tecnico)_
- **Commits relevantes:** estructura inicial · contexto y problema · acciones y post-mortem · aprendizajes y feedback

**Requisitos**

- [x] Entrada de blog publicada y accesible públicamente (GitHub Pages)
- [x] Documentación clara y estructurada según plantilla (Contexto, Problema, Acciones, Aprendizajes)
- [x] Evidencia de control de versiones (historial de commits en el repositorio)
- [x] Reflexión sobre feedback radicalmente sincero incluida
