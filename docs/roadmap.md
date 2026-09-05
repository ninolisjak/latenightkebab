# NO ONION — build roadmap

**Principle: build the part that kills projects first.** Networking before kebab. Every milestone below is playable with friends — if it isn't, it's too big.

---

## Milestone 0 — Setup

- [ ] Unity Hub + Unity 6 LTS installed
- [ ] New 3D project (URP, for the post-processing look), folder `NoOnion`
- [ ] `git init` + Unity `.gitignore` from github/gitignore
- [ ] Initial commit of the empty project
- [ ] FishNet installed and compiling
- [ ] Facepunch.Steamworks + FishySteamworks installed and compiling
- [ ] `CLAUDE.md` and `docs/design.md` in the repo root

Develop against Steam's test App ID (480, Spacewar) until you pay the $100 Steam Direct fee.

---

## Milestone 1 — Four capsules in a grey room *(weeks 1–2)*

The real first boss. Expect most of two weeks.

- [ ] Steam lobby create + join
- [ ] Player prefab with NetworkObject
- [ ] Networked first-person movement, all clients see all players
- [ ] Basic grey-box room

**Done when:** four people on four different machines can walk around the same room.

---

## Milestone 2 — One carryable cube *(week 3)*

- [ ] Pick up, drop, throw
- [ ] Ownership transfers on pickup
- [ ] Two clients grabbing on the same tick doesn't break it
- [ ] Physics stays consistent across clients

**Done when:** you can hand a cube to someone and it doesn't teleport, duplicate, or desync.

**This is the checkpoint.** If networked physics ownership makes sense after this, you can build the whole game. If it doesn't, stop and learn more before scoping further.

---

## Milestone 3 — Proximity voice *(week 4)*

Add it now, not later. Fun playtests are what keep the project alive for eight months.

- [ ] Proximity voice working
- [ ] Falloff tuned for a small interior

---

## Milestone 4 — The truck, faked *(weeks 5–7)*

No audio, no garbling, no progression. Text orders only.

- [ ] Truck interior grey-box: counter, window, one grill, ticket rail
- [ ] Customer queue spawns, waits, despawns
- [ ] Order generated as data, shown as plain text
- [ ] Ticket printed, spiked on the rail
- [ ] Assemble a wrap from components, serve it, get paid or not

**Done when:** four people can run a shift and it's already a little bit funny.

---

## Milestone 5 — The cone *(week 8)*

- [ ] Two-player carry
- [ ] Tips over when bumped
- [ ] Rotates, cooks, decays visibly
- [ ] Cone swap sequence

The single most important object in the game. Give it real time.

---

## Milestone 6 — The order system, properly *(weeks 9–11)*

- [ ] Voice bank recorded (~200 clips, one actor, one weekend)
- [ ] Combinatorial assembly with pauses and filler
- [ ] Audio degradation: pitch shift, slur, music bleed, distance
- [ ] Speech degradation: contradiction, mid-sentence swaps, dropped components
- [ ] Drunkenness float drives all of the above
- [ ] Ticket blanks for unintelligible components
- [ ] Dialogue wheel + patience bar

**Done when:** a playtest produces an argument about what someone said.

---

## Milestone 7 — The inspector *(week 12)*

- [ ] 15-second telegraph
- [ ] Suspicion meter + four stall prompts with different cost/duration
- [ ] Violation flags checked on entry
- [ ] Cleanup timers: grill 5s, fryer 10s smoke
- [ ] Fines, and losing a pitch after three bad inspections

The first real "scene". Should be the best 60 seconds in the game.

---

## Milestone 8 — Economy *(weeks 13–14)*

- [ ] Till: shared total, physical grabbable cash, no lock, no prompt
- [ ] Pocket: private money, personal upgrades
- [ ] Rent, reckoning phase, visible shortfall

**Do not add a steal prompt.** The absence is the mechanic.

---

## Milestone 9 — Progression *(weeks 15–17)*

- [ ] Fame and heat meters
- [ ] Fame tiers changing queue size and customer behaviour
- [ ] Phones out at high fame — recorded violations
- [ ] Menu unlocks + station loadout cap (4 slots, 8 owned)
- [ ] Truck degradation and repairs

---

## Milestone 10 — Map and driving *(weeks 18–20)*

Last, because it's the most cuttable if time runs out.

- [ ] Pitch selection with visible nightly conditions
- [ ] Driving between pitches, unsecured cargo
- [ ] 3–5 pitches with distinct drunkenness and queue profiles
- [ ] Rival truck taking contested spots

---

## Milestone 11 — Ship

- [ ] $100 Steam Direct fee, real App ID
- [ ] Store page live (2 weeks minimum before launch)
- [ ] Capsule art — crossed-out onion
- [ ] Trailer built from real playtest clips, not staged footage
- [ ] Demo for Next Fest
- [ ] W-8BEN, s.p. registration for invoicing

---

## Standing habits

- **Commit before every session.** Vibecoded code needs an undo button.
- **Playtest with friends every two weeks**, even when it's ugly. The design doc is a hypothesis; the playtest is the data.
- **Cut anything that isn't funny after two playtests.** Attachment to unused systems is how solo projects die.
