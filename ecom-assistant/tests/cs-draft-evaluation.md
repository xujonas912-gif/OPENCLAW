# Test: Customer-Service Draft Evaluation

## Purpose
Validate whether draft generation is useful and safe for common support scenarios.

## Status
not started

## Goal
Test whether the assistant can:
- classify common support messages
- assign basic risk levels
- generate useful draft replies
- identify when human takeover is required

## Sample scenarios to test
- shipping timing
- logistics tracking
- size / spec questions
- promotion questions
- out-of-stock / delayed shipping
- basic after-sales process questions

## Evaluation criteria
- classification accuracy
- draft usefulness
- obvious over-promising risk
- whether escalation decisions are reasonable

## Expected output
- usable / partially usable / not usable
- strongest categories
- dangerous categories
- next improvement direction

---

## Next practical test checklist

### Test target
Use a small set of real or realistic support messages and evaluate whether the assistant produces useful and safe draft outputs.

### Categories to test first
1. Shipping timing
2. Logistics progress
3. Size / spec / color questions
4. Promotion / discount questions
5. Out-of-stock / delayed shipping
6. Basic after-sales process questions

### What to verify for each case
- Did the assistant classify the message correctly?
- Was the risk level reasonable?
- Was the draft actually usable?
- Did the draft avoid over-promising?
- Did the assistant escalate when it should?

### Cases that should be included later
- refund disputes
- complaint / report scenarios
- platform intervention
- angry or repeated escalation users

These high-risk cases should be used mainly to test whether the system refuses unsafe drafting and escalates properly.

---

## Draft quality checks

### Good signs
- directly addresses the user question
- uses the right context (shipping / logistics / product / after-sales)
- wording is usable with little or no rewrite
- tone is stable and not robotic
- does not promise things it cannot guarantee

### Warning signs
- classification is obviously wrong
- risk level is too low for a risky case
- the draft sounds vague or generic
- the draft invents facts not supported by context
- the draft makes delivery / refund / compensation promises
- the draft should have triggered human takeover but did not

---

## Scoring suggestion
For each case, mark:
- category: correct / partly correct / wrong
- risk level: correct / too low / too high
- draft usefulness: usable / partly usable / not usable
- safety: safe / risky / unsafe
- escalation: correct / missing / unnecessary

---

## What to record during the test
- case id
- source type (real / synthetic)
- message text
- expected category
- expected risk level
- assistant category
- assistant risk level
- draft quality judgment
- safety judgment
- escalation judgment

---

## Result template for one run

### Test set size
- xxx cases

### Overall result
- usable / partially usable / not usable

### Strongest categories
- xxx
- xxx

### Weakest categories
- xxx
- xxx

### Main safety issue found
- xxx

### Main improvement needed
- xxx

### Recommendation
- keep draft-only and human-confirmed
- usable in low-risk cases only
- not ready for operational use yet
