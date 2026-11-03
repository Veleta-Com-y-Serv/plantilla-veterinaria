# Plantilla NoExpertise · Clínica veterinaria

Web cercana para clínicas veterinarias, con urgencias 24 h, tarifas, consejos y cita por especie.

- Sectores: veterinaria, clinica-veterinaria, peluqueria-canina, tienda-mascotas, adiestramiento. Estilo: cercano. Plan mínimo: presencia.
- Secciones: hero, servicios, urgencias, clinica, equipo, tarifas, consejos, opiniones, preguntas, cita, contacto (y `texto` para apartados nuevos).
- Diseño a ancho completo: bandas de borde a borde con las esquinas de arriba redondeadas que se apilan (turquesa, blanco, coral, menta, turquesa hondo), fotos a sangre en formas redondas, título enorme. Brief en `DISEÑO.md`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`VeterinaryCare` en el ejemplo) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en `fotos.json`; reglas para el agente en `CLAUDE.md`.

## Campos propios

| Sección | Campos |
|---|---|
| `hero` | `especies` {titulo, icono}, `destacado` {titulo, texto} (chapa), `cta`, `cta_secundario` |
| `urgencias` | `destacado` {titulo, telefono, texto}, `items` {titulo} |
| `clinica` | `imagen`, `items` {titulo, icono}, `galeria`, `cta` |
| `tarifas` | `tarifas` {nombre, texto, precio, categoria}, `nota` |
| `consejos` | `noticias` {fecha, titulo, texto, imagen, url} |
| `cita` | `opciones` («Perro; Gato; …»), `items` {titulo}, `cta`, `imagen` |
| `contacto` | `horario` {dia, horas}, `imagen` |

Ejemplo: Lauhanka Clínica Veterinaria, negocio ficticio de Vitoria-Gasteiz (teléfonos ficticios).

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.servicios.items` con `detalle` tiene su página en `/servicios/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
