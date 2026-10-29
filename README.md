# Plantilla NoExpertise · Profesional independiente

Web personal para psicólogos, coaches, consultores, nutricionistas, formadores y otros profesionales que
trabajan por su cuenta: retrato, trayectoria, servicios con precio opcional y petición de cita.

- Sectores: autonomo, consultor, coach, psicologia, nutricion, freelance, formador. Estilo: personal. Plan mínimo: gratis.
- Secciones: hero, sobre, trayectoria, servicios, proceso, opiniones, preguntas, cita, contacto (+ `texto` genérico).
- Campos propios: `hero.destacado`, `sobre.declaracion`, `trayectoria.hitos[]`, `servicios.items[].precio/duracion`,
  `testimonios[].nota`, `cita.enlace_agenda/texto_agenda/nota`, `contacto.boton`.
- Diseño: arena + carbón + terracota, serif del sistema para títulos, portada asimétrica 5/7, columna de lectura
  de 44 rem, línea de tiempo, comillas grandes, cabecera con menú de texto y pie de una sola línea.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`;
  fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`).
Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.
