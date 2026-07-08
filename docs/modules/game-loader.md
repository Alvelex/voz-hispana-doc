---
sidebar_position: 4
---

# GameLoader

## Para qué sirve

`GameLoader` controla la carga inicial del cliente.

Se encarga de:

- mostrar la pantalla de carga;
- esperar a que las templates estén listas;
- esperar a `InitScriptsReadyFlag`;
- pedir al servidor que cargue el character;
- activar los scripts cliente de `ReplicatedStorage.Client`.

## Regla de equipo

No crear loaders paralelos.

Los sistemas cliente deben asumir que serán activados por `GameLoader` al final del flujo de carga.

## Scripts cliente

Para que `GameLoader` pueda activarlos, los scripts cliente deben estar en:

```text
ReplicatedStorage.Client
```

Con:

```text
RunContext = Client
Enabled = false
```
