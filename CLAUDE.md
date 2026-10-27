[claude.md](https://github.com/user-attachments/files/32530487/claude.md)
# Guía de referencia — Portfolio web de Carolina Picone

> Documento de contexto para nuevos chats. Resume las decisiones de diseño, estilo y funcionamiento ya definidas para el portfolio, a partir de la conversación donde se construyó la versión actual del sitio (`index.html`).

---

## 0. Flujo de trabajo (leer primero, en todo chat nuevo)

El portfolio vive en **GitHub**, en el repositorio `CarolinaPicone/miporfolio-carolinapicone`. Ahí están el `index.html`, la carpeta `assets/` con todas las fotos y videos, y este documento. GitHub es la única fuente de verdad: ya **no** se entregan archivos sueltos ni `.zip`, y no hace falta subir nada a la Base de Conocimiento de un Proyecto de Claude.

- **Carolina NO sabe programar ni tiene conocimientos técnicos.** Cualquier explicación sobre archivos, ramas o GitHub tiene que ser en pasos simples, sin asumir que entiende de código, carpetas de proyecto, rutas, etc.
- **Ramas:** cada chat trabaja en su propia rama (un "borrador"); `main` es la versión definitiva. Durante el trabajo, Claude sube los cambios a su rama. Cuando una sección queda terminada, Claude pasa ese trabajo a `main`, con el visto bueno de Carolina.
- **Material que sube Carolina:** sube las fotos y videos del trabajo de ese día (a `main` o a la rama del chat, por ejemplo en una carpeta tipo `assets/02-Nombre del trabajo/`). Claude los convierte a lo que use la web, con **nombres descriptivos y prolijos** (ej. `sombrerera-hero.jpg`, no el nombre original de la cámara), y los guarda en `assets/`.
- **Las imágenes y videos nunca van embebidos** dentro del `index.html` (nada de base64): siempre referenciados por archivo (`src="assets/nombre-del-archivo.jpg"`).
- **Para reemplazar una foto por una versión editada**, alcanza con subir el archivo nuevo con **el mismo nombre exacto** que usa la web (ej. `dualidad-hero.jpg`) en `assets/`: el código sigue pidiendo ese nombre y muestra la versión nueva.
- **Vista previa:** para que Carolina vea los cambios mientras se trabaja, Claude publica una vista previa privada de la web completa (un Artifact) y la actualiza con cada ronda de correcciones.

### Palabra clave de cierre: "listo"

Cuando Carolina escribe **"listo"** (con o sin punto) → Claude hace **directamente** la traducción al inglés de ese trabajo, **sin preguntar antes**, y la carga en la web (botón ES/EN) para que pueda verla en contexto. Si después Carolina quiere seguir haciendo cambios, se sigue trabajando normalmente.

### Traducción al inglés

- El sitio es bilingüe (selector ES/EN), pero las traducciones se van completando **de a un trabajo por vez, en el mismo chat donde se armó ese contenido** — no todas juntas al final en un chat aparte.
- Claude ofrece una primera versión en inglés; Carolina la revisa y la ajusta a su gusto (son decisiones de tono que le pertenecen a ella, no solo corrección idiomática). Sus correcciones se cargan tal cual.

## 1. Identidad visual

### Paleta de colores

| Uso | Color |
|---|---|
| Fondo del sitio (home, Sobre mí, Contacto) y de los trabajos de diseño | `#ffffff` (blanco puro) |
| Fondo de los trabajos que no son de diseño | `#000000` (negro) |
| Texto principal / tinta | `#15140f` |
| Texto secundario, títulos, etiquetas | `#8c8578` ("piedra") |
| Líneas, bordes, divisores | `#e7e4dd` |
| Placeholder oscuro (bloques de "Trabajos") | `#1c1b17` |
| Placeholder claro (bloques de "Trabajos") | `#f2f0ea` |
| Servicios (jerarquía más baja, "Sobre mí") | `#b3ada0` |

No hay ningún color de acento (rojo, azul, etc.) en la interfaz — toda la paleta es neutra (blanco/negro/piedra). El dinamismo del sitio viene del movimiento, no del color.

### Tipografías

- **Instrument Sans** (Google Fonts) — única tipografía tipeada del sitio. Se usa para absolutamente todo el texto: menú, párrafos de "Sobre mí" y "Contacto", servicios, info de ubicación/disponibilidad, etc. Pesos cargados: 400, 500, 600 e itálica 400.
- **Firma manuscrita** (imagen, no es una fuente) — el nombre "Carolina Picone" en el home. Existen dos variantes: una línea (nombre completo) y dos líneas ("Carolina" / "Picone", mismo tamaño de letra real, no de caja).
- **Logo/isotipo** (imagen, no es una fuente) — usado en "Sobre mí" y "Contacto", con efecto de giro y grosor 3D.

*(sin definir)* — Se probaron y descartaron dos alternativas antes de llegar a la firma-imagen: la tipografía "Professor" (no disponible) y "Brittany Signature" de dafont (de uso solo personal, no comercial). Ninguna de las dos se usa en la versión actual.

### Jerarquías tipográficas (valores reales del código — respetarlos a rajatabla)

Todo en **Instrument Sans**. Los tamaños con `clamp()` escalan con el ancho de pantalla (mínimo, ideal, máximo). Salvo pedido puntual de Carolina, cualquier elemento nuevo usa uno de estos niveles, con estos colores.

**Generales del sitio**

| Elemento | Tamaño | Peso / estilo | Espaciado | Color |
|---|---|---|---|---|
| Menú (Trabajos / Sobre mí / Contacto) | 11.5px | 400, MAYÚSCULAS | letter-spacing .1em | tinta `#15140f` |
| Selector ES/EN | 11.5px | activo 600 | .08em | inactivo piedra `#8c8578` · activo tinta |
| Home — "Diseñadora de Indumentaria" | 11px | MAYÚSCULAS | .1em | tinta |
| Home — rol rotativo | 13–15px `clamp(13px,1.3vw,15px)` | 400 | — | piedra |
| Home — url | 11.5px | 400 | .04em | piedra |
| Home / Contacto — ubicación y disponibilidad | 12px, interlineado 1.9 | 400; lugares en 600 | .04em | piedra; lugares en tinta |
| Etiqueta "[ Scroll ]" (hoy solo queda en 7600) | 11px | MAYÚSCULAS | .14em | piedra |
| Sobre mí — títulos "01 — Universo" | 13–18px `clamp(13px,1.6vw,18px)` | MAYÚSCULAS | .09em | piedra |
| Sobre mí — párrafos | 13–15px, interlineado 2 | 400 | — | tinta |
| Sobre mí — servicios | 13–15px | MAYÚSCULAS | .08em | `#b3ada0` |
| Copyright | 11px | MAYÚSCULAS | .06em | piedra |
| Contacto — mail, web, redes | 13–15px, interlineado 1.8 | 400 | — | tinta |

**Dentro de cada trabajo** (mismo esquema en todos)

| Elemento | Tamaño | Peso / estilo | Espaciado | Color (trabajo claro) | Color (trabajo oscuro: Sombrerera, 7600) |
|---|---|---|---|---|---|
| Título del trabajo | 34–64px `clamp(34px,4.6vw,64px)`, interlineado 1.02 | 500 | -.015em | tinta | blanco |
| Subtítulo (categoría + año) | 13–15px `clamp(13px,1.25vw,15px)` | 400; la categoría en `<em>` sin itálica | — | piedra; categoría en tinta | `#9a9488`; categoría en blanco (en 7600 el año va en blanco al 62%) |
| Crédito ("Co-creado por…") | 12.5–14px, interlineado 1.7 | 400 | — | tinta | blanco |
| Servicios / roles | 11.5px, interlineado 2.05 | 400 | .06em | piedra | `#9a9488` (7600: blanco al 62%) |
| Textos de concepto y proceso | 12.5–14px `clamp(12.5px,1.05vw,14px)`, interlineado 1.78–1.85 | 400 | — | tinta | `#d9d5cc` |
| Cita destacada (Sombrerera) | 15–22px, interlineado 1.65 | itálica 400 | -.005em | — | blanco |
| Texto de ficha técnica (geometral de Exprimir) | 12–13.5px, interlineado 1.62 | 400 | — | tinta | — |
| Pies de foto / créditos de foto | 11px | 400 | .04em | piedra | `#9a9488` |
| Etiqueta "click" que sigue al cursor | 10.5px | 400 | .1em | piedra | piedra |

**Excepciones ya pedidas por Carolina**

- **Dualidad Fusionada:** título y subtítulo van **en blanco** sobre la foto de portada (subtítulo en blanco al 78%, categoría en blanco pleno). Los servicios también van en blanco, pero con transparencia (blanco al 72%), para que queden un escalón por debajo del título y el subtítulo.
- **Fondos:** ver la regla de fondos en "Estilo general". Dentro de esa regla, Dualidad Fusionada tiene un matiz propio: el fondo pasa muy de a poco de blanco a `#f4f4f3` durante el concepto y queda así hasta el final (apenas más oscuro que el blanco de los figurines, `#f6f6f6`, para que no se pierdan; además llevan una sombra casi imperceptible). El menú va en blanco mientras está sobre la foto de portada y pasa a tinta al cruzar la prenda.

### Estilo general

Editorial, minimalista, mucho espacio en blanco.

**Regla de fondos (se repite en todo trabajo nuevo):**
- Home, "Sobre mí" y "Contacto": fondo blanco, siempre.
- **Trabajos de diseño** (indumentaria, colecciones — hoy los tres primeros: 01, 02 Dualidad Fusionada y 03 Un Mundo para Exprimir): **fondo blanco**, texto en tinta/piedra (columna "trabajo claro" de la tabla de jerarquías).
- **Trabajos que no son de diseño** (dirección de arte, dirección creativa, editoriales — hoy 04 La Sombrerera y 05 7600): **fondo negro**, a la inversa: texto en blanco / `#9a9488` / `#d9d5cc` (columna "trabajo oscuro"). Se agregan a `DARK_WORKS` en el código.
 Texto de navegación y etiquetas en mayúsculas, tamaño chico, letter-spacing amplio. Nada "tecnológico" ni futurista — el criterio explícito fue evitar que se sintiera como una web de producto de software. El carácter distintivo del sitio pasa por el movimiento (scroll con peso/inercia, transiciones lentas y continuas) más que por recursos gráficos.

---

## 2. Stack técnico

- **HTML + CSS + JavaScript puro**, un único archivo (`index.html`). Sin frameworks (no React, no Vue) y sin librerías de animación (no GSAP, no Framer Motion) — todo el movimiento está resuelto a mano con `@keyframes`/`transition` de CSS y bucles `requestAnimationFrame` en JS para lo que depende del scroll.
- Todas las imágenes y videos (firma, logo, fotos, videos) están en la carpeta `assets/` y el HTML los referencia por nombre de archivo; nada va embebido en base64.
- Única dependencia externa: Google Fonts (Instrument Sans), vía `<link>` en el `<head>`.
- Sin proceso de build, sin `npm`, sin dependencias.

### Estructura del archivo

```
<style> ... todo el CSS ... </style>
<body>
  #loader                     → intro
  .site
    header (nav)              → Trabajos / Sobre mí / Contacto / ES-EN
    #home                     → firma, rol rotativo, los 5 "trabajos" en la esfera
  #panel                      → contiene las 3 "placas" internas, todas en el mismo archivo:
    .panel-page[data-page="about"]
    .panel-page[data-page="contact"]
    .panel-page[data-page="work"]
  #aboutLogoLayer             → logo 3D, capa fija e independiente (compartida entre Sobre mí y Contacto)
  #clickReveal                → overlay blanco para las transiciones entre secciones
<script> ... toda la lógica ... </script>
```

### Convenciones de nombres

- Prefijos por sección: `about-*` (Sobre mí), `ci-*` (contact info, dentro de Contacto), `l3d-*` (capas del logo 3D), `rv-*` (animaciones de entrada reutilizables).
- IDs en camelCase para hooks de JS (`aboutTrack`, `logo3d`, `clickReveal`, `panelInner`, etc.).
- Variables CSS (custom properties) para valores reutilizados: `--white`, `--ink`, `--stone`, `--line`, `--nav-h`, `--sig-h`, `--sig-h-v1`.
- La navegación (Trabajos/Sobre mí/Contacto) son `<button>`, nunca `<a href>` — un link real dispara un aviso de "salir del sitio" en el visor de Claude; con botones no pasa.

---

## 3. Animaciones y transiciones estándar

### 3.1 Intro (loader)

- La web arranca con una **pantalla negra** (`#000`) y "carolinapicone.com" en el centro (12px, letter-spacing .08em, en blanco apagado por un velo negro al 62%). **No hay que hacer click en ningún momento de la intro**: a los 2 segundos sigue sola, y después avanza con el scroll.
- **El cursor "ilumina" el texto**: mismo efecto que el texto conceptual de La Sombrerera (un velo negro con un agujero difuminado que sigue al mouse), pero con un aura más chica (radio 100px, contra 190px en Sombrerera) porque es una sola frase. Cerca del cursor el texto se ve blanco.
- A los 2s: el texto se **funde** (0.8s) y no vuelve a aparecer, mientras arranca el zoom.
- Arranca un **zoom al revés**: lo que se veía negro era el logo ampliadísimo (desde el **centro del logo**: el punto del trazo más cercano a su centro); se retrae hasta quedar centrado sobre fondo blanco, **un 10% más grande** que en "Sobre mí" (`clamp(70px, 7.5vw, 110px)` × 1.1 de ancho, `introLogoW`). **En la intro el logo va en negro puro** (solo acá), para que no haya cambio de color entre la pantalla negra y el logo. Misma curva que el zoom de "Contacto", `cubic-bezier(.165,.84,.44,1)`, pero un poco más rápido: 3600ms (Contacto usa 4200ms) (la escala se interpola en forma logarítmica para que el alejamiento se vea parejo).
- **Mientras se retrae, gira** una vuelta completa sobre su eje vertical, con grosor 3D, igual que al entrar a "Sobre mí" (curva `cubic-bezier(.35,0,.25,1)`, 9px de grosor a su tamaño final): arranca plano, toma volumen al girar y, al terminar la vuelta, se aplana (450ms). En el canvas el grosor se arma dibujando el logo una vez y duplicándolo de costado (1, 2, 4, 8… px), no capa por capa: así no se traba.
- Para que no se "pixele" al quedar chico, el logo se guarda en versiones cada vez más chicas (la mitad cada una) y se dibuja la más cercana al tamaño en pantalla.
- Cuando frena, el logo **queda quieto** en el centro y **para entrar al home hay que hacer click en el logo** (cursor de mano). **Al pasar el cursor, el logo se levanta** como los trabajos del home o un poco más, pero con peso (crece hasta `LH_SCALE = 1.12` y sube 6px, yendo de a poco, `LH_LERP`). **Con el click, el logo se funde con el fondo** (900ms) y **entra el home como al volver de un trabajo**: entradas escalonadas y giro de la esfera.
- *(probado y reemplazado: intro por scroll — "[ Scroll ]", el logo agrandándose y subiendo con el scroll, los textos y los trabajos apareciendo con el scroll y "soltándose" en el giro. El código quedó guardado sin uso (`startScrollIntro`, constantes `SI_*`) por si se vuelve a usar.)*
- Al **volver de un trabajo** o de otra sección, el home entra como siempre (entradas escalonadas y giro de la esfera), no con esta intro.
- *(probado y descartado)* — fondo blanco con grano y estela del cursor ("no me gusta nada"); diluido del logo como acuarela (con y sin click); aura de blur con grano sobre el logo.

**Versión de referencia de la intro:** el commit `21a6597` guarda la intro con click en el texto para arrancar, el logo girando y quieto 1 segundo, y fundido al home.
- Técnica: el logo se dibuja en un `<canvas>` (no con `transform: scale`), porque parte de un zoom de cientos de veces y así no pierde calidad ni se traba.
- *(sin definir)* — la ubicación final de "carolinapicone.com" se va a pulir más adelante.

### 3.2 Transición entre secciones (la más usada — se dispara en cada click de navegación)

Es un **fundido simple a blanco y de blanco a lo nuevo** — la misma idea que el barrido de la intro, pero como cross-fade de pantalla completa. Se probó primero con un círculo que se expandía desde el punto de click (con difuminado tipo blur); se descartó por completo a favor de este fundido, que es más "común" y menos protagónico.

- Duración total: **1150ms** (constante `REVEAL_MS`), timing `ease`.
- El contenido cambia (se ejecuta el callback que abre la nueva sección) a los `REVEAL_MS - 200` ms, es decir, casi al final del fundido a blanco — así el cambio de contenido queda oculto bajo el blanco.
- Se usa para: click en Trabajos / Sobre mí / Contacto, click en cada trabajo individual, y las vueltas automáticas al home.

```javascript
const REVEAL_MS = 1150;
function sectionTransition(midCallback){
  clickReveal.style.display = 'block';
  clickReveal.style.transition = 'none';
  clickReveal.style.opacity = '0';
  clickReveal.offsetHeight; // forzar reflow
  clickReveal.style.transition = `opacity ${REVEAL_MS}ms ease`;
  requestAnimationFrame(() => { clickReveal.style.opacity = '1'; });
  setTimeout(() => {
    midCallback();
    clickReveal.style.transition = `opacity ${REVEAL_MS}ms ease`;
    clickReveal.style.opacity = '0';
    setTimeout(() => { clickReveal.style.display = 'none'; }, REVEAL_MS + 60);
  }, REVEAL_MS - 200);
}
```

### 3.3 Entradas escalonadas del home / paneles (clases `rv-*`, reutilizables)

Seis tipos de entrada distintos, cada elemento con su propio `animation-delay`, para que nada entre "en bloque".

```css
.rv{ opacity:0; }
html.revealed .rv-fade,  .panel.open .rv-fade { animation: fadeIn   .6s  ease forwards; }
html.revealed .rv-down,  .panel.open .rv-down { animation: fromDown .65s cubic-bezier(.22,1,.36,1) forwards; }
html.revealed .rv-up,    .panel.open .rv-up   { animation: fromUp   .65s cubic-bezier(.22,1,.36,1) forwards; }
html.revealed .rv-left,  .panel.open .rv-left { animation: fromLeft .65s cubic-bezier(.22,1,.36,1) forwards; }
html.revealed .rv-right, .panel.open .rv-right{ animation: fromRight .65s cubic-bezier(.22,1,.36,1) forwards; }
html.revealed .rv-scale, .panel.open .rv-scale{ animation: fromScale .7s cubic-bezier(.22,1,.36,1) forwards; }

@keyframes fadeIn{ to{opacity:1;} }
@keyframes fromDown { from{opacity:0; transform:translateY(-10px);} to{opacity:1; transform:translateY(0);} }
@keyframes fromUp   { from{opacity:0; transform:translateY(10px);}  to{opacity:1; transform:translateY(0);} }
@keyframes fromLeft { from{opacity:0; transform:translateX(-14px);} to{opacity:1; transform:translateX(0);} }
@keyframes fromRight{ from{opacity:0; transform:translateX(14px);}  to{opacity:1; transform:translateX(0);} }
@keyframes fromScale{ from{opacity:0; transform:scale(.96) translateY(6px);} to{opacity:1; transform:scale(1) translateY(0);} }
```

Se disparan agregando la clase `revealed` al `<html>` (home) o al abrir un panel (`.panel.open`).

**Entrada del home** (cada bloque distinto, en tiempo y en tipo de movimiento): menú desde arriba (0ms) · ES/EN fundido (250ms) · firma con una leve escala desde abajo (`rv-scale`, 450ms; se probó que se "escribiera" con un barrido y se descartó) · "Based in…" (800ms) y "Available…" (1000ms) desde la derecha, por separado · "Diseñadora de Indumentaria" desde la izquierda (1150ms) · rol rotativo desde abajo (1450ms) · url con un fundido largo (`rv-fade-slow`, 1.4s, desde 1750ms).

### 3.4 Trabajos del home (esfera que se gira arrastrando)

- Los 5 trabajos están repartidos sobre una **esfera invisible centrada en la pantalla** (radio `25.92vw`, entre 243 y 462px: dos veces un 10% más chica que la primera versión), **corrida un poco a la derecha** (centro al 56% del ancho, `SPH_CX`). El reparto es **a propósito desordenado pero equilibrado**: se descartó la espiral de Fibonacci porque, con algunos trabajos adelante, dejaba a los otros cuatro casi equidistantes (en cruz); y un reparto muy al azar dejaba un espacio grande vacío. Ahora, cada vez que se carga la página, se prueban repartos al azar y se ajusta el mejor de a poco, para que con **cualquier** trabajo adelante los demás queden con ángulos y distancias al centro distintos (irregular), pero sin huecos de más de ~115° ni todo cargado para un lado (equilibrado), sin que ninguno quede pegado a otro ni escondido detrás del de adelante. Referencia: el home de gionatannese.com.
- Se ven siempre **de frente**, como tarjetas (no se tuercen con la esfera). La profundidad se nota en el **tamaño** (adelante = tamaño actual de los recuadros, 342×274, un 10% más chicos que los 380×304 originales; atrás, la mitad) y en un **fundido en blanco** (los de atrás se van lavando hacia el blanco, hasta un 72%; **no** se vuelven transparentes, así no se ve lo que queda detrás de cada uno, y nunca desaparecen).
- Algunos trabajos pueden quedar cortados por el borde de la pantalla; está bien.
- **Siempre pasan por debajo de los textos del home.**
- **Se gira arrastrando** (mouse o dedo). El cursor es una mano abierta (`grab`) y se cierra al arrastrar (`grabbing`). Se "agarra" siempre la cara delantera: arrastrar a la derecha lleva lo de adelante a la derecha.
- **Sensibilidad:** liviana, sigue bien al mouse pero con un mínimo de peso (`SPH_SENS = 1`, `SPH_FOLLOW = 0.22`); al soltar sigue un poco por inercia hasta frenar (`SPH_FRICTION = 0.945`). Cuando nadie la toca, queda **quieta**.
- **La ruedita del mouse no hace nada** en el home (ya no hay scroll; se sacó la etiqueta "[ Scroll ]", el resto de los textos quedó en su lugar).
- **Al pasar el cursor**, solo se eleva (`scale(1.1)`) el trabajo que está **adelante** (casi sin fundido).
- **Click** (sin arrastrar): en el de adelante → abre el trabajo; en uno que está más atrás → la esfera gira (950ms) y lo trae **al centro**. Si hubo arrastre, el click no hace nada.
- **Entrada** (después de la intro y al volver al home): cada vez queda **un trabajo distinto al azar en el centro**. El giro alrededor de ese centro se elige para que los demás queden lo más despejados posible (menos superpuestos y menos cortados). La esfera llega girando **en diagonal** (entre horizontal y vertical) y frena en esa posición; **gira bastante** (`SPH_INTRO_A = 2.6` radianes, antes 1.9) en 2600ms (`easeOutCubic`). **No se tiene que notar un corte ni un comienzo:** mientras arranca, los trabajos **salen del blanco** (1.1s, `SPH_INTRO_FADE`), así el giro ya viene andando cuando se ven.

### 3.5 "Sobre mí"

- El **logo queda fijo en el centro de la pantalla** en todo momento, en una capa aparte (`#aboutLogoLayer`, `position:fixed`, fuera de cualquier contenedor con scroll — esto fue clave para que funcionara bien).
- Al entrar: el logo **gira sobre su eje vertical** con efecto 3D real (16 capas apiladas simulando un grosor de 9px, para que no se vea plano al girar). Una vuelta completa, 3s, `cubic-bezier(.35,0,.25,1)`.
- Al terminar el giro, el logo se **aplana de forma gradual** (las capas convergen a profundidad 0 en 450ms) — sutil, y calculado para terminar casi exactamente cuando arranca la caída del texto (mínima superposición). Una vez aplanado, las capas de más se ocultan para recuperar nitidez total.
- El texto entra como un **"scroll al revés"**: arranca mostrando la última línea del último párrafo y retrocede (`easeOutQuart`, 4200ms) hasta frenar mostrando solo el título "01 — Universo".
- Los párrafos se **abren alrededor de una elipse invisible** ajustada al logo (semiejes = mitad del ancho/alto del logo + 60px), línea por línea: cada línea se parte en dos mitades que se separan lo necesario para no tocar el logo. Abrirse es inmediato (nunca puede invadir la elipse); cerrarse es suave (lerp 0.06). Los 4 títulos (01–04) **no** se abren — pasan detrás del logo.
- El **copyright**, al alcanzar al logo durante el scroll, se "engancha" debajo de él como pie de foto (con 42px de separación) en vez de seguir desplazándose con el resto del texto.
- El scroll de esta sección **no es el nativo del navegador**: se maneja a mano (rueda del mouse → variable `aboutTarget` → lerp hacia `aboutCurrent`, factor 0.075) para tener control total del peso y evitar conflictos con otros gestos del sitio.
- **Ya no vuelve solo al home** (se sacó en todo el sitio): el scroll frena arriba en el principio y abajo cuando termina el texto. Al home se vuelve con el menú.

### 3.6 "Contacto"

Dos formas de entrar, mismo resultado final:

- **Desde el home:** mismo giro de logo que en "Sobre mí" → zoom.
- **Desde "Sobre mí"** (por el menú o clickeando el logo): si se scrolleó el texto, termina de caer y desaparece hacia abajo a **velocidad constante** (más rápido que antes: hasta 1.3s, lineal) → zoom. **Si no se scrolleó** (el texto está en su lugar del principio), **el zoom arranca enseguida**, sin esperar.

Zoom: el logo se agranda con `scale()` hasta que una banda vertical específica de la imagen —definida como fracción de su propia altura, `ZOOM_F1 = 0.09` a `ZOOM_F2 = 0.425`— llena la pantalla. Duración **3400ms** (un poco más rápido que los 4200ms de antes), `cubic-bezier(.165,.84,.44,1)`. El aplanado 3D→2D ocurre en el mismo instante que arranca el zoom, para que no se note el corte.

- "Sobre mí" en el menú cambia a **blanco** 2.1s después de arrancar el zoom (para tener contraste sobre el logo oscuro ya ampliado detrás).
- El contenido (tres bloques: email/web · Instagram/LinkedIn · ubicación/disponibilidad) aparece a los **2.5s** (antes 3.3s), cada uno con una entrada distinta y sutil (fundido / deslizamiento / ascenso), también un poco más rápida (.85s, escalonadas 100/240/380ms).
- Si estando ya en Contacto se vuelve a clickear "Contacto", el logo hace un **pequeño rebote** (escala a 0.985, 280ms) en vez de reiniciar toda la entrada.
- **Scrollear ya no devuelve al home** (se sacó el estirado en todo el sitio).
- Sin etiqueta "[ Scroll ]" (se sacó).

### 3.7 Final de cada trabajo: "[ Volver al home ]"

- El scroll normal **frena en un tope**, arriba y abajo, y ahí se queda.
- **Tope de arriba:** el principio del trabajo. **Tope de abajo:** donde termina la última foto (La Sombrerera y Dualidad Fusionada), el video final (7600), el final de las fotos (Nada es Plano; después de ver el video, la pantalla del texto manuscrito) y, en Un Mundo para Exprimir, cuando las tres fotos finales quedan centradas en la pantalla.
- **Ya no se sale estirando** (se sacó de todos lados, también de "Sobre mí" y "Contacto"). Cada trabajo tiene un **margen abajo de 64px** del color de su fondo (salvo 7600, donde el final es el video a pantalla completa y el texto va encima; en Nada es Plano el margen lo tienen las fotos). En los cinco trabajos, **al llegar al tope de abajo aparece "[ Volver al home ]"** (`#workHome`), muy sutil, en el centro del margen inferior (11px, .14em, mayúsculas; piedra en los trabajos claros, blanco al 50% en los oscuros; al pasar el cursor, tinta / blanco). Click → al home con el fundido. Se va ni bien se scrollea para arriba.

### 3.8 Notas por trabajo

- **01 Nada es Plano** (trabajo de diseño, fondo blanco; proyecto de graduación). Clases `nep-*`. Orden: inicial (video → foto de la IA) → concepto → cuaderno → colección → prendas → fotos → "[ Ver video ]" → video → texto manuscrito.
  - **Versión anterior guardada:** el commit `910bdae` (tag `version-anterior-nada-es-plano`) es como estaba antes de este cambio (foto de la IA después del cuaderno, fotos sobre bordó, texto manuscrito en blanco). Si Carolina dice "volver a la versión anterior", se vuelve a esa.
  - **Se acomoda solo** (para bajar **y para subir**, a la inversa): al acercarse con el scroll a ciertos puntos, el recorrido termina solo y frena ahí; después se sigue scrolleando normalmente. **El comienzo no se tiene que notar:** el recorrido automático arranca con la misma velocidad que traía la ruedita y termina frenando suave (una curva continua, `nepGlideTo`); si se scrollea para el otro lado mientras se acomoda, se corta y sigue el scroll normal. Puntos (`at / before / after / msDown / msUp`): **pregunta del concepto** en el centro (al bajar, desde que el degradé de la foto ocupa media pantalla, 1.8s; al subir, 0.9s); **los dos primeros párrafos del cuaderno** en el centro, con el cuaderno asomado (1.6s); **los otros dos párrafos** en el centro (con el próximo scroll, 1.7s; después, scroll normal y el cuaderno se va); y, ya visto el video, **entre el final de las fotos y la pantalla del texto manuscrito** (un solo movimiento, 1.6s). **Centrado muy leve (la colección y las prendas):** no corta el scroll ni lo frena; solo cuando se deja de scrollear (200ms quieta la ruedita) con la sección ya casi en el centro (a menos de un 16% del alto de pantalla), termina sola el recorrido despacio (curva que arranca y frena suave, ~0.9–1.2s; `nepSoftFrame`); cualquier movimiento de la ruedita lo suelta enseguida. Las prendas se centran tomando el centro de las partes de arriba.
  1. **Inicial:** al abrir el trabajo se reproduce el video `nada-es-plano-video.mp4` (5s, sin sonido, a pantalla completa, sin textos; **la barra del menú queda siempre a la vista**; mientras dura no se puede bajar). Cuando le faltan **1.4s**, empieza un **zoom a las caras de las chicas** (hacia 1.42, en 1.7s, con una curva que **nunca frena antes del paso a la foto**: antes frenaba justo cuando arrancaba el paso y se notaba el corte) (punto de apoyo: el medio entre las dos caras, `NEP_FACES`), con el video todavía en movimiento; **se ve el video casi hasta el final** (la chica de la derecha mira hacia adelante) y cuando le faltan **.42s** (se recortan esas décimas, así nunca se ve el último cuadro frenado) pasa a la foto de la IA **sin que se crucen las dos imágenes y rápido, continuo**: el video, todavía acercándose, se aclara hacia los tonos de la foto, se desenfoca apenas y se cubre con el color liso del fondo de la foto (.36s) y, sin quedarse quieto, ese color se va (.5s) y aparece la foto (que se acomoda apenas, de un 3.5% más grande a su tamaño). *(probado: fundido directo video → foto; se veían las dos imágenes cruzadas.)* **Foto de la IA** (`nada-es-plano-ia-creativa.jpg`, extendida recreando su fondo: lienzo de 2400×1840, la foto original en 200,362, sin tocar a las personas): mide un 93.6% del alto de la pantalla (sin pasarse del 95% del ancho), centrada, con los bordes fundidos con su **fondo liso** (`nada-es-plano-ia-creativa-fondo.jpg`, sacado de los bordes de la foto). Ese fondo **sigue hacia abajo** en su mismo color y **se aclara muy de a poco hasta el blanco** (degradé con curva suave, `--nep-ini-g = 58vh`), sin cortes. **Título y subtítulo**: sobre la foto, **arriba de las cabezas de las dos chicas agachadas**, centrados entre las dos que están paradas, apenas a la izquierda (`NEP_HEAD_X = 1628`, entre la posición original 1640 y la de 1615) (a la altura de sus cabezas, donde hay más lugar); si en una pantalla angosta el título no entra entre el pelo de las dos, se achica lo justo. El **año ("2026") y los servicios** van un poco más oscuros que el piedra (`#5e594f`, sin llegar a negro). **Servicios y pie de foto intercambiados** (para probar): los **servicios abajo a la derecha**, alineados a la derecha, a 32px del borde (lo mismo que las letras del menú del borde de arriba); el **pie de foto** "IA creativa @studio.joaquina" (11px, .04em, `#6f685c`) **abajo a la izquierda**, donde estaban los servicios. Los textos aparecen cuando el fundido ya casi terminó (sin animación de entrada). *(probado y descartado: la última imagen del video transformándose como un líquido en las letras, con WebGL; video que se fundía en blanco con los textos sobre blanco; la foto de la IA como sección aparte después del cuaderno — es la versión anterior guardada.)*
  2. **Concepto:** arranca **recién cuando el fondo de la foto de la IA se fundió del todo con el blanco** (ocupa un viewport totalmente en blanco; la separación con la parte inicial la da el degradé, `--nep-ini-g = 58vh`, un poco más corto que antes). **Ni bien el degradé ocupa media pantalla, se desliza solo hasta la pregunta** (1.8s). **El texto se mueve con el mismo peso que el resto de la web** (`NEP_WEIGHT = NEP_Q_WEIGHT = 1`, sin retraso propio; antes era más pesado y se notaba raro). Mientras dura, la pantalla queda quieta y el scroll mueve el texto. **Sin cilindro**: las líneas son planas y **aparecen y desaparecen fundiéndose con el fondo**. Primero aparece **la pregunta sola** ("¿Cómo es posible…?"), en Instrument Sans itálica, en tinta, `clamp(22px,2.5vw,36px)`: se va **"apoyando" letra por letra** a medida que llega al centro, **se acomoda sola en el centro**, se queda un momento quieta y se va fundiéndose con el fondo. Después, los párrafos (columna de `min(60ch,80vw)`, más ancha para que no queden líneas finales muy cortas): **centro nítido de 5 líneas** (`NEP_LINES`); por arriba y por abajo cada línea se funde (`NEP_FADE`). Texto centrado.
  3. **Cuaderno** (arranca **ni bien se va la última línea del concepto**). Toda la sección es **un poco más pesada** (`NB_WEIGHT = 1.25`) para que el cuaderno se mueva más sutil. Fotos `nada-es-plano-cuaderno-N.webp` (fondo transparente, marco común de 2000×1700, lomo en el centro; **se les sacó la tela traslúcida que colgaba por debajo** —la cinta naranja quedó, completada donde la tapaba la tela—, **la tapa y la contratapa están recreadas como un objeto gráfico: un naranja plano (`rgb(212,88,40)`, menos brillante que antes), sin las sombras oscuras de las esquinas ni textura; solo quedan los detalles finos (el elástico, los bordes)**; los papeles y la cinta naranja de abajo quedan como estaban; el borde naranja de las páginas abiertas, igual de plano (el contraste "de foto" no le gustó), y el interior tiene **un poco más de contraste, también más plano**. En la página 6 (que ahora va **antes** que la 4: se intercambiaron la última y la anteúltima página abierta), sobre el papel suelto blanco de la izquierda hay **una foto de la producción impresa en papel** (la de la chica caminando), un poco más chica que el papel, girada como él y sin salirse, con una sombra suave). **Se usan seis:** tapa (1) · 2 "Avíos" · 3 "Despiece" · 6 bocetos (con la foto impresa) · 4 triángulo verde · contratapa (8) (`NB_PAGES`). La tapa mide un 60% del alto de la pantalla. Sobre el margen derecho, **bocetos del proceso** (`nada-es-plano-proceso-bocetos.webp`, su final se funde con el fondo): **son lo primero que aparece** (entran por abajo ni bien termina el concepto) y suben con el scroll. Los **cuatro párrafos** que lo acompañan van **alineados a la izquierda y del mismo ancho** (`min(49ch,37vw)`). Recorrido (todo con la sección fija en la pantalla):
     - **a.** Los **dos primeros párrafos arrancan a la mitad del alto de los bocetos** (todo el texto queda por debajo de esa mitad), suben a la par de ellos, **más a la izquierda**, y se acomodan solos en el centro (de alto).
     - **b.** Todo el movimiento del cuaderno es **más sutil** (curvas que arrancan y frenan muy de a poco). **Empieza a salir un poco antes de que los dos primeros párrafos lleguen al centro** (medio alto de pantalla antes, `a0 = t1 - vh·0.5`: con los primeros párrafos en el centro, el cuaderno ya asoma apenas): con el próximo scroll, los primeros se van por arriba (empujados por el cuaderno hacia el centro mientras se van), los **otros dos** llegan al centro en la misma columna y el cuaderno llega **asomado** (se acomoda solo, 2.1s); los bocetos frenan.
     - **c.** Después **el scroll sigue normal** (la sección se suelta): el texto y los bocetos suben con la página sin moverse de costado, y el cuaderno **se va por donde entró, en línea recta** (se queda a la misma altura en la pantalla y sale hacia la izquierda, el mismo recorrido y la misma curva suave; el escenario solo recorta a los costados, así no se corta abajo mientras sube la colección). Derecho a la colección.
     - **d.** **El click (la "apertura") solo funciona con los otros dos párrafos en el centro.** Con un click (asomado): el cuaderno va **al centro del lado izquierdo**, **se achica un 15%** (`NB_SHRINK`), **empuja el texto hasta la columna de la derecha** y **los bocetos se corren a la derecha hasta salir de la pantalla** (1.7s, `NB_OPEN_MS`). Ahí, cada click **pasa una página** (hoja que gira sobre el lomo, .72s; las páginas de abajo pasan con un fundido). En la **contratapa ya no se puede hacer click**: **"[ Scroll ]" está detrás de la tapa**, centrado en el lado derecho, y **se destapa al pasar la última página**; va corrido hacia afuera (al 70% del ancho de la tapa). Más chico y más sutil que el de la intro (9.5px, `#b3ada0`).
     - **e.** **Con el scroll para abajo, después del click:** se va igual que en c. (volviendo a su tamaño), **mostrando la contratapa**; "[ Scroll ]" **se desvanece rápido**; el texto queda donde está. Si está en una **página del medio**, primero **se cierra hacia la tapa** (rápido). **Para subir**: primero se cierra y **vuelve a quedar asomado** (el texto y los bocetos vuelven a su lugar), así nunca queda en el medio de la pantalla encima de los primeros párrafos. Fuera de esa sección, el cuaderno no está o está asomado a la izquierda: si se sube de cualquier forma (aunque sea rápido), se cierra y vuelve a quedar asomado, y los bocetos vuelven a su lugar (el texto y los bocetos se mueven con un poco de peso, así nunca saltan). Cuando ya salió de la pantalla, **vuelve solo a la tapa y deja de estar abierto**.
  4. **Colección** (scroll normal; **con 40vh de separación** después de los últimos párrafos del proceso; fondo blanco): a la izquierda, **grande** (`min(53.2vw, 79.8vh·1.414)`), los geometrales de las 15 prendas, **cada una por separado** (`nada-es-plano-coleccion-01..15.webp`, de los archivos "1Recurso 1–15" de Carolina, **ya exportados en 3x**, con sus variaciones de color), ubicadas cada una en su lugar de la lámina completa (2000×1414; las posiciones se buscaron comparando con la lámina original). **De a una y al azar, cada prenda se levanta apenas y vuelve a bajar** (sube 3px y crece apenas un 1.2%, con una sombra muy leve, 1.3s; como el logo de la intro al pasar el cursor pero con un recorrido mucho más corto); **poco movimiento: una por vez, con pausas, y como mucho dos casi al mismo tiempo**; la misma prenda no se repite enseguida; solo mientras la colección está en pantalla; a la derecha el texto (de Carolina): "La colección reúne quince prendas desarrolladas a partir de una búsqueda simultánea de color, texturas, estampados y moldería…" / "Los prototipos permitieron llevar estas búsquedas al cuerpo…" (2 párrafos, alineado a la izquierda; "quince" en palabras, también en "De las quince prendas…"). **Calidad:** las prendas sueltas vinieron más chicas de lo que se ven en la lámina; para que se vean nítidas conviene que Carolina las exporte desde Illustrator ("Exportar para pantallas" → Recursos) en **PNG a escala 3x**, sin prefijo y sin sufijo, y las suba con los mismos nombres (lo mismo para los "Recurso 1–4" de las prendas materializadas).
  5. **Las cuatro prendas materializadas** (un viewport): chaqueta verde, pantalón verde, camisa estampada, pantalón estampado (`nada-es-plano-prenda-1..4-frente/espalda.webp`, de los archivos "Recurso 1–4" que pasó Carolina con el color corregido: 1 camisa matices, 2 pantalón dual, 3 pantalón vestigio, 4 chaqueta vestigio; frente a la izquierda y espalda a la derecha en cada archivo; quedan del mismo tamaño que antes). **En una sola fila**, repartidas de forma pareja en el ancho, con su espalda asomando por detrás (a la derecha y apenas más arriba, con sombra leve). **No están centradas en alto**: las partes de arriba y los pantalones **arrancan a la misma altura** (el cuello de unas al nivel de la cintura de los otros). Tamaño: **un 20% más alto** que la versión anterior (`--pz-k`), salvo que no entre a lo ancho de la pantalla: ahí se achica lo justo (en una pantalla de 1440px de ancho queda casi igual que antes). **Al pasar el cursor** por una prenda: las de arriba **bajan** y los pantalones **suben** (`--pz-d`, sin salir de la pantalla), y en el lugar que dejan aparece **su descripción** (título en MAYÚSCULAS 11.5px .09em + texto 12–13.5px, interlineado 1.62, **centrado en el espacio de la delantera con la espalda y un poco más angosto (90%)**, y bien separado de la prenda: el de las partes de arriba termina a 40px de la prenda ya bajada y crece hacia arriba; el de los pantalones arranca a 40px del pantalón ya subido; así nunca se pisa con las prendas), y al final **"Ficha técnica"** con un ícono de descarga fino al principio (11px, .06em, tinta; al pasar el cursor se aclara): descarga el PDF de la ficha (`nada-es-plano-ficha-chaqueta-vestigio / pantalon-vestigio / camisa-matices / pantalon-dual.pdf`; en los PDF se cambió "Modelo:" por el nombre nuevo de cada prenda, con la misma tipografía del PDF, y en los pantalones "tiro medio" por "tiro bajo"). Nombres y textos (de Carolina): **Chaqueta Vestigio**, **Pantalón Vestigio**, **Camisa Matices**, **Pantalón Dual**. Mientras una está abierta, el hueco entre la prenda y su texto también cuenta como "encima". El texto del **último pantalón** es más ancho hacia la derecha (100% en vez de 90%), lo justo para que quede una línea menos. Se puede leer **una sola a la vez**; al salir de la prenda o de su texto vuelve. **Se abre más rápido (.7s) de lo que se cierra (1.15s)** y **sigue al cursor**: si se va antes, vuelve desde donde estaba.
  6. **Fotos** (sobre **blanco**, sin bordó; **42vh en blanco** las separan de las prendas: un poco más que entre la colección y las prendas): las fotos de la producción (`nada-es-plano-foto-01..10.jpg`; **02, 04, 08 y 10 ya son las editadas** por Carolina —`irisywan2-1`, `iris1-1`, `irisywan4-1`, `irisywan3-1`—; cinco recortadas en vertical; la **08** —la chica de verde sentada y la de espaldas— recortada arriba y a la izquierda para que no se vea la sombrilla amarilla, sin cortar los pies de la chica sentada, en la misma proporción 3:2), **de borde a borde y separadas 10px** (como las fotos finales de Un Mundo para Exprimir), bordes apenas redondeados (3px), sin sombra. Se arman en **dos bloques** (uno arriba del otro, separados por una **línea recta**); cada bloque, en **columnas de distinto ancho** (cada foto, del ancho de su columna) que **arrancan y terminan parejas**: así el principio y el final son rectos y ninguna "línea" tiene más de cuatro fotos (las fotos quedan unas más arriba y otras más abajo, sin filas definidas). Bloque de arriba: 03-04-10 · 02-05 · 07-06; bloque de abajo: 09 · 08 · 01 (`data-b` / `data-c` en el HTML; las medidas las calcula `nepPhLayout`). **Créditos de las modelos encima de las fotos**, centrados cerca del borde de abajo (a 14px), en las dos fotos de los costados de la última línea (11px, .04em, piedra clarito `#d9d5cc` al 55%: apenas se leen): la 09 (camisa bordó) "modelo @wandita.s.r_" y la 01 (campera verde) "modelo @iridisenteh" (`data-cap` en el HTML; en inglés "model"). **Al entrar a las fotos, la barra del menú se va, sutil** (.9s), y vuelve al subir. **Click en una foto → se ve completa**, lo más grande posible dejando aire (84% de la pantalla), con el fondo difuminado; otro click (o Esc) la cierra.
  7. **"[ Ver video ]" + video + texto manuscrito:** el **tope de abajo** es el final de las fotos (con un margen blanco de 64px debajo, donde aparece "[ Volver al home ]"). **Si estando en el tope se sigue scrolleando para abajo** (sin que el tope se mueva ni rebote), aparece **"[ Ver video ]"** **en el margen de abajo, apenas debajo de la última foto, centrado** (donde antes estaban los créditos; "[ Volver al home ]" queda debajo, en el mismo margen; antes aparecía en la línea entre los dos bloques de fotos, que se abrían 50px: ya no se abren, `NEP_END_OPEN = 0`) (11px, .14em, piedra; al pasar el cursor, tinta), **"escribiéndose"** como el texto manuscrito (de izquierda a derecha, borde muy difuminado, subiendo apenas). Queda abierto **hasta que se sale de esa pantalla con el scroll** (ahí se cierra; al volver, se abre de nuevo con otro scroll en el tope). Click → **el video** (`nada-es-plano-video-final.mp4`, con sonido, **a todo el ancho de la pantalla**; la marca de agua "clideo.com" se borró **sin recortar el cuadro**) **aparece sutil sobre negro** (mientras se ve, la barra del menú se va); al terminar, o con un **click en cualquier lugar en cualquier momento** (o Esc), **se funde en blanco** y queda **la pantalla del texto manuscrito** ("Tener matices es tener profundidad…", `nada-es-plano-manuscrito.png`, **en negro**, `min(44vw,760px)`, centrado), que **aparece sutil, sin golpe: de difuminado a nítido en ~1.5s (1.4–1.8s), subiendo apenas 8px**, arrancando .4s después del blanco (antes se escribía línea por línea y se veía raro; después apareció demasiado de golpe, en <1s; y con 3s tardaba demasiado). **Esa pantalla pasa a ser el nuevo tope** (solo se llega viendo el video). Desde ahí, **un solo movimiento para arriba** vuelve solo al final de las fotos, con "[ Ver video ]" a la vista; **y la pantalla del texto se bloquea otra vez**: solo se llega a ella viendo el video.
  - **Tarjetas: sin uso por ahora.** Las tres tarjetas que se dan vuelta (arte @sven_pfrommer / @origersht / @alekustn, dorsos "Matiz Irruptivo", "Reverberante Eco", "Albor Indómito") quedaron **guardadas en el código** dentro de un `<template id="nepCardsTpl">` (no se muestra), con su CSS y JS. **Si Carolina escribe "agregar tarjetas"**, se vuelven a usar tal cual estaban (2/3 del tamaño original +15%, equidistantes, bordes de 5px, giro 3D de .95s con 12px de grosor, una sola dada vuelta a la vez).
  - **Inglés (primera versión, a revisar por Carolina):** ya está cargado (botón ES/EN). Concepto: `data-en-text` en la pregunta y los párrafos (el JS los rearma al cambiar de idioma, `nepApplyLang`); proceso y colección: un `<div data-es>` y un `<div data-en>` con los párrafos; prendas, subtítulo, pie de foto, créditos, "Ver video" y "Ficha técnica": `<span data-es>` / `<span data-en>`. El título "Nada es Plano" y los nombres propios de las prendas (Vestigio, Matices, Dual) quedan en castellano: "Vestigio Jacket", "Vestigio Trousers", "Matices Shirt", "Dual Trousers".
- **05 7600 — portada congelada y cortina negra:** al scrollear, la portada queda fija y la cortina negra sube desde abajo hasta dejar la portada visible solo en **menos de un cuarto de la pantalla, arriba** (el negro pleno arranca al 19% del alto; antes 24%, se achicó un poco más). El fundido entre portada y negro mantiene siempre la misma curva; su largo (`--alb-g`, hasta 340px) se ajusta al alto de la pantalla y, si hace falta, arranca apenas por encima de la pantalla para no comprimirse.

### 3.9 Celular (versión móvil, hasta 760px de ancho) — se hace por partes

Regla: en el celular **no se cambia ningún contenido ni información**, solo ubicación y tamaño cuando hace falta, respetando estrictamente la estética. Vista previa aparte para Carolina: un Artifact "Portfolio en el celular" que muestra la web dentro de un celular (iPhone 15 393×852, iPhone SE 375×667, Android 412×915) con botón para verla de nuevo desde la intro (la web va como `sitio.html` y las fotos/videos se copian de la vista previa principal).

- **Parte 1 (hecha): intro, menú y home.**
  - **Menú:** la misma fila (TRABAJOS · SOBRE MÍ · CONTACTO), alineada a la izquierda a 20px, con ES/EN a la derecha (centrada no entra). Barra de 60px de alto. En celulares angostos (≤370px, iPhone SE) las palabras van un poco más juntas (11px, .07em) para que entre en una fila.
  - **Home:** los trabajos son lo central. Después de la intro, la **firma aparece en el centro** (1.45 veces su tamaño final) con **"Diseñadora de Indumentaria" centrado debajo**, se queda un momento (hasta 2.6s, `MOB_SIG_HOLD`) y **se achica hasta su lugar arriba a la izquierda** (1.15s); el subtítulo se va mientras tanto y no queda en la esquina (sería demasiado chico al lado de la firma). Recién ahí **entran los trabajos girando**. Al volver de una sección, la firma ya está en su esquina (entrada normal). El **rol rotativo y la url no se muestran** en el home del celular (para que no compitan con los trabajos). **"Based in… / Available…"** en la esquina de abajo a la derecha, como en la web.
  - **Esfera:** se gira con el dedo igual que con el mouse (mismo peso e inercia; tocar uno de atrás lo trae al centro, tocar el de adelante lo abre). En el celular está **centrada a lo ancho**, en el medio del lugar libre entre la firma y "Based in"; radio = 50% del ancho; recuadros de 52% del ancho (máx. 250px, misma proporción); y **estirada a lo alto** para ocupar ese lugar libre (entre 0.85 y 1.45 veces, `sphYS`), sin cortarse a los costados ni pisar los textos de abajo.
- **Decisiones ya tomadas para las partes que siguen:**
  - **Las cuatro prendas de Nada es Plano:** una por pantalla, **se pasan deslizando hacia el costado**; tiene que notarse que se puede deslizar: **las otras prendas asoman muy levemente a los costados**, sin quitarle protagonismo a la del centro. El texto se abre al tocar.
  - **La Sombrerera:** el aura de luz del texto **sigue al dedo** (aparece donde se apoya y lo sigue; al soltar se queda un momento y se apaga despacio).
- **Pendiente:** Sobre mí y Contacto, y los cinco trabajos (todavía funcionan con la ruedita del mouse: en el celular hay que hacer que se recorran con el dedo).

---

## 4. Tono y estilo de escritura

- **Primera persona**, tono conceptual y reflexivo. El eje es "cómo pienso", no "qué hago" — evita hablar de moda/prendas como fin en sí mismo.
- Evita clichés típicos de portfolio de diseño de indumentaria ("mi pasión por la moda desde chica", etc.).
- Estructura argumentativa: por qué investiga, cómo traduce ideas en decisiones, por qué valora la coherencia por sobre el gusto personal.
- Vocabulario conceptual recurrente: *universo, narrativa, lenguaje, intención, sistema*.
- Frases relativamente largas, con oraciones subordinadas encadenadas por comas — un tono más cercano al ensayo breve que al copy publicitario.

*(proceso definido, ver sección 0)* — La traducción al inglés se hace de a un trabajo por vez, al cierre de cada sección: Claude ofrece una primera versión y Carolina la revisa/ajusta. No se hace todo junto al final del sitio.

---

## 5. Estructura general del sitio

Todo vive en un **único `index.html`**, sin páginas separadas ni rutas — la navegación es 100% interna vía JavaScript, mostrando/ocultando "placas" (`.panel-page`) superpuestas.

1. **Home** — firma **en dos líneas** (elegida por Carolina; la de una línea quedó guardada sin uso; el punto de la "i" de "Picone" se acercó a la mitad de la distancia que tenía, y "Carolina" bajó lo mismo; después, el punto de la "i" de "Carolina" también se acercó a la mitad de su distancia, bajó 60px en `firma-carolina.png`), rol rotativo ("Dirección creativa", "Diseño de indumentaria", etc.), url, info de ubicación/disponibilidad (siempre en inglés), y los 5 "trabajos" sobre una esfera que se gira arrastrando con el mouse (ver 3.4).
2. **Trabajos** (dentro del home) — cada uno de los 5 recuadros es clickeable y abre una placa individual. *(sin definir)* — hoy el contenido es un placeholder ("Funcionó"); falta diseñar cómo se ve el interior de cada proyecto.
3. **Sobre mí** — logo centrado + 4 bloques numerados (01 Universo, 02 Curiosidad, 03 Intención, 04 Forma) + lista de servicios + copyright.
4. **Contacto** — logo ampliado (zoom) + email/web, redes, ubicación/disponibilidad + copyright.

**Navegación:** header fijo arriba con Trabajos / Sobre mí / Contacto + selector ES/EN, todo con `<button>`.

---

## 6. Otras reglas o preferencias importantes

- **Sin teléfono ni WhatsApp visibles** en Contacto — decisión de privacidad explícita de Carolina.
- **Dominio pensado:** `carolinapicone.com`. *(sin definir)* — todavía no se compró ni se conectó; quedó pendiente para cuando el diseño esté cerrado.
- **Redes confirmadas:** Instagram `@caropicone` → `instagram.com/caropicone`; LinkedIn → `linkedin.com/in/carolina-picone-680a20331`.
- **Mail de contacto:** `carolinapicone.t@gmail.com`.
- Los 5 bloques de "Trabajos" en el home son placeholders (patrón diagonal gris/negro) — *(sin definir)* faltan las imágenes reales de cada proyecto.
- **Miniatura de Un Mundo para Exprimir en el home:** `exprimir-thumb.jpg`, recorte de `exprimir-final-3.jpg` (la nena sentada en la escalera), centrada en ella, en la proporción del recuadro (1.25): corta las piernas un poco antes de la botamanga naranja del jardinero (que no se ve), con un zoom apenas mayor (8%) para que la cabeza quede a la misma distancia del borde de arriba (~6%). (Se probó cortar debajo de la cintura: demasiado.) **La escalera está retocada para que se vea nueva**: sin rayones, gastado ni manchas (se suavizó solo a lo largo de las tablas, así quedan la veta y los cantos; la nena y los bordes verticales —pared, columna, costados— no se tocan).
- **Miniatura de Nada es Plano en el home:** `nada-es-plano-thumb.jpg`, de la foto editada `irisywan4-1.JPG` (la chica de verde sentada y la de espaldas), con **la sombrilla amarilla pasada a blanco** (como las sillas, conservando sus pliegues y sombras). **El original `irisywan4-1.JPG` queda en la raíz del repositorio a pedido de Carolina: no borrarlo.**
- **Proyectos a incluir** (según el brief inicial de Carolina, no necesariamente en este orden): *"Nada es Plano"* (proyecto de graduación), *"Dualidad Fusionada"* (puerto de trabajo vs. universo náutico recreativo de Mar del Plata), un proyecto de indumentaria infantil (deliberadamente discreto, va último — no representa su estética pero muestra versatilidad técnica), dirección artística de un cortometraje, dirección creativa de la producción visual de un álbum musical.
- **Metodología de trabajo que funciona bien con Carolina:** cuando algo no queda en el lugar exacto que imagina, suele mandar una captura de pantalla con una grilla o bloques de color marcando la posición exacta en píxeles — es el método más efectivo para ajustes finos de ubicación, más que las descripciones en palabras.
- Cuando algo no funciona como se esperaba, prefiere que se le explique la causa técnica real (qué pasó y por qué), no solo que se corrija en silencio.
- **Archivos que ya no se usan se borran:** todo lo que Carolina suba al repositorio (fotos, videos, carpetas con el material original) y que después ya no use la web —porque se convirtió a otro formato, se renombró con un nombre descriptivo o se descartó— se elimina directamente, sin preguntar. Pero **siempre se le informa** qué se borró y por qué.
- Fondos: **regla no negociable** — blanco para el sitio y los trabajos de diseño, negro para los trabajos que no son de diseño (detalle en "Estilo general").

---

## Campos sin definir — pendientes de tu parte

Estos son los puntos donde no había información clara en la conversación y que conviene definir antes (o durante) de seguir avanzando:

1. **Contenido y diseño de cada placa de "Trabajo" individual** — hoy es un placeholder con el texto "Funcionó".
2. **Imágenes reales** para los 5 recuadros de trabajos del home (hoy son bloques de color placeholder).
3. **Contenido en inglés de cada sección** — el proceso ya está definido (ver sección 0), pero el texto en sí se va completando trabajo por trabajo, así que en cualquier momento puede haber secciones todavía sin su versión en inglés revisada.
4. **Compra y conexión del dominio** `carolinapicone.com`.
5. **Estética y estructura interna** de las páginas de cada trabajo (todavía no se diseñaron).
6. **Posiciones finales exactas** de los tres bloques de "Contacto" (email/web, redes, ubicación) — se ajustaron a ojo en varias rondas sobre un tamaño de pantalla específico; conviene revisarlas en dispositivos/resoluciones reales.
7. **Encuadre final del zoom del logo en "Contacto"** — quedó en un valor razonable, pero es el tipo de detalle visual que suele necesitar un último ajuste al verlo en vivo.
