# Sesion Dia 02 — HTML5: Formularios y Accesibilidad
**Fecha:** 2026-05-16
**Estado:** ✅ Aprobado — listo para Dia 03

---

## Codigo Entregado

```html
<!doctype html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta name="description" content="Esta pagina es un formulario de contacto para el sitio web del portafolio de desarrollo web de Oneyver Rodriguez. Aquí puedes enviar tus consultas, comentarios o solicitudes de información.">
	<title>Formulario de Contacto</title>
	<link rel="stylesheet" href="styles.css">
</head>
<body>
	<header>
		<h1>Formulario de Contacto</h1>
	</header>
	<main>
		<form action="/contacto" method="POST">
			<fieldset>
				<legend>Datos Personales</legend>
				<div class="campo">
					<label for="nombre">Nombre Completo</label>
					<input
							type="text"
							id="nombre"
							name="nombre"
							minlength="3"
							autocomplete="name"
							required
							aria-describedby="nombre-ayuda"
					>
					<span id="nombre-ayuda">Ingresa tu nombre. Mínimo 3 caracteres</span>
				</div>
				<div class="campo">
					<label for="email">Correo Electrónico</label>
					<input
							type="email"
							id="email"
							name="email"
							autocomplete="email"
							required
							aria-describedby="email-ayuda"
					>
					<span id="email-ayuda">Ingresa tu correo electrónico</span>
				</div>
				<div class="campo">
					<label for="asunto">Asunto</label>
					<select name="asunto" id="asunto" required>
						<option value="">--Selecciona un asunto--</option>
						<option value="consulta">Consulta</option>
						<option value="proyecto">Proyecto</option>
						<option value="otro">Otro</option>
					</select>
				</div>
				<div class="campo">
					<label for="mensaje">Mensaje</label>
					<textarea name="mensaje" id="mensaje" cols="30" rows="10" aria-describedby="mensaje-ayuda" required></textarea>
					<span id="mensaje-ayuda">Ingresa el mensaje que desees enviar</span>
				</div>
			</fieldset>
			<fieldset>
				<legend>Términos y condiciones</legend>
				<div class="campo">
					<input
							type="checkbox"
							id="terminos"
							name="terminos"
							required
							aria-describedby="terminos-ayuda"
					>
					<label for="terminos">Términos y condiciones.</label>
					<span id="terminos-ayuda">Al seleccionar esta opcion, aceptas lo terminos y condiciones definidas
						para el envío de la información en este formulario</span>
				</div>
			</fieldset>
			<button type="submit">Enviar Información</button>
		</form>
	</main>
	<footer>
		<p>Oneyver Rodríguez - 2026</p>
	</footer>
</body>
</html>
```

---

## Feedback del Coach

### Puntos positivos

1. `fieldset` + `legend` presentes en el bloque principal — correcto
2. Todos los inputs tienen `label` vinculado por `for`/`id` — correcto
3. Atributo `name` en todos los campos — correcto
4. `aria-describedby` usado en 4 campos (nombre, email, mensaje, terminos) — excelente
5. `required` aplicado en todos los campos obligatorios
6. `<select>` con option vacia como valor por defecto — buena practica
7. Checkbox en su propio `<fieldset>` separado — estructura correcta
8. `<button type="submit">` con texto descriptivo
9. Uso de `pattern` en el nombre — iniciativa propia, bien

### Puntos a corregir

**BUG 1 — `<label>` del asunto esta vacio (linea 50):**
```html
<!-- Como esta (MAL) — label sin texto, invisible e inutil -->
<label for="asunto"></label>
<select name="asunto" id="asunto" required>

<!-- Como debe ser -->
<label for="asunto">Asunto</label>
<select name="asunto" id="asunto" required>
```
Un label vacio rompe la accesibilidad: el lector de pantalla llega al select
y no anuncia ningun texto descriptivo.

---

**BUG 2 — `<select>` fuera del wrapper `.campo` (lineas 50-56):**

El label y el select del asunto estan sueltos dentro del fieldset, sin el
`<div class="campo">` que usaste para los demas campos. Inconsistencia
estructural que luego rompe el CSS.

