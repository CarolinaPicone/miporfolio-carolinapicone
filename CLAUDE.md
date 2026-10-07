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
- Arranca un **zoom al revés**: lo que se veía negro era el logo ampliadísimo (desde el **centro del logo**: el punto del trazo más cercano a su centro); se retrae hasta quedar centrado sobre fondo blanco, del mismo tamaño que en "Sobre mí" (`clamp(70px, 7.5vw, 110px)` de ancho). **En la intro el logo va en negro puro** (solo acá), para que no haya cambio de color entre la pantalla negra y el logo. Misma curva que el zoom de "Contacto", `cubic-bezier(.165,.84,.44,1)`, pero un poco más rápido: 3600ms (Contacto usa 4200ms) (la escala se interpola en forma logarítmica para que el alejamiento se vea parejo).
- **Mientras se retrae, gira** una vuelta completa sobre su eje vertical, con grosor 3D, igual que al entrar a "Sobre mí" (curva `cubic-bezier(.35,0,.25,1)`, 9px de grosor a su tamaño final): arranca plano, toma volumen al girar y, al terminar la vuelta, se aplana (450ms). En el canvas el grosor se arma dibujando el logo una vez y duplicándolo de costado (1, 2, 4, 8… px), no capa por capa: así no se traba.
- Para que no se "pixele" al quedar chico, el logo se guarda en versiones cada vez más chicas (la mitad cada una) y se dibuja la más cercana al tamaño en pantalla.
- Cuando frena, el logo **queda quieto** y aparece **"[ Scroll ]"** abajo al centro (a 28px del borde; 11px, MAYÚSCULAS, .14em, piedra — el estilo que tenía en los paneles), con un fundido.
- **Desde ahí la intro sigue con el scroll** (`SI_*` en el código, con el mismo peso que el resto del sitio):
  - "[ Scroll ]" se funde y desaparece del todo a los **30px** de scroll.
  - El logo **se agranda a la vez que sube**, hasta irse de la pantalla (se redibuja nítido en cada cuadro). El movimiento que sigue al scroll es el **zoom** (`SI_GROW = 220`: cada 220px suma su tamaño una vez más, creciendo desde su borde de abajo); la **subida le "cuesta" bastante más**: menos de un tercio del scroll (`SI_LIFT = 0.3`; antes 0.45, se pidió más pesado). En una pantalla de 900px de alto, sale del todo a los ~1760px de scroll.
  - Cuando el logo **está por irse**, aparecen los bloques de texto del home y **frenan en su lugar** (suben 50px fundiéndose, con freno suave): primero **"Based in… / Available…"**, después el **bloque de la firma** (firma, "Diseñadora de Indumentaria", rol rotativo y url).
  - Después, con más scroll, **los trabajos aparecen "desde el fondo", casi en conjunto** (apenas escalonados, en **orden al azar**): empiezan apenas más chicos (82%) y lavados en blanco y crecen hasta su lugar. El peso es **intermedio** (`SI_WORK = 460`, separados `SI_STEP = 110`; antes 620/340, se pidió menos pesado y más en conjunto) y además siguen al scroll con demora propia (`SI_WORK_LERP`). Mientras aparecen, la esfera está quieta en la posición desde la que arranca el giro de entrada.
  - **En medio de los trabajos**, **baja desde arriba la barra del menú** (Trabajos / Sobre mí / Contacto y ES/EN), a su velocidad de siempre (no se hizo más pesada).
  - Cuando **ya casi aparecieron del todo** (todos al 80%, `SI_RELEASE`), **se "sueltan"**: la esfera **gira en diagonal y frena** (el mismo giro de entrada de siempre, 1700ms) y el resto termina solo, sin más scroll. Un trabajo al azar queda en el centro.
  - Si se scrollea para atrás antes de que se suelten, se deshace. Cuando ya apareció todo, el home queda fijo y funciona como siempre (la ruedita no hace nada).
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

