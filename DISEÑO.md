# Clínica veterinaria: brief de diseño

Plantilla `veterinaria` creada el 29/10/2026 a partir de `salud` con `php artisan plantillas:nueva` y rediseñada
entera a ancho completo. Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: clínicas veterinarias, peluquerías caninas, tiendas de mascotas y adiestradores. Quien entra
  tiene un animal que le preocupa: quiere saber si le atienden ya (urgencias), qué hacen, cuánto cuesta y cómo
  pedir cita.
- **Qué tiene que conseguir la web**: que llamen a urgencias sin buscar (franja de la cabecera, banda coral,
  pie) y que pidan cita (formulario con especie, WhatsApp o teléfono).
- **Tono y estilo** (`cercano`): cálido, alegre, de confianza. Sí: marcas de cuidado de mascotas con color pleno
  y formas redondas. No: la clínica fría de bata blanca ni la caja centrada estrecha con tarjetas blancas.
- **Concepto «chapa de collar»**: las bandas son fichas apiladas a todo el ancho con las esquinas de arriba muy
  redondeadas (`--r`), cada una solapa a la anterior con una sombra suave; los antetítulos llevan la anilla de una
  chapa (círculo coral con agujero) y una línea; la chapa redonda coral girada (`hero.destacado`, «Cómo llegar»,
  404) repite el motivo.
- **Paleta de ejemplo**: primario turquesa `#0b7a75`, acento coral `#ff7a63`, fondo `#ffffff`, texto `#12302f`.
  Derivados con `color-mix`: `--hondo` (turquesa casi negro: hero, tarifas, pie), `--menta` (primario al 11 %),
  `--coral-suave` (acento al 17 %), `--tinta` (texto sobre coral). Texto blanco sobre turquesa y hondo; tinta
  sobre coral.
- **Ritmo de bandas** (ejemplo): hero foto a sangre con velo hondo → servicios blanco → urgencias coral → la
  clínica menta (foto a sangre a la izquierda + franja de 4 fotos) → equipo blanco → tarifas hondo → consejos
  blanco → opiniones coral suave → preguntas blanco → cita turquesa (foto a sangre a la derecha) → contacto blanco
  (foto a sangre a la izquierda) → pie hondo.
- **Tipografía**: pila de sistema («Segoe UI Variable Display», system-ui) a 800-900 con interletrado negativo;
  hero a 6,75 rem en escritorio y 2,6 rem en móvil; la última palabra de cada título va subrayada con un trazo
  coral (`.resalte`, sale sola de `partirTitulo`). Antetítulos en mayúsculas espaciadas.
- **Formas de las fotos**: medio óvalo hacia dentro en las filas 50/50 (clínica, cita, texto), arco de medio punto
  en los consejos, círculos con aro coral desplazado en el equipo, esquina enorme redondeada en contacto. En móvil
  la foto pasa arriba, a todo el ancho, con la base en curva.
- **Apartados**: hero, servicios (`items` con icono), urgencias (`destacado` con teléfono), clinica (sobre +
  galería), equipo (`personas`), tarifas (`tarifas` por `categoria`), consejos (`noticias` con foto), opiniones
  (`testimonios`), preguntas, cita (formulario con `opciones` de especie), contacto (datos + `horario`).
- **Fotos** (`fotos.json`, 11): mascotas sin personas (perro en consulta para el hero, gato en el alféizar para
  la cita), consulta y sala de espera vacías, peluquería, conejo, pinar, transportín, cachorro, fachada sin rótulo.
  Sin texto legible, sin logotipos, sin personas reconocibles.
- **Qué no hacer**: volver al hero partido con foto redondeada y tarjeta flotante de `salud`; tarjetas blancas
  con sombra en columna estrecha; bandas de un solo color seguidas (si se reordena, alterna tonos); tipografías
  externas.

## Responsive

Móvil primero. A 375 px: 16 px de margen del texto, fotos a sangre, servicios en filas (icono a la izquierda),
equipo en 2 columnas, menú plegable, chapa del hero arriba a la derecha. A 768: servicios y tarifas en 2
columnas, galería en 4. Desde 900: filas 50/50 con foto a sangre. Desde 1180: menú en línea. A 1440: servicios y
equipo en 4 columnas, tarifas en 4 grupos, opiniones con la primera a doble ancho.

## Pendiente fuera de esta plantilla

- [ ] Fotos de `fotos.json` y previews (`preview/card.jpg`, `preview/full.jpg`) con `tools/plantillas/previews.mjs`.
- [ ] Repo `Veleta-Com-y-Serv/plantilla-veterinaria` con la etiqueta `v1.0.0`.
- [ ] En la plataforma: `config/plantillas.php` (`repos` y `refs`) y `php artisan plantillas:sync --demos`.
