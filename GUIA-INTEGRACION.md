# Integración de medición: Meta Pixel, Google Tag Manager, GA4 y Google Ads

## Qué quedó preparado en la página

- El Pixel de Meta existente conserva el ID `2438467793316618` y registra `PageView`.
- Los eventos de navegación, visita de secciones y apertura del mensaje secreto se envían al `dataLayer` para que Google Tag Manager los procese.
- Las visitas de sección también se envían a Meta como `ViewContent`; abrir el mensaje secreto se envía como `SecretMessageOpen`.
- El contenedor GTM `GTM-MRC4J7XD` está instalado en el HTML con sus fragmentos estándar para `<head>` y `<body>`.

Meta Pixel, GA4 y Google Ads son destinos de medición distintos. GTM permite administrar las etiquetas de Google desde un punto común; las mismas acciones instrumentadas en la página quedan disponibles para comparar los resultados de cada plataforma.

## Configuración del grupo

1. Crear un contenedor **Web** en Google Tag Manager y copiar su ID, con formato `GTM-XXXXXXX`, en `GTM_CONTAINER_ID` al principio de `index.html`.
2. En GTM, crear una etiqueta **Google tag** con el ID de medición de GA4 (`G-XXXXXXXXXX`) y un activador de inicialización en todas las páginas.
3. Crear activadores de tipo **Evento personalizado** con estos nombres exactos:
   - `content_navigation`
   - `section_view`
   - `secret_message_open`
4. En GA4, crear una etiqueta **Evento de GA4** por cada activador. Usar nombres como `content_navigation`, `section_view` y `secret_message_open`. Se pueden enviar `content_section`, `link_text` y `section_id` como parámetros.
5. En Google Ads, crear una acción de conversión para la interacción que el grupo quiera presentar (por ejemplo, `secret_message_open`). Añadir en GTM la etiqueta **Seguimiento de conversiones de Google Ads** con el ID y la etiqueta de conversión entregados por Ads, y activarla con el evento elegido. Configurar también la etiqueta de vinculación de conversiones en todas las páginas.
6. Probar en **Vista previa** de GTM que cada interacción produce el evento esperado; comprobar las etiquetas de Google con Tag Assistant y los eventos de Meta con Meta Pixel Helper. Después, publicar la versión del contenedor.

## Datos que faltan para una conexión real

Se necesitan el ID de medición de GA4 y el ID más la etiqueta de conversión de Google Ads. Esos valores pertenecen a las cuentas del equipo y no están en este repositorio. Hasta configurarlos y publicar las etiquetas, los eventos están preparados en el código, pero no aparecerán en las propiedades de Google.

Para una exposición, el grupo puede mostrar el recorrido de un evento: interacción en la web → `dataLayer` → GTM → etiqueta de GA4 o conversión de Ads; en paralelo, el Pixel de Meta recibe los eventos Meta indicados arriba.
