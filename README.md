# Actividad Interactiva — Línea de Pobreza Subjetiva

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-live-2ea44f?logo=githubpages&logoColor=white)](https://juanfer-nl.github.io/act_interact_expo_cuentas/)
[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey.svg)](LICENSE)

Actividad interactiva para **Expo Cuentas 2026**, basada en el enfoque de Leyden para estimar la línea de pobreza subjetiva (LPS) a partir del propio gasto de la persona visitante, contrastada contra microdatos reales de la EPH (Encuesta Permanente de Hogares).

🔗 **Ver la actividad en vivo:** https://juanfer-nl.github.io/act_interact_expo_cuentas/

## Qué hace

Es una calculadora de tres pasos, sin backend: la persona ingresa cuánto necesitaría ganar para "no sentirse pobre" desagregado en tres rubros, la actividad calcula su línea de pobreza subjetiva personal y la aplica sobre una muestra real de hogares para mostrar qué porcentaje de la población quedaría por debajo de ese umbral.

### Paso 1 — ¿Cuánto gastás por mes?

Tres campos de ingreso mínimo necesario, sumados en tiempo real (`updateTotal()`):

| Campo (id) | Rubro | Placeholder |
|---|---|---|
| `g_a` | Alimentos | $120.000 |
| `g_s` | Servicios | $50.000 |
| `g_v` | Varios | $80.000 |

La suma de los tres da el **ingreso mínimo (yₘᵢₙ)** de la persona.

### Paso 2 — Tu línea de pobreza subjetiva

Se aplica el **coeficiente de Leyden (0,74)** sobre el ingreso mínimo declarado:

```
LPS = yₘᵢₙ × 0.74
```

(`toStep2()`, redondeado con `Math.round`).

### Paso 3 — Resultados

Se recorre el dataset embebido `EPH` — un array de pares `[ipcf, pondih]` (ingreso per cápita familiar y su ponderador muestral) tomado de microdatos reales de la EPH — y se calcula la **Tasa de Pobreza Nacional Ponderada (TPNP)**:

```
TPNP = Σ pondih(ipcf < LPS) / Σ pondih total
```

es decir, el porcentaje *ponderado* de hogares cuyo ingreso per cápita queda por debajo de la LPS calculada por la persona usuaria. El resultado se visualiza con **Chart.js** en un histograma de 50 buckets de $30.000 (constante `BS=30000`, `NB=50`), con el último bucket como cola abierta (≥ $1.470.000), marcando con una barra destacada en qué tramo cae la LPS calculada.

## Tecnología

Página estática autocontenida: todo el HTML, CSS y JavaScript viven en un único `index.html` (~780 KB, mayormente por el dataset EPH embebido inline), sin proceso de build ni dependencias npm. Usa **Chart.js** (vía CDN) para el histograma y **Tabler Icons** para los íconos.

No hay backend: los datos de la EPH ya vienen precalculados y embebidos como constante JS (`const EPH = [...]`), no se hace ningún fetch en runtime.

## Uso local

Alcanza con abrir `index.html` en un navegador, o servirlo con cualquier servidor estático:

```bash
python3 -m http.server
```

## Relación con otros repos

Esta actividad reemplaza a [`deprecated_act_interact_expo_cuentas`](https://github.com/JuanFer-NL/deprecated_act_interact_expo_cuentas), su versión anterior construida en React + Vite (misma lógica de cálculo — coeficiente 0.74 — pero con carga de datos vía fetch y stack de build). Ver también [`ppt_expo_cuentas`](https://github.com/JuanFer-NL/ppt_expo_cuentas) (presentación) y [`web_page_expo_cuentas`](https://github.com/JuanFer-NL/web_page_expo_cuentas) (página web del proyecto), que embebe esta misma actividad en su sección "Actividad Interactiva".
