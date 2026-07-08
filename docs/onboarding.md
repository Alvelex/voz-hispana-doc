---
sidebar_position: 2
---

# Onboarding

Esta página contiene las reglas mínimas para empezar a trabajar en el proyecto.

## Reglas obligatorias

### 1. Usa `PlayerInit`, no `Players.PlayerAdded`, en templates

Los scripts de templates pueden cargarse cuando ya hay jugadores dentro del servidor. Por eso, en templates no usamos directamente `Players.PlayerAdded`.

Usa siempre:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local PlayerInit = require(ReplicatedStorage:WaitForChild("PlayerInit"))

PlayerInit.Connect(function(player)
	-- Código para jugadores actuales y futuros
end)
```

### 2. No crees scripts nuevos en `StarterPlayerScripts`

Los scripts cliente nuevos deben ir en:

```text
ReplicatedStorage
└── Client
```

Con estas propiedades:

```text
RunContext = Client
Enabled = false
```

`GameLoader` los activa cuando termina la carga inicial del cliente.

### 3. Publica los scripts de templates desactivados

Los scripts que vienen de templates deben publicarse con:

```text
Enabled = false
```

Después el sistema los activa automáticamente cuando corresponde.

### 4. Usa `IgnoreAutoEnable` cuando un script no debe arrancar solo

Añade el tag:

```text
IgnoreAutoEnable
```

a scripts internos de modelos, tools, efectos, componentes clonables o cualquier script que deba activarse manualmente.

### 5. `Core` siempre va primero

La template `Core` debe importarse antes que el resto. Las demás templates pueden extender estructuras ya creadas por `Core`.
