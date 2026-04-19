# Product Check Rules

## Purpose
Define how product listings should be checked for obvious maintenance, quality, inventory, pricing, and state issues.

## Scope
Use for:
- daily listing maintenance checks
- pre-listing checks
- campaign re-checks
- inventory anomaly follow-up
- review / support-driven product review

Do not use for:
- automatic save of product changes
- direct auto-pricing
- direct auto up/down listing
- automatic SKU deletion

---

## Inputs
- product id
- title
- state / listing state / last updated time
- selling points / attributes / description / media info
- SKU structure
- SKU inventory / pricing
- total inventory / campaign price / recent price change context
- audit / violation state
- review concentration
- repeated support signals

---

## Outputs
- product issue list
- health judgment: healthy / needs maintenance / high risk
- suggested maintenance actions
- escalation result

---

## Health model
Check five dimensions:
- information health
- transaction health
- fulfillment health
- experience health
- risk health

---

## Priority levels

### P0
- taken down
- audit abnormal / violation warning
- zero stock while still active
- obvious pricing error
- SKU config error affecting orders

### P1
- low stock on hot SKU
- missing critical attributes
- title missing critical info
- abnormal campaign product state
- concentrated review / after-sales risk

### P2
- weak title expression
- unclear selling points
- media / copy can improve
- stale maintenance
- inconsistent spec naming

### P3
- mild conversion drift
- rising inquiries without identified cause
- weak performance on some SKUs

---

## Check rules

### Title / selling points
Check:
- too short
- keyword stuffing
- missing critical info
- vague wording
- unclear selling points
- mismatch between title and main selling point

### Attributes
Check:
- missing key attributes
- conflicting attribute values
- mismatch across title / attributes / description
- missing required platform fields

### SKU / specs
Check:
- SKU completeness
- naming consistency
- missing variants
- mapping consistency across SKU / stock / price
- invalid SKUs

### Inventory
Check:
- low stock
- hot-SKU low stock
- zero-stock while active
- partial variant stockout
- stale inventory anomaly

### Pricing
Check:
- obvious pricing anomaly
- broken SKU price logic
- campaign pricing conflict
- obvious mismatch with product positioning

### State / risk
Check:
- taken down
- audit abnormal
- violation flags
- stale maintenance
- concentrated review / after-sales risk

---

## Linkages

### From inspection
Send product into product-check when inspection finds:
- stock anomaly
- product state anomaly
- concentrated negative reviews
- campaign product anomaly

### From customer service
Send product into product-check when support shows:
- repeated size/spec confusion
- repeated attribute misunderstanding
- repeated questions on same issue
- concentrated after-sales issues

### To manual review
Anything involving:
- price changes
- inventory changes
- listing-state changes
- final saved edits to title / attributes / SKU

---

## Risk boundary
Product-check may:
- read product info
- detect issues
- prioritize
- suggest actions
- hand off

Product-check may not:
- auto-save edits
- auto-change price
- auto up/down list
- auto delete SKU
- auto batch modify listings

---

## Automation notes
Recommended rollout:
1. read product list and detail fields
2. extract title / attributes / SKU / inventory / price / state
3. run checks
4. output issue list
5. push high-risk items to manual review

---

## Logging fields
At minimum record:
- time
- product id
- checks triggered
- number of issues
- P0/P1/P2/P3 counts
- linked inspection/support source
- sent to manual review or not
