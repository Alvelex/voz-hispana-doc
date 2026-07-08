---
sidebar_position: 4
---

# Templates

El proyecto usa templates publicadas como modelos de Roblox para compartir contenido entre varias places.

## Orden de importación

`Core` siempre debe ir primero.

Ejemplo:

```lua
local TEMPLATES_IDS = {
	137484964666215, -- CORE siempre primero
	92258948630058,  -- GameWorlds
	94091855508048,  -- BuildingSystem
}
```

## Filosofía de merge

El merge es simple:

- si una instancia no existe, se añade;
- si ya existe una instancia con el mismo nombre y la misma clase, se conserva la original y se meten dentro los hijos de la nueva;
- si existe una instancia con el mismo nombre pero distinta clase, se descarta la nueva.

## Ejemplo

Template `Core`:

```text
ReplicatedStorage
└── Shared
    └── Systems
```

Template `BuildingSystem`:

```text
ReplicatedStorage
└── Shared
    └── Systems
        └── Building
```

Resultado final:

```text
ReplicatedStorage
└── Shared
    └── Systems
        └── Building
```

## Regla para desarrolladores

Una template posterior puede traer carpetas o módulos vacíos solo para extender una estructura ya creada por `Core`.

No escribas código en duplicados que solo existen como contenedor de merge. El código principal debe estar en la template propietaria real del sistema.
