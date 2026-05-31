# Sesion Dia 06 — Responsive Design y Mobile First
**Fecha:** 2026-05-30
**Estado:** ✅ Aprobado — listo para Dia 07

---

## Codigo Entregado

```css
*{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
:root{
    --color-texto: #0D530E;
    --color-fondo: #F9F9F9;
    --color-footer: #C4E2F5;
}
body{
    background-color: var(--color-fondo);
    color: var(--color-texto);
    display: grid;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header"
        "main"
        "footer";
    min-height: 100vh;
    font-size: clamp(1rem, 1.2vw, 1.125rem);
}
/*Dimensiones Mobile*/
header{
    grid-area: header;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
    padding: 1rem;
}
main{
    grid-area: main;
}
h1 {
    font-size: clamp(1.5rem, 4vw, 2.5rem);
}
h2 {
    font-size: clamp(1.2rem, 3vw, 1.8rem);
}
nav ul{
    display: flex;
    flex-direction: column;
    list-style: none;
    gap: 8px;
}
#presentacion-personal{
    padding: 16px;
    display: grid;
    grid-template-columns: 1fr;
    gap: 24px;
    align-items: center;
}
#proyectos{
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px,1fr));
    gap: 18px;
    padding: 16px;
}
img{
    max-width: 100%;
    height: auto;
    display: block;
}
footer{
    grid-area: footer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 30px;
    background-color: var(--color-footer);
}
@media (min-width: 768px){
    body{
        padding: 24px;
    }
    header{
        flex-direction: row;
        padding: 0 30px;
        justify-content: space-between;
    }
    nav ul{
        flex-direction: row;
        gap: 24px;
    }
    #presentacion-personal{
        grid-template-columns: 200px 1fr;
        padding: 30px;
    }
    #proyectos {
        padding: 30px;
    }
}

@media (min-width: 1024px){
    body{
        max-width: 1280px;
        margin: 0 auto;
    }
}
```

---

## Feedback del Coach

### Puntos positivos

1. Enfoque Mobile First correcto — CSS base sin media queries funciona en movil
2. `header` con `flex-direction: column` en movil y `row` en tablet — patron correcto
3. `nav ul` con `flex-direction: column` en movil y `row` en tablet
4. `#presentacion-personal` con `1fr` en movil y `200px 1fr` en tablet
5. `img` con `max-width: 100%`, `height: auto`, `display: block` — perfecto
6. `@media (min-width: 768px)` y `@media (min-width: 1024px)` presentes
7. `max-width: 1280px` y `margin: 0 auto` en desktop — contenido centrado
8. Nueva variable `--color-footer` agregada y aplicada — iniciativa propia
9. `clamp()` presente en `h1` — concepto captado

### Puntos a corregir

**BUG 1 — `clamp()` en h1 no es fluido: el valor del medio debe ser `vw`, no `rem`:**

```css
/* Como esta (MAL) — 2rem es fijo, nunca cambia con el viewport */
h1 { font-size: clamp(0.5rem, 2rem, 6rem); }
/* clamp necesita un valor vw en el medio para ser fluido */

/* Como debe ser */
h1 { font-size: clamp(1.5rem, 4vw, 2.5rem); }
/*                      ↑         ↑       ↑
                     minimo   fluido   maximo
                     (24px)  (crece) (40px)  */
```

La funcion clamp solo tiene sentido cuando el valor del medio escala con el viewport.
Con `2rem` fijo en el medio, siempre sera `2rem` — el min y max nunca actuan.

Adicionalmente, `0.5rem` (8px) como minimo es ilegible. El minimo de un `<h1>`
nunca deberia bajar de `1.5rem`.

---

**BUG 2 — `clamp()` en `body` dentro de media queries es incorrecto:**

```css
/* Como esta (MAL) — doble problema */
@media(min-width: 768px){
  body { font-size: clamp(0.5rem, 1.1rem, 6rem); } /* 1.1rem es fijo, nunca fluido */
}
@media(min-width: 1024px){
  body { font-size: clamp(0.5rem, 1.2rem, 4rem); } /* mismo error */
}
```

`clamp()` existe precisamente para eliminar la necesidad de media queries en
tipografia. Si usas clamp correctamente, defines el font-size UNA sola vez
en el CSS base y funciona para todos los tamaños:

```css
/* Como debe ser — una sola regla, fuera de media queries */
body {
  font-size: clamp(1rem, 1.2vw, 1.125rem);
}
```

---

**BUG 3 — `justify-content: space-between` en header mobile no hace nada:**

```css
/* En movil, el header es flex-direction: column sin altura definida */
header {
  flex-direction: column;
  justify-content: space-between; /* ← sin height fijo, no tiene efecto */
}
```

`space-between` en columna solo actua si el contenedor tiene mas alto del
que necesita el contenido. Como el header tiene `height: auto`, los elementos
se apilan uno tras otro sin importar `justify-content`. Quitar esa propiedad
del bloque base — en columna solo necesitas `gap`.

---

**ESTILO — espacio faltante en `@media`:**

```css
/* Como esta */
@media(min-width: 768px){ ... }

/* Convencion estandar */
@media (min-width: 768px) { ... }
```

### Conceptos a reforzar

- `clamp(min, PREFERIDO, max)` — el valor del medio DEBE ser `vw` para que sea fluido
- `clamp()` reemplaza las media queries para tipografia, no se usa dentro de ellas
- `justify-content` en columna solo funciona si el contenedor tiene altura definida


---

## Dudas de la Sesion

<!-- Registrar aqui las preguntas que surgieron durante la practica -->


---

## Resultado Final

**Segunda revision:**

- [x] CSS base correcto para movil
- [x] Header apilado en movil, horizontal en tablet
- [x] Nav links columna en movil, fila en tablet
- [x] @media con espacios correctos
- [x] justify-content: space-between eliminado del header mobile
- [x] clamp() en body con vw en el medio — concepto corregido
- [x] clamp() fuera de media queries
- [x] clamp() en body con valores correctos: clamp(1rem, 1.2vw, 1.125rem)
- [x] h1 y h2 con clamp() y vw correctos
- [x] padding eliminado de img
- [x] justify-content: space-between movido al breakpoint tablet donde tiene efecto real

**Calificacion:** ✅ 10/10 — Dia completado. Avanzar a Dia 07.
