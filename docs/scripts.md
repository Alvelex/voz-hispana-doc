---
sidebar_position: 5
---

# Scripts

## Dónde crear scripts cliente

Los scripts cliente nuevos deben ir en:

```text
ReplicatedStorage
└── Client
```

Propiedades:

```text
RunContext = Client
Enabled = false
```

`GameLoader` los activa al final de la carga inicial.

## Dónde no crear scripts cliente

No crear nuevos scripts en:

```text
StarterPlayerScripts
```

Motivo: `StarterPlayerScripts` se copia al jugador cuando entra. Como nuestro proyecto importa templates durante el arranque, no queremos depender de que scripts nuevos estén ahí.

## Dónde crear módulos compartidos

Los módulos compartidos van normalmente en:

```text
ReplicatedStorage
└── Shared
```

Ejemplos:

```text
ReplicatedStorage.Shared.AnimationButtons
ReplicatedStorage.Shared.BreakDown
ReplicatedStorage.Shared.SoundManager
```

## Auto-enable

Los scripts de templates deben estar desactivados al publicarse:

```text
Enabled = false
```

Después:

- `InitScripts` activa scripts de servidor;
- `GameLoader` activa scripts cliente dentro de `ReplicatedStorage.Client`;
- scripts con tag `IgnoreAutoEnable` no se activan automáticamente.
