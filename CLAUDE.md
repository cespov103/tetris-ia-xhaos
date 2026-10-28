# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Idioma
- Todo en español: textos visibles del juego, comentarios nuevos, README y mensajes de commit.
- Los comentarios existentes en inglés en `game.js` pueden traducirse cuando se toque ese código.

## Ejecutar
- No hay build ni tests. Para probar: `python -m http.server 8000` y abrir `http://localhost:8000`.
- Se permiten dependencias/herramientas si aportan valor; si se añaden, documentar aquí los comandos nuevos.

## Acoplamientos no obvios
- Si cambias `COLS`, `ROWS` o `BLOCK` en `game.js`, actualiza `width`/`height` de `<canvas id="board">` en `index.html` (`COLS×BLOCK` × `ROWS×BLOCK`).
- `drawNext()` asume un lienzo de 4×4 celdas de 30px: mantener `#next-canvas` en 120×120.
- Los IDs del DOM (`score`, `lines`, `level`, `overlay`, `overlay-title`, `overlay-score`, `restart-btn`, `next-canvas`) se leen en `game.js`; renombrar en ambos lados.
- Al cambiar controles, actualizar la tabla del README y la lista `.controls` de `index.html` (hoy `X` para rotar falta en el HTML).

## Automatizaciones de GitHub
- `.github/workflows/claude-issue-triage.yml`: se dispara en `issues` (`opened`, `edited`), ignora bots y usa `CLAUDE_CODE_OAUTH_TOKEN`.
- Crea (si faltan) y asigna solo estos labels: `bug`, `mejora`, `pregunta`, `documentacion`, `gameplay`, `controles`, `ui`, `rendimiento`, `prioridad: alta|media|baja`, `necesita-info`. Si se cambia el conjunto, actualizar el paso "Asegurar labels" y el prompt.
- El diagnóstico es un único comentario (marcador `<!-- claude-triaje -->`) que se reescribe con `gh issue comment --edit-last`; no modifica código.
- Los workflows de `issues` solo corren desde la rama por defecto: hay que fusionar en `main` para probarlo.

## Bug conocido
- `togglePause()` al reanudar no oculta el overlay (`overlay.classList.add('hidden')` falta).
