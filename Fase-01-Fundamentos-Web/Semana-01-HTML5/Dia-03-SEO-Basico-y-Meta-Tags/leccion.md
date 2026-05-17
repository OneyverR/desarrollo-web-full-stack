# Dia 03 — SEO Basico y Meta Tags
**Fase:** 01 - Fundamentos Web
**Semana:** 01 - HTML5
**Fecha:** 2026-05-17
**Estado:** 🟡 En curso

---

## Objetivo del Dia

SEO (Search Engine Optimization) no es magia ni trucos — es construir paginas
que los motores de busqueda puedan leer, entender y clasificar correctamente.
Al terminar este dia sabes exactamente que va en el `<head>` de cada pagina
y por que, incluyendo las etiquetas que controlan como se ve tu sitio cuando
alguien lo comparte en redes sociales.

---

## Concepto 1: Como Google lee tu pagina

Antes de optimizar, hay que entender el proceso:

```
1. Crawling   → Google envía un bot (Googlebot) a leer tu HTML
2. Indexing   → Analiza el contenido y lo guarda en su base de datos
3. Ranking    → Decide en qué posición mostrarlo según cientos de factores
```

Tu HTML afecta directamente los pasos 1 y 2. Sin HTML correcto,
Google no puede indexar bien tu contenido sin importar cuan bueno sea.

---

## Concepto 2: Meta Tags Esenciales

### El `<title>`

```html
<title>Oneyver Rodriguez — Desarrollador Web FullStack | Portafolio</title>
```

Reglas:
- Maximo **60 caracteres** — Google corta el resto en los resultados
- Debe ser unico en cada pagina del sitio
- Formato recomendado: `Tema Principal | Nombre del Sitio`
- Es el texto mas importante para el ranking

### El `<meta name="description">`

```html
<meta
  name="description"
  content="Portafolio de Oneyver Rodriguez, ingeniero electronico formandose como desarrollador web FullStack. Proyectos con HTML, CSS, JavaScript y mas."
/>
```

Reglas:
- Maximo **160 caracteres**
- No afecta el ranking directamente pero sí el Click-Through Rate (CTR)
- Google puede ignorarla y generar la suya — pero la tuya es el punto de partida
- Debe ser descriptiva y contener la propuesta de valor

### El `<meta name="robots">`

```html
<!-- Permitir indexacion (comportamiento por defecto) -->
<meta name="robots" content="index, follow" />

<!-- No indexar esta pagina -->
<meta name="robots" content="noindex, nofollow" />
```

Cuando usarlo:
- `noindex` en paginas de admin, privacidad, confirmacion de pago
- `noindex` en versiones duplicadas del mismo contenido
- Por defecto no necesitas ponerlo si quieres que indexe

### El `<link rel="canonical">`

```html
<link rel="canonical" href="https://oneyver.dev/portafolio/" />
```

Problema que resuelve: si tu pagina es accesible por varias URLs
(`http` vs `https`, `www` vs sin `www`, con `/` vs sin `/`),
Google ve contenido duplicado. El canonical le dice cual es la URL oficial.

Regla: siempre apuntar a la URL exacta, con `https` y con el `/` final si corresponde.

---

## Concepto 3: Open Graph — Como se ve en redes sociales

Cuando alguien comparte tu URL en LinkedIn, WhatsApp o Twitter,
estas plataformas leen las etiquetas Open Graph para construir la vista previa.

```html
<!-- Tipo de contenido -->
<meta property="og:type" content="website" />

<!-- Titulo que aparece en la preview -->
<meta property="og:title" content="Oneyver Rodriguez — Desarrollador Web FullStack" />

<!-- Descripcion en la preview -->
<meta property="og:description" content="Portafolio y proyectos de desarrollo web." />

<!-- URL canonica de la pagina -->
<meta property="og:url" content="https://oneyver.dev/" />

<!-- Imagen de preview (minimo 1200x630px) -->
<meta property="og:image" content="https://oneyver.dev/images/og-portafolio.jpg" />

<!-- Nombre del sitio -->
<meta property="og:site_name" content="Portafolio Oneyver Rodriguez" />

<!-- Idioma -->
<meta property="og:locale" content="es_VE" />
```

### Twitter Cards

Twitter tiene su propio sistema (aunque lee OG como fallback):

```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Oneyver Rodriguez — Desarrollador Web FullStack" />
<meta name="twitter:description" content="Portafolio y proyectos de desarrollo web." />
<meta name="twitter:image" content="https://oneyver.dev/images/og-portafolio.jpg" />
```

Tipos de card:
- `summary` — card pequena con imagen cuadrada
- `summary_large_image` — card grande con imagen horizontal (la mas comun)

---

## Concepto 4: Etiquetas de Configuracion del Navegador

