## 9.6 Dynamic Attributes (Expanded Edition)

### 9.6.1 Overview
Dynamic attributes in ARC describe **real-time interaction, system behavior, and state transitions** inside web applications.
They give AIs the ability to understand how a UI *changes over time*, how elements *react to user input*, and how various
states *affect meaning or visibility*.  
As modern SPAs, dashboards, and reactive interfaces rely heavily on dynamic logic, these attributes help translate that
logic into a machine-understandable semantic layer.

This expanded version deepens explanations, improves tone, and clarifies how dynamic attributes fit into advanced AI reasoning.

---

### 9.6.2 Available Dynamic Attributes
| Attribute | Description | Expanded Use Case | Example Value |
|:--|:--|:--|:--|
| **`data-ai-event`** | Represents user/system-triggered events. | Clicking, loading, submitting, data reception. | `"onClick"`, `"onLoad"` |
| **`data-ai-trigger`** | Describes the condition that initiates an action. | Scroll triggers, hover states, timers, data updates. | `"scroll"`, `"timeout"` |
| **`data-ai-state`** | Describes current or expected UI state. | Opening/closing modals, loading indicators, active elements. | `"expanded"`, `"loading"` |
| **`data-ai-action`** | Defines what happens as a result of an event. | Showing modals, updating charts, toggling menus. | `"show_modal"`, `"reload_data"` |
| **`data-ai-transition`** | Describes visual or animated transformations. | Fade effects, slide transitions, timed delays. | `"fade_in"`, `"slide_up"` |

These attributes allow AIs to trace dynamic sequences as clearly as static markup.

---

### 9.6.3 Example — Event and Action
```html
<button
  data-ai-role="refresh_button"
  data-ai-event="onClick"
  data-ai-action="reload_data"
>
  Refresh Data
</button>
```

**AI Output**
```json
{
  "role": "refresh_button",
  "event": "onClick",
  "action": "reload_data",
  "label": "Refresh Data"
}
```

---

### 9.6.4 Example — State and Transition
```html
<div
  data-ai-section="analytics_chart"
  data-ai-state="loading"
  data-ai-transition="fade_in"
>
  <p data-ai-summary="status">Fetching live analytics data...</p>
</div>
```

**AI Output**
```json
{
  "section": "analytics_chart",
  "state": "loading",
  "transition": "fade_in",
  "status": "Fetching live analytics data..."
}
```

---

### 9.6.5 Example — Trigger and Response
```html
<div
  data-ai-block="promo_banner"
  data-ai-trigger="scroll"
  data-ai-action="show_modal"
  data-ai-transition="slide_up"
>
  <p data-ai-summary="offer">Get 20% off on your first hydroponic system!</p>
</div>
```

**AI Output**
```json
{
  "block": "promo_banner",
  "trigger": "scroll",
  "action": "show_modal",
  "transition": "slide_up",
  "offer": "Get 20% off on your first hydroponic system!"
}
```

---

### 9.6.6 Example — Combined Dynamic States
```html
<section data-ai-section="dashboard" data-ai-state="active">
  <div
    data-ai-group="chart"
    data-ai-event="onDataLoad"
    data-ai-action="update_chart"
  >
    <h2 data-ai-heading="title">Nutrient Levels</h2>
    <canvas data-ai-field="chart_canvas"></canvas>
  </div>
</section>
```

**AI Output**
```json
{
  "section": "dashboard",
  "state": "active",
  "groups": [
    {
      "name": "chart",
      "event": "onDataLoad",
      "action": "update_chart",
      "title": "Nutrient Levels",
      "field": "chart_canvas"
    }
  ]
}
```

---

### 9.6.7 Example — Complex Interaction Chain
```html
<div data-ai-page="reports">
  <button
    data-ai-role="filter_button"
    data-ai-event="onClick"
    data-ai-action="open_filter_panel"
  >
    Filter
  </button>

  <div
    data-ai-block="filter_panel"
    data-ai-state="collapsed"
    data-ai-trigger="button_click"
    data-ai-action="expand_panel"
    data-ai-transition="slide_down"
  >
    <p data-ai-summary="instruction">Select a report category to filter results.</p>
  </div>
</div>
```

**AI Output**
```json
{
  "page": "reports",
  "actions": [
    { "role": "filter_button", "event": "onClick", "action": "open_filter_panel" }
  ],
  "blocks": [
    {
      "name": "filter_panel",
      "state": "collapsed",
      "trigger": "button_click",
      "action": "expand_panel",
      "transition": "slide_down",
      "instruction": "Select a report category to filter results."
    }
  ]
}
```

---

### 9.6.8 Guidelines for Dynamic Attributes
| Rule | Description |
|:--|:--|
| Use `data-ai-event` for anything that initiates change. |
| Use `data-ai-trigger` to describe conditions or signals. |
| Use `data-ai-state` to indicate current or expected UI status. |
| Use `data-ai-action` to define resulting system behavior. |
| Use `data-ai-transition` to specify animations or temporal effects. |
| Prefer descriptive names (e.g., `reload_data` over `fnReload`). |

These rules create clarity and consistency across highly interactive UIs.

---

### 9.6.9 Combined Example — Dynamic Interaction Ecosystem
```html
<div data-ai-page="dashboard">
  <section data-ai-section="data_insights" data-ai-state="ready">
    <button
      data-ai-role="refresh"
      data-ai-event="onClick"
      data-ai-action="reload_data"
    >
      Refresh Insights
    </button>

    <div
      data-ai-block="chart"
      data-ai-trigger="data_update"
      data-ai-action="animate_chart"
      data-ai-transition="fade_in"
    >
      <h2 data-ai-heading="title">Hydration Efficiency</h2>
      <canvas data-ai-field="chart_data"></canvas>
    </div>
  </section>
</div>
```

**AI Output**
```json
{
  "page": "dashboard",
  "sections": [
    {
      "name": "data_insights",
      "state": "ready",
      "actions": [
        { "role": "refresh", "event": "onClick", "action": "reload_data" }
      ],
      "blocks": [
        {
          "name": "chart",
          "trigger": "data_update",
          "action": "animate_chart",
          "transition": "fade_in",
          "title": "Hydration Efficiency",
          "field": "chart_data"
        }
      ]
    }
  ]
}
```

---

### 9.6.10 Why Dynamic Attributes Matter
Dynamic attributes allow AI systems to understand complex UI flows, predict interactions,
and even simulate user behavior.  
They form a crucial bridge between **static semantics** and **interactive logic**, supporting:

- automated testing,
- advanced accessibility tools,
- conversational assistants that narrate UI changes,
- AI agents performing autonomous tasks,
- real-time interface monitoring.

Dynamic attributes make modern web applications fully interpretable and action-ready for AI.

---

*End of Phase 14 — Dynamic Attributes (Expanded)*
