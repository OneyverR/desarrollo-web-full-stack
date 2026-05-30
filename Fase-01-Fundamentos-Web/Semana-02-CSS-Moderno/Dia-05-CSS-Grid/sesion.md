# Sesion Dia 05 — CSS Grid
**Fecha:** 2026-05-30
**Estado:** ✅ Aprobado — listo para Dia 06

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
}
header{
    grid-area: header;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 30px;
}
main{
    grid-area: main;
}
nav ul{
    display: flex;
    list-style: none;
    gap: 24px;
}
#presentacion-personal{
    padding: 30px;
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 24px;
    align-items: center;
}
#proyectos{
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px,1fr));
    gap: 24px;
    padding: 30px;
}
footer{
    grid-area: footer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 30px;
}
```

---

## Feedback del Coach

### Puntos positivos

1. `body` con `display: grid` + `grid-template-areas` correcto
2. `grid-template-rows: auto 1fr auto` — header y footer fijos, main ocupa el resto
3. `min-height: 100vh` presente
4. `header` combina `grid-area` + Flexbox interno — patron correcto, Grid y Flex coexistiendo
5. `main` y `footer` con `grid-area` asignado
6. `nav ul` Flexbox del Dia 04 conservado intacto
7. `#proyectos` con `repeat(auto-fill, minmax(280px, 1fr))` — implementacion perfecta
8. `#presentacion-personal` con grid 2 columnas — el bonus implementado

### Puntos a corregir

**Codigo muerto — `#proyectos article` tiene propiedades Flexbox huerfanas:**

```css
/* Como esta — flex:1 y min-width no hacen nada en un contexto Grid */
#proyectos article {
    flex: 1;        /* ← ignorado: el padre es grid, no flex */
    min-width: 280px; /* ← redundante: minmax(280px,1fr) ya lo controla */
}
```

La leccion indicaba explicitamente quitar estas propiedades al cambiar a Grid.
`flex` solo funciona cuando el padre tiene `display: flex`. El navegador
simplemente las ignora, pero codigo que no hace nada no debe existir.

```css
/* Como debe ser — la regla entera puede eliminarse */
/* #proyectos article ya no necesita reglas propias:
   el grid-template-columns del padre controla el tamano */
```

### Conceptos a reforzar

- Cuando el contexto cambia de Flex a Grid, las propiedades `flex-*` quedan muertas
- `minmax(min, max)` en el grid container ya define el tamano de los items — no hace falta repetirlo en el item
- Codigo que no hace nada es deuda tecnica: confunde a quien lo lee despues


---

## Dudas de la Sesion

No entendi el ajuste realizado a #proyectos. La linea 45. Explicame mas a detalle de como funciona el repeat(auto-fill, minmax(280px, 1fr))


---

## Resultado Final

- [x] body con display:grid y grid-template-areas
- [x] header, main, footer con grid-area asignado
- [x] min-height: 100vh en el body grid
- [x] #proyectos con repeat(auto-fill, minmax(280px, 1fr))
- [x] Flexbox del Dia 04 conservado donde corresponde
- [x] #proyectos article eliminado — codigo muerto removido

**Calificacion:** ✅ 10/10 — Dia completado. Avanzar a Dia 06.
