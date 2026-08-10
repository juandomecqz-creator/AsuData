# AsuData — Rediseño completo del sitio (desde cero)

## Contexto

El sitio actual en `web/` (index, industrias, paquetes, soluciones, nosotros, contacto)
corresponde a un posicionamiento viejo (paquetes Spark/Pulse/Edge) que ya no existe. El
`CLAUDE.md` del proyecto define una marca, mapa de sitio y 5 líneas de servicio nuevas y
cerradas. Este spec cubre la reconstrucción completa del sitio estático siguiendo ese
documento. Fuente de verdad de negocio: `web/CLAUDE.md` (no se repite contenido de negocio
acá salvo donde afecta decisiones de estructura).

Había además cambios staged en git (redisño previo, paleta clara navy/verde) que no siguen
ni el `CLAUDE.md` ni la decisión de este spec — se descartan por completo.

## Decisiones cerradas en esta sesión

1. **Punto de partida:** limpio. Se eliminan `industrias.html`, `paquetes.html`,
   `soluciones.html` (no mapean al nuevo sitemap). `css/main.css` y `js/main.js` se
   reescriben desde cero (el contenido actual usa paleta clara navy/verde, incompatible).
2. **Contacto:** sin formulario ni backend. Botón directo a WhatsApp
   (`https://wa.me/595985309007`) como acción principal en toda página con CTA de contacto.
3. **Logo:** usar `INSTAGRAM/logo asu data sin fondo.png` (fondo transparente), copiado a
   `web/assets/logo.png`. Reemplaza cualquier logo de solo texto.
4. **Paleta:** se mantiene la definida en `CLAUDE.md`, con un ajuste validado contra
   tendencia de diseño 2026 (Linear, PostHog, Attio — dark-mode-first, un solo acento,
   fondo oscuro suave en vez de negro puro):
   - `--dark` pasa de `#080C14` a `#0A1120`
   - Se agrega `--dark-surface:#0F1830` para superficies elevadas (nav, cards, footer)
   - Se agrega `--glow-cyan` (box-shadow sutil) para hover/focus de CTAs primarios
   - Cyan (`#00D4E8`) sigue siendo el único acento primario; el acento cálido (`#E8935A`)
     solo en detalles puntuales de Web/Marca, nunca como CTA principal

## Estructura de archivos

```
web/
├── index.html          (Inicio)
├── servicios.html       (Servicios — overview 5 líneas)
├── sistema-datos.html   (Sistema de Datos para Empresas)
├── casos.html            (Aarón, ore roga, Del Moral)
├── nosotros.html
├── contacto.html
├── css/main.css          (reescrito, tokens abajo)
├── js/main.js             (mismo comportamiento: hamburguesa, reveal on scroll, nav activo)
└── assets/logo.png        (copiado desde INSTAGRAM/)
```

## Design tokens (CSS)

```css
:root{
  --dark:#0A1120;
  --dark-surface:#0F1830;
  --navy:#1A3A6E;
  --cyan:#00D4E8;
  --warm:#E8935A;
  --gray:#8A9AB5;
  --light:#F4F7FF;
  --font-heading:'Syne', sans-serif;   /* 800 */
  --font-body:'DM Sans', sans-serif;
  --glow-cyan:0 0 20px rgba(0,212,232,0.35);
}
```

## Header (todas las páginas)

- Fijo arriba, fondo `--dark-surface`, blur al hacer scroll
- Izquierda: logo (`assets/logo.png`)
- Nav: Inicio · Servicios · Sistema de Datos · Casos · Nosotros · Contacto
- Extremo derecha: botón cyan sólido "Contactar" → link directo a WhatsApp (no a
  `contacto.html`)
- Mobile: hamburguesa → menú full-screen dark

## Footer (todas las páginas)

- Fondo `--dark-surface`, 3 columnas: logo+tagline / links del mapa del sitio / contacto
  (WhatsApp, email `info@asudata.net`, San Lorenzo, Paraguay)
