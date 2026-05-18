# Dia 04 — CSS Flexbox
**Fase:** 01 - Fundamentos Web
**Semana:** 02 - CSS Moderno
**Fecha:** 2026-05-17
**Estado:** 🟡 En curso

---

## Objetivo del Dia

Flexbox resolvio el problema de alineacion en CSS que durante años obligo a usar
hacks con floats y tablas. Al terminar este dia puedes centrar cualquier elemento,
distribuir espacio entre items y construir layouts de una dimension (fila o columna)
de forma limpia y predecible.

---

## Concepto 1: El Modelo Mental de Flexbox

Flexbox opera en dos niveles:

```
┌─────────────────────────────────────────┐
│  FLEX CONTAINER  (display: flex)        │
│  ┌────────┐  ┌────────┐  ┌────────┐    │
│  │ item 1 │  │ item 2 │  │ item 3 │    │
│  └────────┘  └────────┘  └────────┘    │
└─────────────────────────────────────────┘
```

- **Container** → el elemento padre donde aplicas `display: flex`
- **Items** → los hijos directos del container

Las propiedades se dividen entre las que van en el container y las que van
en cada item. Confundirlas es el error mas comun en Flexbox.

---

## Concepto 2: Propiedades del Container

### `display: flex`

```css
.container {
  display: flex; /* activa flexbox en los hijos directos */
}
```

### `flex-direction` — el eje principal

```css
.container {
  flex-direction: row;            /* → izquierda a derecha (default) */
  flex-direction: row-reverse;    /* ← derecha a izquierda */
  flex-direction: column;         /* ↓ arriba a abajo */
  flex-direction: column-reverse; /* ↑ abajo a arriba */
}
```

### `justify-content` — alineacion en el eje principal

```css
.container {
  justify-content: flex-start;    /* items al inicio (default) */
  justify-content: flex-end;      /* items al final */
  justify-content: center;        /* items centrados */
  justify-content: space-between; /* espacios iguales entre items, sin margen en bordes */
  justify-content: space-around;  /* espacio igual alrededor de cada item */
  justify-content: space-evenly;  /* espacio exactamente igual entre todos */
}
```

### `align-items` — alineacion en el eje cruzado

```css
.container {
  align-items: stretch;     /* items se estiran para llenar el alto (default) */
  align-items: flex-start;  /* items al inicio del eje cruzado */
  align-items: flex-end;    /* items al final del eje cruzado */
  align-items: center;      /* items centrados verticalmente */
  align-items: baseline;    /* items alineados por su linea base de texto */
}
```

### `flex-wrap` — control de desbordamiento

```css
.container {
  flex-wrap: nowrap;       /* todos en una linea, puede desbordar (default) */
  flex-wrap: wrap;         /* items saltan a siguiente linea si no caben */
  flex-wrap: wrap-reverse; /* saltan pero en direccion inversa */
}
```

### `gap` — espacio entre items

```css
.container {
  gap: 16px;         /* mismo espacio entre filas y columnas */
  gap: 16px 24px;    /* 16px entre filas, 24px entre columnas */
  row-gap: 16px;
  column-gap: 24px;
}
```

> Usar `gap` en lugar de `margin` entre items flex — es mas limpio y no
> genera margen extra en el primer o ultimo item.

---

## Concepto 3: Propiedades de los Items

### `flex` — shorthand esencial

```css
/* flex: flex-grow  flex-shrink  flex-basis */
.item { flex: 1; }      /* equivale a flex: 1 1 0 — crece para llenar espacio */
.item { flex: auto; }   /* equivale a flex: 1 1 auto */
.item { flex: none; }   /* equivale a flex: 0 0 auto — tamano fijo */

/* Distribucion proporcional */
.item-doble  { flex: 2; } /* ocupa el doble de espacio que .item-simple */
.item-simple { flex: 1; }
```

### `align-self` — override individual de align-items

```css
.item-especial {
  align-self: center;    /* este item se centra aunque los demas no */
  align-self: flex-end;
  align-self: flex-start;
  align-self: stretch;
}
```

### `order` — orden visual sin tocar el HTML

```css
.item { order: 0; }    /* default para todos */
.primero { order: -1; } /* aparece antes que todos */
.ultimo  { order: 1; }  /* aparece despues que todos */
```

---

## Concepto 4: El Eje Principal vs el Eje Cruzado

Este es el concepto que mas confunde al principio:

```
flex-direction: row (default)
──────────────────────────────→  eje principal  → justify-content
│
↓  eje cruzado  → align-items

flex-direction: column
│
↓  eje principal  → justify-content
──────────────────────────────→  eje cruzado  → align-items
```

**Regla practica:** `justify-content` siempre mueve en la direccion del flex,
`align-items` siempre mueve en la direccion perpendicular.

---

## Concepto 5: Patrones Practicos

### Centrado perfecto

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
```

### Navbar: logo izquierda, links derecha

```css
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
}

nav ul {
  display: flex;
  list-style: none;
  gap: 24px;
}
```

### Cards en fila que se adaptan

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

.card {
  flex: 1;
  min-width: 280px; /* evita que se achiquen demasiado */
}
```

### Sidebar + contenido principal

```css
.layout {
  display: flex;
  gap: 24px;
}

.sidebar  { flex: 0 0 280px; } /* ancho fijo */
.contenido { flex: 1; }        /* ocupa el resto */
```

---

## Ejercicio del Dia

Crea `styles.css` en tu carpeta `portafolio/` y aplica Flexbox para
darle estructura visual al `index.html` existente.

### Lo que debes implementar

**1. Reset y variables base**
```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --color-primario: #FF653F;  /* tu color de tema */
  --color-texto: #1a1a1a;
  --color-fondo: #f9f9f9;
}
```

**2. Header** — nombre a la izquierda, nav a la derecha, verticalmente centrados

**3. Nav links** — en fila horizontal con espacio entre ellos

**4. Seccion de proyectos** — los articles en fila, con wrap y gap

**5. Footer** — contenido centrado horizontal y verticalmente

### Requisitos tecnicos

- `gap` para espaciar items (no `margin` entre flex items)
- `flex-wrap: wrap` en la seccion de proyectos
- Sin `float` en ningun lugar
- Sin `position: absolute` para centrar
- Los articles de proyectos deben tener un ancho minimo con `min-width`

---

## Entrega

Pega el contenido completo de tu `styles.css` en el chat.

---

## Recursos

- CSS-Tricks Flexbox Guide: https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- Flexbox Froggy (juego): https://flexboxfroggy.com/
- MDN Flexbox: https://developer.mozilla.org/es/docs/Web/CSS/CSS_flexible_box_layout
