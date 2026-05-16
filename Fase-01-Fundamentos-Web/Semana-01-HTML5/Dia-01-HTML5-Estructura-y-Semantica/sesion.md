# Sesion Dia 01 — HTML5: Estructura y Semantica
**Fecha:** 2026-05-16
**Estado:** ✅ Aprobado — listo para Dia 02

---

## Codigo Entregado

```html
<!doctype html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta name="description" content="Ejemplo de estructura básica de un documento HTML5">
	<title>Sesión 1</title>
	<link rel="stylesheet" href="styles.css">
</head>
<body>
	<header>
		<h1>Oneyver Rodríguez Novoa</h1>
		<nav>
			<ul>
				<li><a href="#">Inicio</a></li>
				<li><a href="#">Proyectos</a></li>
				<li><a href="#">Contacto</a></li>
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
		<section id="proyectos-001">
			<article id="proyecto1">
				<header>
					<h2>Aprender Desarrollo Web con Claude Code</h2>
					<time datetime="2026-05-16">16 de mayo de 2026</time>
				</header>
				<p>
					Mi objetivo principal con este proyecto es aprender desarrollo web, de la mano con Claude Code
					quien será mi instructor guía en este maravilloso proceso. El objetivo es volvernos expertos en
					esta profesión, considerada una de las más demandadas en el mercado laboral actual.
			</article>
		</section>
		<section  id="proyectos-002">
			<article id="proyecto2">
				<header>
					<h2>¿Por qué Aprender con Claude Code?</h2>
					<time datetime="2026-05-16">16 de mayo de 2026</time>
				</header>
				<p>
					Soy consciente de que existen muchas plataformas y recursos para aprender desarrollo web, pero he
					decidido elegir a Claude Code por su enfoque práctico, su experiencia en la industria y su capacidad
					Para adaptarse a las necesidades de los estudiantes.
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

1. `<!doctype html>` correcto (minusculas es valido en HTML5)
2. `lang="es"` presente — bien
3. `charset` y `viewport` correctos
4. `<nav>` usa `<ul>` con `<li>` — exactamente como debe ser
5. `<time datetime="...">` implementado correctamente — detalle de nivel profesional
6. `<header>` dentro de cada `<article>` — uso avanzado correcto
7. Cero `<div>` innecesarios — el objetivo principal cumplido

### Puntos a corregir

**BUG CRITICO — etiqueta `<p>` sin cerrar en proyecto1:**
```html
<!-- Como esta (MAL) -->
<p>
    Mi objetivo principal con este proyecto...
</article>   ← el </p> nunca se cierra

<!-- Como debe ser -->
<p>
    Mi objetivo principal con este proyecto...
</p>
</article>
```
El navegador lo corrige automaticamente pero en produccion esto genera
comportamientos inesperados. Siempre cerrar todas las etiquetas.

---

**ESTRUCTURA — una section por articulo es incorrecto:**

La `<section>` agrupa contenido relacionado. Tener una section que solo
contiene un articulo no tiene sentido semantico. La estructura correcta es:

```html
<!-- Como esta (MAL) -->
<section id="proyectos-001">
    <article>...</article>
</section>
<section id="proyectos-002">
    <article>...</article>
</section>

<!-- Como debe ser -->
<section id="proyectos">
    <h2>Mis Proyectos</h2>
    <article id="proyecto1">...</article>
    <article id="proyecto2">...</article>
</section>
```

---

**TITLE no descriptivo:**
```html
<!-- Como esta (MAL) -->
<title>Sesión 1</title>

<!-- Como debe ser -->
<title>Oneyver Rodriguez — Desarrollador Web FullStack</title>
```

---

**META description no corresponde a la pagina:**
```html
<!-- Como esta -->
<meta name="description" content="Ejemplo de estructura básica de un documento HTML5">

<!-- Como debe ser -->
<meta name="description" content="Portafolio de Oneyver Rodriguez, ingeniero electronico en formacion como desarrollador web FullStack.">
```

---

**Mayuscula incorrecta mid-sentence en proyecto2:**
```
"su capacidad\nPara adaptarse"  ←  "Para" no debe ir en mayuscula
```

### Conceptos a reforzar

- `<section>` agrupa multiples elementos relacionados, no envuelve uno solo
- Las `<section>` deben tener siempre un encabezado propio (`<h2>`, `<h3>`, etc.)
- El `<title>` es la primera impresion en Google — debe ser descriptivo

---

## Respuesta a la Duda: section dentro de article vs article dentro de section

Ambas son validas. La diferencia es el contexto:

**`<article>` dentro de `<section>`** — cuando tienes una coleccion:
```html
<section id="proyectos">
    <h2>Proyectos</h2>        ← titulo del grupo
    <article>Proyecto 1</article>
    <article>Proyecto 2</article>
</section>
```
Usa esto cuando varios articulos pertenecen a una misma categoria.

**`<section>` dentro de `<article>`** — cuando un articulo tiene partes:
```html
<article>
    <h2>Mi Gran Proyecto</h2>
    <section>
        <h3>Descripcion</h3>
        <p>...</p>
    </section>
    <section>
        <h3>Tecnologias usadas</h3>
        <p>...</p>
    </section>
</article>
```
Usa esto cuando un solo articulo necesita subdivisiones internas.

**Para el portafolio:** la forma correcta es `<article>` dentro de `<section>`,
porque cada proyecto es un articulo dentro de la seccion "Proyectos".


---

## Dudas de la Sesion
1. Tengo la duda del uso de las etiquetas section, ya que en los recursos se indicaba que iban como para dividir la structure
de la etiqueta artículo; sin embargo, en el ejemplo se usaron para dividir la estructura del main, entonces no sé si es correcto 
usarlo de esa forma o si es mejor usarlo dentro de cada artículo para dividir la estructura de cada proyecto.


---

## Resultado Final

**Version corregida revisada el 2026-05-16**

- [x] Estructura base correcta (DOCTYPE, lang, charset, viewport)
- [x] Etiquetas semanticas correctas (header, nav, main, article, footer, time)
- [x] Jerarquia de encabezados correcta (h1 → h2 → h3)
- [x] Sin divs innecesarios
- [x] Title descriptivo
- [x] Meta description relevante al portafolio
- [x] Etiqueta p cerrada en proyecto1
- [x] Una sola section para proyectos con h2 propio
- [x] Typo en h2: "Poyectos" → "Proyectos" corregido

**Calificacion:** ✅ 10/10 — Dia completado. Avanzar a Dia 02.