```html
<!-- Favicon — icono en la pestana del navegador -->
<link rel="icon" type="image/png" href="/images/favicon.png" />

<!-- Favicon SVG (moderno, escala sin pixelarse) -->
<link rel="icon" type="image/svg+xml" href="/images/favicon.svg" />

<!-- Icono para Apple (cuando guardan tu web en el home del iPhone) -->
<link rel="apple-touch-icon" href="/images/apple-touch-icon.png" />

<!-- Color de la barra del navegador en movil -->
<meta name="theme-color" content="#0f172a" />
```

---

## Concepto 5: El `<head>` Completo y Profesional

Aqui esta la plantilla que usaras de base en todos tus proyectos:

```html
<!doctype html>
<html lang="es">
<head>
  <!-- Configuracion basica -->
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- SEO primario -->
  <title>Titulo de la Pagina | Nombre del Sitio</title>
  <meta name="description" content="Descripcion de 150-160 caracteres." />
  <meta name="robots" content="index, follow" />
  <link rel="canonical" href="https://tusitio.com/esta-pagina/" />

  <!-- Open Graph -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="Titulo de la Pagina" />
  <meta property="og:description" content="Descripcion para redes sociales." />
  <meta property="og:url" content="https://tusitio.com/esta-pagina/" />
  <meta property="og:image" content="https://tusitio.com/images/og.jpg" />
  <meta property="og:site_name" content="Nombre del Sitio" />
  <meta property="og:locale" content="es_VE" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Titulo de la Pagina" />
  <meta name="twitter:description" content="Descripcion para Twitter." />
  <meta name="twitter:image" content="https://tusitio.com/images/og.jpg" />

  <!-- Iconos -->
  <link rel="icon" type="image/svg+xml" href="/images/favicon.svg" />
  <link rel="apple-touch-icon" href="/images/apple-touch-icon.png" />
  <meta name="theme-color" content="#0f172a" />

  <!-- CSS -->
  <link rel="stylesheet" href="/styles.css" />
</head>
```

---

## Concepto 6: SEO y HTML Semantico

El HTML semantico que aprendiste en el Dia 01 tiene impacto directo en SEO:

| Elemento semantico | Impacto SEO |
|---|---|
| `<h1>` unico y descriptivo | Google lo usa como el titulo principal del contenido |
| `<h2>`, `<h3>` jerarquicos | Definen la estructura de temas de la pagina |
| `<article>` | Indica contenido independiente y rastreable |
| `<time datetime="...">` | Google entiende la fecha de publicacion |
| `<a>` con texto descriptivo | Mejor que "click aqui" — el texto del link es una senal |
| `alt` en imagenes | Google no ve imagenes, lee el texto alternativo |

### El atributo `alt` en imagenes

```html
<!-- MAL — no dice nada -->
<img src="foto.jpg" alt="foto" />
<img src="foto.jpg" alt="" />   <!-- vacio solo si es imagen decorativa -->

<!-- BIEN — descriptivo -->
<img src="portafolio-preview.jpg" alt="Captura de pantalla del portafolio de Oneyver Rodriguez" />

<!-- Imagen decorativa (iconos, separadores) — alt vacio es correcto -->
<img src="decoracion.svg" alt="" role="presentation" />
```

---

## Ejercicio del Dia

Actualiza el `<head>` de tu `index.html` del portafolio aplicando todo lo aprendido:

1. `<title>` con maximo 60 caracteres en formato `Nombre | Rol`
2. `<meta description>` de 150-160 caracteres descriptiva y con propuesta de valor
3. `<meta name="robots" content="index, follow" />`
4. `<link rel="canonical">` apuntando a tu URL (puedes usar `https://tuusuario.github.io/portafolio/` o inventar una)
5. Las 6 etiquetas Open Graph (`type`, `title`, `description`, `url`, `image`, `site_name`)
6. Las 3 etiquetas Twitter Card (`card`, `title`, `description`)
7. `<link rel="icon">` apuntando a un favicon (puede ser ruta inventada por ahora)
8. `<meta name="theme-color">` con el color que elijas

Adicionalmente, revisa todas las imagenes del portafolio y asegurate
de que tengan atributo `alt` descriptivo.

### Criterio de exito

El `<head>` debe verse profesional — el mismo que usarias en un proyecto real.
Alguien que copie tu `<head>` deberia poder usarlo como plantilla.

---

## Entrega

Pega el contenido completo de tu `index.html` actualizado en el chat.

---

## Recursos de Consulta

- Google Search Central — Como funciona la busqueda: https://developers.google.com/search/docs
- Open Graph Protocol: https://ogp.me/
- Herramienta para probar Open Graph: https://www.opengraph.xyz/
- Validador de Twitter Cards: https://cards-dev.twitter.com/validator
