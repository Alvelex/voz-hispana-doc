---
sidebar_position: 1
---

# PlayerInit

## Dónde está

```text
ReplicatedStorage.PlayerInit
```

## Para qué sirve

Permite registrar lógica que debe ejecutarse para jugadores actuales y futuros.

Es obligatorio usarlo en templates cuando necesites lógica equivalente a `Players.PlayerAdded`.

## Uso básico

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local PlayerInit = require(ReplicatedStorage:WaitForChild("PlayerInit"))

PlayerInit.Connect(function(player)
	print("Jugador listo:", player.Name)
end)
```

## Por qué no usamos `Players.PlayerAdded` directamente

Las templates pueden importarse cuando ya hay jugadores dentro. Un script que se carga tarde puede perder el evento nativo `PlayerAdded`.

`PlayerInit` ejecuta el callback para jugadores que ya estaban dentro y también para los que entren después.
