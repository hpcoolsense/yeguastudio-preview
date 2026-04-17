# Prompt para reconstruir el mockup de YEGUA STUDIO

Copiá todo lo que está debajo y pegáselo a otro Claude (ideal Claude Code o Claude con Artifacts). Después adjuntale la imagen del telón rojo de fondo como archivo.

---

## PROMPT

Necesito que construyas un **mockup de landing page de una sola página** para una marca de indumentaria llamada **Yegua Studio**. Es una marca real de Córdoba, Argentina, inspirada en el cine, hecha por Ailén Rausch y Emilia Salto (`@ailen.rausch` y `@emiliasalto`, Instagram `@yegua.studio`). La estética de la marca es **teatral / cinematográfica vintage**: telón rojo, luces, letreros de cine antiguos.

Te paso como adjunto una **foto de un telón rojo** — usala como fondo embebido en base64 dentro del HTML (no la enlaces desde disco, tiene que ser un archivo 100% portable).

### 1. Identidad visual — CRÍTICO

**Paleta de colores** (usá estas variables CSS exactas):
```
--yegua-yellow: #F4D03F         /* amarillo del logo */
--yegua-yellow-deep: #E8C02A
--yegua-red: #8B0000             /* rojo intenso */
--yegua-red-curtain: #5c0a0a     /* rojo telón oscuro */
--yegua-cream: #f4ead6           /* crema para textos */
--yegua-ink: #0a0504             /* negro cálido casi café */
--yegua-paper: #efe7d3           /* papel vintage */
```

**Tipografías** (desde Google Fonts):
- **Bodoni Moda** (weights 400, 700, 900 + italics) — para títulos, logo y todo lo de display. Es una serif de alto contraste.
- **Cormorant Garamond** (weights 300, 400, 500 + italics) — para body text y textos itálicos elegantes.
- Incluí también **Playfair Display** y **Caveat** por si hacen falta.

**El logo "YEGUA STUDIO" es el elemento más importante.** Tiene que verse así:
- Color amarillo `#F4D03F`
- Tipografía `Bodoni Moda` peso 900
- `text-transform: uppercase`
- `transform: scaleY(1.25)` para estirarla verticalmente y que parezca condensada/alta (imita la tipografía del logo real)
- Sombra negra 3D escalonada con stack de text-shadows: capas a 4, 6, 8, 10, 12, 14, 16px en negro sólido, y la última con blur y opacidad para dar profundidad:
```css
text-shadow:
  4px 4px 0 #000,
  6px 6px 0 #000,
  8px 8px 0 #000,
  10px 10px 0 #000,
  12px 12px 0 rgba(0,0,0,0.9),
  14px 14px 0 rgba(0,0,0,0.8),
  16px 16px 24px rgba(0,0,0,0.6);
```
- `font-size: clamp(90px, 17vw, 260px)` para que escale responsive
- Animación de "spotlight" al cargar: opacity 0→1 + translateY 40px→0 + filter brightness 0.3→1, duración 3s ease-out

### 2. Estructura de secciones (en este orden)

1. **Top bar fija** con blur: logo chico "YEGUA·STUDIO" a la izquierda en amarillo, nav al medio (Próxima función, Colección, Manifiesto, Contacto), "Bolsa (0)" a la derecha.

2. **Hero** con la imagen del telón embebida como `background-image` + `background-size: cover`. Overlay con gradiente radial oscuro para dar foco al centro. Contiene:
   - Kicker "Marca de indumentaria inspirada en el cine" con ✦ decorativos
   - El LOGO GIGANTE (descripto arriba), "Yegua" y "Studio" en líneas separadas
   - Tag: "Hecho en **Córdoba** — Argentina / Envíos a todo el país"
   - CTA amarillo con borde negro y box-shadow desplazado estilo neobrutalist: "Próximamente la función"

3. **Ticker amarillo** (franja horizontal) con texto rodando infinito (animación `scroll-left` 30s linear), bordes negros arriba y abajo, texto "Pearl × Yegua · Nueva colección · Hecho en Córdoba · Próximamente · Indumentaria de autor · Inspirada en el cine" separado por estrellas rojas. Duplicá el contenido para que el loop sea perfecto.

