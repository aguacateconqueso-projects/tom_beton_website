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

### 2026-07-22 — Hero: relieve 3D de terracota (EXPLORACIÓN, sin mergear) — 🔬 EN CURSO
_Rama `claude/session-gwqrzq`. Prototipo en artifact, NO tocamos `index.html`._

**La idea (de Adrián):** el fondo del hero (solo el hero; las demás secciones
llevarán otro fondo) debe verse como la foto de close-up de una obra de Tom —
una pared de bloques de **terracota** tipo Lego/maqueta. Los bloques **suben y
bajan** para dar un efecto "inception". Mismo color, copiar el patrón.

**Cómo se está construyendo:** CSS 3D puro + JS mínimo (sin librerías, cabe en
el `index.html` de archivo único). Cada bloque es una caja 3D real; la altura se
anima solo con `transform` (`scaleZ`) → va por GPU, sin reflow. El motor de
animación se apaga solo al asentarse y solo revive con input.

**Artifact interactivo (prototipo, privado):**
https://claude.ai/code/artifact/28d330ac-daa2-4eb7-b95a-1e1caef50abb
Archivo de trabajo: `scratchpad/relief_proto.html` (no está en el repo).

**Iteraciones y feedback de Adrián:**
- v1: vista isométrica (diagonal 45°) con ondas perpetuas. ❌ Rechazada.
- v2: vista cenital/frontal con patrón de mesetas/escalones; movimiento SÓLIDO
  (quieto en reposo, solo reacciona a hover + scroll). Mejor, pero…
- **DIRECCIÓN FINAL PEDIDA (pendiente de lograr):** ⚠️ **sin ángulo de cámara /
  sin perspectiva inclinada.** Quiere la retícula **totalmente de frente** (como
  mirar una pared de baldosas de plano). El **3D debe nacer ÚNICAMENTE del
  movimiento de los bloques** (empujándose hacia el espectador), NO de una
  cámara en perspectiva/diagonal. En reposo debe verse **plano (2D)**.
- v3 (última, sin validar por Adrián): `.world` sin `rotateX`, de frente;
  `perspective` solo para que el bloque "salga" hacia ti al elevarse y revele
  sus lados; reposo plano (`--s ≈ 0.03`); hover levanta en gaussiana, scroll
  levanta en ola (nunca por debajo del plano). Falta que Adrián lo apruebe.

**Pendiente para la próxima sesión:**
1. Validar v3 (de frente, 3D solo por movimiento) con Adrián y ajustar.
2. Al aprobar: portar al hero real en `index.html` (tipografías reales Archivo +
   Space Mono, responsive, tope de bloques en móvil por rendimiento), abrir PR a
   `main` siguiendo la regla #1.

### 2026-07-22 — Color apagado en las piezas — ⚠️ MERGEADO A MAIN, A REVERTIR (PR #3)
_**OJO / pendiente urgente:** este cambio fue un **malentendido** — los cuadros
de color son placeholders para las FOTOS reales de las obras, NO para colorear;
Adrián pidió colorizar backgrounds/botones, no las piezas. Se intentó **cerrar
sin mergear**, pero el **PR #3 terminó MERGEADO a `main`** (commit
`Merge pull request #3` → `1f82bea`). Es decir: **los placeholders con color
están AHORA MISMO en vivo en Vercel.**_

**Pendiente para la próxima sesión (antes que nada):** revertir el PR #3 en
`main` (rama nueva → PR de revert → merge) para devolver los placeholders a
neutro, o rehacer el color como Adrián realmente lo quiere (backgrounds/botones,
no las piezas). Hasta entonces `main` tiene las piezas coloreadas.

- Objetivo original (equivocado): quitar el look "super gris" coloreando las
  piezas. Referencia mal interpretada: esculturas brutalistas de rejilla con
  colores **apagados pero presentes** (mostaza, terracota, salvia, azul polvo,
  granate).
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
