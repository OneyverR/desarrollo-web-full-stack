# Sesion Dia 03 — SEO Basico y Meta Tags
**Fecha:** 2026-05-17
**Estado:** ✅ Aprobado — listo para Dia 04

---

## Codigo Entregado

```html
<!doctype html>
<html lang="es">
<head>
	<!--Configuracion Basica-->
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	
	<!--SEO primario-->
	<title>Ing Oneyver Rodriguez - Desarrollador Web | Portafolio</title>
	<meta name="description" content="Portafolio personal de Oneyver Rodríguez, desarrollador web FullStack. Aquí encontrarás información sobre proyectos y experiencia en el desarrollo web">
	<meta name="robots" content="index, follow">
	<link rel="canonical" href="https://ingoneyverrodriguez.com/">
	
	
	<!--Open Graph-->
	<meta property="og:type" content="website">
	<meta property="og:title" content="Ing Oneyver Rodriguez - Desarrollador Web">
	<meta property="og:description" content="Portafolio personal de Oneyver Rodríguez, desarrollador web FullStack. Aquí encontrarás información sobre proyectos y experiencia en el desarrollo web">
	<meta property="og:url" content="https://ingoneyverrodriguez.com/">
	<meta property="og:image" content="https://ingoneyverrodriguez.com/images/og.jpg">
	<meta property="og:site_name" content="Portafolio Oneyver Rodriguez">
	<meta property="og:locale" content="es_CO">
	
	<!--Twitter Card-->
	<meta name="twitter:card" content="summary_large_image">
	<meta name="twitter:title" content="Ing Oneyver Rodriguez - Desarrollador Web">
	<meta name="twitter:description" content="Portafolio personal de Oneyver Rodríguez">
	<meta name="twitter:image" content="https://ingoneyverrodriguez.com/images/og.jpg">
	
	<!--Icon-->
	<link rel="icon" type="image/svg+xml" href="/favicon.svg">
	<meta name="theme-color" content="#FF653F">
	
	<!--CSS-->
	<link rel="stylesheet" href="styles.css">

</head>
<body>
	<header>
		<h1>Oneyver Rodríguez Novoa</h1>
		<nav>
			<ul>
				<li><a href="/">Inicio</a></li>
				<li><a href="/">Proyectos</a></li>
				<li><a href="/">Contacto</a></li>
			</ul>
		</nav>
	</header>
	<main>
		<section id="presentacion-personal">
			<h2>Presentacion Personal</h2>
			<p>Hola, mi nombre es Oneyver Rodríguez, Soy ingeniero electrónico y actualmente deseo iniciar mi
				proyecto de formación en desarrollo web, apoyado con Claude Code. Esta es mi primera sesión y mi
				primera actividad para esta formación. Estoy emocionado de ser el mejor en esto.</p>
		</section>
		<section id="proyectos">
			<h2>Proyectos y Preguntas Personales</h2>
			<article id="proyecto1">
				<header>
					<h3>Aprender Desarrollo Web con Claude Code</h3>
					<time datetime="2026-05-16">16 de mayo de 2026</time>
				</header>
				<p>
					Mi objetivo principal con este proyecto es aprender desarrollo web, de la mano con Claude Code
					quien será mi instructor guía en este maravilloso proceso. El objetivo es volvernos expertos en
					esta profesión, considerada una de las más demandadas en el mercado laboral actual.
				</p>
			</article>
			<article id="proyecto2">
				<header>
					<h3>¿Por qué Aprender con Claude Code?</h3>
					<time datetime="2026-05-16">16 de mayo de 2026</time>
				</header>
				<p>
					Soy consciente de que existen muchas plataformas y recursos para aprender desarrollo web, pero he
					decidido elegir a Claude Code por su enfoque práctico, su experiencia en la industria y su capacidad
					para adaptarse a las necesidades de los estudiantes.
				</p>
			</article>
		</section>
	</main>
	<footer>
		<p>Oneyver Rodríguez Novoa - 2026</p>
	</footer>
</body>
</html>
```

---

## Feedback del Coach

### Puntos positivos

1. Estructura del `<head>` bien organizada con comentarios por secciones
2. `<title>` descriptivo y dentro del limite de 60 caracteres (53 chars) — correcto
3. `<meta description>` informativa y dentro del limite de 160 caracteres
4. `<meta robots>` presente con valores correctos
5. `<link rel="canonical">` con dominio propio — buena iniciativa usar un dominio real
6. Las 6 etiquetas Open Graph presentes y completas
7. Twitter Card con `summary_large_image` — tipo correcto
8. Favicon SVG — formato moderno, correcto
9. `theme-color` presente

### Puntos a corregir

**BUG 1 — Typo en `twitter:title` (linea 34):**
```html
<!-- Como esta (MAL) — "tittle" tiene doble t, el tag no funciona -->
<meta name="twitter:tittle" content="...">

<!-- Como debe ser -->
<meta name="twitter:title" content="...">
```
Con el typo, Twitter ignora este tag y no muestra titulo en la preview.

---

**BUG 2 — `theme-color` sin `#` en el valor hex (linea 39):**
```html
<!-- Como esta (MAL) — color invalido, el navegador lo ignora -->
<meta name="theme-color" content="FF653F">

<!-- Como debe ser -->
<meta name="theme-color" content="#FF653F">
```

---

**BUG 3 — `twitter:image` ausente:**

Declaraste `summary_large_image` pero no incluiste la imagen.
Sin imagen, Twitter degrada la card a `summary` simple.
```html
<!-- Agregar despues de twitter:description -->
<meta name="twitter:image" content="https://ingoneyverrodriguez.com/images/og.jpg">
```

---

**MEJORA — `og:image` sigue con URL de placeholder (linea 29):**
```html
<!-- Como esta — URL del template de la leccion -->
<meta property="og:image" content="https://tusitio.com/images/og.jpg">

<!-- Como debe ser — URL consistente con tu dominio -->
<meta property="og:image" content="https://ingoneyverrodriguez.com/images/og.jpg">
```

---

**MEJORA — `og:site_name` repite el titulo (linea 30):**

`og:site_name` es el nombre de la marca del sitio, no el titulo de la pagina.
```html
<!-- Como esta -->
<meta property="og:site_name" content="Ing Oneyver Rodriguez - Desarrollador Web">

<!-- Como debe ser — nombre corto del sitio -->
<meta property="og:site_name" content="Portafolio Oneyver Rodriguez">
```

---

**MEJORA — `og:locale` faltante:**

Estaba en la plantilla de la leccion. Agrega:
```html
<meta property="og:locale" content="es_VE">
```

### Conceptos a reforzar

- Los nombres de meta tags son exactos — un solo caracter mal los inutiliza
- `theme-color` requiere el `#` para valores hexadecimales
- `summary_large_image` sin `twitter:image` no muestra imagen grande


---

## Dudas de la Sesion

<!-- Registrar aqui las preguntas que surgieron durante la practica -->


---

## Resultado Final

**Segunda revision — bugs corregidos:**

- [x] Title con maximo 60 caracteres en formato correcto (53 chars)
- [x] Meta description de 150-160 caracteres
- [x] Meta robots presente
- [x] Link canonical con URL valida
- [x] 6 etiquetas Open Graph completas
- [x] twitter:title corregido
- [x] twitter:image agregada
- [x] theme-color con # correcto
- [x] og:image con URL del dominio propio
- [x] og:site_name como nombre corto
- [x] og:locale agregado (es_CO)
- [x] twitter:card corregido: "summary_large_image"

**Calificacion:** ✅ 10/10 — Dia completado. Avanzar a Dia 04.
