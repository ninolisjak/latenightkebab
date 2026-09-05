# NO ONION
### Co-op game design document — v1.0

> Working title: **NO ONION** · Steam page title candidate: *NO ONION: Late Night Kebab*

---

## 1. THE PITCH

You and up to three friends run an unlicensed kebab truck. The food is questionable, the meat has a history, and every customer is too drunk to order properly. Make rent before the city shuts you down.

**Tagline:** *The meat is fine. Stop asking about the meat.*

**Why it's fun:** You're not cooking — you're getting away with something at 3am while four people try to work out what a drunk guy just said.

**Genre position:** 4-player co-op, first person, physics-driven, single-location with a light map layer. Sits alongside Lethal Company, Content Warning, Fish and Gamble, Schedule 1 — but the comedy comes from *communication failure* rather than combat or criminality.

**Visual identity:** the name gives us a logo for free — a crossed-out onion. Circle, some lines, a red slash. That's the Steam capsule, the icon, and the sticker.

---

## 2. THE FOUNDATIONAL RULE

**Voice is never an input the game reads.**

Every mechanic runs on prompts and in-world objects. Nothing in the game listens to a microphone or requires a player to speak.

This exists because a large share of players mute proximity chat and play in Discord. Any mechanic that depends on in-game voice breaks for them. So:

- Proximity chat makes the game funnier
- Discord players lose flavour, never function
- Solo or quiet players can still complete every system

This constraint shaped the ticket rail and the inspector design below. Treat it as non-negotiable when adding new systems.

---

## 3. THE CORE LOOP

One night ≈ 20 minutes. Three phases.

### Phase 1 — DAY (≈5 min)
Buy supply, choose your pitch, choose your loadout, spend money. The argument phase.

### Phase 2 — NIGHT (≈12 min)
Run the truck. Serve, panic, survive the inspector.

### Phase 3 — RECKONING (≈3 min)
Rent is due. The till is counted in front of everyone. Discrepancies are visible; the culprit isn't.

---

# 4. MECHANICS

## 4.1 The Order System

**Orders are generated, not scripted.** Each order is a data structure:

```
{
  base:      wrap | plate | box
  meat:      lamb | chicken | mixed | none
  sauces:    [garlic, chilli, house, ...]
  removals:  [onion, salad, tomato, ...]
  extras:    [cheese, extra meat, jalapenos, ...]
  drink:     cola | water | none
}
```

Each customer carries a **drunkenness value (0.0 – 1.0)** that degrades how that order is delivered.

### Audio degradation
- Pitch and formant shift
- Slur — time-stretch plus low-pass filter
- Club music bleeding over the top
- Distance falloff from the window

### Speech degradation
- Self-contradiction — "no onions… extra onions"
- Mid-sentence swaps — they change their mind halfway through
- Components mumbled below intelligibility
- Questions that aren't on the menu ("do you do pizza?")

### Difficulty scaling
Drunkenness is set by location and time. Business park at lunch: **0.2**. Club district at 3am: **0.9**. The same system produces a completely different game at either end. This is the highest-leverage single variable in the design.

### Production cost
~200 short voice clips, one actor, roughly a weekend of recording. Combinatorial assembly means the bank never runs dry the way scripted lines would.

---

## 4.2 The Ticket

The counter player sees a ticket with intelligible components filled in and unintelligible ones as blanks:

```
KEBAB · [???] · NO ????? · EXTRA CHILLI
```

They know something is missing. They have to decide whether to chase it.

### Dialogue wheel — talking to customers

Prompt-based. No free speech, no voice recognition.

| Prompt | Effect |
|---|---|
| **Again?** | They repeat, differently garbled, mildly annoyed |
| **Onions?** (targeted) | Confirms one specific component, resolves one blank |
| **Yes / No** | Answers their off-menu nonsense |
| **Next!** | Commits the ticket and moves the queue |

### The patience bar

Every customer has one. Asking again costs patience. Empty it and they leave angry — or stay and get loud, which raises heat.

This is what stops "ask again" being a universal solution. Clarification is a **resource**, not a fix.

### The real decision

**You can commit a ticket with blanks still on it.** Guessing is faster and often correct. During a rush, you will guess. That gamble — accuracy versus throughput — is the moment-to-moment tension of the counter role.

---

## 4.3 The Ticket Rail — the relay mechanic

The counter player fills a ticket and **spikes it on a physical rail**. The kitchen reads the rail.

This is the information channel between front and back: in-world, and immune to whether anyone is using voice chat.

