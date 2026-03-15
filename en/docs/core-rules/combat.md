# Combat

## Durability: two layers

Combat damage operates across two distinct layers. These are not interchangeable — they represent fundamentally different things.

### Vitality

Stamina, adrenaline, near-misses, and the absorption provided by armour and positioning. Vitality depletes freely in combat with no fictional weight attached — the character is not yet being cut. It recovers relatively quickly outside of combat.

Vitality maximum is derived from Constitution and class.

### Wounds

The actual body. A fixed, low number (Constitution ÷ 4, minimum 1) representing how much real anatomical damage a character can sustain before death or permanent incapacitation. When Vitality reaches zero, overflow damage threatens Wounds directly.

Wounds do not recover quickly. Minor wounds require rest and treatment. Serious and Grievous wounds require a surgeon, not a healer — they sit outside the reach of magic.

---

## Damage dice

Every weapon has two dice:

**Base die** — the force of the hit. Scales with weapon, not character level. A dagger is d4; a greatsword is d10. A character's power at higher levels comes from more Vitality and better defences, not from absorbing more stab wounds.

**Injury die** — rolled only when a hit reaches Wounds. Always d6, determining wound severity regardless of weapon:

| Injury die | Severity |
| ---------- | -------- |
| 1–2        | Minor    |
| 3–4        | Serious  |
| 5–6        | Grievous |

---

## Hit locations

When a Wound is inflicted, roll or choose a hit location. The location is determined narratively where possible — a prone opponent is far more likely to take a head wound than a standing one.

| d6  | Location               | Condition                        |
| --- | ---------------------- | -------------------------------- |
| 1   | Head                   | Concussion; perception impaired  |
| 2   | Throat / neck          | Silenced; bleeding               |
| 3   | Chest                  | Stamina penalty; broken rib risk |
| 4   | Abdomen                | Winded; infection risk           |
| 5   | Arm (weapon or shield) | Disarm risk; attack penalty      |
| 6   | Leg                    | Movement halved; fall risk       |

A staggered or prone opponent shifts the location roll — the GM may reroll or choose, biasing toward head and neck. This reflects the historical record: killing blows in medieval combat were disproportionately delivered to downed opponents, targeting exposed anatomy.

---

## Wound severity

Wounds are not just hit point reductions. Each wound imposes a **condition** lasting until properly treated.

| Severity | Mechanical effect                                                                      | Treatment                   |
| -------- | -------------------------------------------------------------------------------------- | --------------------------- |
| Minor    | Disadvantage on one relevant action type                                               | Rest + basic treatment      |
| Serious  | Ongoing Vitality loss (1 per round or per scene); hard penalty                         | Physician + time            |
| Grievous | Immediate stabilisation check or unconscious; permanent scar / impairment if untreated | Surgeon + extended recovery |

Multiple simultaneous wounds stack their conditions. A Grievous leg wound means the character is dragging a ruined leg — this is not abstracted away.

---

## Armour

Armour reduces injury **severity** rather than raw damage. A hit that reaches Wounds against a heavily armoured opponent rolls the injury die at disadvantage (take the lower result). This reflects the historical reality: armour doesn't stop force, it redistributes and reduces its anatomical consequence.

Armour tiers:

| Tier | Example          | Injury die                                 |
| ---- | ---------------- | ------------------------------------------ |
| 0    | Unarmoured       | Normal roll                                |
| 1    | Padded / leather | Normal roll                                |
| 2    | Mail             | Roll twice, take lower                     |
| 3    | Plate            | Roll twice, take lower; Minor on 1–4       |
| 4    | Full plate       | Roll twice, take lower; Grievous only on 6 |

---

## Critical hits

A critical hit bypasses Vitality entirely — the attack finds a gap in the defence and strikes anatomy directly.

### Critical Threshold (CT)

Every successful attack has a CT the attacker must also meet or beat:

```
CT = 15 + Defender Armour Tier − Attacker Precision Bonus
```

**Precision** is weapon-gated. A stiletto, estoc, or bodkin-tipped arrow can have high Precision. A greatsword cannot. This encodes the historical logic: armour is bypassed with the right tool, not raw strength.

Precision bonus is approximately −1 per 3 levels, capped by weapon type.

### The assassin exception

If the attacker is **undetected** at the moment of the strike, CT is replaced by:

```
CT = 10 − Attacker Precision Bonus
```

A skilled assassin with Precision +4 needs a 6 or better. This is their one window. Detection before the strike reverts CT to the standard formula.

### Critical effect

1. Bypass Vitality entirely
2. Roll the injury die **twice**, apply the worse result
3. Injury die is automatically d6 regardless of weapon base die

The double roll is not a guaranteed Grievous — two Minor results in different locations may be more debilitating than one Serious, depending on conditions.
