
## 8. Conventions of ARC 

### 8.1 Overview
The AI Readability Convention (ARC) establishes a consistent, predictable, and extensible semantic layer
for HTML. While ARC attributes are lightweight and easy to apply, they follow a carefully designed set
of rules that ensure long‑term scalability, cross‑framework compatibility, and clear AI interpretability.
This expanded section explains ARC’s stylistic rules, attribute hierarchies, compositional logic, and
best‑practice conventions, giving developers a solid foundation for designing AI‑ready interfaces.

---

### 8.2 General Syntax Rules
ARC attributes comply with a strict and readable syntax to maintain clarity across diverse codebases.

| Rule | Description |
|:--|:--|
| **Prefix** | Every attribute begins with `data-ai-` to provide a unified namespace. |
| **Lowercase Only** | Attribute names are lowercase and hyphen-separated for readability. |
| **Concise Values** | Values should be short but descriptive—not coded IDs or internal variable names. |
| **No HTML Conflicts** | ARC never overrides native attributes or ARIA roles. |
| **Human-Centric** | Attribute values are written to reflect human intention, not machine identifiers. |

**Example**
```html
<div data-ai-section="hero" data-ai-intent="introduce_brand">
  <h1 data-ai-heading="title">Welcome to AquaGrow</h1>
  <p data-ai-summary="intro">Hydroponic solutions for every home.</p>
</div>
```

**AI Output**
```json
{
  "section": "hero",
  "intent": "introduce_brand",
  "title": "Welcome to AquaGrow",
  "summary": "Hydroponic solutions for every home."
}
```

---

### 8.3 Attribute Structure and Composition
ARC attributes are designed to be composable. Developers can mix, match, and nest attributes to create
layers of meaning.

| Type | Description | Example |
|:--|:--|:--|
| **Singular** | One attribute per meaning. | `data-ai-role="button"` |
| **Composite** | Combine multiple semantic hints. | `data-ai-role="submit" data-ai-intent="register_user"` |
| **Nested** | Children inherit parent meaning. | `<div data-ai-section="form"><input data-ai-field="email"/></div>` |

**Example**
```html
<form data-ai-section="signup" data-ai-intent="register_user">
  <input data-ai-field="email" data-ai-context="personal" />
  <button data-ai-role="submit" data-ai-intent="form_submit">Sign Up</button>
</form>
```

**AI Output**
```json
{
  "section": "signup",
  "intent": "register_user",
  "fields": [
    { "field": "email", "context": "personal" }
  ],
  "actions": [
    { "role": "submit", "intent": "form_submit", "label": "Sign Up" }
  ]
}
```

---

### 8.4 Inheritance and Context Propagation
ARC’s context propagation allows elements within a block to automatically inherit parent attributes.
This reduces duplication and maintains semantic consistency.

**Example**
```html
<section data-ai-section="contact" data-ai-intent="collect_inquiry">
  <input data-ai-field="name" />
  <input data-ai-field="email" />
</section>
```

**AI Output**
```json
{
  "section": "contact",
  "intent": "collect_inquiry",
  "fields": [
    { "field": "name" },
    { "field": "email" }
  ]
}
```

Inheritance ensures that a complete semantic picture is preserved even if children contain minimal markup.

---

### 8.5 Descriptive and Declarative Intent
ARC encourages descriptive values over technical identifiers.  
The goal is readability—for humans and AIs.

| Poor Example | Recommended |
|:--|:--|
| `data-ai-role="btn1"` | `data-ai-role="submit_button"` |
| `data-ai-section="main"` | `data-ai-section="user_signup"` |
| `data-ai-intent="doThing"` | `data-ai-intent="purchase_product"` |

**Guideline:**  
Name attributes based on **meaning**, not on implementation details.

---

### 8.6 Attribute Grouping by Category
To keep ARC scalable and organized, attributes fall under clear functional categories.

| Category | Prefix Example | Purpose |
|:--|:--|:--|
| **Structural** | `data-ai-page`, `data-ai-section`, `data-ai-group` | Defines layout logic and hierarchy. |
| **Content** | `data-ai-heading`, `data-ai-summary`, `data-ai-field` | Describes human-facing information. |
| **Meta** | `data-ai-type`, `data-ai-context`, `data-ai-status` | Adds descriptive metadata. |
| **Relational** | `data-ai-link`, `data-ai-ref`, `data-ai-depends` | Connects relationships and dependencies. |
| **Contextual** | `data-ai-intent`, `data-ai-purpose`, `data-ai-scope` | States intention, behavior, or logic. |
| **Dynamic** | `data-ai-event`, `data-ai-trigger`, `data-ai-state` | Captures runtime or state-driven meaning. |

This categorization reflects a full semantic ecosystem applicable to static pages, SPAs, and enterprise dashboards.

---

### 8.7 Attribute Nesting Hierarchy
Nesting follows predictable inheritance logic.  
AIs interpret ARC attributes recursively to reconstruct clean semantic trees.

**Example**
```html
<div data-ai-page="dashboard">
  <section data-ai-section="reports">
    <div data-ai-group="sales_chart">
      <h2 data-ai-heading="title">Quarterly Report</h2>
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
      "name": "reports",
      "groups": [
        {
          "name": "sales_chart",
          "title": "Quarterly Report"
        }
      ]
    }
  ]
}
```

Nesting ensures clean relational mapping without the need for external schemas.

---

### 8.8 Readability and Commenting Practices
ARC encourages human-readable documentation alongside attributes.

**Example**
```html
<!-- ARC: product detail section -->
<section data-ai-section="product_detail" data-ai-intent="display_info">
  <h1 data-ai-heading="name">Solar Water Pump</h1>
  <p data-ai-summary="description">A low-power, solar-assisted water pump system.</p>
</section>
```

Comments improve onboarding, handoff, and collaboration among developers unfamiliar with ARC.

---

### 8.9 Summary of Conventions
| Principle | Description |
|:--|:--|
| **Consistency** | Maintain a unified naming style for all ARC attributes. |
| **Clarity** | Use values that communicate plain meaning. |
| **Context Propagation** | Children inherit parent meaning automatically. |
| **Compatibility** | ARC works with HTML, ARIA, and Schema.org. |
| **Scalability** | Suitable for small static sites and large SPAs alike. |

Through these conventions, ARC creates a predictable, expressive, and AI-ready markup system that brings clarity
to both humans and intelligent systems.

---

*End of Phase 8 — Conventions of ARC (Expanded)*