- Los 5 trabajos están repartidos sobre una **esfera invisible centrada en la pantalla** (radio `32vw`, entre 300 y 570px). El reparto es **a propósito desordenado pero equilibrado**: se descartó la espiral de Fibonacci porque, con algunos trabajos adelante, dejaba a los otros cuatro casi equidistantes (en cruz); y un reparto muy al azar dejaba un espacio grande vacío. Ahora, cada vez que se carga la página, se prueban repartos al azar y se ajusta el mejor de a poco, para que con **cualquier** trabajo adelante los demás queden con ángulos y distancias al centro distintos (irregular), pero sin huecos de más de ~115° ni todo cargado para un lado (equilibrado), sin que ninguno quede pegado a otro ni escondido detrás del de adelante. Referencia: el home de gionatannese.com.
- Se ven siempre **de frente**, como tarjetas (no se tuercen con la esfera). La profundidad se nota en el **tamaño** (adelante = tamaño actual de los recuadros, 380×304; atrás, la mitad) y en un **fundido en blanco** (los de atrás se van lavando hacia el blanco, hasta un 72%; **no** se vuelven transparentes, así no se ve lo que queda detrás de cada uno, y nunca desaparecen).
- Algunos trabajos pueden quedar cortados por el borde de la pantalla; está bien.
- **Siempre pasan por debajo de los textos del home.**
- **Se gira arrastrando** (mouse o dedo). El cursor es una mano abierta (`grab`) y se cierra al arrastrar (`grabbing`). Se "agarra" siempre la cara delantera: arrastrar a la derecha lleva lo de adelante a la derecha.
- **Sensibilidad:** liviana, sigue bien al mouse pero con un mínimo de peso (`SPH_SENS = 1`, `SPH_FOLLOW = 0.22`); al soltar sigue un poco por inercia hasta frenar (`SPH_FRICTION = 0.945`). Cuando nadie la toca, queda **quieta**.
- **La ruedita del mouse no hace nada** en el home (ya no hay scroll; se sacó la etiqueta "[ Scroll ]", el resto de los textos quedó en su lugar).
- **Al pasar el cursor**, solo se eleva (`scale(1.1)`) el trabajo que está **adelante** (casi sin fundido).
- **Click** (sin arrastrar): en el de adelante → abre el trabajo; en uno que está más atrás → la esfera gira (950ms) y lo trae **al centro**. Si hubo arrastre, el click no hace nada.
- **Entrada** (después de la intro y al volver al home): cada vez queda **un trabajo distinto al azar en el centro**. El giro alrededor de ese centro se elige para que los demás queden lo más despejados posible (menos superpuestos y menos cortados). La esfera llega girando **en diagonal** (entre horizontal y vertical) y frena en esa posición (1700ms, `easeOutCubic`).

### 3.5 "Sobre mí"

- El **logo queda fijo en el centro de la pantalla** en todo momento, en una capa aparte (`#aboutLogoLayer`, `position:fixed`, fuera de cualquier contenedor con scroll — esto fue clave para que funcionara bien).
- Al entrar: el logo **gira sobre su eje vertical** con efecto 3D real (16 capas apiladas simulando un grosor de 9px, para que no se vea plano al girar). Una vuelta completa, 3s, `cubic-bezier(.35,0,.25,1)`.
- Al terminar el giro, el logo se **aplana de forma gradual** (las capas convergen a profundidad 0 en 450ms) — sutil, y calculado para terminar casi exactamente cuando arranca la caída del texto (mínima superposición). Una vez aplanado, las capas de más se ocultan para recuperar nitidez total.
- El texto entra como un **"scroll al revés"**: arranca mostrando la última línea del último párrafo y retrocede (`easeOutQuart`, 4200ms) hasta frenar mostrando solo el título "01 — Universo".
- Los párrafos se **abren alrededor de una elipse invisible** ajustada al logo (semiejes = mitad del ancho/alto del logo + 60px), línea por línea: cada línea se parte en dos mitades que se separan lo necesario para no tocar el logo. Abrirse es inmediato (nunca puede invadir la elipse); cerrarse es suave (lerp 0.06). Los 4 títulos (01–04) **no** se abren — pasan detrás del logo.
- El **copyright**, al alcanzar al logo durante el scroll, se "engancha" debajo de él como pie de foto (con 42px de separación) en vez de seguir desplazándose con el resto del texto.
- El scroll de esta sección **no es el nativo del navegador**: se maneja a mano (rueda del mouse → variable `aboutTarget` → lerp hacia `aboutCurrent`, factor 0.075) para tener control total del peso y evitar conflictos con otros gestos del sitio.
- Al llegar al final del contenido (o intentar scrollear hacia arriba desde el principio) vuelve automáticamente al home, con la misma transición de fundido + las animaciones de entrada del home post-intro.

### 3.6 "Contacto"

Dos formas de entrar, mismo resultado final:

- **Desde el home:** mismo giro de logo que en "Sobre mí" → zoom.
- **Desde "Sobre mí"** (por el menú o clickeando el logo): el texto termina de caer y desaparece hacia abajo a **velocidad constante** (2000ms, lineal, sin desacelerar) → zoom.

Zoom: el logo se agranda con `scale()` hasta que una banda vertical específica de la imagen —definida como fracción de su propia altura, `ZOOM_F1 = 0.09` a `ZOOM_F2 = 0.425`— llena la pantalla. Duración 4200ms, `cubic-bezier(.165,.84,.44,1)`. El aplanado 3D→2D ocurre en el mismo instante que arranca el zoom, para que no se note el corte.

