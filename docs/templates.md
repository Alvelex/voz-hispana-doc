---
sidebar_position: 4
---

# Templates

## Qué son las templates

Las templates son modelos publicados en Roblox que contienen sistemas reutilizables del juego. Sirven para compartir código, assets, módulos, remotes, UI y configuración entre las distintas places de la experiencia.

El juego tiene muchas places, pero no todas necesitan exactamente los mismos sistemas. Por eso existe una template común llamada `Core` y luego otras templates específicas como `GameWorlds`, `BuildingSystem` u otras.

## Dónde se trabaja con las templates

Las templates se editan desde el place principal del juego. Ese place es la fuente de trabajo real.

No se debe trabajar directamente sobre copias de templates dentro de otras places, salvo pruebas muy puntuales.

## Cómo se prueban templates en otra place

Cada place puede tener una carpeta:

```text
ServerStorage/
  TemplatesTesting/
```

Si quieres probar una versión local de una template en una place concreta, copia la template dentro de `ServerStorage > TemplatesTesting` de esa place.

Cuando `ImportTemplates` detecta una template con el mismo nombre dentro de `TemplatesTesting`, usa esa copia local en vez del asset publicado.

Esto permite probar cambios sin publicar una nueva versión del asset.

### Advertencia sobre TemplatesTesting

Las templates dentro de `TemplatesTesting` de cualquier place que no sea el place principal se consideran temporales.

Pueden ser eliminadas en cualquier momento si alguien las dejó ahí por error.

**Reglas:**

- No trabajar de forma permanente dentro de `TemplatesTesting` de una place secundaria.
- No dejar cambios importantes únicamente en `TemplatesTesting`.
- No asumir que una copia en `TemplatesTesting` es la versión oficial.
- Los cambios reales deben hacerse en la template del place principal.

## Orden de importación

`Core` siempre debe ir primero.

```lua
local TEMPLATES_IDS = {
	137484964666215, -- Core
	92258948630058,  -- GameWorlds
	94091855508048,  -- BuildingSystem
}
```

`Core` contiene la base común que comparten todas o casi todas las places. Las templates que vienen después pueden añadir contenido encima de `Core`.

## Cómo funciona el merge

Cuando una template se importa, su contenido se coloca dentro de los servicios correspondientes:

- `ReplicatedStorage`
- `ServerScriptService`
- `ServerStorage`
- `StarterGui`
- `ReplicatedFirst`
- `StarterPack`
- `Lighting`
- etc.

Si una instancia no existe, se añade.

Si una instancia ya existe con el mismo nombre y la misma clase, no se reemplaza. Se conserva la instancia original y se mueven dentro de ella los hijos de la nueva instancia.

Esto permite que una template posterior extienda una estructura creada por `Core`.

### Ejemplo de merge

`Core`:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Economy/
```

`BuildingSystem`:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Building/
```

Resultado final:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Economy/
      Building/
```

La carpeta `Shared` y la carpeta `Systems` ya existían por `Core`. `BuildingSystem` solo añade su contenido dentro de la estructura existente.

### Duplicado usado como contenedor

`Core`:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Player/
```

Otra template:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Player/
        ExtraModule
```

Resultado:

```text
ReplicatedStorage/
  Shared/
    Systems/
      Player/
        ExtraModule
```

En este caso, la carpeta o módulo `Player` de la segunda template solo existe para que el merge pueda insertar `ExtraModule` dentro del `Player` original de `Core`.

**Regla importante:** No escribas código en duplicados que solo existen como contenedor de merge. El código real debe estar en la template propietaria del sistema.

## Qué no hacer

- No cambiar el orden de `Core`.
- No trabajar permanentemente en `TemplatesTesting` de una place secundaria.
- No escribir código importante en duplicados vacíos usados solo para merge.
- No publicar scripts de templates con `Enabled = true`.
- No crear scripts cliente nuevos en `StarterPlayerScripts`.
