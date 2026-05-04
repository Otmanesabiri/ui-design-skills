# UX Writing & Micro-copy

Sources: NNGroup · Google Material Guidelines · Torrey Podmajersky (Strategic Writing for UX)

> **Agent Instruction:** Load this file ONLY when writing UI text (button labels, errors, empty states). For component structure (where to place buttons/labels), see `references/composants.md`. For ethical formulations, see `references/antipatterns-ethique.md`. For CSS values, reference `references/tokens.md`.

---

## Core Principles

### 1. Clarity Over Cleverness
The user is completing a task, not reading a novel. Every word must serve the action.

| ❌ Avoid | ✅ Prefer |
|----------|----------|
| "Oops! Something went sideways!" | "Payment failed. Your card was not charged." |
| "Let's get started!" | "Create your account" |
| "Are you sure you want to do this?" | "Delete this merchant? This cannot be undone." |

### 2. Front-Load the Key Information
Users scan, they don't read. The most important word comes first.

```
❌ "Click here to download your invoice"
✅ "Download invoice"

❌ "If you want to cancel your subscription, click here"
✅ "Cancel subscription"
```

### 3. Use the User's Language
Avoid internal jargon, technical terms, or business-speak.

| Internal Term | User-Facing Term |
|---------------|-----------------|
| "Entity" | "Merchant" or "Account" |
| "Payload" | "Data" or "Information" |
| "Authenticate" | "Log in" or "Verify your identity" |
| "Instantiate" | "Create" |
| "RBAC" | "Permissions" |

---

## Button Labels

### The Formula: Verb + Object

Every button must answer: *"What will happen when I click this?"*

```
❌ "OK"          → Too vague. OK to what?
❌ "Submit"      → Submit what?
❌ "Confirm"     → Confirm what?

✅ "Save changes"
✅ "Send payment"
✅ "Delete merchant"
✅ "Create account"
✅ "Download report"
```

### Destructive Actions: Be Explicit

```
❌ "Delete"
✅ "Delete this merchant permanently"

❌ "Remove"
✅ "Remove card ending in 4242"
```

### Button Hierarchy and Label Tone

| Button Type | Tone | Examples |
|------------|------|----------|
| **Primary** | Action-oriented, confident | "Start free trial", "Save changes" |
| **Secondary** | Neutral, alternative | "Cancel", "Go back", "Skip for now" |
| **Destructive** | Clear, explicit consequence | "Delete account", "Revoke access" |
| **Ghost/Link** | Informative | "Learn more", "View details" |

### Capitalization
- **Sentence case** preferred: "Save changes" (not "Save Changes")
- Exception: proper nouns ("Log in with Google")

---

## Error Messages

### The 3-Part Structure

Every error message must contain:

```
1. WHAT happened (clear statement)
2. WHY it happened (cause, if relevant)
3. HOW to fix it (actionable next step)
```

### Examples

```
❌ "Error 422"
❌ "Invalid input"
❌ "Something went wrong"

✅ Structure:
┌──────────────────────────────────────────────┐
│ ✗ Payment declined                           │  ← WHAT
│                                              │
│ Your bank declined the transaction.          │  ← WHY
│ Try a different card or contact your bank.   │  ← HOW
│                                              │
│ [Try another card]  [Contact support]        │
└──────────────────────────────────────────────┘
```

### Error Message Patterns by Context

| Context | Message Pattern |
|---------|----------------|
| **Required field** | "[Field name] is required" |
| **Format error** | "Enter a valid [type]. Example: [example]" |
| **Server error** | "We couldn't [action]. Please try again." |
| **Permission** | "You don't have permission to [action]. Contact your admin." |
| **Not found** | "We couldn't find [item]. It may have been deleted." |
| **Timeout** | "This is taking longer than usual. Please try again." |

### Never Display

```
❌ Error 500
❌ NullPointerException
❌ ECONNREFUSED
❌ Unhandled promise rejection
❌ "An error occurred" (without explanation)
```

---

## Empty States

### Structure

Every empty state must guide the user toward action:

```
[Illustration or Icon]

Title: Descriptive, not blame-y
Body: Brief explanation of what goes here
CTA: One clear action button

Example:
┌──────────────────────────────────────────┐
│         📊                               │
│                                          │
│   No transactions yet                    │
│                                          │
│   Transactions will appear here once     │
│   your first payment is processed.       │
│                                          │
│         [Process a payment]              │
└──────────────────────────────────────────┘
```

