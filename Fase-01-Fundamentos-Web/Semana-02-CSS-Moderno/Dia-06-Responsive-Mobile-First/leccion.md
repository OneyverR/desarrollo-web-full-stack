# Dia 06 — Responsive Design y Mobile First
**Fase:** 01 - Fundamentos Web
**Semana:** 02 - CSS Moderno
**Fecha:** 2026-05-30
**Estado:** 🟡 En curso

---

## Objetivo del Dia

Responsive Design no es "hacer que se vea bien en movil". Es una filosofia de
diseno que parte del dispositivo mas pequeno y escala hacia arriba. Al terminar
este dia sabes escribir media queries correctamente, entiendes por que Mobile
First es el estandar y puedes adaptar cualquier layout a multiples pantallas.

---

## Concepto 1: Por que Mobile First

**Desktop First (enfoque viejo):**
```css
/* Disenas para escritorio primero */
.container { width: 1200px; }

/* Luego "arreglas" para movil */
@media (max-width: 768px) {
  .container { width: 100%; }
}
```

**Mobile First (enfoque correcto):**
```css
/* Diseñas para movil primero — el CSS base */
.container { width: 100%; }

/* Luego "mejoras" para pantallas mas grandes */
@media (min-width: 768px) {
  .container { max-width: 1200px; margin: 0 auto; }
}
```

**Por que Mobile First es mejor:**

1. **Performance** — los moviles descargan solo el CSS base, sin sobreescribir estilos de desktop
2. **Forced clarity** — obliga a priorizar el contenido esencial
3. **Estandar de la industria** — Google usa Mobile-First Indexing desde 2019
4. **Progressive Enhancement** — se añade complejidad hacia arriba, no se quita hacia abajo

---

## Concepto 2: Media Queries

### Sintaxis basica

```css
@media (condicion) {
  /* estilos que aplican cuando la condicion es verdadera */
}
```

### Breakpoints con `min-width` (Mobile First)

```css
/* Movil: sin media query — es el CSS base */
.nav { flex-direction: column; }

/* Tablet: 768px en adelante */
@media (min-width: 768px) {
  .nav { flex-direction: row; }
}

/* Desktop: 1024px en adelante */
@media (min-width: 1024px) {
  .nav { gap: 48px; }
}

/* Desktop grande: 1280px en adelante */
@media (min-width: 1280px) {
  .container { max-width: 1280px; margin: 0 auto; }
}
```

### Breakpoints estandar del mercado (2025)

| Nombre | Valor | Dispositivo tipico |
|--------|-------|-------------------|
| sm | 640px | Movil grande / landscape |
| md | 768px | Tablet |
| lg | 1024px | Laptop |
| xl | 1280px | Desktop |
| 2xl | 1536px | Desktop grande |

> Estos son los breakpoints de Tailwind CSS, el framework mas usado actualmente.
> Aprenderlos ahora te adelanta cuando lleguemos a la Fase 3.

### Otras condiciones utiles

```css
/* Orientacion */
@media (orientation: landscape) { ... }
@media (orientation: portrait) { ... }

/* Pantallas de alta densidad (Retina) */
@media (min-resolution: 2dppx) { ... }

/* Preferencia del sistema: modo oscuro */
@media (prefers-color-scheme: dark) {
  :root {
    --color-fondo: #0f172a;
    --color-texto: #f1f5f9;
  }
}

/* Preferencia del sistema: reducir animaciones */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}

/* Multiples condiciones */
@media (min-width: 768px) and (orientation: landscape) { ... }
```

---

## Concepto 3: Unidades Relativas

Las unidades fijas (`px`) no escalan. Las relativas se adaptan:

| Unidad | Relativa a | Uso tipico |
|--------|-----------|------------|
| `%` | El elemento padre | Anchos fluidos |
| `em` | El `font-size` del elemento actual | Padding/margin proporcional al texto |
| `rem` | El `font-size` del `<html>` (16px por defecto) | Tipografia consistente |
| `vw` | 1% del ancho del viewport | Elementos que ocupan porcentaje de pantalla |
| `vh` | 1% del alto del viewport | Secciones de pantalla completa |
| `svh` | 1% del alto del viewport pequeño (sin barra del browser) | Movil |
| `clamp()` | Min, preferido, max | Tipografia fluida |

