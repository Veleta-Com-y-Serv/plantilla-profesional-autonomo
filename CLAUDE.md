# Plantilla «Profesional independiente» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **personal**
(arena + carbón + terracota, serif grande para títulos, columna de lectura de 44 rem, portada asimétrica 5/7 con
retrato, comillas grandes, línea de tiempo, cabecera con el nombre y menú de texto sin botón, pie de una línea).
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = terracota de botones y detalles, acento = puntos y comillas, fondo = arena, texto = carbón). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`, `bg-primario/10`… Los tonos derivados (banda, líneas, texto suave) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-texto`, `--fuente-titulos`, `--lectura`, botones `.btn`/`.btn-sec`, cabecera `.cabecera--autonomo`, pie `.pie--autonomo`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/`; las de respaldo en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/consulta.jpg`). El retrato de la portada es `/placeholders/persona.svg` (silueta) hasta que el cliente suba su foto: **no se generan caras**.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en serif.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Un apartado nuevo puede reutilizar un diseño con `tipo: <id>`.
- `hero` → `hero.astro`: retrato 3:4 (`imagen`), nombre, `antetitulo`, `titulo`, `texto`, `destacado {titulo, texto, icono}`, `cta`, `cta_secundario`.
- `sobre` → `sobre.astro`: `texto` en párrafos (línea en blanco entre ellos), `declaracion` (frase entre comillas grandes), `imagen`, `items` (formación, colegiación, idiomas… con `icono`), `galeria` (tira de fotos del espacio).
- `trayectoria` → `trayectoria.astro`: `hitos` (línea de tiempo), `texto`, `imagen`. Sin hitos no se pinta.
- `servicios` → `servicios.astro`: `items` con `precio` y `duracion` opcionales, `imagen` panorámica, `cta`.
- `proceso` → `proceso.astro`: `items` (3-4 pasos numerados), `cta`.
- `opiniones` → `opiniones.astro`: `testimonios` (la primera, destacada). Sin testimonios no se pinta.
- `preguntas` → `preguntas.astro`: `preguntas` en acordeón. Sin preguntas no se pinta.
- `cita` → `cita.astro`: bloque oscuro con `texto`, `cta`, `enlace_agenda` + `texto_agenda`, `nota`, `imagen`.
- `contacto` → `contacto.astro`: datos de `contacto`, `texto`, `imagen`, `boton`; formulario con desplegable de los títulos de `servicios.items`.
- `texto` → `texto.astro`: apartado genérico (`tipo: texto`) con `declaracion`, `items`, `imagen`, `cta`.

## Campos propios de esta plantilla (además del esquema común)
- `hero.destacado`: `{ titulo, texto, icono }` (p. ej. «Consulta online y presencial»).
- `sobre.declaracion`: frase corta. `sobre.items`: `[{titulo, texto, icono}]`.
- `trayectoria.hitos`: `[{anio, titulo, texto}]`. `anio` es cadena («2016», «2019-2021», «Hoy»). Máximo 24.
- `servicios.items`: `[{titulo, texto, icono, precio, duracion}]`. `precio` siempre como cadena («desde 60 €», «60 €», «Gratuita»); vacío = no se muestra. `duracion` («50 min»), vacía = no se muestra.
- `testimonios[].nota`: detalle opcional bajo el autor («Terapia individual»).
- `cita.enlace_agenda`: url de una agenda online (opcional; vacía = sin botón). `cita.texto_agenda`: texto de ese botón. `cita.nota`: aviso pequeño.
- `contacto.boton`: texto del botón del formulario.
- `boton_cabecera` vacío a propósito: si se rellena, se muestra como un enlace más del menú (esta cabecera no lleva botón).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para varios valores, una cadena separada por «;».
5. **No inventes** precios, cifras, años, colegiaciones ni opiniones: si el cliente no los da, deja el campo vacío o la lista vacía (`hitos: []`, `testimonios: []`); el componente lo oculta.
6. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Sección nueva**: mejor un id nuevo con `tipo:` (`texto`, `servicios`, `proceso`…). Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)`, `Seccion` y `Titular`. `src/pages/index.astro` la recoge sola.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral (`.contenedor`), sin scroll horizontal en móvil, ids `hero` y `contacto`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

Fotos: `fotos.json` describe las fotos de `public/fotos/` (se generan aparte, sin personas reconocibles); los SVG de `public/placeholders/` quedan de respaldo.
