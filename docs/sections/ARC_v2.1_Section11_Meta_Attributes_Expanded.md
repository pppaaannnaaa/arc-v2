## 9.3 Meta Attributes 

### 9.3.1 Overview
Meta attributes provide the deeper descriptive layers of ARC’s semantic system.  
While structural attributes define hierarchy and content attributes express human-facing information,
meta attributes explain **what the content represents**, **how it should be interpreted**, and **what state or sensitivity it carries**.

This is crucial for AI systems that must differentiate between:
- types of entities (Product, User, Report),
- privacy contexts (personal, financial, sensitive),
- system state (active, archived, pending),
- importance or visibility levels.

The expanded section refines tone, improves clarity, and elaborates on best practices and real-world usage.

---

### 9.3.2 Available Meta Attributes
| Attribute | Description | Expanded Use Case | Example Value |
|:--|:--|:--|:--|
| **`data-ai-type`** | Defines conceptual identity of the element. | Helps AIs classify items for indexing or reasoning. | `"Product"`, `"User"`, `"BlogPost"` |
| **`data-ai-status`** | Indicates current lifecycle or state. | Useful for dashboards, alerts, workflow steps. | `"active"`, `"pending"`, `"archived"` |
| **`data-ai-context`** | Declares situational or sensitivity context. | Helps AI apply privacy/risk considerations. | `"personal"`, `"sensitive"`, `"financial"` |
| **`data-ai-category`** | Groups related content under a common classification. | Useful for product groups, topics, taxonomies. | `"Hydroponics"`, `"AI"`, `"Education"` |
| **`data-ai-visibility`** | Represents visual or logical priority. | Helps AIs decide relevance in summaries. | `"primary"`, `"secondary"`, `"hidden"` |

---

### 9.3.3 Example — Categorization and Type Definition
```html
<div data-ai-type="Product" data-ai-category="Hydroponics">
  <h2 data-ai-heading="title">AquaGrow Tower</h2>
  <p data-ai-summary="description">A modular hydroponic system for urban homes.</p>
</div>
```

**AI Output**
```json
{
  "type": "Product",
  "category": "Hydroponics",
  "title": "AquaGrow Tower",
  "description": "A modular hydroponic system for urban homes."
}
```

This helps AIs accurately store, classify, and interpret entities.

---

### 9.3.4 Example — Context and Sensitivity Tagging
```html
<form data-ai-section="user_signup" data-ai-intent="register_user">
  <input data-ai-field="email" data-ai-context="personal" />
  <input data-ai-field="password" data-ai-context="sensitive" />
</form>
```

**AI Output**
```json
{
  "section": "user_signup",
  "intent": "register_user",
  "fields": [
    { "field": "email", "context": "personal" },
    { "field": "password", "context": "sensitive" }
  ]
}
```

Meta attributes ensure AIs understand privacy requirements.

---

### 9.3.5 Example — Visibility and State
```html
<section data-ai-section="notifications">
  <div data-ai-type="message" data-ai-status="unread" data-ai-visibility="primary">
    <p data-ai-content="text">Your hydroponic system shipment is on its way!</p>
  </div>
  <div data-ai-type="message" data-ai-status="read" data-ai-visibility="secondary">
    <p data-ai-content="text">Welcome to AquaGrow!</p>
  </div>
</section>
```

**AI Output**
```json
{
  "section": "notifications",
  "messages": [
    {
      "type": "message",
      "status": "unread",
      "visibility": "primary",
      "text": "Your hydroponic system shipment is on its way!"
    },
    {
      "type": "message",
      "status": "read",
      "visibility": "secondary",
      "text": "Welcome to AquaGrow!"
    }
  ]
}
```

AIs can prioritize content using `status` + `visibility`.

---

### 9.3.6 Example — Combined Meta Use
```html
<article data-ai-type="BlogPost" data-ai-category="AI" data-ai-status="published">
  <h1 data-ai-heading="title">ARC — A Universal Language for AI Readability</h1>
  <p data-ai-summary="intro">
    How ARC bridges human design and machine understanding.
  </p>
</article>
```

**AI Output**
```json
{
  "type": "BlogPost",
  "category": "AI",
  "status": "published",
  "title": "ARC — A Universal Language for AI Readability",
  "intro": "How ARC bridges human design and machine understanding."
}
```

This enables AIs to handle sorting, filtering, and summarization logic automatically.

---

### 9.3.7 Guidelines for Meta Attributes
| Rule | Description |
|:--|:--|
| Use `data-ai-type` to establish conceptual identity early. |
| Apply `data-ai-context` whenever personal, financial, or sensitive data appears. |
| Combine `data-ai-status` and `data-ai-visibility` in dynamic systems such as dashboards or notifications. |
| Keep categories simple and general for better grouping. |
| Meta attributes describe **what something is**, not **why it exists**—that’s the role of `data-ai-intent`. |

Meta attributes enhance AI reasoning by providing classification, state, sensitivity, and priority.

---

### 9.3.8 Summary
Meta attributes strengthen ARC’s semantic depth by adding classification, state, and contextual metadata.
They enable AI systems to perform high-quality reasoning, filtering, and summarization while remaining inline,
lightweight, and fully compatible with existing markup.

---

*End of Phase 11 — Meta Attributes (Expanded)*