### Tone Rules

| ❌ Avoid | ✅ Prefer |
|----------|----------|
| "Nothing here" | "No transactions yet" |
| "No data" | "No results match your filters" |
| "Empty" | "You haven't added any team members" |

---

## Form Labels & Helper Text

### Labels

```
Rules:
1. Always above the field, not to the left
2. Short and specific: "Email address" not "Please enter your email"
3. Required fields: mark optional fields instead of required ones
   → "(optional)" suffix is clearer than asterisks

Example:
  Company name
  [________________________]

  Phone number (optional)
  [________________________]
```

### Placeholder Text

```
Rules:
1. NEVER use placeholder as the only label (it disappears on focus)
2. Use placeholder for format hints only

✅ Label:  "Card number"
   Placeholder: "4242 4242 4242 4242"

✅ Label:  "Date of birth"
   Placeholder: "DD/MM/YYYY"

❌ Placeholder-only: "Enter your email..."
```

### Helper Text

```
Rules:
1. Below the field, smaller font, muted color
2. Explain constraints BEFORE the user makes a mistake
3. Keep under 1 line

Example:
  Password
  [________________________]
  At least 8 characters with one number

Not:
  Password
  [________________________]
  Your password must contain at least 8 characters, including at least
  one uppercase letter, one lowercase letter, one number, and one
  special character from the following set: !@#$%^&*
```

---

## Confirmation Dialogs

### Destructive Action Confirmation

```
Title: Action + Object + Consequence
Body: What will happen, irreversibility
Primary button: Repeat the action verb (not "OK" or "Yes")
Secondary button: "Cancel" (never shaming)

Example:
┌──────────────────────────────────────────┐
│ Delete merchant "Acme Corp"?             │
│                                          │
│ This will permanently delete the         │
│ merchant and all associated data.        │
│ This action cannot be undone.            │
│                                          │
│     [Cancel]        [Delete merchant]    │
└──────────────────────────────────────────┘

❌ "Are you sure?" → Too vague
❌ [No] [Yes] → Which is which?
❌ "Do you really want to delete?" → Condescending
```

---

## Loading & Progress Copy

| Duration | Copy Pattern |
|----------|-------------|
| < 2s | No text needed (spinner or skeleton only) |
| 2-5s | "Loading..." or "Processing payment..." |
| 5-15s | "This usually takes a few seconds..." |
| 15s+ | "Still working... This is taking longer than usual." |
| Background | "Your report is being generated. We'll email you when it's ready." |

---

## Success Messages

```
Rules:
1. Be specific about what succeeded
2. Suggest a next action if relevant
3. Use a positive but not exaggerated tone

✅ "Payment processed successfully. Receipt sent to john@example.com."
✅ "Merchant created. You can now configure payment methods."

❌ "Success!"
❌ "Yay! 🎉 Everything worked!"
❌ "Done."
```

---

## Tooltips & Contextual Help

```
Rules:
1. Max 1-2 sentences
2. Explain WHY, not just WHAT (the label already says what)
3. Trigger on hover (desktop) or info icon tap (mobile)
4. Never put critical information in tooltips only

Example:
  Settlement delay   ⓘ
  Tooltip: "The number of business days before funds
            are transferred to the merchant's bank account."

Not:
  Tooltip: "Settlement delay"  ← just repeats the label
```

---

## Checklist UX Writing

```
Buttons
[ ] Every button uses Verb + Object (not "OK" or "Submit")
[ ] Destructive buttons explicitly state the consequence
[ ] Sentence case used consistently

Errors
[ ] Every error has WHAT + WHY + HOW
[ ] No technical jargon exposed to users
[ ] Error tone is helpful, not blaming

Empty States
[ ] Every empty state has title + explanation + CTA
[ ] Tone is encouraging, not dismissive

Forms
[ ] Labels above fields, never placeholder-only
[ ] Helper text explains constraints before mistakes
[ ] Optional fields marked, not required ones

Confirmations
[ ] Destructive dialogs repeat the action verb
[ ] No "Are you sure?" without context
[ ] Cancel option is always neutral (no shaming)

General
[ ] Key information front-loaded in every sentence
[ ] No internal jargon — user's language only
[ ] Consistent terminology across the entire application
```
