# Plan de Entrenamiento — Temporada 2026

## Descripción
Aplicación web de una sola página (HTML + JS vanilla) con el plan de entrenamiento y nutrición de Jaycee para la temporada 2026 del CAP Ciudad de Murcia, ya en liga. Sin frameworks, sin build system — un único archivo HTML autocontenido.

## Archivo principal
`plan-entrenamiento.html` — contiene todo: HTML, CSS y JS en un solo fichero.

## Estructura del plan
Ya no es una cuenta atrás de 7 semanas/3 fases (esa pretemporada no se completó y la liga ya empezó). Ahora es una **semana tipo que se repite indefinidamente**, ajustada al calendario real:
- **Martes y jueves**: entreno de equipo fijo, 21:30–22:45h
- **Lunes, miércoles, viernes**: entreno propio (cardio/fuerza), con toggle mañana en ayunas / tarde
- **Domingo**: partido de liga cada 15 días (toggle "hay partido" / "descanso") — sábado es el día de descanso/activación antes del domingo

## Estructura del JS (en orden de aparición)
1. **Firebase init** — conexión a Realtime Database para sincronización entre dispositivos
2. **PLAN_SEMANA** — los 7 días tipo (Lunes–Domingo) con su tipo de sesión
3. **Sistema de checks de entreno** — `completados` (por día de la semana, 0–6), `toggleDia()`, `resetSemanaEntreno()` (botón "Reiniciar" manual, no hay fecha de corte automática)
4. **DIETA_SEMANA** — un único menú semanal con 4 "modos" de día: `propio` (toggle mañana/tarde), `equipo` (horario fijo con snack pre-entreno 19:00h y recuperación ligera a las 23:00h en vez de cena completa), `descanso` (sábado), `variable` (domingo: toggle partido/descanso)
5. **RECETAS** — indexadas por `"{dia}-{slot}"` (ej. `"lunes-g1"`, `"martes-recup"`, `"domingo-partido-c"`), cada una con `ingredientes` (cantidades para 1 persona) y `pasos`
6. **COMPRA** — lista de la compra única (no por semana), para 2 personas, cubre toda la semana tipo incluidas ambas variantes del domingo
7. **Init** — bloque final que arranca todo y expone funciones a `window.*`

## Firebase
- Proyecto: `plan-atpalmar`
- Base de datos: `https://plan-atpalmar-default-rtdb.europe-west1.firebasedatabase.app`
- Rutas: `/completados` (checks de entreno) y `/compra` (lista de la compra)
- SDK via ES modules desde `gstatic.com`
- El script usa `type="module"` — todas las funciones usadas en `onclick` están expuestas via `window.*` al final
- Reglas de lectura/escritura abiertas (`.read`/`.write`: true) — cuidado si se revisan de nuevo, las reglas de "modo prueba" caducan a los 30 días por defecto

## Despliegue
- GitHub Pages: `https://josecharlie.github.io/plan-futbol/plan-entrenamiento.html`
- Para desplegar: commit + push a rama `main`, GitHub Pages se actualiza en ~2 min
- **Nunca hacer `git push` sin confirmación explícita del usuario en el chat**, incluso si la autenticación ya funciona

## Contexto del usuario
- Juega en el CAP Ciudad de Murcia, liga ya en marcha (no completó la pretemporada de 7 semanas)
- Entreno de equipo: martes y jueves 21:30–22:45h. Partido: domingos alternos
- Sigue en déficit calórico moderado para seguir adelgazando, compaginado con ganar fondo y fuerza
- Menú para 2 personas
