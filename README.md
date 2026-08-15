# MADDI — Sitio web (Inicio · Foro · Nosotros)

## Estructura (la que armaste vos)
```
index.html
style.css
main.js
img/
  logo.webp
  banner.webp
  fondol.webp
  icon-tienda.webp     ← agregada por mí, faltaba
  zonas-banner.webp    ← agregada por mí, faltaba
pages/
  foro.html
  nosotros.html
```

## Qué estaba roto y qué arreglé
Al mover los archivos a esta estructura (raíz sin subcarpetas `css/`/`js/`, carpeta `img/` en vez de `images/`, y `foro.html`/`nosotros.html` dentro de `pages/`) quedaron rutas viejas apuntando a lugares que ya no existían. Eso hacía que no se vieran las imágenes. Puntualmente:

- **El fondo de batalla no se veía** porque `index.html` seguía apuntando a `images/fondo-battle.png` (carpeta que ya no existe). Lo corregí a `img/fondol.webp`.
- El resto de las imágenes (logo, banner, ícono de tienda, banner de zonas) también apuntaban a la vieja carpeta `images/` — las redirigí todas a `img/`.
- El CSS y el JS estaban enlazados como `css/style.css` y `js/main.js` — los corregí a `style.css` y `main.js`, que es donde están ahora, en la raíz.
- Como `foro.html` y `nosotros.html` viven un nivel más adentro (`pages/`), sus enlaces a `style.css`, `main.js` y las imágenes ahora usan `../` (por ejemplo `../style.css`, `../img/logo.webp`), y su link a "Inicio" apunta a `../index.html`. Entre ellos dos se enlazan directo (`foro.html`, `nosotros.html`) porque están en la misma carpeta.
- Faltaban dos imágenes en tu `img/`: el ícono de la tienda y el banner de zonas. Te las agregué (son las mismas que ya te había pasado antes) para que no se rompa nada.

No toqué el diseño, el contenido ni la estructura de carpetas que armaste — solo las rutas.

## Cómo verlo
Abrí `index.html` directamente, o mejor: serví la carpeta con un servidor local (por ejemplo "Live Server" de VS Code) para que las fuentes y el estado del servidor (jugadores online) funcionen sin restricciones de `file://`.

## Jugadores online reales (ya funciona)
`main.js` consulta la API pública gratuita mcsrvstat.us apuntando a `SERVER_IP = "maddi.lat"`, cada 60 segundos, sin backend propio.

## Formulario del Foro (envío a maddisoporte@gmail.com)
`pages/foro.html` usa FormSubmit (formsubmit.co) para mandar el mensaje directo a `maddisoporte@gmail.com`, con selector de asunto (Reportar abuso / Reportar problema / Consultas). **La primera vez** que alguien lo envíe, FormSubmit manda un correo de activación a esa casilla que hay que confirmar una sola vez.

## Tabla de "compras recientes"
Sigue siendo un placeholder visual (con nota abajo en el HTML). Mostrar compras reales de Tebex necesita la Tebex Headless API o un webhook — lo conectamos cuando tu tienda esté lista.

## Pendiente antes de publicar
1. Reemplazar los `href="#"` de "Tienda" (en `index.html`, `pages/foro.html`, `pages/nosotros.html`) por la URL real de tu Storefront de Tebex.
2. Confirmar el correo de activación de FormSubmit.
3. Revisar que `SERVER_IP` en `main.js` coincida con la IP final.
4. Reemplazar el placeholder de "modalidad destacada" en `index.html` por una captura real del lobby/arena.
