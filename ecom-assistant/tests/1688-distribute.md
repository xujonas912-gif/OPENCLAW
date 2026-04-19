# Test: 1688 Distribute Chain

## Purpose
Track the real feasibility of the 1688 distribute / listing workflow.

## Status
partial

## Latest assessed state
The chain is no longer blocked at authorization or page readability. It is now partially validated with the remaining hard point concentrated on stable selector/control access for the fixed bottom action bar inside nested iframes.

## Goal
Validate the full chain from product page to final distribute / publish action.

## What has been validated
- Open and read a 1688 product page.
- Enter the product detail page.
- Trigger the "立即铺货" action.
- Reach the authorization checkpoint.
- Click "去授权".
- Complete the Taobao OAuth step for the related app.
- Return to the product page and confirm authorized state.
- Enter the distribute settings page / container.

## Current blocker
- The settings-page body is now readable and real controls have been found.
- The remaining blocker is the fixed bottom action bar inside nested iframes: the final buttons are visible in screenshots, but their clickable refs/selectors are not yet stable in the current ACP snapshot path.

## Conclusion so far
- Authorization path: validated
- Settings-entry path: validated
- Settings-page body readability: validated
- Nested iframe structure: validated as the main technical cause of earlier read issues
- In-frame settings controls: partially validated (real form controls can be located and clicked)
- Final publish / sync action: only partially validated because the fixed bottom buttons are visible but not yet stably targetable

## Newly validated details
- The `channel=thyny` distribute settings page body can now be read stably.
- The page clearly contains sections such as:
  - 选择店铺
  - 基础信息
  - 属性设置
  - 价格设置
  - 规格设置
  - 同步设置
  - 服务信息
  - 内容信息
  - 拦截设置
  - 分账申请
- The page structure is effectively:
  - top container: `ufuwu.1688.com/page/fuwu_work_isv_container.htm`
  - iframe: `name=fuwu_work_isv_container_frame`
  - bridge/container layer under `page.1688.com`
  - inner business DOM where the real content lives
- Real in-frame controls have already been located and interacted with, including examples like:
  - `选择对应平台店铺` combobox
  - `商品类目 -> 自动匹配` radio
- The fixed bottom action bar is visually confirmed to contain:
  - `保存配置`
  - `保存并同步到其他店铺`
  - `取消修改`

---

## Next practical test checklist

### Test target
Do not re-verify the whole page. Focus only on the fixed bottom action bar and determine whether its controls can be stably targeted inside the nested iframe structure.

### Narrow next-step objective
Confirm the real DOM location and stable selector/ref path for:
- 保存配置
- 保存并同步到其他店铺
- 取消修改

### What to verify next
1. Whether the fixed bottom action bar lives in the same inner frame as the settings form, or in another layer / frame / portal-like container.
2. Whether the action-bar buttons exist in the real DOM of the active frame, not just visually in screenshots.
3. Whether any of those buttons can be stably located by text / selector.
4. Whether hover / locate works reliably before any real click attempt.
5. Whether the current limitation is:
   - frame mismatch
   - sticky / fixed overlay behavior
   - selector instability
   - ACP snapshot/ref-tree limitation

### Specific signs of progress
- action-bar container is found
- one or more bottom buttons appear in the real DOM of the correct frame
- a stable selector or ref path is found
- hover / locate works repeatedly

### Specific signs the blocker remains
- buttons stay visible only in screenshots but not in targetable DOM
- correct frame still cannot expose the action bar
- refs remain unstable across retries
- only visual confirmation exists, without stable interaction path

---

## What to capture during the next test

Record these if possible:
- the exact page title
- URL pattern
- whether there are nested panels / frames
- visible labels / button text
- whether content appears after waiting / refresh / re-entry
- whether another open tab contains a more readable version of the same flow

---

## Result template for the next run

### Run status
- success / partial / blocked

### Newly validated
- xxx
- xxx

### Still blocked at
- xxx

### Most likely blocker type
- rendering delay
- nested container / frame
- auth / environment issue
- unsupported reading method
- unknown

### Next recommended action
- xxx
