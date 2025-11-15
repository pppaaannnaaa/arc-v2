## 9.5 Contextual Attributes 

### 9.5.1 Overview
Contextual attributes in ARC supply the missing layer of *why* behind UI elements.  
While structural attributes define layout and content attributes express what something contains,
contextual attributes explain **purpose, intention, behavior, and operational scope**.  
They allow AIs to move from static interpretation to true **functional reasoning**, enabling systems to
infer motivations, workflows, and user goals.

This expanded version increases clarity, deepens explanations, and strengthens tone to better convey how
crucial contextual metadata is for AI comprehension.

---

### 9.5.2 Available Contextual Attributes
| Attribute | Description | Expanded Use Case | Example Value |
|:--|:--|:--|:--|
| **`data-ai-intent`** | Primary purpose or goal of an element. | Captures user or system intent behind interactions. | `"register_user"`, `"purchase_product"` |
| **`data-ai-purpose`** | Human-facing justification or descriptive reasoning. | Explains *why* a feature exists. | `"onboarding"`, `"educational"` |
| **`data-ai-scope`** | Defines logical or operational boundaries. | Controls persistence, session behavior, or component-level logic. | `"global"`, `"session"` |
| **`data-ai-mode`** | Specifies interaction state. | Useful for editable dashboards, previews, or locked content states. | `"read"`, `"edit"`, `"preview"` |
| **`data-ai-behavior`** | Expected dynamic UX or system behavior. | Helps AIs understand runtime flows and user interaction mechanics. | `"auto_save"`, `"expand_on_hover"` |

---

### 9.5.3 Example — Intent and Purpose
```html
<section data-ai-section="signup" data-ai-intent="register_user" data-ai-purpose="onboarding">
  <h1 data-ai-heading="title">Join the AquaGrow Community</h1>
  <input data-ai-field="email" />
  <button data-ai-role="submit" data-ai-intent="form_submit">Sign Up</button>
</section>
```

**AI Output**
```json
{
  "section": "signup",
  "intent": "register_user",
  "purpose": "onboarding",
  "elements": [
    { "field": "email" },
    { "role": "submit", "intent": "form_submit", "label": "Sign Up" }
  ]
}
```

Intent reveals function; purpose clarifies reasoning.

---

### 9.5.4 Example — Behavioral Context
```html
<form data-ai-section="feedback" data-ai-intent="collect_feedback">
  <textarea data-ai-field="message" data-ai-behavior="auto_save"></textarea>
  <button data-ai-role="submit" data-ai-behavior="submit_form">Send Feedback</button>
</form>
```

**AI Output**
```json
{
  "section": "feedback",
  "intent": "collect_feedback",
  "fields": [
    { "field": "message", "behavior": "auto_save" }
  ],
  "actions": [
    { "role": "submit", "behavior": "submit_form", "label": "Send Feedback" }
  ]
}
```

Behavior attributes reveal dynamic system operations.

---

### 9.5.5 Example — Operational Scope and Mode
```html
<div data-ai-section="dashboard" data-ai-scope="session" data-ai-mode="edit">
  <h2 data-ai-heading="title">Manage Devices</h2>
  <p data-ai-summary="details">Edit or remove connected hydroponic units.</p>
</div>
```

**AI Output**
```json
{
  "section": "dashboard",
  "scope": "session",
  "mode": "edit",
  "title": "Manage Devices",
  "details": "Edit or remove connected hydroponic units."
}
```

Mode tells AI how the interface should behave at this moment.

---

### 9.5.6 Example — Combined Contextual Layers
```html
<section data-ai-section="education" data-ai-purpose="learning" data-ai-mode="read">
  <article data-ai-group="lesson" data-ai-intent="teach_concept">
    <h3 data-ai-heading="title">Photosynthesis and Hydroponics</h3>
    <p data-ai-summary="content">
      Understanding how light absorption affects plant growth in controlled environments.
    </p>
  </article>
</section>
```

**AI Output**
```json
{
  "section": "education",
  "purpose": "learning",
  "mode": "read",
  "lessons": [
    {
      "intent": "teach_concept",
      "title": "Photosynthesis and Hydroponics",
      "content": "Understanding how light absorption affects plant growth in controlled environments."
    }
  ]
}
```

Contextual layering enables richly interpretable educational structures.

---

### 9.5.7 Example — Context-Aware Dynamic Interaction
```html
<div data-ai-section="profile_settings" data-ai-mode="edit" data-ai-intent="update_user_info">
  <input data-ai-field="name" data-ai-behavior="auto_save" />
  <input data-ai-field="photo_upload" data-ai-behavior="expand_on_hover" />
</div>
```

**AI Output**
```json
{
  "section": "profile_settings",
  "mode": "edit",
  "intent": "update_user_info",
  "fields": [
    { "field": "name", "behavior": "auto_save" },
    { "field": "photo_upload", "behavior": "expand_on_hover" }
  ]
}
```

Contextual attributes turn dynamic UI behavior into machine-readable semantics.

---

### 9.5.8 Guidelines for Contextual Attributes
| Rule | Description |
|:--|:--|
| Use `data-ai-intent` as the primary marker of purpose or action. |
| Use `data-ai-purpose` for secondary or human-centered rationale. |
| Use `data-ai-scope` to define how widely meaning applies. |
| Use `data-ai-mode` to represent current interaction state. |
| Use `data-ai-behavior` to document dynamic or UX-level behavior. |

These rules ensure consistency and clarity across AI interpretations.

---

### 9.5.9 Combined Example — Full Context Map
```html
<section data-ai-section="user_profile" data-ai-intent="update_user_data" data-ai-scope="global">
  <h2 data-ai-heading="title">Profile Management</h2>
  <form data-ai-group="personal_info" data-ai-purpose="identity_maintenance">
    <input data-ai-field="name" data-ai-behavior="auto_save" />
    <input data-ai-field="email" data-ai-behavior="submit_form" />
  </form>
</section>
```

**AI Output**
```json
{
  "section": "user_profile",
  "intent": "update_user_data",
  "scope": "global",
  "title": "Profile Management",
  "groups": [
    {
      "purpose": "identity_maintenance",
      "fields": [
        { "field": "name", "behavior": "auto_save" },
        { "field": "email", "behavior": "submit_form" }
      ]
    }
  ]
}
```

---

*End of Phase 13 — Contextual Attributes (Expanded)*