- "Sobre mí" en el menú cambia a **blanco** 2.6s después de arrancar el zoom (para tener contraste sobre el logo oscuro ya ampliado detrás).
- El contenido (tres bloques: email/web · Instagram/LinkedIn · ubicación/disponibilidad) aparece recién a los 3.3s, cada uno con una entrada distinta y sutil (fundido / deslizamiento / ascenso).
- Si estando ya en Contacto se vuelve a clickear "Contacto", el logo hace un **pequeño rebote** (escala a 0.985, 280ms) en vez de reiniciar toda la entrada.
- Scrollear (para cualquier lado) devuelve al home con la misma transición de fundido, con un estirado casi imperceptible (10px, contra los 46px que usa el resto del sitio).
- Sin etiqueta "[ Scroll ]" (se sacó).

### 3.7 Salir de un trabajo estirando (arriba o abajo)

- El scroll normal **frena en un tope**, arriba y abajo, y ahí se queda: recorrer el trabajo de ida y vuelta nunca saca a nadie sin querer.
- **Tope de arriba:** el principio del trabajo. **Tope de abajo:** donde termina la última foto (La Sombrerera y Dualidad Fusionada), el video final (7600), las tarjetas (Nada es Plano) y, en Un Mundo para Exprimir, cuando las tres fotos finales quedan centradas en la pantalla.
- Para salir al home hay que hacer **un movimiento más** con la ruedita estando en el tope (después de una pausa; el envión del scroll que venía no cuenta) y **sostenerlo un poco menos de un segundo** (800ms). Mientras se sostiene, el trabajo se va estirando (hasta 90px arriba, 140px abajo); al cumplirse el tiempo, se va al home con el fundido.
- Si se suelta antes (más de 320ms sin mover la ruedita), el estirado vuelve suave al tope.
- Constantes en el código: `PULL_HOLD`, `PULL_GAP`, `PULL_LET_GO`, `PULL_TOP`, `PULL_BOTTOM`.

### 3.8 Notas por trabajo

