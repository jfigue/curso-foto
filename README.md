# Enfoque — Curso de fotografía para Galaxy S25+

App web autónoma (PWA) con el curso de fotografía de paisajes y retratos:
26 lecciones en 4 niveles, 5 herramientas interactivas y seguimiento de progreso.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | La app completa: contenido, estilos y lógica en un solo archivo |
| `manifest.json` | Datos de instalación de la PWA (nombre, iconos, colores) |
| `sw.js` | Service worker: hace que la app funcione sin conexión |
| `icon-192.png` | Icono de la app |
| `icon-512.png` | Icono de la app en alta resolución |
| `icon-maskable-512.png` | Icono adaptativo para Android |

## Cómo instalarla en el teléfono

La PWA necesita estar servida por HTTPS, así que el camino más corto es el mismo
que usamos para la app de guitarra: un repositorio con GitHub Pages.

1. Creá un repositorio nuevo en GitHub, por ejemplo `Curso-fotografia`.
2. Subí los 6 archivos a la raíz del repositorio.
3. Entrá en **Settings → Pages**, y en *Source* elegí la rama `main` y la carpeta `/ (root)`.
4. Esperá un minuto y abrí la URL que te da GitHub:
   `https://<tu-usuario>.github.io/Curso-fotografia/`
5. En el teléfono, abrila en Chrome y usá **⋮ → Add to Home screen**
   (*Agregar a la pantalla de inicio*).

Queda como una app más: icono propio, pantalla completa, sin barra del navegador
y funciona sin conexión después de la primera visita.

## Notas técnicas

- **Sin dependencias.** No carga nada de ningún CDN. Todo es HTML, CSS y
  JavaScript propio, y los dibujos de las herramientas son Canvas 2D.
- **Los datos no salen del teléfono.** El progreso, las notas y los checklists se
  guardan en `localStorage`. Las fotos que cargues en la herramienta de
  cuadrículas se procesan en el navegador y no se suben a ningún servidor.
- **Todas las lecturas y escrituras de `localStorage` están dentro de
  `try/catch`**, así que la app sigue funcionando en modo incógnito o con el
  almacenamiento del sitio bloqueado, sólo que sin recordar el progreso.
- **Si cambiás `index.html`**, subí también el número de versión del caché en
  `sw.js` (`const CACHE = 'enfoque-v1'` → `v2`). Si no, el service worker va a
  seguir sirviendo la versión vieja desde el caché.
- Probada en Chromium headless a 412 × 915 px, sin errores de consola, en tema
  oscuro y claro.

## Estado del contenido

- **Nivel 1 (lecciones 1 a 6):** completas, con teoría, bloque "Para el
  ingeniero", videos verificados, práctica paso a paso, tabla de errores
  comunes, evaluación y checklist.
- **Niveles 2 a 4 (lecciones 7 a 26):** muestran objetivo y contenido previsto.
  Se van escribiendo en el chat a medida que avanzás, para poder ajustarlas a lo
  que haya que reforzar.

Para agregar una lección ya dictada, editá el array `LESSONS` en `index.html`:
cambiá `ready:false` por `ready:true` y completá los campos `teoria`, `eng`,
`videos`, `practica`, `errores`, `evaluacion` y `checklist`, con la misma
estructura que tienen las lecciones 1 a 6.
