# Instructivo de deploy — Cimiento en dev.0xsamuraios.com/conectores/

Todos los archivos ya están listos y validados. Esto es lo que necesita hacer el dueño de la URL para publicarlos — sin tocar código, solo subir archivos a las rutas correctas.

## 1. Archivos y dónde va cada uno

Todo vive bajo el subdirectorio `/conectores/` del dominio, **excepto `robots.txt`**, que va en la raíz del dominio.

| Archivo | Ruta final |
|---|---|
| `index.html` | `https://dev.0xsamuraios.com/conectores/index.html` (y debe responder también en `https://dev.0xsamuraios.com/conectores/`) |
| `resultado.html` | `https://dev.0xsamuraios.com/conectores/resultado.html` |
| `assets/logo-odoo.png` | `https://dev.0xsamuraios.com/conectores/assets/logo-odoo.png` |
| `assets/logo-erpnext.png` | `https://dev.0xsamuraios.com/conectores/assets/logo-erpnext.png` |
| `sitemap.xml` | `https://dev.0xsamuraios.com/conectores/sitemap.xml` |
| `robots.txt` | `https://dev.0xsamuraios.com/robots.txt` ⚠️ **en la raíz del dominio, no dentro de `/conectores/`** |

**No incluir** ninguna carpeta tipo "Claude outputs" ni capturas/borradores — solo los 6 archivos de la tabla.

## 2. ⚠️ Punto que el dueño de SamuraiOS debe confirmar

El `robots.txt` que entregamos reemplaza **todo** el robots.txt del dominio `dev.0xsamuraios.com`, no solo la parte de `/conectores/`. Si ese dominio ya sirve otro contenido (otro proyecto, otra ruta) con su propio robots.txt, hay que **fusionar** las reglas en vez de sobreescribir — de lo contrario se puede desindexar sin querer algo que no es Cimiento. Si `/conectores/` es lo único que vive en ese dominio, se puede subir tal cual.

Contenido a fusionar/subir:
```
User-agent: *
Allow: /conectores/

# Permitir explícitamente motores de búsqueda de IA y respuestas generativas
User-agent: Google-Extended
Allow: /conectores/

User-agent: GPTBot
Allow: /conectores/

User-agent: ClaudeBot
Allow: /conectores/

User-agent: PerplexityBot
Allow: /conectores/

Sitemap: https://dev.0xsamuraios.com/conectores/sitemap.xml
```

## 3. Checklist de verificación post-deploy

Una vez subido, confirmar lo siguiente (todo debería funcionar sin tocar nada más):

- [ ] `https://dev.0xsamuraios.com/conectores/` carga la landing completa (nav, diagnóstico, pricing, FAQ).
- [ ] Los links del menú (Desktop y mobile) navegan a las secciones correctas.
- [ ] El autodiagnóstico completa el flujo de 9 preguntas y redirige a `resultado.html` con los parámetros en la URL (`?nivel=...&giro=...`).
- [ ] `resultado.html` muestra el resultado correcto según el giro e industria.
- [ ] El botón "Descargar PDF" del resultado genera el PDF con el branding rojo de SamuraiOS.
- [ ] `https://dev.0xsamuraios.com/robots.txt` responde con el contenido correcto (fusionado si aplica).
- [ ] `https://dev.0xsamuraios.com/conectores/sitemap.xml` carga y es XML válido.
- [ ] Vista en celular (375px) sin scroll horizontal ni elementos cortados.

## 4. Pendientes conocidos (no bloquean el deploy)

Estos tres puntos están pendientes de una decisión de JP, no de acción del dueño de SamuraiOS:

1. **Imagen de vista previa social (`og-image.jpg`)** — `index.html` y `resultado.html` ya referencian `https://dev.0xsamuraios.com/conectores/og-image.jpg`, pero ese archivo todavía no existe. Sin él, al compartir el link en WhatsApp/redes no habrá imagen de preview (solo texto). No rompe la página.
2. **Favicon** — no se ha definido uno todavía; el sitio no lo referencia aún.
3. **Contraste del rojo sobre fondo oscuro** — el acento `#941B1B` (rojo cinabrio) no cumple el mínimo de accesibilidad AA cuando se usa como texto sobre fondos oscuros (widget de diagnóstico, `resultado.html`, PDF). Es una mejora cosmética/accesibilidad, no un bloqueante funcional.

Ninguno de los tres impide que el sitio funcione correctamente hoy.
