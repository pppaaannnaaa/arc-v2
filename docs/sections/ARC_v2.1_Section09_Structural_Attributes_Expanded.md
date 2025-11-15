## 9.1 Structural Attributes 

### 9.1.1 Overview
Structural attributes form the backbone of ARC’s semantic architecture. They define how the different
parts of a webpage relate to each other, how content is grouped, and how the AI should reconstruct the
page as a hierarchical dataset.  
This expanded section explains the purpose, design principles, extended use cases, and deeper reasoning
behind ARC’s structural attribute system. It clarifies how these attributes allow AIs to interpret page
architecture with precision—something traditional HTML structure alone cannot guarantee.

---

### 9.1.2 Available Structural Attributes
ARC provides a set of structural attributes designed for clarity and hierarchical mapping.  
The expanded descriptions below include additional use cases:

| Attribute | Description | Expanded Use Cases | Example Values |
|:--|:--|:--|:--|
| **`data-ai-page`** | Defines the logical page-level identity. | Helps AIs categorize full-page intent. | `"product"`, `"dashboard"`, `"case_study"` |
| **`data-ai-section`** | Represents major content or functional divisions. | Useful for splitting long or dynamic pages into meaning blocks. | `"features"`, `"pricing"`, `"testimonials"` |
| **`data-ai-group`** | Groups related items within a section. | Ideal for lists, repeating units, or grid components. | `"plan"`, `"feature"`, `"card_set"` |
| **`data-ai-subgroup`** | A subgroup nested within a group. | Helps create multi-tiered structures like pricing tiers, FAQs, modules. | `"basic_plan"`, `"tier_1"` |
| **`data-ai-block`** | Identifies standalone reusable units. | Works well for banners, footers, widgets, modular UI components. | `"hero_banner"`, `"stats_card"` |

These structural markers provide a universal vocabulary for mapping the visual UI to a semantic tree.

---

### 9.1.3 Basic Example — Page and Section Structure
```html
<div data-ai-page="product">
  <section data-ai-section="features">
    <div data-ai-group="feature">
      <h2 data-ai-heading="title">Water Efficiency</h2>
      <p data-ai-summary="description">Reduces water usage by 80%.</p>
    </div>
  </section>
</div>
```

**AI Structural Output**
```json
{
  "page": "product",
  "sections": [
    {
      "name": "features",
      "groups": [
        {
          "name": "feature",
          "title": "Water Efficiency",
          "description": "Reduces water usage by 80%."
        }
      ]
    }
  ]
}
```

This demonstrates ARC’s ability to translate markup into structured, machine-friendly data.

---

### 9.1.4 Example — Group and Subgroup Nesting
```html
<section data-ai-section="pricing">
  <div data-ai-group="plans">
    <div data-ai-subgroup="basic_plan">
      <h3 data-ai-heading="title">Basic</h3>
      <p data-ai-summary="details">Includes 3 modules and email support.</p>
    </div>
    <div data-ai-subgroup="premium_plan">
      <h3 data-ai-heading="title">Premium</h3>
      <p data-ai-summary="details">Includes 10 modules and 24/7 support.</p>
    </div>
  </div>
</section>
```

**AI Output**
```json
{
  "section": "pricing",
  "groups": [
    {
      "name": "plans",
      "subgroups": [
        {
          "name": "basic_plan",
          "title": "Basic",
          "details": "Includes 3 modules and email support."
        },
        {
          "name": "premium_plan",
          "title": "Premium",
          "details": "Includes 10 modules and 24/7 support."
        }
      ]
    }
  ]
}
```

Subgroups introduce multi-level structure that mirrors real business logic.

---

### 9.1.5 Example — Using `data-ai-block` for Reusable Components
`data-ai-block` is essential for modular design systems such as banners, widgets, and cards.

```html
<section data-ai-section="homepage">
  <div data-ai-block="hero_banner">
    <h1 data-ai-heading="title">Grow Smarter with Hydroponics</h1>
    <p data-ai-summary="tagline">Technology meets sustainable farming.</p>
  </div>
</section>
```

**AI Output**
```json
{
  "section": "homepage",
  "blocks": [
    {
      "name": "hero_banner",
      "title": "Grow Smarter with Hydroponics",
      "tagline": "Technology meets sustainable farming."
    }
  ]
}
```

Blocks help AIs classify modular UI regions that can appear repeatedly across pages.

---

### 9.1.6 Guidelines for Structural Attributes
This expanded guideline table adds clarity on best practices:

| Rule | Description |
|:--|:--|
| **Use `data-ai-page` once** | A top-level identifier should not be repeated. |
| **Sections may repeat** | Useful for long pages with recurring patterns. |
| **Groups must belong to a section** | Ensures consistent hierarchy. |
| **Blocks can be independent** | Ideal for isolated UI components. |
| **Limit nesting depth** | A maximum depth of 3 avoids semantic ambiguity. |
| **Name structurally, not visually** | Use logical names, not CSS-inspired identifiers. |

These guidelines ensure predictable parsing and future-proof markup.

---

### 9.1.7 Combined Structural Example
```html
<div data-ai-page="dashboard">
  <section data-ai-section="overview">
    <div data-ai-group="summary_cards">
      <div data-ai-block="sales">
        <h2 data-ai-heading="title">Sales</h2>
        <p data-ai-summary="data">$25,000 this quarter</p>
      </div>
      <div data-ai-block="users">
        <h2 data-ai-heading="title">Users</h2>
        <p data-ai-summary="data">1,250 active</p>
      </div>
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
      "name": "overview",
      "groups": [
        {
          "name": "summary_cards",
          "blocks": [
            { "name": "sales", "title": "Sales", "data": "$25,000 this quarter" },
            { "name": "users", "title": "Users", "data": "1,250 active" }
          ]
        }
      ]
    }
  ]
}
```

This combined example demonstrates how all structural attributes work together to form a complete semantic map.

---

*End of Phase 9 — Structural Attributes (Expanded)*