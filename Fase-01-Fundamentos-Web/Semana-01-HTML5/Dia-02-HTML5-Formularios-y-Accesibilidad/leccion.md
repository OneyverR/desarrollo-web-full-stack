# Dia 02 — HTML5: Formularios y Accesibilidad
**Fase:** 01 - Fundamentos Web
**Semana:** 01 - HTML5
**Fecha:** 2026-05-16
**Estado:** 🟡 En curso

---

## Objetivo del Dia

Los formularios son el principal punto de interaccion entre el usuario y una
aplicacion web. Un formulario mal construido es inaccessible, dificil de mantener
y propenso a errores. Al terminar este dia debes poder construir formularios
semanticos, accesibles y con validacion nativa de HTML5.

---

## Concepto 1: La Anatomia de un Formulario Correcto

```html
<form action="/contacto" method="POST" novalidate>
  <fieldset>
    <legend>Datos de Contacto</legend>

    <div class="campo">
      <label for="nombre">Nombre completo</label>
      <input
        type="text"
        id="nombre"
        name="nombre"
        required
        autocomplete="name"
        aria-describedby="nombre-ayuda"
      />
      <span id="nombre-ayuda">Ingresa tu nombre tal como aparece en tu documento.</span>
    </div>

    <div class="campo">
      <label for="email">Correo electronico</label>
      <input
        type="email"
        id="email"
        name="email"
        required
        autocomplete="email"
      />
    </div>

  </fieldset>

  <button type="submit">Enviar mensaje</button>
</form>
```

### Por que cada parte importa

| Elemento | Razon |
|---|---|
| `<fieldset>` + `<legend>` | Agrupa campos relacionados — obligatorio para accesibilidad |
| `<label for="id">` | Conecta el texto al input — click en el label activa el campo |
| `id` en el input | Debe ser unico en la pagina y coincidir con el `for` del label |
| `name` en el input | Es el key que recibe el servidor — sin `name` el dato no se envia |
| `autocomplete` | Ayuda al navegador a autocompletar — mejora UX |
| `aria-describedby` | Conecta texto de ayuda al campo para lectores de pantalla |

---

## Concepto 2: Tipos de Input en HTML5

HTML5 introdujo tipos de input especializados. Cada uno activa el teclado
correcto en movil y proporciona validacion nativa:

```html
<!-- Texto libre -->
<input type="text" />

<!-- Email — valida formato automaticamente -->
<input type="email" />

<!-- Telefono — teclado numerico en movil -->
<input type="tel" />

<!-- URL — valida que sea una URL valida -->
<input type="url" />

<!-- Numero con limites -->
<input type="number" min="1" max="100" step="1" />

<!-- Fecha -->
<input type="date" />

<!-- Fecha y hora -->
<input type="datetime-local" />

<!-- Contrasena — oculta el texto -->
<input type="password" autocomplete="current-password" />

<!-- Checkbox — si/no -->
<input type="checkbox" id="terminos" name="terminos" />
<label for="terminos">Acepto los terminos y condiciones</label>

<!-- Radio — una opcion de varias -->
<fieldset>
  <legend>Nivel de experiencia</legend>
  <input type="radio" id="junior" name="nivel" value="junior" />
  <label for="junior">Junior</label>
  <input type="radio" id="senior" name="nivel" value="senior" />
  <label for="senior">Senior</label>
</fieldset>

<!-- Seleccion de lista -->
<select id="pais" name="pais">
  <option value="">-- Selecciona tu pais --</option>
  <option value="ve">Venezuela</option>
  <option value="co">Colombia</option>
  <option value="mx">Mexico</option>
</select>

<!-- Texto multilinea -->
<textarea id="mensaje" name="mensaje" rows="4" cols="50"></textarea>

<!-- Archivo -->
<input type="file" accept=".pdf,.doc" />

<!-- Busqueda -->
<input type="search" />

<!-- Color -->
<input type="color" />
```

---

## Concepto 3: Validacion Nativa de HTML5

Sin escribir JavaScript, HTML5 puede validar tus formularios:

```html
<!-- Campo obligatorio -->
<input type="text" required />

<!-- Longitud minima y maxima -->
<input type="text" minlength="3" maxlength="50" />

<!-- Rango de valores -->
<input type="number" min="18" max="99" />

<!-- Patron con expresion regular -->
<input
  type="text"
  pattern="[A-Za-z]{3,}"
  title="Solo letras, minimo 3 caracteres"
/>

<!-- URL valida -->
<input type="url" required />

<!-- Email valido -->
<input type="email" required />
```

