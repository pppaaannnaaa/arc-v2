## 2. How AIs Read the Web — The Three Levels of Understanding 

### 2.1 Overview
Artificial Intelligence systems—including search crawlers, LLMs, ranking algorithms, accessibility agents, and knowledge graph builders—attempt to extract *meaning* from HTML. However, without explicit guidance, their understanding remains inconsistent.

ARC defines a **three-tiered comprehension model**—Structural, Semantic, and Contextual—so developers know exactly how different systems interpret their markup. This framework allows AI to move from merely *seeing elements* to *understanding intent*. 

The expanded section below provides deeper explanations, richer examples, and clearer transitions to illustrate how AI systems gradually elevate their reasoning.

---

### 2.2 Level 1 — Structural Reading
Structural reading is AI at its shallowest but most foundational stage. At this level, machines perceive only what is visually or explicitly present in the DOM. They register tags, simple hierarchies, and element layouts.

AI does **not** infer purpose, meaning, relationships, or business logic here. It merely identifies visible structure.

**Example:**
```html
<section>
  <h1>Signup Form</h1>
  <input type="email" placeholder="Email" />
</section>
```

**AI Interpretation:**
```json
{
  "structure": {
    "section": "Signup Form",
    "fields": ["email"]
  }
}
```

**Narrative Response:**  
> “This is a signup section containing an email input field.”

This level is comparable to a human skimming a page without reading deeply—recognizing containers and items but not understanding relationships.

Structural reading answers: **What exists on the page?**

It cannot answer: **Why is it here? What does it do?**

---

### 2.3 Level 2 — Semantic Reading
Semantic reading goes a step deeper. AI now interprets elements not just by their presence but by their *roles*, *descriptions*, and textual or attribute-based clues.

At this level, AI attempts lightweight reasoning based on patterns:
- form titles,
- input names,
- attribute hints,
- textual cues.

However, machines still lack explicit intent. They infer meaning from context—but this inference can be incorrect if the markup is unclear.

**Example:**
```html
<section>
  <h1>Signup Form</h1>
  <input type="email" placeholder="Enter your email" name="user_email" />
</section>
```

**AI Semantic Output:**
```json
{
  "form": {
    "title": "Signup Form",
    "fields": [
      { "name": "user_email", "type": "email" }
    ]
  }
}
```

**Narrative Response:**  
> “This represents a signup form requesting the user’s email.”

Semantic reading provides structure **plus inferred meaning**, but intent remains ambiguous.

It answers: **What is this element probably for?**

It still cannot reliably answer: **What is its true purpose and how does it relate to the page’s goals?**

---

### 2.4 Level 3 — Contextual Reasoning
Contextual reasoning is the deepest—and the level ARC is designed to enable. Here, AI is not simply interpreting elements but understanding purpose, relationships, user pathways, and business intent.

ARC’s inline attributes (`data-ai-*`) supply the missing layer that modern web pages lack.

**ARC Example:**
```html
<section data-ai-page="signup" data-ai-intent="register_user">
  <h1 data-ai-heading="title">Create Your Account</h1>
  <input data-ai-field="email" data-ai-context="personal" />
</section>
```

**AI Contextual JSON:**
```json
{
  "page": "signup",
  "intent": "register_user",
  "elements": [
    { "type": "heading", "value": "Create Your Account" },
    { "field": "email", "context": "personal" }
  ]
}
```

**Narrative Response:**  
> “This section registers a new user by collecting their personal email.”

Contextual reading answers:  
- **What is the user trying to accomplish here?**  
- **How do these elements relate to each other?**  
- **What business action does this page represent?**

This is the level at which AI reads with human-like clarity—because ARC removes guesswork.

---

### 2.5 Summary of Levels
Below is the expanded comparison showing the increasing depth of AI understanding:

| Level | Mode | Description | Example Output |
|:--|:--|:--|:--|
| **1 — Structural** | Surface Recognition | Identifies visible elements and layout. | “This is a form with an email field.” |
| **2 — Semantic** | Interpretation | Infers roles and probable meaning using clues. | “This is a signup form asking for the user’s email.” |
| **3 — Contextual** | Intent Understanding | Grasps purpose, relationships, and user intent. | “This collects personal email to register a new user.” |

ARC’s purpose is to elevate AI from Levels 1 and 2—which rely on guesswork—to **Level 3**, where understanding becomes deterministic.

---

*End of Phase 2 — How AIs Read the Web (Expanded)*
