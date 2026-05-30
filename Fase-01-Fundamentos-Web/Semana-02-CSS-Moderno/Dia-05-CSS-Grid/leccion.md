# Dia 05 — CSS Grid
**Fase:** 01 - Fundamentos Web
**Semana:** 02 - CSS Moderno
**Fecha:** 2026-05-30
**Estado:** 🟡 En curso

---

## Objetivo del Dia

Flexbox controla una dimension: fila O columna. Grid controla dos dimensiones
a la vez: filas Y columnas simultaneamente. Al terminar este dia puedes construir
layouts de pagina completos — headers, sidebars, areas de contenido, footers —
en pocas lineas de CSS, sin hacks ni calculos manuales.

---

## Concepto 1: El Modelo Mental de Grid

```
┌──────────┬──────────┬──────────┐  ← fila 1
│  item 1  │  item 2  │  item 3  │
├──────────┼──────────┼──────────┤  ← fila 2
│  item 4  │  item 5  │  item 6  │
├──────────┴──────────┴──────────┤  ← fila 3
│         item 7 (span 3)        │
└────────────────────────────────┘
```

- **Grid Container** → el padre con `display: grid`
- **Grid Items** → los hijos directos
- **Grid Lines** → las lineas que dividen filas y columnas (numeradas desde 1)
- **Grid Track** → el espacio entre dos lineas (una fila o columna)
- **Grid Cell** → la interseccion de una fila y una columna
- **Grid Area** → uno o mas cells ocupados por un item

---

## Concepto 2: Definir el Grid

### `grid-template-columns` y `grid-template-rows`

```css
.container {
  display: grid;

  /* 3 columnas de ancho fijo */
  grid-template-columns: 200px 200px 200px;

  /* 3 columnas iguales — la unidad fr (fraccion del espacio disponible) */
  grid-template-columns: 1fr 1fr 1fr;

  /* Shorthand con repeat() */
  grid-template-columns: repeat(3, 1fr);

  /* Columnas mixtas */
  grid-template-columns: 280px 1fr;       /* sidebar fija + contenido flexible */
  grid-template-columns: 1fr 2fr 1fr;     /* la del centro es el doble */

  /* Filas */
  grid-template-rows: 80px 1fr 60px;      /* header fijo, main flexible, footer fijo */
}
```

### La unidad `fr` — fraccion del espacio libre

```css
/* El espacio disponible se divide proporcionalmente */
grid-template-columns: 1fr 2fr 1fr;
/* columna 1: 25% | columna 2: 50% | columna 3: 25% */
```

### `gap` en Grid

```css
.container {
  gap: 24px;           /* mismo gap en filas y columnas */
  gap: 16px 24px;      /* 16px entre filas, 24px entre columnas */
  row-gap: 16px;
  column-gap: 24px;
}
```

---

## Concepto 3: Posicionar Items en el Grid

### Por numero de linea

Las lineas del grid se numeran desde 1. Tambien puedes usar numeros negativos
desde el final (-1 es la ultima linea).

```css
.item {
  grid-column: 1 / 3;   /* desde linea 1 hasta linea 3 (ocupa 2 columnas) */
  grid-row: 1 / 2;      /* desde linea 1 hasta linea 2 (ocupa 1 fila) */
}

/* Con span — mas legible */
.item {
  grid-column: 1 / span 2;  /* empieza en linea 1, ocupa 2 columnas */
  grid-row: span 2;          /* ocupa 2 filas desde donde este */
}

/* Ocupar todo el ancho */
.item {
  grid-column: 1 / -1;  /* desde la primera hasta la ultima linea */
}
```

---

## Concepto 4: `grid-template-areas` — El Patron mas Potente

Permite nombrar zonas del grid con texto, haciendo el layout completamente
legible:

```css
.container {
  display: grid;
  grid-template-columns: 280px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
}

/* Asignar cada elemento a su area */
header  { grid-area: header; }
aside   { grid-area: sidebar; }
main    { grid-area: main; }
footer  { grid-area: footer; }
```

Resultado visual:
```
┌─────────────────────────┐
│         header          │
├──────────┬──────────────┤
│ sidebar  │    main      │
├──────────┴──────────────┤
│         footer          │
└─────────────────────────┘
```

El punto `.` en `grid-template-areas` representa una celda vacia:
```css
grid-template-areas:
  "header header"
  ".      main  "   /* la celda de sidebar queda vacia */
  "footer footer";
```

---

## Concepto 5: `auto-fill` y `auto-fit` — Grids Responsivos sin Media Queries

```css
/* auto-fill: crea columnas automaticamente segun el espacio disponible */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}
```

- `minmax(280px, 1fr)` → cada columna tiene minimo 280px y maximo 1fr
- `auto-fill` → llena el espacio con tantas columnas como quepan
- `auto-fit` → igual que auto-fill pero colapsa columnas vacias

Esto crea un grid completamente responsivo sin escribir ningun `@media query`.

---

## Concepto 6: Flexbox vs Grid — Cuando usar cada uno

| Situacion | Herramienta |
|---|---|
| Layout de pagina completo (2D) | **Grid** |
| Galeria de cards responsiva | **Grid** con auto-fill |
| Navbar con items en fila | **Flexbox** |
| Centrar un elemento | **Flexbox** |
| Alinear items con alturas distintas | **Grid** |
| Componentes pequenos (boton, badge) | **Flexbox** |

**Regla practica:** si necesitas controlar filas Y columnas al mismo tiempo, usa Grid.
Si controlas solo una dimension, usa Flexbox. En proyectos reales se usan los dos.

---

## Ejercicio del Dia

Agrega a tu `styles.css` existente los estilos de Grid para el portafolio.

### Lo que debes implementar

**1. Layout de pagina con grid-template-areas**

Envuelve el contenido de `<body>` en un grid que defina claramente
las areas `header`, `main` y `footer`:

```css
body {
  display: grid;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header"
    "main"
    "footer";
  min-height: 100vh;
}

header { grid-area: header; }
main   { grid-area: main; }
footer { grid-area: footer; }
```

**2. Grid de proyectos responsivo**

Reemplaza el Flexbox de `#proyectos` por un Grid con `auto-fill`:

```css
#proyectos {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
  padding: 30px;
}
```

> Nota: cuando uses Grid en #proyectos, quita el display:flex y flex-wrap
> que pusiste ayer — Grid los reemplaza completamente.

**3. Bonus — Grid de 2 columnas para la presentacion**

La seccion de presentacion puede tener imagen a la izquierda y texto a la derecha:

```css
#presentacion-personal {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 24px;
  align-items: center;
  padding: 30px;
}
```

### Requisitos tecnicos

- `grid-template-areas` para el layout de pagina
- `repeat(auto-fill, minmax(...))` en la seccion de proyectos
- `grid-area` en header, main y footer
- Mantener los estilos Flexbox del Dia 04 donde siguen siendo apropiados

---

## Entrega

Pega el `styles.css` completo y actualizado en el chat.

---

## Recursos

- CSS-Tricks Grid Guide: https://css-tricks.com/snippets/css/complete-guide-grid/
- Grid Garden (juego): https://cssgridgarden.com/
- MDN Grid: https://developer.mozilla.org/es/docs/Web/CSS/CSS_grid_layout
