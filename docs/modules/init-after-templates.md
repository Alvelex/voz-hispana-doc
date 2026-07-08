---
sidebar_position: 3
---

# InitAfterTemplates

## Dónde está

```text
ReplicatedStorage.InitAfterTemplates
```

## Para qué sirve

Permite esperar a que las templates hayan terminado de importarse.

## Uso

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")

require(ReplicatedStorage:WaitForChild("InitAfterTemplates"))
```

Después de este `require`, el script puede acceder a objetos que vienen de templates.

## Cuándo usarlo

Úsalo si tu script necesita objetos que pueden venir de una template cargada durante el arranque.
