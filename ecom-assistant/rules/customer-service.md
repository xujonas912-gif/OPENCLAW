# Customer-Service Draft Rules

## Purpose
Define how support messages should be classified, risk-ranked, drafted, and escalated.

## Scope
Use for:
- shop support message handling
- DM / conversation assistance
- FAQ drafting
- basic review-reply assistance
- sales / after-sales triage

Do not use for:
- final refund / compensation decisions
- direct auto-send of high-risk messages
- final platform dispute replies
- legal / liability judgments

---

## Inputs
- current customer message
- recent conversation context
- timing / message frequency
- emotion / escalation signals
- order status
- shipping / logistics state
- product title / SKU / attributes / inventory / promotion info
- rules, templates, blacklists

---

## Outputs
- category
- risk level (L1 / L2 / L3)
- suggested draft reply or handling strategy
- suggested action: use / confirm / human takeover
- handoff result

---

## Categories

### 1. Pre-sales inquiry
Examples:
- availability
- size / spec / color
- materials / function / fit
- shipping timing
- promotions
Default: L1

### 2. Shipping timing inquiry
Examples:
- when will it ship
- can it ship today
- why not shipped yet
Default: L1/L2

### 3. Logistics progress inquiry
Examples:
- where is it now
- why tracking not moving
- when will it arrive
Default: L1/L2

### 4. Out-of-stock / delayed shipping
Examples:
- why still not shipped
- is it out of stock
- how long do I wait
Default: L2

### 5. After-sales process inquiry
Examples:
- how to return / exchange
- defects / wrong items / missing items
Default: L2, escalate to L3 if liability / compensation involved

### 6. Refund / complaint / dispute
Examples:
- I want a refund
- I want to complain
- platform intervention
- report / rights defense
Default: L3

### 7. Review-related communication
Examples:
- negative review handling
- misunderstanding in review
- public review reply
Default: L2

### 8. Angry / tangled / unclassifiable
Examples:
- repeated angry follow-up
- hostile tone
- multiple mixed issues in one thread
Default: L3

---

## Risk levels

### L1: low risk
- standardized issue
- clear info
- no dispute / liability / compensation promise
Action: draft allowed, human quick review still recommended at first

### L2: medium risk
- likely to affect satisfaction
- wording matters
- may involve delay, after-sales explanation, implied compensation
Action: draft allowed, human confirmation required

### L3: high risk
- complaint / refund / compensation / liability / platform intervention
Action: no final auto-send draft, only handling strategy; human takeover required

---

## Escalation triggers
Escalate one level or directly to L3 if any apply:
- complaint / report / rights defense / platform intervention / fake / compensation keywords
- repeated dissatisfaction across multiple turns
- explicit money / liability / compensation discussion
- requests for hard delivery / refund / re-send promises
- mixed multi-topic issue
- low confidence classification

---

## Drafting rules

### Standard L1 draft
- answer directly
- add necessary info
- optionally invite follow-up

### Logistics explanation draft
- explain current logistics state
- explain likely cause
- give follow-up timing or next step

### Delay-soothing draft
- apologize first
- explain cause
- give available options
- do not promise compensation automatically

### After-sales process draft
- confirm the issue
- explain process
- tell user what info is needed
- explain next follow-up path

### L3 handling strategy
- do not output final send-ready text
- output issue summary, risk points, suggested human handling strategy

---

## Sensitive wording blacklist
Do not auto-send these by default:
- compensation
- full responsibility
- guaranteed today
- platform will definitely support you
- guaranteed refund success
- immediate refund
- guaranteed re-send

---

## Mandatory human takeover
- complaint / report / rights defense / platform intervention
- compensation / money / liability / refund dispute
- strong emotion or repeated escalation
- evidence-heavy / image-heavy complex issue
- mixed complex themes
- low-confidence classification

---

## Linkages

### To order check
- shipping / logistics / after-sales issue tied to order state
- complaint linked to fulfillment anomaly

### To product check
- repeated size/spec/attribute confusion
- repeated misunderstanding on same product
- concentrated negative reviews / after-sales on same product

### To manual review pool
- any outbound message requiring confirmation
- any high-risk thread needing human takeover

---

## Risk boundary
CS module may:
- classify
- risk-rank
- draft
- suggest handling
- hand off

CS module may not:
- auto-send high-risk messages
- promise refund / compensation / liability
- close complex disputes autonomously

---

## Logging fields
At minimum record:
- time
- conversation id
- category
- risk level
- keyword hit or not
- draft generated or not
- escalated or not
- linked to order/product checks or not
