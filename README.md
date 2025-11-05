# CaudataHAMB — Calculadora de Nómina

Proyecto sencillo que contiene una calculadora de nómina proporcional en un único HTML con CSS y JS separados.

Estructura relevante

- `CaudataHAMB.html` — interfaz principal (usa `css/styles.css` y `js/script.js`).
- `css/styles.css` — estilos del proyecto.
- `js/script.js` — lógica de la calculadora y generación de PDF (usa jsPDF desde CDN).
- `img/Logo.png` y `img/logo.svg` — logos usados en la interfaz; el PDF incrusta un SVG embebido convertido a PNG para evitar problemas de CORS.

Prueba local rápida

1. Abrir localmente

   - Opción A (doble clic): abre `CaudataHAMB.html` en tu navegador por doble clic (funciona en muchos entornos).
   - Opción B (servidor local recomendado): para evitar restricciones del navegador con recursos locales, ejecuta un servidor HTTP desde la carpeta del proyecto:

```bash
# si tienes Python 3
python3 -m http.server 8000
# luego abre http://localhost:8000/CaudataHAMB.html
```

2. Interactuar

- Marca "¿Trabajaste menos de 30 días?" para mostrar campos de días.
- Ajusta los valores y presiona "Calcular Nómina".
- Luego haz clic en "Descargar PDF" para obtener `bauche_nomina.pdf`.

Notas sobre el PDF y CORS

- La generación del PDF incrusta un logo que proviene del SVG embebido en el propio código JS (data URL). Esto evita la mayoría de problemas de CORS asociados con cargar imágenes desde el sistema de archivos o desde dominios remotos.
- Si por alguna razón tu navegador no puede crear el canvas a partir del SVG embebido, el código tiene un fallback que genera el PDF sin el logo.

Cómo desactivar el logo en el PDF

- Edita `js/script.js` y busca el bloque dentro de la función que genera el PDF. Si deseas eliminar el logo por completo, reemplaza la sección que carga/dibuja la imagen por una llamada directa a `drawRest(...)`, por ejemplo:

```js
// dibujar PDF sin logo
drawRest(44);
```

Soporte y mejoras sugeridas

- Si quieres que el PDF incluya un nombre de empresa o firma, puedo añadir un campo opcional en la UI que luego se inyecte en el PDF.
- Para producción, podríamos minificar `css/styles.css` y `js/script.js`, y asegurar rutas absolutas o CDN para fuentes.

Si quieres que haga algún ajuste (por ejemplo quitar el logo del PDF, incrustar `Logo.png` en base64 en el JS, o añadir un campo para introducir nombre de empresa/firma), dime cuál prefieres y lo implemento.