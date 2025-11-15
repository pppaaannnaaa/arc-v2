## 9.2 Content Attributes (Expanded Edition)

### 9.2.1 Overview
Content attributes form the expressive core of ARC’s semantic model. While structural attributes define
the layout, content attributes express the **actual meaning** of text, media, labels, and user inputs.
They allow AIs to understand *what the content represents*, *how it should be interpreted*, and *why it
exists*, enabling high-fidelity reasoning across both structural and narrative AI modes.

This expanded section clarifies deeper usage patterns, edge cases, attribute interactions, and best
practices for designing content-rich, AI-readable interfaces.

---

### 9.2.2 Available Content Attributes
The ARC content attribute set provides precise tools for annotating human-visible elements.

| Attribute | Description | Expanded Context | Example Value |
|:--|:--|:--|:--|
| **`data-ai-heading`** | Defines logical titles or major headings. | Supports multi-level hierarchy and semantic emphasis. | `"title"`, `"category"`, `"author_name"` |
| **`data-ai-summary`** | Provides summaries or short descriptive text. | Ideal for taglines, previews, or supporting messages. | `"intro"`, `"benefit"` |
| **`data-ai-field`** | Identifies user-input fields. | Helps AIs map form structure, validation, and purpose. | `"email"`, `"username"` |
| **`data-ai-label`** | Attaches semantic labels to fields or actions. | Ensures label-field association remains unambiguous. | `"email_label"` |
| **`data-ai-media`** | Tags multimedia assets. | Includes images, icons, diagrams, and videos. | `"hero_image"`, `"thumbnail"` |
| **`data-ai-content`** | Marks arbitrary rich text blocks. | Useful for articles, paragraphs, reviews, descriptions. | `"body"`, `"review_text"` |

ARC content attributes enable granular AI comprehension with minimal markup.

---

### 9.2.3 Example — Headings and Summaries
```html
<section data-ai-section="intro">
  <h1 data-ai-heading="title">Welcome to AquaGrow</h1>
  <p data-ai-summary="tagline">Hydroponic solutions for a sustainable tomorrow.</p>
</section>
```

**AI Output**
```json
{
  "section": "intro",
  "title": "Welcome to AquaGrow",
  "tagline": "Hydroponic solutions for a sustainable tomorrow."
}
```

Headings convey topic; summaries provide narrative highlights.

---

### 9.2.4 Example — Input Fields and Labels
```html
<form data-ai-section="signup" data-ai-intent="register_user">
  <label data-ai-label="email_label">Email Address</label>
  <input data-ai-field="email" type="email" />
  <label data-ai-label="password_label">Password</label>
  <input data-ai-field="password" type="password" />
</form>
```

**AI Output**
```json
{
  "section": "signup",
  "intent": "register_user",
  "fields": [
    { "field": "email", "label": "Email Address", "type": "email" },
    { "field": "password", "label": "Password", "type": "password" }
  ]
}
```

Labels create explicit connections between text and field elements.

---

### 9.2.5 Example — Content Blocks and Media
```html
<article data-ai-section="blog_post">
  <h2 data-ai-heading="title">AI in Hydroponics</h2>
  <img src="ai-plant.jpg" data-ai-media="illustration" />
  <p data-ai-content="article_body">
    Artificial Intelligence can optimize water and nutrient delivery in hydroponic systems.
  </p>
</article>
```

**AI Output**
```json
{
  "section": "blog_post",
  "title": "AI in Hydroponics",
  "media": { "illustration": "ai-plant.jpg" },
  "content": "Artificial Intelligence can optimize water and nutrient delivery in hydroponic systems."
}
```

Media markers help AIs understand visual context.

---

### 9.2.6 Example — Multi-Content Structure
```html
<div data-ai-section="testimonials">
  <div data-ai-group="review">
    <h3 data-ai-heading="author">Priya Sen</h3>
    <p data-ai-content="review_text">
      The AquaGrow system made home farming effortless and clean.
    </p>
  </div>
  <div data-ai-group="review">
    <h3 data-ai-heading="author">Ravi Kumar</h3>
    <p data-ai-content="review_text">
      I’ve reduced water usage by 70% since switching to hydroponics.
    </p>
  </div>
</div>
```

**AI Output**
```json
{
  "section": "testimonials",
  "reviews": [
    {
      "author": "Priya Sen",
      "review_text": "The AquaGrow system made home farming effortless and clean."
    },
    {
      "author": "Ravi Kumar",
      "review_text": "I’ve reduced water usage by 70% since switching to hydroponics."
    }
  ]
}
```

ARC automatically interprets repeating groups as collections.

---

### 9.2.7 Guidelines for Content Attributes

| Rule | Description |
|:--|:--|
| Pair `data-ai-heading` with summary or content when possible for richer meaning. |
| `data-ai-label` should be used wherever fields rely on textual guidance. |
| Use media attributes consistently to help AIs map rich media to semantics. |
| Avoid ambiguous descriptors—prefer explicit roles. |
| For collections, ensure group names reflect plural meaning. |

These guidelines ensure clarity, maintainability, and consistent AI reasoning.

---

### 9.2.8 Combined Example — Content-Rich Section
```html
<section data-ai-section="features">
  <div data-ai-group="feature">
    <h3 data-ai-heading="title">Water Efficiency</h3>
    <p data-ai-summary="benefit">Reduces water usage by up to 80%.</p>
    <img src="feature1.png" data-ai-media="icon" />
  </div>
  <div data-ai-group="feature">
    <h3 data-ai-heading="title">Modular Design</h3>
    <p data-ai-summary="benefit">Stackable structure allows easy expansion.</p>
    <img src="feature2.png" data-ai-media="icon" />
  </div>
</section>
```

**AI Output**
```json
{
  "section": "features",
  "features": [
    {
      "title": "Water Efficiency",
      "benefit": "Reduces water usage by up to 80%.",
      "media": "feature1.png"
    },
    {
      "title": "Modular Design",
      "benefit": "Stackable structure allows easy expansion.",
      "media": "feature2.png"
    }
  ]
}
```

---

*End of Phase 10 — Content Attributes (Expanded)*