### El atributo `novalidate`

Cuando se agrega `novalidate` al `<form>`, se desactiva la validacion nativa
del navegador. Se usa cuando quieres manejar la validacion con JavaScript
(lo haremos en fases posteriores). Por ahora lo usamos sin el.

---

## Concepto 4: Accesibilidad en Formularios

### Error 1: Usar placeholder como unico label

```html
<!-- MAL — el placeholder desaparece al escribir -->
<input type="text" placeholder="Tu nombre" />

<!-- BIEN — label visible siempre + placeholder como ayuda opcional -->
<label for="nombre">Nombre</label>
<input type="text" id="nombre" placeholder="Ej: Juan Perez" />
```

### Error 2: Inputs sin label

```html
<!-- MAL — un lector de pantalla no sabe que es este campo -->
<input type="email" />

<!-- BIEN -->
<label for="email">Correo electronico</label>
<input type="email" id="email" />

<!-- ALTERNATIVA si el label es visual y no quieres mostrarlo -->
<input type="email" aria-label="Correo electronico" />
```

### Error 3: Botones sin texto descriptivo

```html
<!-- MAL -->
<button>X</button>
<button><img src="enviar.png" /></button>

<!-- BIEN -->
<button type="button" aria-label="Cerrar dialogo">X</button>
<button type="submit">
  <img src="enviar.png" alt="" aria-hidden="true" />
  Enviar formulario
</button>
```

### El atributo `aria-describedby`

Conecta un campo con texto de ayuda adicional:

```html
<label for="password">Contrasena</label>
<input
  type="password"
  id="password"
  aria-describedby="password-requisitos"
/>
<p id="password-requisitos">
  Minimo 8 caracteres, una mayuscula y un numero.
</p>
```

El lector de pantalla lee: *"Contrasena. Minimo 8 caracteres, una mayuscula y un numero."*

---

## Concepto 5: `<button>` vs `<input type="submit">`

```html
<!-- input type submit — menos flexible -->
<input type="submit" value="Enviar" />

<!-- button — preferido, permite contenido HTML dentro -->
<button type="submit">Enviar mensaje</button>
<button type="button">Cancelar</button>   <!-- no envia el form -->
<button type="reset">Limpiar</button>     <!-- resetea todos los campos -->
```

Siempre especifica el `type` del boton. Sin `type`, dentro de un `<form>`
el navegador asume `type="submit"` — comportamiento inesperado.

---

## Ejercicio del Dia

Crea el archivo `contacto.html` dentro de tu carpeta `portafolio/`:

```
portafolio/
├── index.html      (ya existe)
├── contacto.html   ← nuevo
├── styles.css
└── images/
```

Construye un formulario de contacto completo que incluya:

1. `<fieldset>` con `<legend>` para agrupar los campos
2. Campo **Nombre** — tipo `text`, requerido, minimo 3 caracteres
3. Campo **Email** — tipo `email`, requerido
4. Campo **Asunto** — `<select>` con al menos 3 opciones (Consulta, Proyecto, Otro)
5. Campo **Mensaje** — `<textarea>` requerido
6. **Checkbox** de aceptar terminos — requerido
7. Boton `<button type="submit">` con texto descriptivo

### Requisitos tecnicos

- Cada input con su `<label>` correctamente vinculado por `for`/`id`
- Atributos `name` en todos los campos
- Validacion nativa: `required` donde corresponda
- Al menos un campo con `aria-describedby` con texto de ayuda
- Los radio o checkbox deben ir dentro de un `<fieldset>`

### Criterio de exito

Al hacer click en Enviar sin llenar los campos, el navegador debe mostrar
mensajes de error nativos en los campos incorrectos.

---

## Entrega

Pega el codigo de `contacto.html` en el chat cuando termines.

---

## Recursos de Consulta

- MDN — formularios: https://developer.mozilla.org/es/docs/Learn/Forms
- MDN — tipos de input: https://developer.mozilla.org/es/docs/Web/HTML/Element/input
- WAI-ARIA — formularios accesibles: https://www.w3.org/WAI/tutorials/forms/
