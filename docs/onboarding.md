---
sidebar_position: 2
---

# Guía inicial para desarrolladores

Esta guía resume las normas básicas que debe conocer cualquier persona que entre al proyecto para poder trabajar sin romper el sistema de templates, scripts o carga inicial.

## Reglas rápidas

- En templates, usar `PlayerInit` en vez de `Players.PlayerAdded` directamente.
- No crear scripts nuevos en `StarterPlayerScripts`.
- Los scripts cliente van en `ReplicatedStorage > Client`.
- Los scripts cliente deben tener `RunContext = Client` y `Enabled = false`.
- Los scripts de templates deben publicarse con `Enabled = false`.
- Usar el tag `IgnoreAutoEnable` en scripts que no deben activarse automáticamente.
- `Core` siempre debe ir primero en `ImportTemplates`.
- No trabajar directamente en templates copiadas dentro de `TemplatesTesting` de places secundarias.
- Para animaciones comunes de botones de UI, usar `ReplicatedStorage.Shared.AnimationButtons`.

## PlayerInit

Los scripts de templates pueden cargarse cuando ya hay jugadores dentro del servidor. Por eso, `Players.PlayerAdded` puede no dispararse para jugadores que ya estaban conectados.

Usa siempre `PlayerInit` dentro de templates:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local PlayerInit = require(ReplicatedStorage:WaitForChild("PlayerInit"))

PlayerInit.Connect(function(player)
	-- Código seguro para jugadores actuales y futuros
end)
```

## Scripts cliente

- No usar `StarterPlayerScripts` para nuevos sistemas.
- Los scripts cliente van en `ReplicatedStorage > Client`.
- Deben tener `RunContext = Client` y `Enabled = false`.
- `GameLoader` los activa al final de la carga inicial del cliente.

## Auto-enable

- `InitScripts` activa scripts de servidor después de importar templates.
- `GameLoader` activa scripts cliente dentro de `ReplicatedStorage.Client`.
- Scripts con el tag `IgnoreAutoEnable` no se activan automáticamente. Útil para scripts internos de modelos, tools, efectos o componentes clonables.

## Templates

Para entender cómo funcionan las templates, el orden de importación y el merge, consulta [Templates](./templates.md).
