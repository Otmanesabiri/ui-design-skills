# Checklists: UI Components

## Buttons
- Minimum interactive size: 44 x 44px
- 1 primary button maximum in an action group
- No equivalent double CTA
- Text = precise action verb, not "OK" or "Submit"
- Dangerous action visually separated from current action
- Frequent actions in the thumb zone on mobile
- Focus, hover, active, disabled, and loading states mandatory

## Forms
- Mandatory persistent label for every field
- Group fields by theme
- Break into multi-step if the form exceeds 5 to 7 visible fields
- Validation on blur, except non-intrusive positive feedback
- Accept common input formats: spaces, dashes, case, prefixes
- Error message = problem + cause if useful + correction

## Modals and Dialogs
- One modal = one decision
- Visible close button in top right
- Escape and overlay click according to risk level
- Mandatory focus trap
- Actions at the bottom, primary clearly distinguished
- Destructive action confirmed by explicit text

## Feedback and States
- Under 300ms: not necessarily visual feedback
- 300ms to 1s: discreet spinner or local pending state
- 1s to 3s: skeleton or content structure
- Over 3s: progression, status text, or possibility to cancel
- Success: confirm the action and show the next step
- Error: explain without jargon and propose an action