Critically, the ticket carries **only what the counter player committed** — including their guesses and their blanks. A blank on the rail means the kitchen has to decide for themselves.

**Why this matters:** miscommunication is preserved as a *mechanic* rather than depending on players talking. With proximity chat, people shout over the rail anyway and it gets funnier. Without it, the game is mechanically unchanged. That is the correct dependency direction.

---

## 4.4 The Meat Cone

The physics centerpiece of the game.

- **Heavy** — two-player carry by default (one player with upgraded gloves)
- **Unstable** — tips over if you're bumped
- **Swapping a fresh cone mid-rush** is a four-person disaster sequence
- **Dropped meat is still technically servable**, and someone always argues for it
- **Quality decays visibly** through the night

Almost all of the game's unscripted comedy comes from this object. It should get more animation and physics attention than anything else in the build.

---

## 4.5 The Meat Economy

The spine of the day phase.

| Source | Cost | Risk |
|---|---|---|
| Wholesale | High | None |
| Discount supplier | Medium | Occasional bad batch |
| The guy with a van | Very low | Sick customers, inspector interest, unclear species |

**Consequences are delayed and shared.** Bad meat doesn't fail at purchase — it fails during a rush two or three nights later, when a customer collapses outside the truck and a crowd forms.

That delay is what makes the day-phase argument real. Someone lobbies for cheap meat every night, and someone else remembers what happened last time.

---

## 4.6 The Inspector

### Trigger
Unannounced, but telegraphed by roughly **15 seconds**. A specific car door. A clipboard silhouette crossing the window. Long enough to panic, too short to fully clean.

### The stall — suspicion meter

One player goes to the window. A **suspicion meter** fills while the inspector is there. The stalling player gets prompts to slow it:

| Prompt | Effect | Cost |
|---|---|---|
| **Small talk** | Slows the meter | Cooldown between uses |
| **Offer free food** | Large pause | Costs stock — *and he eats it*, so bad meat backfires spectacularly |
| **Paperwork** | 8-second read | Once per night |
| **Point at something** | Weak slow | Spammable, low value |

**Nothing stops the meter.** You are buying seconds, and each tool has a different cost-to-duration ratio, so the stalling player is running a genuine optimisation problem under pressure.

Meter fills → he comes inside → he sees whatever state the truck is in.

### Violations — world-state flags checked on entry
- Meat on the floor
- Unlicensed second grill running
- Cone temperature out of range
- Open bins
- Fryer running
- Anyone visibly bleeding

### The cleanup — physical and timed

Cleanup costs the same seconds you need for service:

- Grills take **5 seconds** to power down
- The fryer smokes for **10 seconds** after you kill it
- Meat has to physically go somewhere — a bin, or out the window

**Customers keep queuing throughout.** You are being inspected and losing money simultaneously. That is the point of the scene.

### Outcome

Fines scale with the number of violations. **Three violation-inspections at a single pitch and you lose that location permanently** for the run. Real stakes without a game-over screen.

### Why this design
Two players are doing completely different urgent things, connected only by a timer both can see. That is a strong co-op scene regardless of whether anyone is talking.

---

## 4.7 The Till and the Pocket

The economy is deliberately split in two. This split is what makes theft meaningful rather than spiteful.

### THE TILL (shared)
Pays rent. Buys meat. Buys truck upgrades and new stations. Fail rent and everyone loses the night.

### YOUR POCKET (private)
Buys things only you get:

- **Better gloves** — carry the cone alone
- **Good knife** — faster, cleaner cuts
- **Non-slip shoes** — stop dropping things
- **Radio earpiece** — hear the counter from anywhere in the truck
- **Cosmetics** — which in this genre matter more than they should

### The theft mechanic

**There isn't one.**

The till is a drawer. The cash is a physical object. There is no lock and no prompt. Nothing in the game tells players this is possible. They discover it — typically around night four — and it changes the group permanently.

**Why it works:** that €40 in your pocket buys gloves that make you genuinely better at the job. So theft is partly selfish and partly justifiable. *"I bought gloves, we all benefit"* is an argument a real player will make at 1am.

### Detection is social, not systemic

The counter shows total takings. A rent shortfall is obvious. Who took it isn't.

Someone turning up next shift in new shoes is the best evidence system you could design, and it costs zero UI.

---

## 4.8 The Map — pitches

Each night you drive somewhere. The truck drives badly and everything in the back is unsecured.

