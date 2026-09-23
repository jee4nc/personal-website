---
name: blog-post
description: Guía de voz, estructura y convenciones para escribir o editar posts del blog de jcaldea.dev (src/content/blog/*.mdx). Invocar SIEMPRE antes de redactar, reescribir o revisar un post, o al proponer ideas de artículos.
---

# Escribir un post para jcaldea.dev

El blog es de Jean: SE en Chile, trabaja en la pega con Node/React/Go, y en paralelo construye cosas propias (Mariner, taghound, packwatch, Arcadia Poker, domo IA). El lector es un colega dev hispanohablante.

**La regla de oro: si el post lo podría haber escrito cualquiera googleando, no sirve.** Cada post tiene que tener algo que solo Jean vivió: un bug, una decisión, un incidente, un intento fallido, un número medido.

## Antes de escribir

Si falta la materia prima personal, **pregunta antes de redactar**. No rellenes con generalidades. Preguntas útiles:

- ¿Qué fue lo que más te costó / qué te sorprendió?
- ¿Qué intentaste primero que no funcionó?
- ¿Dónde lo usaste (pega, side project, freelance)? ¿Qué número/screenshot tienes?
- ¿Qué sacrificaste o qué no es ideal de la solución?

Nunca inventes anécdotas, métricas ni contexto laboral. Si no lo sabes, pregunta o déjalo como `{/* TODO: ... */}`.

## Voz

- **Primera persona, informal pero técnico.** Como explicarle algo a un colega en el almuerzo.
- **Español de Chile, tuteo.** "tú puedes", "sigues", "piensa en". **Nunca voseo** ("pensá", "seguís", "tenés"). Chilenismos suaves están bien: "la pega", "jodido", "un cacho". Nada forzado.
- **Spanglish técnico natural**: runtime, build, deploy, friction, momentum, approach. No traducir términos que nadie traduce.
- **Guiones largos (—)** para apartes.
- **Opinión honesta**: qué se sacrificó, cuándo NO usar lo que recomienda.
- **Frases cortas con punch** para cerrar ideas. Ejemplos reales del blog:
  - "Simple en concepto, sorprendentemente jodido en ejecución."
  - "Para un blog es usar un cañón para matar una mosca."
  - "El bloqueante no venía de lo que escribimos, venía de lo que dejamos resolver al azar en cada build."
  - "Si hay algo que me llevo es que los iframes son simples hasta que dejan de serlo."

## Anti-patrones (suenan a IA o a docs genéricas)

Evitar:

- Muletillas: "Suena a magia, pero…", "Acá va lo importante", "La guía definitiva", "En este artículo exploraremos", "Sin más preámbulo", "Trátalo con el respeto que merece", "Es importante destacar", "En resumen", "¡Vamos a ello!".
- Títulos de sección con clichés ("Los 4 jinetes del Apocalipsis", "El santo grial").
- **Negritas** en cada párrafo. Máximo una o dos por sección, solo para la idea que el lector no puede perderse.
- Listas "cuándo usar / cuándo no" o tablas comparativas sin experiencia propia detrás. Si hay tabla, que salga de algo que Jean probó o que resuma lo ya contado.
- Secciones que parafrasean la documentación oficial. Enlazar a la doc y contar lo que la doc no dice.
- Cierres motivacionales vacíos ("¡Ahora te toca a ti!").
- Emojis en el texto (en bloques de código como marcador ✅/❌ está bien, con moderación).

## Estructura que funciona

No es plantilla rígida, pero los mejores posts (`iframe-page-builder`, `lockfile-npm`) siguen este arco:

1. **Escena / contexto concreto** — qué estaba construyendo o qué se rompió. Sin intro genérica.
2. **El problema** — por qué la solución obvia no sirve.
3. **Intentos y trampas** — lo que probé, por qué falló. Aquí vive el valor del post.
4. **Lo que funcionó** — código corto y comentado.
5. **Lo que aprendí** — viñetas que empiezan con una frase en negrita + explicación.
6. **Cierre** — una o dos líneas, idealmente con punch. Opinión, no resumen.

## Código

- Snippets cortos (≤ ~30 líneas), recortados a lo relevante, con comentarios útiles en español.
- Lenguaje en el fence (`tsx`, `bash`, `go`, `swift`…). Shiki usa `github-dark-default`.
- Verificar que lo técnico sea correcto (flags, nombres de archivos, versiones actuales). Ante la duda, comprobar antes de afirmar.

## Formato del archivo

- Ruta: `src/content/blog/<slug-kebab-case>.mdx`. El slug es `post.id`.
- Frontmatter (schema en `src/content.config.ts`):

```yaml
---
title: "Título con gancho, no genérico"
description: "Una o dos frases concretas de qué problema resuelve el post."
date: YYYY-MM-DD
tags: ["tag1", "tag2"]   # minúsculas; reusar existentes: frontend, css, javascript, typescript, node, devops, backend, astro, opinión
draft: true              # dejar en true hasta que Jean lo revise
---
```

- Secciones con `##`, subsecciones con `###`. No usar `#` (el título lo pone el layout).
- Imágenes: `src/assets/blog/<slug>/` + `import { Image } from 'astro:assets'` con `width={720} format="webp" quality={80}` y `alt` descriptivo en español.
- GIFs animados que deban seguir animados: `<img src="/blog/<slug>/x.gif" alt="…" />` desde `public/blog/<slug>/` (la sintaxis `![]()` no se renderiza bien).
- Fechas en texto con formato chileno (`13 de abril de 2026`).

## Checklist final

- [ ] ¿Hay al menos una experiencia real y concreta de Jean?
- [ ] ¿Cero voseo? (`grep -nE "\b(pensá|seguís|tenés|podés|sabés|mirá|fijate)\b"`)
- [ ] ¿Ninguna muletilla de la lista de anti-patrones?
- [ ] ¿Negritas con moderación?
- [ ] ¿Se dice qué se sacrificó o cuándo no aplica?
- [ ] ¿Lo técnico está verificado y al día?
- [ ] `npm run build` pasa.