4. **Próxima función** (fondo `--yegua-ink`): kicker "Se levanta el telón", título grande "Pearl × Yegua" con la misma técnica de scaleY + sombra, countdown con 4 cajas (Días / Horas / Min / Seg) con borde amarillo fino, meta "Capítulo 01 · Córdoba · Función única".

5. **Colección** (fondo `--yegua-paper` color papel): borde superior con patrón de tiras negro/crema que simula un rollo de película. Grilla de 3 columnas × 2 filas = **6 productos**. Cada producto tiene:
   - Frame con `border: 2px solid ink` y `box-shadow: 8px 8px 0 ink` (estilo neobrutalist)
   - Tag amarilla arriba a la izquierda (Nuevo, Edición limitada, Lanzamiento, Archivo, Back in stock, Pre-venta)
   - **SVG inline** con silueta estilizada de la prenda (viewBox 300×400) — hacé siluetas simples de: vestido rojo, vestido de lunares blanco con puntos negros, slip dress crudo, camisa a rayas rojas, pantalón negro, camisola coral. Cada uno con fondo de color acorde.
   - Nombre en Bodoni Moda 900 + subtítulo en Cormorant italic (material/tela)
   - Precio en rojo, formato "$78.000" (pesos argentinos)

6. **Manifiesto** (fondo oscuro): comilla gigante decorativa de fondo con opacity 0.08, blockquote centrado con Bodoni italic: *"Cada prenda es una escena, cada colección una película. Cosemos en Córdoba con la calma de un set y la obsesión de una directora de arte. Yegua no viste: pone en escena."* Firma "— Ailén & Emilia, directoras de vestuario".

7. **Newsletter** (fondo rojo `--yegua-red`): los bordes superior e inferior tienen perforaciones tipo ticket de cine (usá `radial-gradient` repetido para crear los agujeros). Adentro un **ticket de cine** en color papel con:
   - Header: "ADMIT ONE" + "Fila A · Butaca 07", separador con línea dashed
   - Título "Sumate a la próxima función" con scaleY
   - Subtítulo italic
   - Form con input email + botón negro "Reservar" (onsubmit cambia el texto a "¡Entrada reservada!")
   - Footer: "@yegua.studio" + "Córdoba · AR"

8. **Footer** (fondo ink): logo "Yegua Studio" enorme centrado con la misma técnica, links (Instagram, Envíos, Cambios, Mayoristas, Prensa), y "By @ailen.rausch & @emiliasalto · Córdoba, Argentina · © 2026".

### 3. Efectos y detalles obligatorios

- **Grano de película** global: un `body::before` con `position: fixed` de SVG noise (feTurbulence) en blend-mode overlay, opacity 0.12, z-index 9999. Esto le da textura vintage a todo.
- Todas las sombras de cajas, botones y tickets usan el estilo **neobrutalist** (offset sólido sin blur, como `6px 6px 0 #000`).
- Hover en productos: `translateY(-6px)` suave.
- Hover en CTA: se desplaza y la sombra crece.
- Todos los títulos de secciones usan un "kicker" previo en itálicas amarillas con guiones: `— Se levanta el telón —`.

### 4. Responsive

- Desktop: grilla de 3 columnas en colección.
- ≤ 900px: grilla de 2 columnas, nav desaparece, form del ticket vertical.
- ≤ 560px: grilla de 1 columna, padding de secciones reducido, countdown más chico.

### 5. Entrega técnica

- **Un solo archivo HTML** (todo inline: CSS y JS).
- La imagen del telón debe ir **embebida en base64** como `data:image/png;base64,...` dentro de una variable CSS `--curtain-bg`. NO uses rutas a archivos externos — tiene que abrirse en cualquier navegador sin dependencias.
- Idioma: español (rioplatense, tuteo/voseo: "sumate", "dejá", etc.).
- HTML semántico (`<section>`, `<article>`, `<blockquote>`, `<footer>`).

### 6. Tono y redacción

El copy tiene que sonar a marca chica, independiente, con personalidad. Usá referencias teatrales/cinematográficas: "función", "telón", "escena", "acto", "capítulo", "butaca", "vestuario", "directora de arte". No suene a e-commerce genérico.

---

**Importante:** Antes de escribir código, leé el SKILL `frontend-design` si lo tenés disponible. Generá TODO el HTML en un solo artifact/archivo. Si estás en Claude Code, guardalo como `yegua_studio.html`.
