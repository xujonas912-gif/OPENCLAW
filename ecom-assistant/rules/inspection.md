# Inspection Rules

## Purpose
Define how the inspection module should detect store-level issues, prioritize them, and hand them off to downstream modules.

## Scope
Use for:
- daily store inspection
- midday / evening re-checks
- exception review
- daily report generation
- periodic read-only inspection tasks

Do not use this file for:
- direct product edits
- direct customer reply sending
- direct price / inventory / listing-state changes

---

## Inputs

### Orders
- order id
- order status
- payment time
- remaining ship deadline
- product title
- SKU
- notes
- after-sales status

### Support / messages
- conversation id
- latest message content
- latest message time
- unreplied flag
- timeout flag
- linked order info
- linked product info

### Inventory
- product id
- SKU
- current inventory
- inventory update time
- hot-selling SKU flag
- active listing state

### Products
- product title
- product state
- listing state
- review / audit state
- abnormal / violation flags
- last updated time

### Reviews
- review id
- review time
- rating / sentiment
- review content
- replied flag
- linked product

### Campaigns (optional)
- campaign name
- start time
- end time
- enrollment state
- linked products

---

## Outputs
- daily inspection report
- exception list
- prioritized todo list
- handoff queue for cs draft / product check / manual review

---

## Priority levels

### P0: immediate
Examples:
- near-timeout unshipped orders
- complaint / platform-intervention messages
- zero inventory while still selling
- product taken down / serious violation state
- concentrated new negative reviews

### P1: today
Examples:
- low-stock hot items
- high-risk unreplied support messages
- unhandled negative reviews
- after-sales backlog
- campaign state not checked near deadline

### P2: soon
Examples:
- products needing optimization
- incomplete attributes
- stale product maintenance
- missing support templates

### P3: observe
Examples:
- inquiry volume rising
- SKU stock trending down but not critical yet
- mild review quality drift

---

## Rules by domain

### Orders
- remaining shipping time < 4h -> P1
- remaining shipping time < 2h -> P0
- after-sales case above threshold -> P1
- repeated abnormal orders on same product -> P2/P1 depending on count
- unusual notes -> at least P1, human check needed

### Support / messages
- unreplied > 15 min -> P2
- unreplied > 30 min -> P1
- complaint / refund / platform / compensation / rights-defense keywords -> P0/P1
- repeated angry follow-ups -> P1
- standard unanswered message -> handoff to cs draft module

### Inventory
- inventory <= 5 -> P2/P1
- hot-selling SKU inventory <= 3 -> P1
- inventory = 0 while still active -> P0
- partial SKU stockout -> P1/P2
- stale inventory anomaly -> P2

### Products
- taken down -> P0
- audit abnormal / violation flag -> P0/P1
- long unmaintained -> P2
- obvious title / attribute / state issue -> P1/P2
- linked inventory/review/product anomaly -> escalate to product check

### Reviews
- one new negative review -> P2/P1
- >= 2 new negative reviews in a day -> P1
- strong negative wording -> at least P1
- unreplied negative review -> P1/P2
- concentrated negative reviews on one product -> P1 + handoff to product check

### Campaigns
- campaign starting soon but not checked -> P1
- campaign ending soon and needs re-check -> P2/P1
- campaign product low inventory -> P1
- campaign product abnormal state -> P1/P0

---

## Handoffs

### To customer-service draft module
- standard unanswered support scenarios
- low / medium-risk customer messages suitable for drafting

### To product-check module
- product state anomaly
- inventory anomaly
- concentrated review anomaly
- likely product-info issue causing repeated questions or reviews

### To manual review
- any action involving execution
- price / inventory / listing-state changes
- compensation / complaint / refund / promise situations

---

## Risk boundary
Inspection is read-only by default:
- read
- judge
- prioritize
- report
- hand off

Inspection should not:
- edit products
- send customer replies
- submit price or inventory changes
- change listing states
- auto-handle refunds / after-sales

---

## Automation notes
Recommended rollout:
1. fetch pages / exports on a schedule
2. extract key fields
3. judge anomalies by rules
4. produce report
5. separately alert on P0 / P1
6. hand off to cs / product modules

---

## Logging fields
At minimum record:
- time
- scope
- data source
- anomaly counts
- P0/P1/P2/P3 counts
- output location
- handoff status
- interrupted or not
