# Automation Control Rules

## Purpose
Define task classes, execution boundaries, confirmation gates, stop conditions, and audit expectations for backend automation.

## Scope
Use for:
- scheduled inspection
- report collection
- support-draft preparation
- product-check tasks
- confirmation-gated execution tasks
- fixed backend SOP automation

Do not use for:
- unconfirmed high-risk submissions
- unbounded multi-store batch actions
- execution without logs

---

## Task classes

### 1. Read-only
- collect
- judge
- output
- no write action

Examples:
- inspection
- report export
- status checks
- review monitoring
- message monitoring
- product state checks

### 2. Draft-preparation
- analyze
- generate suggestions
- prepare drafts / action plans
- no submit

Examples:
- support drafts
- listing improvement suggestions
- pricing suggestion sheet
- replenishment suggestion sheet

### 3. Confirmed execution
- system prepares action
- human confirms
- system executes within limits

Examples:
- batch replies in safe scenarios
- whitelisted listing edits
- fixed SOP backend clicks

### 4. Forbidden automation
- system may only remind or prepare advice
- no autonomous submit

Examples:
- final refund / compensation handling
- high-risk repricing
- large-scale up/down listing
- final platform dispute reply
- high-risk public replies
- unbounded cross-store actions

---

## Required confirmation gate
Every confirmed-execution task must show:
- target object
- reason
- risk note
- impact scope
- expected count
- confirmation status

Before execution, the operator must see:
- what will be changed
- why
- risk level
- scope
- rollback possibility if relevant

---

## Default forbidden actions
- automatic refunds
- automatic compensation promises
- automatic high-risk repricing
- automatic large-scale listing-state changes
- automatic high-risk public review replies
- automatic dispute-message sending
- automatic cross-store batch operations
- automatic platform-complaint handling

---

## Default confirmation-required actions
- outbound messages
- batch support / review replies
- batch save of listing edits
- price changes
- inventory-related changes
- listing-state changes
- campaign enrollment / configuration submissions

---

## Good early automation targets
- inspection
- aggregation
- reminders
- draft generation
- suggestion sheets
- exports
- fixed-format daily / weekly reports

---

## Stop-immediately conditions
Stop the workflow if any of these occur:
- login failure / expired auth
- unexpected page structure
- missing critical elements
- data extraction failure
- abnormal target count
- scope outside whitelist
- confirmation missing where required
- result clearly inconsistent with expectation

When stopped, record:
- failure step
- failure reason
- current task state
- manual check recommendation

---

## Quantity limits
Always set limits for:
- draft generation batch size
- pending confirmation batch size
- execution batch size
- forced split or manual review above threshold

---

## Whitelist principle
No clear whitelist, no execution.
Whitelist may include:
- target store
- product subset
- message type subset
- campaign subset
- test-only scope

---

## Audit logging
At minimum record:
- task name
- run time
- module
- input source
- extraction result
- generated suggestion
- entered confirmation gate or not
- execution action
- success / failure
- failure reason

For confirmed execution also record:
- who confirmed
- confirmation time
- number of objects acted on
- actual result
