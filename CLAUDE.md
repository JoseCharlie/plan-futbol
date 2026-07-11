# Plan de Entrenamiento — Temporada 2026

## Descripción
Aplicación web de una sola página (HTML + JS vanilla) que contiene el plan de pretemporada de fútbol de Jaycee para la temporada 2026 del CAP Ciudad de Murcia. Sin frameworks, sin build system — un único archivo HTML autocontenido.

## Archivo principal
`plan-entrenamiento.html` — contiene todo: HTML, CSS y JS en un solo fichero.

## Estructura del JS (en orden de aparición)
1. **PLAN** — datos del plan de entrenamiento (7 semanas, 3 fases)
2. **Firebase init** — conexión a Realtime Database para sincronización entre dispositivos
3. **Sistema de checks de entreno** — `completados`, `cargarCompletados()`, `guardarCompletados()`, `toggleDia()`
4. **Render del plan** — `renderSemanas()`, `renderDiasConEstado()`, `actualizarTodo()`
5. **DIETA** — datos del menú semanal (7 días, 4 comidas/día con kcal y macros)
6. **RECETAS** — objeto con 28 recetas hardcoded indexadas por `"diaIdx-comidaIdx"`
7. **Render del menú** — `renderDieta()`, `toggleReceta()`
8. **COMPRA** — lista de la compra semana 1 para 2 personas (8 secciones)
9. **Render de la compra** — `cargarCompra()`, `renderCompra()`, `toggleCompra()`
10. **Init** — bloque final que arranca todo en orden

## Firebase
- Proyecto: `plan-atpalmar`
- Base de datos: `https://plan-atpalmar-default-rtdb.europe-west1.firebasedatabase.app`
- Rutas: `/completados` (checks de entreno) y `/compra` (lista de la compra)
- SDK via ES modules desde `gstatic.com`
- El script usa `type="module"` — todas las funciones usadas en `onclick` están expuestas via `window.*` al final

## Despliegue
- GitHub Pages: `https://josecharlie.github.io/plan-futbol/plan-entrenamiento.html`
- Para desplegar: commit + push a rama `main`, GitHub Pages se actualiza en ~2 min

## Contexto del usuario
- Entrena a las 7h en ayunas (natación, running, mancuernas)
- Plan de 7 semanas hacia pretemporada de agosto 2026
- Menú para 2 personas adaptado a entreno matutino en ayunas
