# NO ONION — friction mechanics

Small physical failures that make the truck feel awkward to work in, and make upgrades feel earned rather than numeric.

Companion to `design.md`. Nothing here is committed — this is a menu to pull from.

---

## The governing principle

**A failure must be caused by something the player did, not rolled against them.**

- ❌ "Slips randomly 10% of the time" — punishment, unlearnable, rage-quit fuel
- ✅ "Slips if you sprint while carrying, or turn too fast, or your hands are greasy" — a skill you can learn and a mistake you can own

That distinction is the entire difference between funny and frustrating. Every mechanic below should be checked against it before it goes in.

### The second principle

**The best upgrades change your behaviour, not a number.**

Non-slip shoes shouldn't make you faster. They should let you *sprint through a spill* instead of walking around it. That's a different decision, not a better stat. Aim for that shape every time.

---

## 1. Grip and slippage

| Mechanic | Detail |
|---|---|
| **Greasy hands** | Handling meat coats your hands. Wipe on your apron to reset — costs seconds you don't have during a rush. |
| **Wet hands** | After washing, you have to actually dry them before you can grip properly. |
| **Sprinting while carrying** | Multiplies drop chance. Walking is safe. A speed-versus-safety decision on every trip. |
| **Stacked items** | A plate with three things on it is far less stable than a single item. Encourages multiple trips, punishes greed. |
| **Hot items** | Only holdable for a few seconds before you fumble. Forces you to plan where it's going before you pick it up. |

**Upgrade:** better gloves — grip that survives grease, plus solo carry on the meat cone.

---

## 2. Vision and awareness

| Mechanic | Detail |
|---|---|
| **Fryer steam** | Fogs your screen when you're near it. The fryer station is permanently slightly blind. |
| **Cone smoke** | If the cone burns, smoke fills the truck and nobody can read the ticket rail. A shared failure with a shared consequence. |
| **Greasy window** | Accumulates at high fame. You can barely see the customer you're trying to read. Cleaning it costs service time. |
| **Neon flicker** | The sign strobes the interior. Atmosphere, but also genuinely disruptive at the worst moments. |

---

## 3. Sound as friction

Sound is underused as a difficulty axis and it's cheap to implement.

| Mechanic | Detail |
|---|---|
| **Club music** | Drowns out orders. The closer the pitch is to the club, the worse you hear — which ties directly to the pitch that pays best. |
| **Extractor fan** | Roars over the station timers. You miss the beep, the food burns. |
| **General truck noise** | Fryer, cone motor, queue chatter — all competing with the one thing you need to hear. |

**Upgrade:** the radio earpiece. Cuts through all of it. Should be the single most desirable purchase in the game, which is what makes stealing from the till tempting enough to be a real dilemma.

---

## 4. Movement in a tiny space

The truck is ~8x4m with four people in it. Space itself is the antagonist.

| Mechanic | Detail |
|---|---|
| **Bumping** | Collide with a teammate and you both stumble. Whatever either of you was carrying is now in question. |
| **Wet floor** | After any spill. Everyone slides until it's mopped — and mopping is time nobody wants to spend. |
| **Narrow corners** | Genuinely too tight for two people. Forces real-time negotiation about who moves first. |
| **Doorways** | The single worst place to meet someone carrying a cone. |

**Upgrade:** non-slip shoes — sprint through spills instead of routing around them.

---

## 5. Tools degrading

Ties directly into the truck degradation system in `design.md` §5.3.

| Mechanic | Detail |
|---|---|
| **Blunt knife** | Takes twice as long to cut, and occasionally slips off the cone. |
| **Worn tongs** | Drop things at predictable *intervals* rather than random chance — learnable, so it's frustration you can plan around. |
| **Cracked plates** | Break if you set them down hard. Teaches you to place rather than drop. |

**Upgrade:** the good knife — faster, cleaner, no slip.

---

## Why this layer matters

Without it, the truck is a set of stations and a timer. With it, the truck is a *place* — awkward, loud, greasy, and shared with three people who keep getting in your way.

It also solves a progression problem cheaply: personal upgrades become obviously worth buying, which makes the pocket economy meaningful, which makes the unlocked till a genuine temptation rather than pure spite.

---

## Selection guidance

Don't ship all of these. Pick roughly:

- **2–3 grip mechanics** — enough that carrying feels considered, not so many it's fussy
- **2 vision mechanics** — steam and smoke are the strongest
- **2 sound mechanics** — club music and the extractor fan
- **All the movement ones** — they're nearly free and they generate the most clips
- **2 tool degradation** — tied to repairs so there's a decision attached

Test each in a playtest. If it produces a laugh, keep it. If it produces a sigh, cut it. That's the only metric that matters for this layer.
