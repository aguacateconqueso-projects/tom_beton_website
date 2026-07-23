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
- **Secciones del sitio:** Hero (CTA único «Acquire») · **Acquire (carrusel
  infinito de 5 piezas)** · Sign-up / Footer.
  (Workshop / Maker siguen retirados; «The Work» volvió reconvertida en
  **Acquire**, ahora como carrusel horizontal en loop.)

---

## Registro de sesiones

Cada entrada = un PR. Se anota de arriba (más reciente) hacia abajo.

### 2026-07-23 — Acquire como carrusel infinito de piezas — ✅ MERGEADO (PR #15)
_Rama `claude/progreso-acquire-section-o8m6ym` (reiniciada sobre `main` tras
mergear el PR #14)._
La sección **Acquire** deja de ser una grilla estática y pasa a un **carrusel
horizontal de productos en loop eterno**, inspirado en un video de referencia de
Adrián (e-commerce brutalista de sneakers). Se mantiene en un solo `index.html`,
vanilla, sin librerías.
- **Tarjetas de producto** (`.acq-card`): "imagen" = el visual `.piece-ph` de
  cada pieza (se reutiliza tal cual, con sus `mark`/tono/etiqueta), y debajo una
  fila con **código** (`PIECE 0X`), **nombre** y **precio**. Separadores crema
  entre tarjetas (look de rejilla brutalista).
- **Movimiento (opción elegida, sin secuestrar el scroll):** el track **deriva
  solo hacia la izquierda en loop infinito** (se clonan los ítems hasta llenar
  ≥2× el viewport y se envuelve por el ancho de un set) y **toma prestada la
  velocidad del scroll de la página** como empujón suave — nunca hace
  `preventDefault`, así que el scroll fuerte sigue bajando la página con
  normalidad. Hover pausa la deriva para poder leer.
- **Controles:** flechas **‹ ›** (impulso ~1 tarjeta, con fricción), **arrastre**
  con el puntero (con momentum al soltar) y enlace **VIEW ALL →**. Etiqueta de
  categoría «MADE TO ORDER · SMALL BATCHES» a la izquierda (oculta en móvil).
- **Accesibilidad:** respeta `prefers-reduced-motion` → sin auto-loop; la tira se
  vuelve un **scroll horizontal nativo** con `scroll-snap` y las flechas hacen
  `scrollBy`. Botones con `:focus-visible`. Cada tarjeta con `aria-label`
  (nombre + precio).
- Descartado el *scroll-jacking* fiel al video (fijar la sección y forzar el
  avance): frágil entre dispositivos y hostil para una web de venta. Se logró la
  misma sensación sin atrapar la página.
- El CSS/markup del catálogo estático (`.catalogue`/`.work-item`/`.spec-*`) queda
  inerte de nuevo, disponible para una futura ficha de producto.

_Cierre de sesión: la sección **Acquire** quedó como carrusel horizontal en loop
eterno (deriva sola + reacciona al scroll sin secuestrarlo, flechas y arrastre),
mergeado a `main` en el PR #15 y validado por Adrián. El sitio queda: **Hero
(CTA Acquire) · Acquire (carrusel de piezas) · Sign-up / Footer**. Fin de la
sesión._

### 2026-07-23 — Vuelve el catálogo, ahora como «Acquire» — ✅ MERGEADO (PR #14)
_Rama `claude/progreso-acquire-section-o8m6ym`._
Se **recupera la sección The Work** (catálogo de 5 piezas con ficha técnica) que
se había retirado en el PR #12, y **renace como la sección `#acquire`**: el sitio
deja de tener solo un formulario de captura y vuelve a **mostrar las piezas**.
- **HTML del catálogo restaurado** desde el commit `33bb588` (5 `.work-item`:
  BLOCK NO. 4, TOWER 01, VESSEL, TWO FORMS, SLAB), ahora dentro de
  `<section id="acquire">` con eyebrow **ACQUIRE** (antes «THE WORK»).
- **Nav y CTA del hero ya apuntaban a `#acquire`**: ahora ese destino aterriza en
  el catálogo, no en el formulario. Flujo: Hero → **Acquire (piezas)** → captura
  de email + Etsy/redes + footer.
- **El signup + footer** (que antes era `#acquire`) pasa a **`#notify`** para no
  duplicar id; conserva su formulario y enlaces, sin el eyebrow «ACQUIRE»
  repetido. Queda como cierre debajo del catálogo.
- **CSS reusado tal cual** (`.catalogue`/`.work-item`/`.piece-ph`/`.mark`/
  `.spec-*`): estaba inerte y se reactiva sin cambios. Solo se renombró el
  selector de fondo `#work` → `#acquire` y el del signup a `#notify`. Sigue
  siendo un solo `index.html` (regla #5).

### 2026-07-23 — Botones brutalistas 3D + web enfocada en vender — ✅ MERGEADO (PR #12)
_Rama `claude/web-visual-buttons-redesign-rt5d0c`._
La web pasa a tener un solo objetivo: **VENDER**. Menos ruido, un CTA claro y un
sistema de botones nuevo.
- **Botones nuevos = bloque brutalista 3D que crece.** Cada `.btn` es un bloque
  con cara superior de color y, al hover/focus, se **eleva** mientras una
  **pared lateral se extruye** por debajo (mismo mecanismo que el relieve del
  hero: `--lift` sube la cara y `::before` crece la pared; `::after` es la
  sombra que se profundiza). `:active` baja el bloque. Respeta
  `prefers-reduced-motion` (sin movimiento).
- **Color de paleta aleatorio por botón.** Variantes `.v-rust/clay/maroon/sage/
  purple/tan` (cara + pared más oscura + color de texto). JS asigna una variante
  **al azar** a todo `.btn` que no traiga una fija. Fijos: hero **Acquire =
  sage**, logo **Tom Beton = purple** (colores distintos del naranja del fondo).
- **Un solo CTA en el hero.** Se elimina «See the work»; queda **un botón
  «Acquire»** (la idea es vender, no pasear).
- **«Tom Beton» (arriba) ahora es botón** con la misma animación 3D (púrpura).
- **Nav podado:** se eliminan los enlaces **Work, Workshop y Maker**; en el nav
  **solo queda Acquire**, también como botón 3D.
- **Se eliminan las secciones Work, Workshop y Maker.** Lo que era **The Work**
  se convertirá en la **tienda** más adelante (concepto aparte de Adrián); no se
  arma todavía. El sitio queda: **Hero (CTA Acquire) · Acquire/Footer**.
- CSS de esas secciones queda inerte (sin HTML que la use) a la espera del
  rediseño de tienda; el botón «Notify me» del footer también adopta el formato
  3D con color aleatorio. Sigue siendo un solo `index.html` (regla #5).

### 2026-07-23 — Relieve del hero recoloreado a naranja #FF521B — ✅ MERGEADO (PR #10)
_Rama `claude/hero-section-redesign-kstx80`._
- **El relieve/animación se mantiene idéntico** (mismo empaquetado Mondrian,
  mismo hover/scroll, mismo scrim). **Solo cambia el color** a la familia naranja
  `#FF521B`:
  - Caras: `--t0 #EE4614` · `--t1 #F84C18` · `--t2 #FF521B` · `--t3 #FF5D2A` ·
    `--t4 #FF6A3B` (bajo contraste, casi uniforme, como antes).
  - Paredes: `--wall-lit #D8410F` · `--wall-dark #BE380B`. Grout `#9A2A07`.
- Nota: en un paso anterior (PR #9, mergeado) se había **eliminado** el relieve
  por un malentendido; se revirtió y se restauró completo antes de recolorear.

_Cierre de sesión: hero con StackSans, headline «Handmade / Brutalist Designs»,
sitio en tema oscuro con texto crema, y relieve del hero recoloreado a naranja
`#FF521B` (animación intacta). Todo mergeado a `main`. Fin de la sesión._

### 2026-07-23 — Tema oscuro + headline nuevo — ✅ MERGEADO (PR #8)
_Rama `claude/hero-section-redesign-kstx80`._
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
