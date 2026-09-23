[claude.md](https://github.com/user-attachments/files/32530487/claude.md)
# Guía de referencia — Portfolio web de Carolina Picone

> Documento de contexto para nuevos chats. Resume las decisiones de diseño, estilo y funcionamiento ya definidas para el portfolio, a partir de la conversación donde se construyó la versión actual del sitio (`index.html`).

---

## 0. Flujo de trabajo de archivos (leer primero, en todo chat nuevo)

Carolina trabaja este portfolio en **chats separados por proyecto**, dentro de un mismo Proyecto de Claude. Este documento y el `index.html` liviano viven en la Base de Conocimiento del Proyecto. Reglas fijas para cualquier chat que continúe este trabajo:

- **El `index.html` que está en la Base de Conocimiento es siempre "liviano"**: tiene todo el código, estructura, animaciones y lógica funcionando, pero las imágenes/videos están referenciados por archivo (`src="assets/nombre-del-archivo.jpg"`), **no** embebidos como base64 adentro del HTML. Esto es intencional — embeber archivos pesados como base64 hace que el archivo no entre en la capacidad de la Base de Conocimiento (ver por qué, más abajo).
- **Durante el trabajo en el chat**, Carolina va a subir las fotos/videos del proyecto puntual que esté armando ese día, para poder ver la web funcionando de verdad con esas imágenes puestas (visualización real, no placeholders). Está bien y es lo esperado que en el archivo de trabajo del chat las imágenes SÍ estén embebidas o accesibles para poder previsualizar — el paso de "aligerar" pasa recién al final.
- **Carolina NO sabe programar ni tiene conocimientos técnicos.** Cualquier instrucción sobre archivos tiene que ser en pasos simples, sin asumir que entiende de código, carpetas de proyecto, rutas relativas, etc.

### Regla obligatoria: secuencia exacta de cierre, con palabras clave

Carolina cierra cada trabajo con una secuencia fija, disparada por palabras exactas suyas — **no** es a criterio de Claude detectar "si parece que terminó":

1. Cuando Carolina escribe **"listo."** → Claude le pregunta para confirmar si quiere pasar a la traducción al inglés de ese trabajo (no arranca la traducción todavía, solo confirma).
2. Si Carolina confirma que sí → Claude hace la traducción (ver "Traducción al inglés" más abajo) y espera su revisión.
3. Cuando Carolina escribe **"traducción lista"** → Claude, **automáticamente y sin volver a preguntar**, arma y entrega los dos archivos finales (ver "Entrega de archivos" más abajo).

Si Carolina dice "listo." pero después decide no traducir todavía, o quiere seguir hacienda cambios, la secuencia se pausa ahí — no hay que forzar los pasos siguientes.

### Traducción al inglés

- El sitio es bilingüe (selector ES/EN), pero las traducciones se van completando **de a un trabajo por vez, en el mismo chat donde se armó ese contenido** — no todas juntas al final en un chat aparte.
- Se dispara cuando Carolina escribe **"listo."** y confirma que sí (ver secuencia arriba): ahí Claude ofrece una primera versión en inglés del texto en español de esa sección.
- Carolina revisa y ajusta esa versión a su gusto — no se da por definitiva sin que ella la lea, porque son decisiones de tono que le pertenecen a ella (no solo corrección idiomática).
- Cuando Carolina termina de revisar, escribe **"traducción lista"**, que dispara automáticamente la entrega de archivos (siguiente paso).

### Entrega de archivos

Se dispara automáticamente cuando Carolina escribe **"traducción lista"** — en ese momento Claude entrega, sin necesidad de preguntar de nuevo, los dos archivos finales:

1. Un **`.zip`** que contenga el `index.html` liviano (imágenes/videos ya extraídos y referenciados por ruta, no embebidos) + una carpeta `assets/` con únicamente los archivos nuevos de ESE proyecto (fotos/videos que subió en ESE chat), con nombres de archivo descriptivos y prolijos (ej: `sombrerera-hero.jpg`, no el nombre original de la foto tal cual se la subió).
2. El **`index.html` liviano suelto** también aparte (mismo contenido que el de adentro del zip), para subir directo a la Base de Conocimiento sin tener que descomprimir nada.

### Por qué se hace así (contexto técnico, por si hace falta explicarlo de nuevo)

- La Base de Conocimiento de Claude **no acepta imágenes ni videos como archivos propios** — solo documentos de texto (HTML, PDF, DOCX, TXT, etc.).
- Cuando una imagen/video se embebe como base64 adentro de un HTML, ese texto codificado pesa muchísimo en términos de "capacidad de lectura" de Claude (mucho más que su peso en MB), y hace que el archivo no entre en el límite manejable de la Base de Conocimiento, aunque el archivo en sí pese poco en MB.
- Por eso la separación código/medios no es opcional ni cosmética: es lo que permite que el `index.html` siempre pueda subirse sin problema a la Base de Conocimiento.

### Cómo maneja Carolina esto en su compu (para su propia referencia, no requiere saber programar)

- Tiene **una carpeta `assets` maestra en su computadora**, que va creciendo a medida que termina cada proyecto — hoy tiene las fotos/videos de "La Sombrerera", después va a sumar las de cada trabajo nuevo.
- Cada vez que termina un proyecto y recibe el zip: el `assets` del zip nuevo trae **solo** los archivos de ESE proyecto puntual (el chat no conoce ni tiene los de proyectos anteriores). Carolina **arrastra/suma** esos archivos nuevos dentro de su carpeta `assets` maestra (no reemplaza nada, solo agrega).
- El `index.html`, en cambio, **se reemplaza completo** cada vez — el nuevo que entrega el chat ya incluye todas las referencias anteriores más las nuevas, así que no hay que "sumarlo", solo reemplazar el archivo viejo por el nuevo en la Base de Conocimiento.
- El nombre de archivo que usa el código (ej. `sombrerera-hero.jpg`) **no es el nombre original** que tenía la foto en la cámara/celular de Carolina — es un nombre nuevo, descriptivo, que le puso el chat al armar el código. Para reemplazar una foto por una versión editada más adelante, Carolina tiene que renombrar su archivo nuevo con **ese mismo nombre exacto** y reemplazar el archivo viejo en la carpeta `assets` — así el código (que sigue pidiendo ese nombre de archivo) automáticamente muestra la versión nueva, sin tocar ni entender el código.

---

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
- **Firma manuscrita** (imagen, no es una fuente) — el nombre "Carolina Picone" en el loader y en el home. Existen dos variantes: una línea (nombre completo) y dos líneas ("Carolina" / "Picone", mismo tamaño de letra real, no de caja).
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
| Etiqueta "[ Scroll ]" | 11px | MAYÚSCULAS | .14em | tinta (home) / piedra (paneles) |
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
- **Fondos:** ver la regla de fondos en "Estilo general". Dentro de esa regla, Dualidad Fusionada tiene un matiz propio: el fondo pasa muy de a poco de blanco a `#f2f2f1` durante el concepto y queda así hasta el final (apenas más oscuro que el blanco de los figurines, `#f6f6f6`, para que no se pierdan; además llevan una sombra casi imperceptible). El menú va en blanco mientras está sobre la foto de portada y pasa a tinta al cruzar la prenda.

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
- Todas las imágenes (firma en sus variantes, logo) están **embebidas en el propio HTML como `data:` URI en base64**, para que el archivo funcione solo, sin depender de otros archivos sueltos.
- Única dependencia externa: Google Fonts (Instrument Sans), vía `<link>` en el `<head>`.
- Sin proceso de build, sin `npm`, sin dependencias.

### Estructura del archivo

```
<style> ... todo el CSS ... </style>
<body>
  #loader                     → intro
  .site
    header (nav)              → Trabajos / Sobre mí / Contacto / ES-EN
    #home                     → firma, rol rotativo, los 5 "trabajos" dispersos
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

Firma + URL aparecen con un barrido de opacidad de **izquierda a derecha, a velocidad constante** (no acelera ni desacelera). Se sostiene un momento y se desvanece.

- Aparición: 2.3s (`linear`)
- Sostenido: 0.8s
- Desvanecido: 0.8s

Técnica: un `div.reveal-cover` con un gradiente (transparente → blanco) que se desliza con `transform: translateX()`, revelando el contenido a medida que se corre.

```css
.reveal-cover{
  position:absolute; top:0; left:-13%; width:113%; height:100%;
  background: linear-gradient(90deg, transparent 0%, var(--white) 13.3%, var(--white) 100%);
  transform: translateX(0%);
  transition: transform 2.3s linear;
}
.loader-inner.show .reveal-cover{ transform: translateX(100%); }
```

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

### 3.4 Trabajos del home (recorrido diagonal disperso)

- 5 elementos recorren individualmente una diagonal de **esquina inferior izquierda a superior derecha**, atados al scroll.
- Fórmula de posición por trabajo (`p` = progreso individual, 0 a 1, según su ventana de tiempo dentro del scroll total):
  ```
  x = -w + p·(vw+w) + laneOffset[i]
  y = vh - p·(vh+h) + laneOffset[i] + laneExtraY[i]
  ```
- 5 "carriles" fijos (`laneOffset`) para que nunca se superpongan, dentro de un corredor diagonal acotado (definido a partir de una captura de referencia con líneas rojas).
- El scroll tiene **peso/inercia**: se suaviza con un lerp — `currentG += (targetG - currentG) * 0.022`. Cuanto más chico el factor, más "pesado" se siente.
- Al terminar la intro, los trabajos hacen una **entrada en reversa**: arrancan ya "recorridos" (fuera de pantalla, arriba a la derecha) y retroceden con `easeOutCubic` durante 1450ms hasta frenar con el primer trabajo cerca del centro.
- No hay tope de scroll — los trabajos simplemente van desapareciendo a medida que avanzás.
- Puntas de los recuadros levemente redondeadas (`border-radius:6px`); al pasar el cursor, se agrandan levemente (`scale(1.1)`, transición de 0.2s).

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

1. **Home** — firma (una línea o dos líneas, alternando cada 15s para poder comparar), rol rotativo ("Dirección creativa", "Diseño de indumentaria", etc.), url, info de ubicación/disponibilidad (siempre en inglés), y los 5 "trabajos" dispersos en diagonal.
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
