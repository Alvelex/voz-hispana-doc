# Voz Hispana Docs — Agent Instructions

Este repositorio contiene la documentación técnica de Voz Hispana para desarrolladores.

## Objetivo

- Mantener documentación concisa, práctica y orientada al uso.
- No explicar implementación interna salvo que sea necesario para evitar errores.
- Escribir en español.
- Usar tono claro, directo y profesional.
- Priorizar ejemplos copiables en Luau cuando aplique.

## Estructura

- `docs/intro.md`: entrada principal.
- `docs/onboarding.md`: guía inicial para nuevos devs.
- `docs/project-rules.md`: reglas obligatorias del proyecto.
- `docs/templates.md`: sistema de templates.
- `docs/scripts.md`: reglas sobre scripts cliente/servidor.
- `docs/startup-flow.md`: flujo ImportTemplates, InitScripts y GameLoader.
- `docs/modules/`: módulos compartidos.
- `docs/systems/`: sistemas del juego documentados como fachada.

## Reglas de contenido

- Cada sistema debe documentarse como "cómo se usa", no como "cómo funciona por dentro".
- Cada página de sistema debe tener:
  1. Para qué sirve
  2. Dónde está
  3. Cómo se usa
  4. Ejemplos mínimos
  5. Reglas / cosas que no hacer

## Reglas del proyecto

- En templates se usa `PlayerInit`, no `Players.PlayerAdded` directamente.
- No crear scripts nuevos en `StarterPlayerScripts`.
- Scripts cliente en `ReplicatedStorage > Client`.
- Scripts cliente con `RunContext = Client` y `Enabled = false`.
- Scripts de templates con `Enabled = false`.
- Usar `IgnoreAutoEnable` para scripts que no deben autoactivarse.
- `Core` siempre va primero en `ImportTemplates`.
- El merge de templates conserva la instancia original y añade hijos de la nueva si tienen mismo nombre y clase.
- `GameLoader` activa scripts cliente al final de la carga.
- `InitScripts` activa scripts de servidor después de importar templates.

## No hacer

- No cambiar workflows, `moonwave.toml` ni configuración del repo salvo petición explícita.
- No inventar APIs.
- No añadir secciones largas o teóricas.
- No hacer push automáticamente.
- Antes de cambios grandes, explicar el plan.