- **01 Nada es Plano** (trabajo de diseño, fondo blanco; proyecto de graduación). Clases `nep-*`. Orden: inicial → concepto → cuaderno → foto de la IA → colección → conjuntos → tarjetas.
  1. **Inicial:** al abrir el trabajo se reproduce el video `nada-es-plano-video.mp4` (5s, sin sonido, a pantalla completa, sin textos ni menú; mientras dura no se puede bajar). **En su último segundo se funde en blanco** (1.7s) mientras se le hace un **leve zoom a las caras de las chicas** (el punto de apoyo del zoom es el medio entre las dos caras, `NEP_FACES`). Ya en blanco, entran "desde el fondo" **el título**, y después **el subtítulo junto con los servicios** (y el menú). *(probado y descartado: la última imagen del video transformándose como un líquido en las letras, con WebGL.)*
  2. **Concepto:** arranca **encimado con la parte inicial** (casi sin espacio en blanco): la pregunta empieza a armarse ni bien se van el título y los servicios. Mientras dura, la pantalla queda quieta y el scroll mueve el texto. **Sin cilindro**: las líneas son planas y **aparecen y desaparecen fundiéndose con el fondo**. Primero aparece **la pregunta sola** ("¿Cómo es posible…?"), en la tipografía de la cita del concepto de La Sombrerera (Instrument Sans itálica), en tinta y más grande (`clamp(22px,2.5vw,36px)`): se va **"apoyando" letra por letra** (cada letra baja apenas y se funde desde el blanco) a medida que el scroll la lleva al centro; se queda un momento quieta y se va subiendo y fundiéndose con el fondo. **La pregunta es más pesada** que los párrafos (`NEP_Q_WEIGHT = 2.7`, contra `NEP_WEIGHT = 1.7`), para dar tiempo a leerla. Recién cuando ya se fue, entran los párrafos. El **centro nítido mide 5 líneas** (`NEP_LINES`); por arriba y por abajo cada línea se funde con el fondo (`NEP_FADE`, 2.6 líneas). El texto sigue al scroll con demora propia (`NEP_LERP`). Texto centrado.
  3. **Cuaderno** (arranca **ni bien se va la última línea del concepto**, sin espacio entre medio): fotos `nada-es-plano-cuaderno-N.webp` (fondo transparente), alineadas en un mismo marco de 2000×1700 (lomo en el centro, tapa de 1000 de alto). **Se usan solo seis:** tapa (1) · 2 "Avíos" · 3 "Despiece" · 4 triángulo verde · 6 bocetos · contratapa (8) (`NB_PAGES`; la 5 y la 7 se sacaron). La tapa mide un 60% del alto de la pantalla. El texto que lo acompaña va **alineado a la izquierda**. Recorrido con el scroll (la sección queda fija):
     - **a.** La tapa entra **desde el borde izquierdo** y **frena "asomada"** (se ve un poco más de la mitad). A la vez, los **dos primeros párrafos** ("La investigación sobre color…", columna más ancha, centrada) suben por el centro y se funden arriba.
     - **b.** Los **otros dos párrafos** los siguen y **frenan en el centro**.
     - **c.** El cuaderno termina de salir y, al avanzar, **empuja esos dos párrafos hasta la columna de la derecha**; el cuaderno queda **en el centro del lado izquierdo** (no centrado en la pantalla).
     - **d.** Ahí aparece **"click"** junto al cursor: cada click **pasa una página** (una hoja que gira sobre el lomo, .72s, con sombra suave; las páginas de abajo pasan con un **fundido**, nada cambia de golpe). Al llegar a la **contratapa ya no se puede hacer click** y aparece **"[ Scroll ]"** abajo al centro (estilo de la intro). Si se scrollea **para arriba con el cuaderno abierto, primero se cierra** (rápido).
     - **e.** Con más scroll, el cuaderno **se va por la derecha** (mismo movimiento de antes) **con el texto a la par**. Cuando ya salió de la pantalla, **vuelve solo a la tapa**.
  4. **Foto de la IA** (`nada-es-plano-ia-creativa.jpg`): mientras el cuaderno se va, **el fondo pasa de blanco al de la foto** y, cuando el cuaderno ya casi se fue, la foto aparece sobre él, sin cortes. La foto original se **extendió** (2240×1460: se completó su fondo para que llene cualquier pantalla) y la capa de fondo es ese mismo fondo difuminado y sin las figuras (`nada-es-plano-ia-creativa-fondo.jpg`, capa `.nep-bg`, fija a la pantalla). Pie de foto abajo a la izquierda, con la estética de los pies de las tarjetas: "IA creativa @studio.joaquina" (en un tono de piedra más oscuro, `#6f685c`, para que se lea sobre el beige). Después, con el scroll normal, la foto se va (fundiéndose) y **el fondo vuelve a blanco**.
  5. **Colección** (scroll normal): a la izquierda los geometrales de las 15 prendas (`nada-es-plano-coleccion.webp`, del alto de la tapa del cuaderno y en el mismo lugar que él) y a la derecha el texto "El desarrollo de la colección…" (alineado a la izquierda, en la misma columna donde quedaron los párrafos del cuaderno).
  6. **Conjuntos materializados** (un viewport): los dos conjuntos en geometral (`nada-es-plano-conjunto-1/2-frente/espalda.webp`, recortados con fondo transparente), **equidistantes** en todo el ancho y del **alto de la tapa del cuaderno**. Cada uno con **su espalda por detrás de la delantera**, asomando a la derecha (se ve un poco menos de la mitad) y apenas más arriba, con una **sombra leve** de la delantera sobre ella.
  7. **Tarjetas** (un viewport, al final): tres obras en una fila, **equidistantes a todo el ancho de la pantalla**, al **2/3 del tamaño original +15%**, con **bordes levemente redondeados** (5px) y su pie centrado: "arte @sven_pfrommer", "arte @origersht", "arte @alekustn" (en minúscula). Al pasar el cursor se levantan apenas (`scale(1.04)`). **Click → se dan vuelta en 3D** (.95s) con **12px de grosor**; el dorso y el canto son de su color (#89a3eb "Matiz Irruptivo", #eeede4 "Reverberante Eco", #f5b920 "Albor Indómito"), con título (MAYÚSCULAS, .09em) y texto en tinta, centrados (si el texto no entra, el JS lo achica un poco más). **Solo una tarjeta puede estar dada vuelta.** *(Antes iban después del concepto; se movieron.)*
  - Por ahora los textos están solo en castellano (la traducción va con "listo").
- **05 7600 — portada congelada y cortina negra:** al scrollear, la portada queda fija y la cortina negra sube desde abajo hasta dejar la portada visible solo en **menos de un cuarto de la pantalla, arriba** (el negro pleno arranca al 19% del alto; antes 24%, se achicó un poco más). El fundido entre portada y negro mantiene siempre la misma curva; su largo (`--alb-g`, hasta 340px) se ajusta al alto de la pantalla y, si hace falta, arranca apenas por encima de la pantalla para no comprimirse.

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

1. **Home** — firma (una línea o dos líneas, alternando cada 15s para poder comparar), rol rotativo ("Dirección creativa", "Diseño de indumentaria", etc.), url, info de ubicación/disponibilidad (siempre en inglés), y los 5 "trabajos" sobre una esfera que se gira arrastrando con el mouse (ver 3.4).
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
