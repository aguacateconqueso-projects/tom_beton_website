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