```html
<!-- Como debe ser -->
<div class="campo">
  <label for="asunto">Asunto</label>
  <select name="asunto" id="asunto" required>
    <option value="">-- Selecciona un asunto --</option>
    <option value="consulta">Consulta</option>
    <option value="proyecto">Proyecto</option>
    <option value="otro">Otro</option>
  </select>
</div>
```

---

**BUG 3 — segundo `<fieldset>` sin `<legend>` (linea 63):**

Todo `<fieldset>` debe tener un `<legend>`. Sin el, el lector de pantalla
no sabe de que grupo se trata.

```html
<!-- Como esta (MAL) -->
<fieldset>
  <div class="campo">
    <label for="terminos">Términos y condiciones</label>
    ...

<!-- Como debe ser -->
<fieldset>
  <legend>Terminos y condiciones</legend>
  <div class="campo">
    <input type="checkbox" id="terminos" ...>
    <label for="terminos">Acepto los terminos y condiciones</label>
    ...
```

Nota adicional: en checkboxes el `<label>` va despues del `<input>`, no antes.
Es una convencion de UX — el usuario ve la   casilla y luego lee que esta aceptando.

---

**MEJORA — `pattern` no soporta tildes (linea 33):**

```html
<!-- Como esta — rechaza "Oneyver Rodríguez" porque la í no esta en el patron -->
pattern="[A-Za-z\s]{3,}"

<!-- Como debe ser — incluir caracteres con tilde -->
pattern="[A-Za-záéíóúÁÉÍÓÚüÜñÑ\s]{3,}"
```
O usar simplemente `minlength="3"` si no necesitas restringir a solo letras.

---

**MEJORA — agregar `autocomplete` a nombre y email:**

```html
<input type="text" id="nombre" name="nombre" autocomplete="name" ...>
<input type="email" id="email" name="email" autocomplete="email" ...>
```
El navegador puede autocompletar estos campos si el usuario ya los ingreso antes.
Mejora la UX considerablemente.

### Conceptos a reforzar

- Todo `<fieldset>` necesita `<legend>` — sin excepcion
- El `<label>` de un campo siempre debe tener texto visible
- En checkboxes: primero `<input>`, despues `<label>`
- Los patrones HTML no soportan `\w` ni `\s` de forma consistente — usar clases de caracteres explicitas


---

## Dudas de la Sesion

<!-- Registrar aqui las preguntas que surgieron durante la practica -->


---

## Resultado Final

**Revision final — contacto.html (Portafolio)**

- [x] fieldset con legend en bloque principal
- [x] Label de asunto con texto visible
- [x] Select dentro de div.campo
- [x] Segundo fieldset con legend
- [x] Checkbox: input antes que label
- [x] autocomplete en nombre y email
- [x] minlength="3" — solucion mas robusta que pattern para este caso
- [x] Todos los labels con texto visible
- [x] Footer con contenido

**Calificacion contacto.html:** ✅ 10/10 — Todos los bugs corregidos.

---

## Revision Bonus — contacto_EX.html

Archivo de exploracion donde se practicaron TODOS los tipos de input de la leccion.
Iniciativa excelente. Errores encontrados para aprendizaje:

1. `<!Doctype html>` — usar `<!doctype html>` todo en minusculas
2. `lang="ES"` — codigos de idioma en minusculas: `lang="es"`
3. Linea 25: caracter `0` suelto antes de `pattern` — typo de edicion
4. `aria-label` redundante — cuando hay `<label>` visible con `for/id`, no agregar `aria-label` al input
5. Radio `name="senior"` — BUG CRITICO: ambos radios deben tener `name="nivel"` para formar un grupo exclusivo
6. `<label for="pais"></label>` — label vacio
7. `<label for="mensaje"></label>` — label vacio
8. `autocomplete="password"` — invalido. Usar `"current-password"` o `"new-password"`
9. `cols="5"` en textarea — demasiado angosto, probablemente typo de `cols="50"`
10. Select de pais fuera de fieldset — campos sueltos sin agrupacion semantica
