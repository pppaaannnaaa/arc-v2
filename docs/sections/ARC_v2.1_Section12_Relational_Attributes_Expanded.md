## 9.4 Relational Attributes 

### 9.4.1 Overview
Relational attributes in ARC establish **connections, references, and dependencies** between elements,
allowing AI systems to interpret not only *what* elements exist but *how those elements relate* to one another.
While structural attributes map hierarchy and content attributes describe meaning, relational attributes
bind the interface together into an entity–relationship model that an AI can traverse deterministically.

This module clarifies relational models, provides deeper examples, and strengthens tone and clarity.

---

### 9.4.2 Available Relational Attributes
| Attribute | Description | Expanded Use Case | Example Value |
|:--|:--|:--|:--|
| **`data-ai-link`** | Establishes cross-entity linking. | Connects page content to related sections, articles, media. | `"related_products"` |
| **`data-ai-ref`** | Direct reference to an object or identifier. | Binds an element to a specific target. | `"author_profile"` |
| **`data-ai-depends`** | Declares logical dependency. | Indicates steps that must happen first. | `"cart_validation"` |
| **`data-ai-rel`** | Defines explicit relational semantics. | Parent–child, sibling, or associative relationships. | `"parent"`, `"child"` |
| **`data-ai-source`** | Indicates origin of data. | Useful in API-driven or CMS-driven systems. | `"database"`, `"external_api"` |

---

### 9.4.3 Example — Linking Entities
```html
<article data-ai-type="BlogPost" data-ai-link="author_profile">
  <h1 data-ai-heading="title">AI in Agriculture</h1>
  <p data-ai-summary="intro">How AI is transforming hydroponic farming.</p>
</article>

<div data-ai-type="Author" data-ai-ref="author_profile">
  <h3 data-ai-heading="name">Panna Das</h3>
  <p data-ai-summary="bio">Software engineer exploring sustainable agriculture.</p>
</div>
```

**AI Output**
```json
{
  "type": "BlogPost",
  "title": "AI in Agriculture",
  "intro": "How AI is transforming hydroponic farming.",
  "linked_author": {
    "name": "Panna Das",
    "bio": "Software engineer exploring sustainable agriculture."
  }
}
```

---

### 9.4.4 Example — Dependency Relationships
```html
<form data-ai-section="checkout">
  <div data-ai-group="billing" data-ai-depends="cart_validation">
    <h3 data-ai-heading="title">Billing Information</h3>
    <input data-ai-field="card_number" />
  </div>
</form>
```

**AI Output**
```json
{
  "section": "checkout",
  "groups": [
    {
      "name": "billing",
      "depends_on": "cart_validation",
      "fields": ["card_number"]
    }
  ]
}
```

---

### 9.4.5 Example — Cross-Linking Between Pages
```html
<div data-ai-page="product" data-ai-link="related_articles">
  <h2 data-ai-heading="title">Hydroponic Tower</h2>
</div>

<section data-ai-section="related_articles" data-ai-source="cms">
  <article data-ai-group="article">
    <h3 data-ai-heading="title">Maintaining Nutrient Balance</h3>
  </article>
  <article data-ai-group="article">
    <h3 data-ai-heading="title">Indoor Lighting Tips</h3>
  </article>
</section>
```

**AI Output**
```json
{
  "page": "product",
  "title": "Hydroponic Tower",
  "related_articles": [
    { "title": "Maintaining Nutrient Balance" },
    { "title": "Indoor Lighting Tips" }
  ]
}
```

---

### 9.4.6 Example — Parent–Child Relationships
```html
<div data-ai-group="project" data-ai-rel="parent">
  <h2 data-ai-heading="name">Urban Farming Initiative</h2>
  <div data-ai-subgroup="sub_project" data-ai-rel="child">
    <h3 data-ai-heading="title">School Hydroponic Program</h3>
  </div>
</div>
```

**AI Output**
```json
{
  "project": {
    "name": "Urban Farming Initiative",
    "sub_project": {
      "title": "School Hydroponic Program"
    }
  }
}
```

---

### 9.4.7 Guidelines for Relational Attributes
| Rule | Description |
|:--|:--|
| Use `data-ai-link` for cross-content logical references. |
| Use `data-ai-ref` when referencing a specific object or identifier. |
| Use `data-ai-depends` to define clear dependency flow. |
| `data-ai-rel` should clarify structural relationships (e.g., parent/child). |
| Use `data-ai-source` to show origin of external or dynamic data. |

These guidelines ensure that relational graphs remain predictable, structured, and AI-friendly.

---

### 9.4.8 Combined Example — Full Relational Map
```html
<div data-ai-page="dashboard" data-ai-source="api">
  <section data-ai-section="analytics" data-ai-link="data_sources">
    <h2 data-ai-heading="title">Analytics Overview</h2>
  </section>

  <div data-ai-group="data_sources" data-ai-source="database">
    <p data-ai-summary="details">Pulling live data from hydroponic sensors.</p>
  </div>
</div>
```

**AI Output**
```json
{
  "page": "dashboard",
  "source": "api",
  "sections": [
    {
      "name": "analytics",
      "title": "Analytics Overview",
      "linked": {
        "data_sources": {
          "source": "database",
          "details": "Pulling live data from hydroponic sensors."
        }
      }
    }
  ]
}
```

---

*End of Phase 12 — Relational Attributes (Expanded)*
