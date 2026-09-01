# Actividad Interactiva — Línea de Pobreza Subjetiva

Actividad interactiva para **Expo Cuentas 2026**, basada en el enfoque de Leyden para estimar la línea de pobreza subjetiva.

🔗 **Ver la actividad en vivo:** https://juanfer-nl.github.io/act_interact_expo_cuentas/

## Qué hace

La persona visitante ingresa cuánto gasta por mes y la actividad calcula, en base a esa respuesta, una estimación de su línea de pobreza subjetiva y muestra los resultados de forma visual e interactiva.

Flujo de la página:

1. **¿Cuánto gastás por mes?** — el usuario ingresa su gasto mensual.
2. **Tu línea de pobreza subjetiva** — cálculo del umbral según el enfoque de Leyden.
3. **Resultados** — visualización del resultado obtenido.

## Tecnología

Página estática autocontenida: todo el HTML, CSS y JavaScript viven en un único `index.html`, sin proceso de build ni dependencias externas.

## Uso local

Alcanza con abrir `index.html` en un navegador, o servirlo con cualquier servidor estático:

```bash
python3 -m http.server
```

## Relación con otros repos

Esta actividad reemplaza a [`deprecated_act_interact_expo_cuentas`](https://github.com/JuanFer-NL/deprecated_act_interact_expo_cuentas), su versión anterior construida en React + Vite. Ver también [`ppt_expo_cuentas`](https://github.com/JuanFer-NL/ppt_expo_cuentas) (presentación) y [`web_page_expo_cuentas`](https://github.com/JuanFer-NL/web_page_expo_cuentas) (página web del proyecto).