### `clamp()` — el valor mas potente

```css
/* font-size fluido: minimo 16px, preferido 2.5vw, maximo 24px */
h1 {
  font-size: clamp(1rem, 2.5vw, 1.5rem);
}

/* Padding fluido */
.section {
  padding: clamp(16px, 5vw, 80px);
}
```

`clamp(min, preferido, max)` elimina la necesidad de media queries para
tipografia y espaciados — el valor se ajusta fluidamente al tamaño del viewport.

---

## Concepto 4: Imagenes Responsivas

```css
/* La imagen nunca supera su contenedor */
img {
  max-width: 100%;
  height: auto;     /* mantiene la proporcion */
  display: block;   /* elimina el espacio de linea base */
}
```

En HTML, el atributo `srcset` permite servir distintas imagenes segun el dispositivo:

```html
<img
  src="imagen-400.jpg"
  srcset="
    imagen-400.jpg  400w,
    imagen-800.jpg  800w,
    imagen-1200.jpg 1200w
  "
  sizes="(min-width: 768px) 50vw, 100vw"
  alt="Descripcion de la imagen"
/>
```

El navegador elige automaticamente la imagen mas adecuada segun el ancho
del viewport y la densidad de pantalla.

---

## Concepto 5: El Viewport Meta Tag

Ya lo tienes desde el Dia 01, pero ahora entiendes por que:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Sin este tag, los moviles renderizan la pagina con un ancho virtual de ~980px
y luego la reducen — haciendo inutiles todas las media queries.

---

## Ejercicio del Dia

Actualiza tu `styles.css` aplicando Mobile First al portafolio.

### Punto de partida

El CSS actual asume pantalla de escritorio. Debes invertirlo:
el CSS base debe ser para movil y las media queries deben agregar
estilos para pantallas mas grandes.

### Lo que debes implementar

**1. Reorganizar el CSS base para movil:**

```css
/* MOVIL: el header apila verticalmente */
header {
  flex-direction: column;
  align-items: flex-start;
  gap: 16px;
  padding: 16px;
}

/* MOVIL: nav links en columna */
nav ul {
  flex-direction: column;
  gap: 8px;
}

/* MOVIL: presentacion en una sola columna */
#presentacion-personal {
  grid-template-columns: 1fr;
  padding: 16px;
}
```

**2. Agregar breakpoint para tablet (768px):**

```css
@media (min-width: 768px) {
  header {
    flex-direction: row;
    padding: 0 30px;
  }
  nav ul {
    flex-direction: row;
    gap: 24px;
  }
  #presentacion-personal {
    grid-template-columns: 200px 1fr;
    padding: 30px;
  }
}
```

**3. Agregar breakpoint para desktop (1024px):**

```css
@media (min-width: 1024px) {
  body {
    max-width: 1280px;
    margin: 0 auto;
  }
}
```

**4. Tipografia fluida con `clamp()`:**

```css
h1 { font-size: clamp(1.5rem, 4vw, 2.5rem); }
h2 { font-size: clamp(1.2rem, 3vw, 1.8rem); }
```

### Requisitos tecnicos

- CSS base sin media queries debe verse correcto en movil (320px)
- `@media (min-width: 768px)` para tablet
- `@media (min-width: 1024px)` para desktop
- Al menos un uso de `clamp()` para tipografia
- Imagenes con `max-width: 100%`

### Como probar

En WebStorm, abre el archivo en el navegador y usa las DevTools
(F12) → icono de dispositivo movil para simular distintos tamaños.
Arrastra el borde para ver como cambia el layout.

---

## Entrega

Pega el `styles.css` completo en el chat.

---

## Recursos

- MDN Media Queries: https://developer.mozilla.org/es/docs/Web/CSS/CSS_media_queries
- MDN clamp(): https://developer.mozilla.org/es/docs/Web/CSS/clamp
- Responsive Design Checker: https://responsivedesignchecker.com/