| Pitch | Character |
|---|---|
| **Club district** | Enormous rush, maximum drunkenness, best money, most chaos |
| **Stadium** | One massive wave then dead silence — all-or-nothing prep |
| **Rest stop** | Few customers, absurd order volumes, long dead stretches that make sabotage tempting |
| **Festival** | No power hookup — a generator someone keeps tripping over |
| **Business park** | Sober customers who actually notice the meat |

**Pitches are contested.** Arrive late and a rival truck has taken the good corner.

---

# 5. PROGRESSION

This section exists to solve the staleness problem. The night doesn't change — the *context* around it changes until you are effectively playing a different game.

## 5.1 Fame and Heat — the two-meter spine

Not one reputation meter. **Two, that pull against each other.**

**FAME** — how many people know about you. Drives queue size and money.
**HEAT** — how much the city has noticed. Drives inspector frequency, fine size, and eventually losing pitches.

**There is no way to get rich quietly.** Almost everything that raises fame also raises heat.

### How fame is earned
- Speed of service
- Order accuracy
- Regulars satisfied
- Surviving a big rush intact

### How heat is earned
- Violations
- Fines
- Ambulances
- Complaints
- Anything loud

### The strategic decision
Late in a run you are famous enough to make real money and are being inspected every other night. The genuine choice becomes: keep pushing, or deliberately take a bad pitch for a night to cool off?

**This is an uncommon shape — you are being punished for succeeding.** That's the design's most distinctive idea and worth protecting.

### Fame tiers

| Tier | What the night feels like |
|---|---|
| **Unknown** | Thin queues, nobody cares, forgiving |
| **Local spot** | Steady queue, first named regulars appear |
| **Known** | Queue never empties, a food blogger shows up and films you |
| **Famous** | Enormous queues, constant phones out, inspector visits near-guaranteed |

### Phones out — the high-fame twist

At high fame, customers film you. Violations get **recorded**. Drop meat on the floor and it's a clip — heat spikes with no inspector present.

This attaches a cost to the physics comedy without adding a new system. The thing that was funny on night 2 is dangerous on night 18.

---

## 5.2 Menu unlocks — the collection axis

The equivalent of new fish per island. Something to work toward that isn't just a bigger number.

**Design rule: a new item must change the truck, not just the menu.** Every unlock introduces a new spatial or timing problem.

| Unlock | What it actually changes |
|---|---|
| **Loaded fries** | Fryer station. Hot oil, a timer that doesn't wait, two people now need the same corner. Rewires the truck's whole flow. |
| **Wraps** | Assembly on a flat surface — needs counter space you don't have |
| **Chicken cone** | Second cone, second rotisserie. The cone-swap disaster now happens twice as often. |
| **Falafel** | Cheap stock, keeps vegetarians happy, but needs a separate fryer or you cross-contaminate — which is a violation |
| **Burger** | Own grill, own timing, competes directly with cone space |
| **Soft drinks / fridge** | Trivial to make, big margin, but the fridge eats floor space |
| **Kebab pizza** | Oven, long cook time — a commitment made two minutes before you know if it's needed |
| **The Challenge Item** | An absurd four-portion monster. Rarely ordered, enormous payout, enormous fame. When it appears the whole truck stops to make it. A genuine set piece. |

### Gate on fame, not money
Money can be ground out. Fame requires actually being good. Gating on fame means unlocks arrive at the pace the difficulty is climbing.

### Sauces as a parallel collection
Cheaper, faster unlocks — garlic, chilli, a house sauce, something absurdly hot. Small dopamine hits between the big ones. They also multiply the order-combination space, so tickets get harder to read for free.

### The loadout cap — the critical trap to avoid

**Do not let players unlock everything and run it all at once.**

Cap what physically fits in the truck. You have space for **four stations** and you own eight. Each day the crew picks a loadout.

This turns unlocks from a checklist you finish into an ongoing decision, and forces an argument in the day phase — exactly the friction that phase needs.

---

## 5.3 Truck degradation

Equipment degrades permanently unless you pay to repair it. Repairs compete directly with rent and stock.

- The fryer runs cool
- A burner dies
- The window sticks
- The cone motor stutters, so the cone stops rotating and burns on one side

**Why this beats random events:** the *same* actions get worse. Your muscle memory keeps failing on things you already knew how to do. That's more durable than a power cut you've seen three times.

It's also **blameable**, which matters socially. "Who didn't fix the fryer" is a real argument.

---

## 5.4 Nightly conditions

