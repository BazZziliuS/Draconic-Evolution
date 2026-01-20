# Configurable Reactor and Portal Features

## Overview
Added configuration options to control reactor explosion behavior and portal cross-dimension teleportation for non-player entities.

## New Configuration Options

All options are located in `config/brandon3055/DraconicEvolution.cfg`

### Portal Settings (Server section)

| Option | Default | Description |
|--------|---------|-------------|
| `portalCrossDimensionMobTeleport` | `false` | If false, non-player entities (mobs, items, etc.) will not be able to teleport through portals to different dimensions. Players can always teleport. |

### Reactor Settings (Server > Reactor section)

| Option | Default | Description |
|--------|---------|-------------|
| `reactorExplosionDestroyBlocks` | `true` | If false, reactor explosion will not destroy blocks. |
| `reactorExplosionSpawnLava` | `true` | If false, reactor explosion will not spawn lava. |
| `reactorExplosionEffect` | `true` | If false, reactor explosion visual effect will be disabled. |
| `reactorExplosionDamage` | `true` | If false, reactor explosion will not damage entities. |
| `reactorExplosionCountdown` | `60` | Time in seconds before reactor explodes after meltdown. |
| `reactorMinimalBoom` | `true` | If false, the minimal explosion (when `disableLargeReactorBoom` is true) will be disabled completely - only the reactor block will be removed. |
| `reactorComponentExplosion` | `true` | If false, reactor components will not explode during meltdown, blocks will just be removed silently. |

## Use Cases

### Server-Friendly Reactor (No Griefing)
To completely disable reactor destruction:
```
reactorExplosionDestroyBlocks = false
reactorExplosionSpawnLava = false
reactorExplosionDamage = false
reactorMinimalBoom = false
reactorComponentExplosion = false
```

### Visual-Only Explosion
Keep the visual effect but no actual damage:
```
reactorExplosionDestroyBlocks = false
reactorExplosionSpawnLava = false
reactorExplosionDamage = false
reactorExplosionEffect = true
```

### Quick Explosion (for testing)
Reduce countdown time:
```
reactorExplosionCountdown = 10
```

### Prevent Mob Teleportation Between Dimensions
This is enabled by default. To allow mobs to teleport:
```
portalCrossDimensionMobTeleport = true
```

## Modified Files
- `DEConfig.java` - Added new configuration fields and loading logic
- `Portal.java` - Added dimension check for non-player entities
- `ProcessExplosion.java` - Wrapped explosion effects in config checks
- `TileReactorCore.java` - Added config checks for component explosions, countdown timer, and minimal boom
- `TileDislocatorReceptacle.java` - Made `getTargetPos()` method public for Portal access
