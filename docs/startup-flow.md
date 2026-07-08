---
sidebar_position: 6
---

# Flujo de arranque

El arranque del juego sigue este orden general:

```text
ImportTemplates
↓
InitAfterTemplates
↓
InitScripts activa scripts de servidor
↓
GameLoader espera InitScriptsReadyFlag
↓
GameLoader pide LoadCharacter
↓
GameLoader activa scripts cliente
```

## `ImportTemplates`

Carga las templates configuradas para la place y mueve su contenido a los servicios correspondientes.

## `InitAfterTemplates`

Módulo usado para esperar a que las templates estén listas antes de acceder a objetos importados.

Uso:

```lua
require(ReplicatedStorage:WaitForChild("InitAfterTemplates"))
```

## `InitScripts`

Activa scripts de servidor después de que las templates estén colocadas.

No activa scripts dentro de `ReplicatedStorage.Client`; esos los activa `GameLoader`.

## `GameLoader`

Controla la carga inicial del cliente, pide al servidor que cargue el character y activa los scripts cliente al final.

No crees loaders paralelos.
