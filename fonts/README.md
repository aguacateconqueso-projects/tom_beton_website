# fonts/

Fuente de titulares del sitio: **StackSans**.

Sube aquí el archivo con el nombre exacto:

    fonts/StackSans.otf

El `@font-face` en `index.html` ya la referencia como
`url('fonts/StackSans.otf') format('opentype')`. Mientras el archivo no
exista, los titulares caen a **Archivo** (fallback) sin romper nada.

> Si prefieres mantener el sitio en un solo archivo (regla #5), en vez de
> dejar el `.otf` suelto podemos incrustarlo como data URI base64 dentro
> del `@font-face`. Dime y lo cambio.
