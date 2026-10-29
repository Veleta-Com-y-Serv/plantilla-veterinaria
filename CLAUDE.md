# Plantilla «Clínica veterinaria» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **cercano**
(concepto «chapa de collar», ver `DISEÑO.md`). Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y `src/styles/global.css` saca los derivados con `color-mix` (`--hondo`, `--menta`, `--coral-suave`, `--tinta`). Tailwind los expone como `bg-primario`, `text-acento`…
- **Tipografías y aspecto general**: `src/styles/global.css` (bandas `.banda` + `.tono-*`, antetítulo con anilla, `.resalte`, botones `.btn`/`.btn-sec`/`.btn--turquesa`, fichas, cabecera y pie). Fuentes del sistema: no añadas fuentes externas.
- **Bandas**: cada sección usa `src/components/ui/Seccion.astro` con un `tono` (`claro`, `menta`, `coral`, `coral-suave`, `turquesa`, `hondo`). Las bandas tienen las esquinas de arriba redondeadas y se solapan con la anterior (`--r`); no quites ese solape ni metas una sección en una caja estrecha.
- **Imágenes**: en `public/`. Las de relleno están en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos nuevas del cliente van en `public/fotos/`. Personas: `/placeholders/persona.svg` mientras no haya foto.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = chapa redonda con la inicial y el nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `src/components/secciones/hero.astro` (foto a sangre, chapa de urgencias)
- `servicios` → `servicios.astro` (fichas con icono)
- `urgencias` → `urgencias.astro` (banda coral con el teléfono gigante)
- `clinica` → `clinica.astro` (50/50 con foto a sangre + franja de galería)
- `equipo` → `equipo.astro`
- `tarifas` → `tarifas.astro` (agrupadas por categoría)
- `consejos` → `consejos.astro` (artículos en `noticias`)
- `opiniones` → `opiniones.astro`
- `preguntas` → `preguntas.astro`
- `cita` → `cita.astro` (formulario con especie, `src/components/ui/FormularioCita.astro`)
- `contacto` → `contacto.astro` (datos, horario y foto; si `cita` no está activa, también el formulario de contacto)
- `texto` → `texto.astro` (genérico para apartados nuevos con `tipo: texto`)

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas.
4. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`, con bandas (`<section class="banda tono-turquesa">…`); enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
5. **Sección nueva**: crea `src/components/secciones/<id>.astro` (copia la estructura de una existente: `seccion(id)`, `Seccion` con su `tono`, `Titular`) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
6. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
7. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto en móvil (las fotos y los fondos sí tocan el borde), sin scroll horizontal a 375 px, botones de 44 px de alto como mínimo. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `titulo`/`nombre` de la ficha); las decorativas, `alt=""`.
8. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioCita.astro` y `FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.especies` {titulo, icono}: animales que atendéis, en píldoras. `hero.destacado` {titulo, texto}: chapa coral redonda («24 h · Urgencias todos los días»). `hero.cta_secundario`: segundo botón.
- `urgencias.destacado` {titulo, telefono, texto}: el teléfono de urgencias (sin `telefono`, el de contacto). También sale en la franja de la cabecera y en el pie. `urgencias.items` {titulo}: cuándo llamar.
- `clinica.items` {titulo, icono}, `clinica.galeria` (fotos en franja), `clinica.cta`.
- `tarifas.tarifas` {nombre, texto, precio, categoria}: precio siempre como cadena; se agrupan por `categoria`. `tarifas.nota`.
- `consejos.noticias` {fecha, titulo, texto, imagen, url}: con `url`, la ficha es un enlace.
- `cita.opciones`: especies del desplegable, separadas por «;». `cita.items` {titulo}: pasos. `cita.cta.texto`: botón de WhatsApp (destino `cta.url` o, vacío, el WhatsApp de contacto). `cita.imagen`.
- `contacto.horario` {dia, horas}, `contacto.imagen` (fachada; la chapa «Cómo llegar» abre el mapa).

Iconos disponibles (`icono`): los de `src/components/ui/Icono.astro`, entre ellos `estetoscopio`, `vacuna`, `bisturi`, `microscopio`, `diente`, `tijeras`, `hueso`, `huella`, `gato`, `corazon`, `cruz`, `pastilla`.

Fotos de partida en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`, sin derechos de terceros); los SVG de `public/placeholders/` siguen de respaldo.
