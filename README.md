# Legalize CL

### Legislación chilena consolidada en Markdown, versionada con Git.

Cada ley es un fichero. Cada reforma es un commit.

**Fuente oficial:** [Biblioteca del Congreso Nacional (BCN)](https://www.bcn.cl/leychile/) — Ley Chile

Forma parte del proyecto [Legalize](https://github.com/legalize-dev/legalize) · [legalize.dev](https://legalize.dev)

> **Fase inicial** — Este repositorio está en desarrollo activo. La estructura de los ficheros, el historial de commits y el contenido pueden cambiar significativamente, incluyendo regeneraciones completas.

## Inicio rápido

```bash
# Clonar la legislación chilena
git clone https://github.com/legalize-dev/legalize-cl.git

# Leer la Constitución Política de la República de Chile
less cl/CL-242302.md

# Buscar en el Código Tributario
grep -A 5 "Artículo 1" cl/CL-6374.md

# Ver el historial de modificaciones de una ley
git log --oneline -- cl/CL-1138479.md

# Leer el Código del Trabajo
less cl/CL-207436.md
```

## Estructura

```
cl/
  CL-242302.md     — Constitución Política de la República de Chile (DS 100/2005)
  CL-6374.md       — Código Tributario (DL 830/1974)
  CL-172986.md     — Código Civil (DFL 1/2000)
  CL-207436.md     — Código del Trabajo (DFL 1/2003)
  CL-1138479.md    — Ley 21.180 — Transformación Digital del Estado
  CL-1222281.md    — Ley 21.808 — Subsidio Unificado de Empleo
  ...
```

La estructura del fichero es **plana** — un solo directorio por país, sin subdirectorios por rango. El identificador `CL-{idNorma}` corresponde al ID interno de la BCN. El tipo de norma está en el frontmatter YAML de cada fichero:

| Rank (frontmatter) | Tipo |
|---|---|
| `constitucion` | Constitución Política |
| `ley_organica_constitucional` | Ley Orgánica Constitucional |
| `ley_quorum_calificado` | Ley de Quórum Calificado |
| `ley` | Ley ordinaria |
| `decreto_con_fuerza_de_ley` | Decreto con Fuerza de Ley (DFL) |
| `decreto_ley` | Decreto Ley (DL) |
| `decreto_supremo` | Decreto Supremo (DS) |
| `decreto` | Decreto |
| `tratado` | Tratado Internacional |
| `resolucion` | Resolución |

## Formato

Cada fichero es Markdown con frontmatter YAML:

```yaml
---
title: "FIJA EL TEXTO REFUNDIDO, COORDINADO Y SISTEMATIZADO DE LA CONSTITUCION POLITICA DE LA REPUBLICA DE CHILE"
identifier: "CL-242302"
country: "cl"
rank: "constitucion"
publication_date: "2005-09-22"
last_updated: "2025-10-07"
status: "in_force"
source: "https://www.bcn.cl/leychile/navegar?idNorma=242302"
department: "MINISTERIO SECRETARÍA GENERAL DE LA PRESIDENCIA"
bcn_schema_version: "1.0"
is_treaty: "no"
promulgation_date: "2005-09-17"
official_type: "Decreto"
official_number: "100"
gazette: "Diario Oficial"
gazette_issue_number: "38268"
parts_repealed: "1"
transitory_parts: "55"
---
```

El cuerpo del Markdown contiene **únicamente el texto legal** consolidado (libros, títulos, capítulos, párrafos, artículos, anexos y firmantes). Las anotaciones marginales del Diario Oficial (referencias a leyes que reforman cada artículo) **no son parte del texto legal** y se excluyen del cuerpo del fichero.

Las imágenes y figuras embebidas en formato JPEG (esquemas, tablas escaneadas) se reemplazan por la marca `[imagen omitida]` y se contabilizan en el campo `images_dropped` del frontmatter.

Los tipos de commit son: `[bootstrap]` (publicación original), `[reforma]` (modificación), `[nueva]` (norma nueva), `[derogacion]` (derogación) y `[correccion]` (corrección de errata).

## Fuente

Los datos provienen de la API pública XML de [Ley Chile](https://www.leychile.cl/), el sistema de información jurídica de la **Biblioteca del Congreso Nacional de Chile (BCN)**, certificada ISO 9001. El endpoint primario es:

```
GET https://www.leychile.cl/Consulta/obtxml?opt=7&idNorma={id}
```

La BCN publica el contenido bajo una **licencia abierta**: el contenido de la legislación es de dominio público y la BCN proporciona acceso libre y gratuito a través de su API.

## Licencia

[MIT](LICENSE) — el contenido de las normas es de dominio público; el código del pipeline es MIT.

---

Generado por el pipeline [legalize-pipeline](https://github.com/legalize-dev/legalize-pipeline).
