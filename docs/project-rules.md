---
sidebar_position: 3
---

# Reglas del proyecto

## Player lifecycle

En templates, usa `PlayerInit`.

No uses directamente:

```lua
Players.PlayerAdded:Connect(function(player)
	-- No usar directamente en templates
end)
```

Usa:

```lua
local PlayerInit = require(ReplicatedStorage:WaitForChild("PlayerInit"))

PlayerInit.Connect(function(player)
	-- Seguro para jugadores actuales y futuros
end)
```

## Scripts cliente

No crear nuevos scripts en `StarterPlayerScripts`.

Los scripts cliente van en:

```text
ReplicatedStorage > Client
```

Propiedades obligatorias:

```text
RunContext = Client
Enabled = false
```

## Scripts servidor

Los scripts servidor se importan desde templates y son activados por `InitScripts` después de que `ImportTemplates` haya terminado.

Propiedad obligatoria en templates:

```text
Enabled = false
```

## Excluir scripts del auto-enable

Usa el tag:

```text
IgnoreAutoEnable
```

Ejemplos donde suele usarse:

- scripts internos de modelos;
- scripts dentro de tools;
- efectos;
- componentes clonables;
- scripts que deben arrancar manualmente.

## UI y botones

Para animaciones comunes de botones de UI, usa `ReplicatedStorage.Shared.AnimationButtons`.

No dupliques lógica de hover, click o sonido en cada interfaz si el comportamiento ya existe en este módulo.