- Línea legal: © AsuData 2026
- Sin redes sociales por ahora

## Esqueleto por página

### Inicio (`index.html`)
1. Header
2. Hero — narrativa datos→decisiones, 5 líneas como instrumentos. CTA primario WhatsApp,
   CTA secundario "Ver Sistema de Datos"
3. Bloque de conexión — 3-4 pasos visuales ("esta web genera datos → alimenta un dashboard
   → centraliza tu sistema"), sin copy largo
4. Casos destacados — preview de los 3 casos, link "Ver todos los casos"
5. Las 5 líneas, overview rápido — grid de 5 cards (ícono + nombre + frase corta, sin
   precios), cada card linkea a Servicios o a Sistema de Datos
6. CTA final — banda WhatsApp
7. Footer

### Servicios (`servicios.html`)
1. Header
2. Hero de página — refuerza que las 5 líneas son instrumentos de una misma promesa, no
   servicios sueltos
3. Las 5 líneas en detalle, orden: Sistema de Datos para Empresas (insignia, con link
   "ver a fondo" a su página propia) → Análisis de Datos → Páginas Web → Apps/Sistemas a
   medida (apps móviles mencionadas sin CTA fuerte) → Registro de Marca. Cada línea:
   tagline + pain-first + tabla de paquetes (paquete/precio/entrega) + texto legal de
   plazos una sola vez al pie de la sección de precios
4. CTA final
5. Footer

### Sistema de Datos para Empresas (`sistema-datos.html`)
1. Header
2. Hero de página — "Toda tu empresa, un solo lugar", conecta con hero de Inicio
3. El problema — pain-first (planillas sueltas, WhatsApp perdido, sin vista completa)
4. Los 3 tiers a fondo (bloques grandes, no tabla comprimida): Integración Departamental,
   Integración Empresarial, Plataforma Empresarial — cada uno con qué incluye, para quién
   es, precio, entrega, texto legal de plazos al pie
5. Cómo funciona / proceso — pasos genéricos (diagnóstico → integración → entrega), sin
   nombrar herramientas técnicas
6. Caso relacionado — si aplica, destacar uno de los 3 casos con link a Casos
7. CTA final
8. Footer

### Casos (`casos.html`)
1. Header
2. Hero de página — foco hiperlocal Paraguay
3. Los 3 casos, mismo peso, cada uno bloque propio (resultado/decisión primero, luego
   herramienta técnica): Aarón (gastronomía informal), ore roga (estudio de arquitectura,
   Arq. Lyda Valiente), Del Moral Relojes
4. CTA final — gancho "¿Tu negocio puede ser el próximo caso?"
5. Footer

### Nosotros (`nosotros.html`)
1. Header
2. Hero de página — institucional, serio
3. Historia/origen breve — sin nombres propios, sin mención de situación societaria
4. Misión / Visión
5. Método — cómo trabaja la marca (pain-first, hiperlocal, data-led), no lista genérica de
   valores
6. Por qué Paraguay / hiperlocal
7. CTA final
8. Footer

### Contacto (`contacto.html`)
1. Header
2. Hero de página — corto ("Hablemos")
3. Bloque de contacto directo — botón grande WhatsApp como acción principal, sin
   formulario
4. Canales adicionales — email, teléfono (texto), San Lorenzo, Paraguay
5. Footer

## Deploy

- No pushear a `asudatapy.vercel.app` (deploy real conectado a Vercel) hasta tener el
  sitio completo — evitar dejarlo a medio construir en una URL que ya está en uso.
  Confirmado con el usuario 2026-08-10.
- No publicar en el dominio real `asudatapy.net` hasta que esté liberado (regla ya
  existente en `CLAUDE.md`).

## Fuera de alcance de este spec

- Copy final de cada sección (se escribe página por página en la fase de implementación,
  mostrando esqueleto ya aprobado acá como base — no se vuelve a aprobar estructura)
- SEO/meta tags, sitemap.xml, analytics — a definir si se pide