Each pitch rolls a condition, **visible before you commit** — so it's a choice, not a surprise.

- **Match night** — one colossal wave, everyone orders the same thing, chaos is pure throughput
- **Rain** — half the customers, but they crowd inside and won't leave
- **Crackdown** — inspector comes twice, fines doubled, pays extra
- **Stag party** — one group order of 14 items, all garbled, on a single ticket
- **Nothing on** — dead night. Which is exactly when people start opening the till

---

## 5.5 The shape of a night

Don't run 12 flat minutes. Run a curve, with drunkenness rising on a schedule:

1. **Early** — sober, forgiving, time to prep
2. **Midnight peak** — maximum queue, maximum pressure
3. **3am** — shambles, drunkenness at 0.9, orders barely parse
4. **5am** — a strange quiet stretch where one entirely lucid person orders something impossible

The same night should feel like three different games.

---

## 5.6 Recurring characters

A handful of named regulars who return across nights and **remember**.

- The guy whose order you ruined on night 3 comes back on night 8, and he's brought friends
- Well-treated regulars will defend you to the inspector
- Standing orders — they don't even say it, they just nod

Cheap to build (a persistent flag on a customer), and it makes a run feel like it has a history.

---

# 6. SYSTEM INTERLOCK

Every system feeds the next:

```
cheap meat  →  more violations  →  bigger fines  →  pressure on the till
     ↑                                                      ↓
less money for good meat  ←  theft matters more  ←  rent shortfall
```

And in parallel:

```
better service  →  more fame  →  bigger queues  →  more money
                        ↓
                   more heat  →  more inspections  →  more fines
                        ↓
              phones out  →  violations get recorded  →  more heat
```

**The late-run state:** famous, understaffed, running a broken truck with a menu too big for it, being filmed. That is a fundamentally different game from night one, and no part of it is borrowed from another title.

---

# 7. ART DIRECTION

**Style: PS1 / low-poly, and commit to it.** In this genre the cheap look is the aesthetic, not a compromise. Flat untextured colours or tiny textures, no smooth shading, vertex snapping and affine texture warping via shader, aggressive fog to hide draw distance. Bad proportions read as intentional jank.

**Props are primitives.** A wrap is a cylinder. Fries are stretched cubes. The cone is a cone. Each is roughly 20 minutes in Blender.

**Characters — don't model them from scratch.**
- Blocky proportions: capsule body, cube head, no hands, two dots for a face
- Ragdoll everything — physics bodies are funny and need no animation, and drunk customers *should* have bad locomotion
- Mixamo for free rigged characters and animations
- Synty POLYGON packs (~$30–60) for a consistent base set

**Lighting does the work, not models.** Neon truck sign, one warm interior light, wet asphalt, heavy fog, film grain, slight chromatic aberration. Effort goes into the post-processing stack, not Blender.

**The two things to make by hand:** the Steam capsule image and the truck. Those are what people see before they buy. The crossed-out-onion logo covers the capsule.

---

# 8. PRODUCTION

## Why it's buildable solo

- One room, one counter, one grill
- No open world
- No AI pathfinding beyond a queue
- No combat
- Customers are a queue with garbled audio and a patience bar

Nearly everything expensive about game development, this design doesn't need.

## The hard part

**Networking.** Budget the majority of learning time here.

- **Unity 6 LTS + FishNet**
- **Steam P2P transport** via FishySteamworks + Facepunch.Steamworks — no server costs
- **Proximity voice** — Steam voice API or Dissonance
- The real time sinks are client-side prediction, ownership handoff, and desync bugs

## Steam logistics

- **$100 Steam Direct fee** per app, refundable after $1000 revenue
- Store page live **2 weeks** before launch
- Builds go through a short review
- Valve takes **30%**
- W-8BEN for US withholding; an s.p. to invoice the income cleanly

## The commercial reality

The genre is saturated and success is close to a lottery. These games don't win on quality — they win on one clippable mechanic that makes streamers scream.

For this game, that clip is: **four people arguing about what a drunk man said while a meat cone falls over.**

Build wishlists early, get a demo into Next Fest, treat marketing as roughly half the project.

---

# 9. OPEN QUESTIONS

- Does the failure state land better as going broke, or as being shut down?
- How many nights is a full run? (Suggested target: 15–20)
- Is there permanent meta-progression across runs, or does each run start clean?
- Does the rival truck ever become an active antagonist, or stay as ambient pressure?
- Solo play — viable, or explicitly co-op only?
