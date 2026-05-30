# Sesion Dia 04 — CSS Flexbox
**Fecha:** 2026-05-17
**Estado:** ✅ Aprobado — listo para Dia 05

---

## Codigo Entregado

```css
*{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
:root{
    --color-primario: #FF653F;
    --color-texto: #1a1a1a;
    --color-fondo: #F9F9F9;
}

.header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 24px;

}
nav ul{
    display: flex;
    list-style: none;
    gap: 24px;
}
#proyectos{
    display: flex;
    flex-wrap: wrap;
    gap: 24px;
}
#proyecto1{
    flex: 1;

}
#proyecto2{
    flex: 1;
}

footer{
    display: flex;
    align-items: center;
    justify-content: center;
}
```

---

## Feedback del Coach

### Puntos positivos

1. Reset correcto — `box-sizing`, `margin: 0`, `padding: 0`
2. Variables CSS en `:root` con los 3 colores definidos
3. `justify-content: space-between` + `align-items: center` en el header — logica correcta
4. `nav ul` con `display: flex` + `list-style: none` + `gap` — correcto
5. `#proyectos` con `flex-wrap: wrap` y `gap` — correcto
6. Footer con `justify-content: center` + `align-items: center` — correcto
7. Sin `float` ni `position: absolute`

### Puntos a corregir

**BUG CRITICO — selector `.header` no existe en el HTML (linea 21):**

`.header` busca un elemento con `class="header"`. Tu HTML usa la etiqueta
semantica `<header>` sin clase. El CSS del header no se aplica en absoluto.

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
}
header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 30px;
}
nav ul{
    display: flex;
    list-style: none;
    gap: 24px;
}
#presentacion-personal{
    padding: 30px;
}
#proyectos{
    display: flex;
    flex-wrap: wrap;
    gap: 24px;
    padding: 30px;
}
#proyectos article{
    flex: 1;
    min-width: 280px;
}
footer{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 30px;
}
```

---

**ESCALABILIDAD — `#proyecto1` y `#proyecto2` como reglas separadas:**

Si agregas un tercer proyecto necesitas una tercera regla. No escala.
El patron correcto es seleccionar todos los articles del contenedor:

```css
/* Como esta (MAL) — repeticion, no escala */
#proyecto1 { flex: 1; }
#proyecto2 { flex: 1; }

/* Como debe ser — aplica a todos los articles automaticamente */
#proyectos article {
  flex: 1;
  min-width: 280px;
}
```

---

**REQUISITO FALTANTE — `min-width` en los articles:**

Era un requisito explicito del ejercicio. Sin `min-width` los articles
se achican indefinidamente en pantallas pequenas y `flex-wrap` no actua
hasta que el contenido desborda, no cuando el elemento queda ilegible.

---

**MEJORA — variables CSS definidas pero no usadas:**

Definiste `--color-texto` y `--color-fondo` pero no las aplicas en ningun lado.
Las variables tienen valor cuando las consumes:

```css
body {
  color: var(--color-texto);
  background-color: var(--color-fondo);
  font-family: sans-serif;
}
```

### Conceptos a reforzar

- `.clase` selecciona `class="clase"` — `etiqueta` selecciona la etiqueta HTML
- Los selectores de ID son para un elemento unico; para grupos usar clase o descendiente
- Definir una variable CSS no hace nada hasta que se usa con `var()`


---

## Dudas de la Sesion

<!-- Registrar aqui las preguntas que surgieron durante la practica -->


---

## Resultado Final

**Revision final:**

- [x] Reset correcto
- [x] Variables en :root consumidas en body con var()
- [x] body con background-color y color aplicados
- [x] header con selector de etiqueta correcto
- [x] Nav links en fila con gap
- [x] #proyectos article escalable con flex:1 y min-width:280px
- [x] Sin display:flex innecesario en los articles
- [x] padding: 30px sin valores redundantes
- [x] Footer centrado
- [x] #presentacion-personal con padding (bonus)

Nota: --color-primario fue removido del :root. Agregarlo de vuelta
cuando se empiece a usar en botones, links y acentos visuales.

**Calificacion:** ✅ 10/10 — Dia completado. Avanzar a Dia 05.
