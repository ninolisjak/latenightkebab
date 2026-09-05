# NO ONION — repo guide

4-player co-op physics comedy game. Players run an unlicensed kebab truck: take garbled orders from drunk customers, cook, survive health inspections, make rent. Full design in `docs/design.md`.

## Stack

- Unity 6 LTS, C#
- FishNet — networking
- FishySteamworks + Facepunch.Steamworks — Steam P2P transport
- **No dedicated server, ever.** Host is a player. 1–4 players on home internet.
- Proximity voice: Steam voice API or Dissonance (TBD)

## Developer context

First game, first networked project. Strong on Java/JS/backend, new to C# and Unity. Explain networking decisions; don't explain ordinary C#.

## Hard rules

1. **Voice is never a game input.** No mechanic may require a player to speak. Proximity chat is flavour only — many players run Discord with in-game voice muted.
2. **No dedicated-server solutions.** If something only works with authoritative hosting infrastructure, it's out.
3. **Simplest thing that survives 4 players** beats the theoretically correct thing.
4. **Scope discipline.** One truck interior (~8x4m) plus a small exterior. No open world, no combat, no pathfinding beyond a queue.

## Architecture conventions

- One system per folder under `Assets/Scripts/`
- Networking code isolated in `Assets/Scripts/Net/` — gameplay systems talk to it through interfaces, never to FishNet directly
- ScriptableObjects for all static data: menu items, sauces, customer archetypes, pitch definitions, upgrade definitions
- Run state (money, fame, heat, unlocks) is a single serialisable object owned by the server
- Prefer composition over inheritance on interactables

## Systems (build order)

1. `Net/` — connection, lobby, player spawn, ownership *(current focus)*
2. `Carry/` — pickup, drop, handoff, two-player carry (the meat cone)
3. `Orders/` — order generation, degradation, ticket data, ticket rail
4. `Stations/` — grills, fryer, cone, cooking timers and food state
5. `Inspector/` — suspicion meter, dialogue prompts, violation flags
6. `Economy/` — till, pocket, rent, upgrades
7. `Progression/` — fame, heat, unlocks, loadout
8. `Map/` — driving, pitch selection, nightly conditions

## Style

- No comments explaining what code does; comments only for *why* something non-obvious was done
- Small files, clear boundaries — vibecoded code degrades fastest when everything's tangled
- Ask before restructuring anything in `Net/`

## Current state

Project setup. Nothing built yet.
