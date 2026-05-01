# Antipatterns & UI Ethics

Objective: identify and avoid interfaces that exploit cognitive biases against the user's interest. A persuasive interface can guide. A manipulative interface pushes the user towards an action they might regret.

Principle:
- Acceptable Persuasion: clarifies value, reduces friction, helps decide
- Forbidden Manipulation: hides, distorts, shames, traps, or makes refusal difficult

---

## Ground Rule

A user decision must be:
- Informed: consequences, costs, and conditions visible before action
- Free: accepting and refusing are both accessible
- Reversible when risk is high
- Understandable without jargon
- Not dependent on artificial pressure

If the design only works because the user doesn't see, doesn't understand, or doesn't dare refuse, it's a dark pattern.

---

## Critical Antipatterns

### Confirmshaming

Definition: formulating refusal in a shaming or humiliating way.

Examples:
- "No thanks, I prefer paying more"
- "I don't want to improve"
- "Ignore this opportunity"

Fix:
- Use a neutral refusal: "No thanks", "Continue without subscription", "Later"

### Hidden costs

Definition: revealing fees, taxes, conditions, or commitments only at the end of the path.

Fix:
- Display total cost before engaging action
- Explain variable fees as soon as they become calculable
- Do not use checkout as a surprise moment

### Roach motel

Definition: easy to enter, hard to exit.

Typical cases:
- 1-click signup, manual support cancellation
- Hidden account deletion
- Cancellation behind several asymmetrical confirmations

Fix:
- Exit as accessible as entry
- Cancellation in expected settings
- Clear confirmation, without punitive friction

### Misdirection

Definition: drawing attention towards an action beneficial to the business and away from the action important to the user.

Fix:
- Hierarchy based on user importance
- Destructive or engaging actions visible and explicit
- No primary color to mask a less favorable option

### Disguised ads

Definition: ad or sponsored content presented as normal content.

Fix:
- "Sponsored", "Advertisement", or equivalent label visible
- Style distinct from editorial or functional content
- No imitation of system notifications

### Trick questions

Definition: ambiguous formulation, double negation, or checkbox that reverses intention.

Examples:
- "Uncheck this box if you do not wish not to receive..."
- Pre-checked consent

Fix:
- Simple positive phrase
- Explicit opt-in consent
- One box = one clear intention

### Forced continuity

Definition: converting a free trial into payment without a clear reminder.

Fix:
- Reminder before billing
- Date and amount visible
- Easy cancellation before renewal

### Sneaking

Definition: adding a product, service, insurance, or option without explicit action.

Fix:
- Additional options in opt-in
- Clear summary before payment
- No automatic addition to cart

### Artificial Scarcity or Urgency

Definition: fake scarcity or fake countdown to accelerate decision.

Fix:
- Use urgency only if it is real and verifiable
- Explain the cause: stock, deadline, capacity
- Do not reset a timer artificially

### Obstruction

Definition: making a useful action unnecessarily long or confusing.

Typical cases:
- Closing an account
- Exporting data
- Refusing tracking
- Changing a subscription

Fix:
- Direct path
- Explicit labels
- No unnecessary steps

---

## Sensitive Patterns

These patterns are not forbidden, but must be controlled.

### Defaults

Acceptable if:
- The default choice corresponds to the user's probable interest
- It is visible
- It is easy to change

Risk if:
- Paid option checked by default
- Consent given by inaction
- Recommended choice without justification

### Recommendations

Acceptable if:
- The recommendation is explained
- Alternatives remain comparable
- Criteria are useful to the user

Risk if:
- "Recommended" only means "more profitable"
- The highlighted option hides a commitment

### Gamification

Acceptable if:
- It motivates without punishing
- It leaves control to the user
- It does not create excessive anxiety

Risk if:
- Streaks, losses, or rewards push to regrettable behaviors
- Shaming notifications

### Personalization

Acceptable if:
- Data used is relevant
- Control is explicit
- User can modify or deactivate

Risk if:
- Opaque profiling
- Prices or options manipulated according to supposed vulnerability

---

## Ethics Checklist Before Delivery

- Does the user understand what they are accepting?
- Can they refuse without humiliation or excessive friction?
- Is the total cost visible before engagement?
- Are important consequences explicit?
- Is consent opt-in when it concerns data, marketing, or payment?
- Is cancellation as findable as signup?
- Do destructive actions require confirmation?
- Do error messages help instead of blaming?
- Are recommended options justifiable on the user side?
- Does the design remain acceptable if the user is tired, rushed, or novice?

---

## Blocking Red Flags

- Pre-checked consent for tracking, marketing, or payment
- Hidden fees until the last screen
- Refusal formulated in a shaming way
- Hidden cancellation or only via support
- Data deletion without explicit confirmation
- Artificial timer or scarcity
- Ad disguised as content or notification
- Paid option added automatically

Every red flag must be fixed before delivery.

---

## Recommended Formulations

| Situation | Avoid | Prefer |
|---|---|---|
| Newsletter refusal | No, I don't want benefits | No thanks |
| Free trial | Start | Start free trial - then 12 EUR/month |
| Deletion | OK | Delete permanently |
| Tracking | Improve my experience | Accept analysis cookies |
| Cancellation | Continue | Keep my subscription |

---

## Simple Test

Ask yourself this question:

> Would I be comfortable explaining this design choice to the concerned user, face to face?

If the answer is no, the pattern must be modified.
