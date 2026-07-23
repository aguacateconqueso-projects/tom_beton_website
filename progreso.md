# Progreso — Tom Beton Website

Registro vivo del proyecto. Aquí se anota **todo** lo que hacemos, sesión por
sesión, y las reglas de trabajo que seguimos.

---

## Reglas del proyecto

1. **PR nuevo por cada cambio (regla #1, la más importante).**
   TODO lo que hagamos —una sección nueva, un texto, un color, un ajuste
   mínimo de lo mismo— se arma en una **rama nueva** y se abre un **Pull
   Request nuevo hacia `main`**. Nunca se hace push directo a `main`.
   El flujo es siempre: rama → PR a `main` → **tú mergeas** → **visualizas en
   Vercel**. Cada ajuste, por pequeño que sea, es su propio PR.

2. **`main` es la fuente de verdad.**
   `main` es lo que Vercel despliega. Solo llega código a `main` a través de un
   PR mergeado. Si algo no está en `main`, no está publicado.

3. **Un PR = un cambio con foco.**
   Cada PR describe qué cambia y por qué. Nada de mezclar cambios no
   relacionados en el mismo PR.

4. **Este archivo se actualiza en cada PR.**
   Cada PR que hace un cambio real añade su entrada en el registro de abajo,
   dentro del mismo PR. Así `progreso.md` siempre refleja el estado real.

5. **El sitio sigue siendo un solo archivo.**
   `index.html` autocontenido: todo el CSS y el JS inline, sin frameworks ni
   librerías externas. Única dependencia externa permitida: Google Fonts.
   Portable, listo para Vercel.

---

## Estado actual

- **Entregable:** `index.html` (sitio de demostración, un solo archivo).
- **Rama de despliegue:** `main` (la despliega Vercel).
- **Secciones del sitio:** Hero · The Work (catálogo, 5 piezas) · The Workshop ·
  The Maker · Acquire / Footer.

---

## Registro de sesiones

Cada entrada = un PR. Se anota de arriba (más reciente) hacia abajo.

### 2026-07-23 — Hero: naranja sólido, fuera el relieve — 🚧 EN PR
_Rama `claude/hero-section-redesign-kstx80`, PR nuevo tras mergear #8._
- El relieve de concreto generado (bloques Mondrian terracota que reaccionaban a
  hover/scroll) se sentía **demasiado complicado** y el terracota apagado no
  convencía. Se **elimina por completo** (CSS `.hero-relief`/`.hero-scrim`/`.blk`,
  los dos `<div>` del hero y todo el `<script>` del generador) y el hero pasa a un
  **naranja sólido y limpio `--orange #FF521B`**.
- El resto (texto crema, botones, nav) se mantiene. El sitio queda más simple.
- Pendiente charlar: las secciones internas siguen en **tema oscuro** (PR #8); si
  también hay que aclararlas/simplificarlas, es otro paso.

### 2026-07-23 — Tema oscuro + headline nuevo — ✅ MERGEADO (PR #8)
_Rama `claude/hero-section-redesign-kstx80`, sobre el mismo PR #7._
- **Headline nuevo:** «Concrete, Geometry, and Light» → **«Handmade / Brutalist
  Designs»** (dos líneas más cortas, calza mucho mejor con StackSans).
- **Paleta nueva → sitio oscuro con texto crema.** El hero naranja se mantiene;
  el resto del sitio se **invierte a tema oscuro** con la paleta indicada:
  - Texto y líneas estructurales: **crema `#F1E0C5`** (`--paper`).
  - Fondos: `--concrete #241E18` (base) y `--charcoal #2E2720` (cards/workshop/
    footer); `--ink #14110C` como negro más profundo (sombras, texto sobre tonos
    claros, grout del hero).
  - Acento: **rust `#C34A36`**. Tonos de piezas remapeados: `--ochre`→tan
    `#C9B79C`, `--dusty`→purple `#B47EB3`, `--sage` `#71816D` (se conservan los
    nombres de clase para no tocar el HTML de las piezas). `--maroon`/`--clay`
    se mantienen como rojos cálidos que armonizan.
  - Bordes brutalistas y sombras duras pasan a **crema** para leerse sobre
    oscuro; divisores `rule-top` entre secciones también en crema.
- **StackSans embebida en base64** (viene del trabajo previo del PR #7):
  `StackSansHeadline-Bold` como data URI en el `@font-face`, un solo archivo
  (regla #5), fallback Archivo. `fonts/README.md` = atribución + OFL 1.1.
- **Hero centrado** (del trabajo previo del PR #7): copy centrado y sin el
  eyebrow; se eliminó el media query viejo de dos columnas.

### 2026-07-23 — Hero: título centrado, StackSans (cableado) y nuevo subtítulo — ✅ MERGEADO
_PR mergeado a `main`._
- **Titulares en StackSans** vía `@font-face` (primer cableado apuntando a un
  `.otf` en `fonts/`; luego se embebió en base64, ver entrada de arriba).
- **Hero centrado:** copy con `text-align: center`, subtítulo `margin: 0 auto`
  y `max-width: 52ch`, botones centrados; scrim pasa a **radial centrado**.
- Se **elimina el eyebrow** «RAW CONCRETE · CAST BY HAND».
- **Subtítulo nuevo:** «Somewhere between sculpture, architecture, and design
  object. Influenced by photography and minimalism, creating objects that
  continuously change throughout the day as the light shifts across their
  surfaces.»
- Título se mantiene: «Concrete, Geometry, and Light».

### 2026-07-22 — Fondo del hero: relieve de concreto + nuevo título — ✅ MERGEADO
_PR #4 mergeado a `main` y desplegado en Vercel._
- Se reemplaza el fondo del hero por un **relieve de concreto generado por
  código**: empaquetado tipo Mondrian de bloques terracota a distintas alturas,
  vista **frontal ortográfica** (sin isometría ni 45°), inspirado en una obra de
  relieve de Tom.
- **Reacciona a hover y scroll, nunca en reposo:** al pasar el cursor los bloques
  cercanos **se elevan** (la cara superior sube y crece una pared lateral, se
  paran sobre la superficie); al hacer scroll el campo se **pliega**. En reposo
  todo vuelve a su altura base y el bucle de animación se apaga solo. Respeta
  `prefers-reduced-motion`.
- Orden de capas **fijo** (painter's order, los de abajo delante) para que no
  haya parpadeo al subir/bajar.
- Paleta **pastel, mate y de bajo contraste** (coral-terracota), afinada contra
  la referencia; el color lo carga el relieve, no el brillo. Copy sobre un
  **scrim** a la izquierda para legibilidad.
- Se retira el placeholder de pieza del hero (el relieve pasa a ser el visual).
- **Título:** «Concrete you want to touch.» → **«Concrete, Geometry, and Light»**.
- Todo inline en `index.html` (regla #5): CSS + JS, sin librerías.

_Cierre de sesión: PR #4 mergeado. El fondo del hero (relieve reactivo) y el
título quedan en `main`. Fin de la sesión del hero._

### 2026-07-22 — Color apagado en las piezas (primer pase) — ✅ MERGEADO
_PR #3 mergeado a `main` y desplegado en Vercel._
- Objetivo: quitar el look "super gris". Referencia: esculturas brutalistas de
  rejilla con colores **apagados pero presentes** (mostaza, terracota, salvia,
  azul polvo, granate).
- Se amplía la paleta con una familia de tonos apagados: `--ochre #C79A45`,
  `--sage #93A085`, `--dusty #869BA0`, `--maroon #7C3A31`, `--clay #C36A47`.
  `--rust` se mantiene. El concreto/papel/carbón siguen igual: el color lo
  cargan **las piezas**, el fondo se queda callado.
- Nuevo sistema en los bloques placeholder:
  - Variantes de tono (`.tone-ochre/sage/dusty/clay/maroon/rust`) con etiquetas
    que ajustan su color según el tono sea claro u oscuro.
  - Marcas geométricas planas (`.mark` → `circle`, `block`, `bars`, `bar`) con
    utilidades de color (`.fill-*`), que evocan las composiciones de las
    esculturas de referencia.
- Asignación por pieza: Hero = ocre + círculo óxido · BLOCK NO. 4 = ocre +
  bloque granate · TOWER 01 = azul polvo + barras granate · VESSEL = clay +
  bloque crema · TWO FORMS = salvia + bloque clay/barra granate · SLAB = granate
  + barras ocre.
- Sin tocar estructura, tipografía ni JS. Sigue siendo un solo `index.html`.
- Primer pase deliberadamente "a criterio"; Adrián ajusta tonos/asignaciones.

### 2026-07-22 — PR #1 · Sitio inicial + reglas del proyecto — ✅ MERGEADO
_Estado: mergeado a `main` y desplegado en Vercel._
- Se construye `index.html`: sitio de demostración para Tom Beton, escultor
  brutalista de concreto. Un solo archivo autocontenido (CSS + JS inline),
  Google Fonts como única dependencia externa. Mobile-first.
- Paleta cálida de concreto: concreto `#ACA599`, papel crudo `#EAE4D7`,
  carbón `#4A4640`, tinta `#17140E`, óxido `#B5482A` como único acento (uso
  mínimo).
- Tipografía: Archivo (titulares/cuerpo) + Space Mono (metadata y eyebrows).
- Estructura brutalista: rejilla visible, sombras duras desplazadas, bloques
  placeholder intencionales para las piezas (fáciles de reemplazar por fotos
  reales), divisiones con líneas duras.
- Secciones: Hero, The Work (catálogo de 5 piezas con ficha técnica en mono),
  The Workshop (proceso en 4 pasos), The Maker, Acquire / Footer (captura de
  email demo sin backend + enlaces a Etsy, Instagram, TikTok).
- Comportamiento: scroll suave desde nav y botones, reveal sutil al hacer
  scroll, captura de email demo con mensaje en línea.
- Se crea `progreso.md` con las reglas de trabajo y este registro.

_Cierre de sesión: PR #1 mergeado. Fin de la primera sesión de trabajo._
