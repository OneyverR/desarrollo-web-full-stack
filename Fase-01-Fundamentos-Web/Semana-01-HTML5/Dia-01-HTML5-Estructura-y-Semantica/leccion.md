# Dia 01 — HTML5: Estructura y Semantica
**Fase:** 01 - Fundamentos Web
**Semana:** 01 - HTML5
**Fecha:** 2026-05-16
**Estado:** 🟡 En curso

---

## Objetivo del Dia

Comprender que HTML semantico no es una preferencia sino un estandar profesional.
Al terminar este dia debes poder construir el esqueleto de cualquier pagina web
con estructura correcta, jerarquia de encabezados y etiquetas semanticas apropiadas.

---

## Concepto 1: La Estructura Base Correcta

Todo documento HTML profesional comienza asi:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Descripcion de la pagina para SEO (max 160 caracteres)" />
    <title>Titulo de la Pagina | Nombre del Sitio</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <!-- Contenido aqui -->
  </body>
</html>
```

### Por que cada linea importa

| Linea | Proposito |
|---|---|
| `<!DOCTYPE html>` | Activa el modo estandar HTML5 en el navegador |
| `lang="es"` | Lectores de pantalla usan esto para pronunciar correctamente |
| `charset="UTF-8"` | Soporta tildes, emojis y caracteres especiales |
| `viewport` | Sin esto la pagina se ve rota en dispositivos moviles |
| `description` | Google la muestra como resumen en resultados de busqueda |

---

## Concepto 2: Etiquetas Semanticas vs Div Soup

### Lo que NO se hace (pasado)

```html
<div class="header">
  <div class="nav">
    <div class="nav-item">Inicio</div>
  </div>
</div>
<div class="main">
  <div class="article">
    <div class="title">Mi Articulo</div>
  </div>
</div>
<div class="footer">...</div>
```

### HTML5 semantico correcto

```html
<header>
  <nav>
    <ul>
      <li><a href="/">Inicio</a></li>
      <li><a href="/blog">Blog</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <header>
      <h1>Titulo del Articulo</h1>
      <time datetime="2026-05-16">16 de Mayo, 2026</time>
    </header>
    <section>
      <h2>Primera Seccion</h2>
      <p>Contenido...</p>
    </section>
  </article>

  <aside>
    <h2>Articulos relacionados</h2>
  </aside>
</main>

<footer>
  <p>&copy; 2026 Oneyver Rodriguez</p>
</footer>
```

### Mapa de etiquetas semanticas esenciales

| Etiqueta | Uso correcto |
|---|---|
| `<header>` | Cabecera de pagina O de una seccion/articulo |
| `<nav>` | Bloque de navegacion principal |
| `<main>` | Contenido principal — solo uno por pagina |
| `<article>` | Contenido independiente (post, noticia, producto) |
| `<section>` | Agrupacion tematica dentro de un articulo |
| `<aside>` | Contenido complementario (sidebar) |
| `<footer>` | Pie de pagina o de seccion |
| `<figure>` + `<figcaption>` | Imagen con descripcion |
| `<time>` | Fechas y horas con atributo datetime |

---

## Concepto 3: Jerarquia de Encabezados

```html
<!-- MAL: saltar niveles -->
<h1>Titulo Principal</h1>
<h3>Subtitulo</h3>

<!-- BIEN: jerarquia secuencial -->
<h1>Titulo Principal</h1>
  <h2>Seccion Principal</h2>
    <h3>Subseccion</h3>
  <h2>Otra Seccion</h2>
```

**Regla de oro:** Solo un `<h1>` por pagina. Los encabezados definen el indice
del documento — Google y lectores de pantalla lo usan para navegar el contenido.

---

## Ejercicio del Dia

Crea en WebStorm el siguiente proyecto:

```
portafolio/
├── index.html
├── styles.css     (vacio por ahora)
└── images/        (carpeta vacia)
```

Construye `index.html` con la estructura de un portafolio personal que incluya:

1. `<header>` con tu nombre y `<nav>` con 3 links: Inicio, Proyectos, Contacto
2. `<main>` con una `<section>` de presentacion personal
3. `<section>` de proyectos con al menos 2 `<article>` (proyectos inventados)
4. `<footer>` con tu nombre y año

### Requisitos tecnicos

- Estructura `<!DOCTYPE html>` correcta con `lang="es"`
- Jerarquia de encabezados sin saltar niveles
- Cero `<div>` donde pueda ir una etiqueta semantica
- `<title>` descriptivo

### Criterio de exito

La estructura debe poder leerse como el indice de un libro sin necesidad de CSS.

---

## Entrega

Pega tu codigo HTML en el chat cuando termines.
El feedback sera sobre estructura, no sobre apariencia visual — CSS viene despues.

---

## Recursos de Consulta

- MDN Web Docs — HTML elements reference: https://developer.mozilla.org/es/docs/Web/HTML/Element
- HTML5 Outliner (herramienta para verificar jerarquia): https://gsnedders.html5.org/outliner/
