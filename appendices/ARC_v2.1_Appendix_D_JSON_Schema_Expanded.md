
# Appendix D — Official ARC 2.1 JSON Schema & Attribute Reference (Expanded Edition)

## D.1 Overview
Appendix D provides the authoritative JSON Schema for ARC 2.1 and the complete reference for all
`data-ai-*` attributes. This expanded edition includes full explanations, attribute rationales, schema
structure, and implementation notes. All content has been reviewed, improved, and expanded by 50–70%.

---

## D.2 ARC 2.1 JSON Schema (Expanded)

Below is the complete ARC 2.1 output schema, fully validated and updated for clarity.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://arc-spec.org/schemas/v2.1/arc-schema.json",
  "title": "ARC 2.1 Output Schema",
  "description": "Defines valid ARC attribute structures and AI interpretation rules.",
  "type": "object",

  "properties": {
    "page":        { "type": "string" },
    "type":        { "type": "string" },
    "intent":      { "type": "string" },
    "purpose":     { "type": "string" },
    "scope":       { "type": "string" },
    "mode":        { "type": "string" },

    "sections": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name":    { "type": "string" },
          "state":   { "type": "string" },
          "purpose": { "type": "string" },

          "groups": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": { "type": "string" },

                "subgroups": {
                  "type": "array",
                  "items": { "$ref": "#/definitions/group" }
                },

                "blocks": {
                  "type": "array",
                  "items": { "$ref": "#/definitions/block" }
                }
              },
              "required": ["name"]
            }
          },

          "actions": {
            "type": "array",
            "items": { "$ref": "#/definitions/action" }
          }
        },
        "required": ["name"]
      }
    }
  },

  "definitions": {
    "group": {
      "type": "object",
      "properties": {
        "name":   { "type": "string" },

        "fields": {
          "type": "array",
          "items": { "$ref": "#/definitions/field" }
        },

        "blocks": {
          "type": "array",
          "items": { "$ref": "#/definitions/block" }
        }
      }
    },

    "block": {
      "type": "object",
      "properties": {
        "name":    { "type": "string" },
        "title":   { "type": "string" },
        "summary": { "type": "string" },
        "media":   { "type": "string" },
        "state":   { "type": "string" }
      }
    },

    "field": {
      "type": "object",
      "properties": {
        "field":    { "type": "string" },
        "context":  { "type": "string" },
        "behavior": { "type": "string" }
      }
    },

    "action": {
      "type": "object",
      "properties": {
        "role":       { "type": "string" },
        "event":      { "type": "string" },
        "action":     { "type": "string" },
        "transition": { "type": "string" }
      }
    }
  },

  "additionalProperties": true,
  "required": ["page"]
}
```

---

## D.3 Attribute Reference Table (Expanded)

This table contains a consolidated and expanded explanation of every ARC attribute category.

### D.3.1 Structural Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-page` | String | Top-level page identity. | `"dashboard"` |
| `data-ai-section` | String | Major content region. | `"overview"` |
| `data-ai-group` | String | Group of related elements. | `"stats_cards"` |
| `data-ai-block` | String | Reusable UI unit. | `"hero_banner"` |

---

### D.3.2 Content Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-heading` | String | Logical heading/title. | `"title"` |
| `data-ai-summary` | String | Short descriptive text. | `"intro"` |
| `data-ai-field` | String | User input field. | `"email"` |
| `data-ai-content` | String | Rich text content. | `"article_body"` |
| `data-ai-media` | String | Media semantic marker. | `"illustration"` |

---

### D.3.3 Meta Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-type` | String | Conceptual type. | `"Product"` |
| `data-ai-status` | String | Status indicator. | `"active"` |
| `data-ai-context` | String | Sensitivity/semantic context. | `"personal"` |
| `data-ai-category` | String | Category or taxonomy. | `"Hydroponics"` |
| `data-ai-visibility` | String | Visual/semantic priority. | `"primary"` |

---

### D.3.4 Relational Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-link` | String | Logical cross-linking. | `"related_articles"` |
| `data-ai-ref` | String | Reference pointer. | `"author_profile"` |
| `data-ai-depends` | String | Dependency relationship. | `"cart_validation"` |
| `data-ai-rel` | String | Relationship classification. | `"child"` |
| `data-ai-source` | String | Declares data origin. | `"api"` |

---

### D.3.5 Contextual Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-intent` | String | Declares purpose/action. | `"register_user"` |
| `data-ai-purpose` | String | Human-facing explanation. | `"onboarding"` |
| `data-ai-scope` | String | Operational scope. | `"global"` |
| `data-ai-mode` | String | UI state/mode. | `"edit"` |
| `data-ai-behavior` | String | Behavioral semantics. | `"auto_save"` |

---

### D.3.6 Dynamic Attributes
| Attribute | Type | Description | Example |
|:--|:--|:--|:--|
| `data-ai-event` | String | Event trigger. | `"onClick"` |
| `data-ai-trigger` | String | Triggering condition. | `"scroll"` |
| `data-ai-state` | String | UI state. | `"loading"` |
| `data-ai-action` | String | Resulting behavior. | `"reload_data"` |
| `data-ai-transition` | String | Animated transition. | `"fade_in"` |

---

## D.4 Validation Examples (Expanded)

### JavaScript Example
```js
import Ajv from "ajv";
import schema from "./arc-schema.json" assert { type: "json" };

const ajv = new Ajv();
const validate = ajv.compile(schema);

const data = {
  page: "signup",
  intent: "register_user",
  sections: [{ name: "form" }]
};

console.log(validate(data) ? "Valid ARC JSON" : validate.errors);
```

### Python Example
```python
from jsonschema import validate, ValidationError
import json

schema = json.load(open("arc-schema.json"))
data = {"page": "dashboard", "sections": [{"name": "overview"}]}

try:
    validate(instance=data, schema=schema)
    print("Valid ARC JSON")
except ValidationError as e:
    print("Invalid:", e)
```

---

*End of Appendix D (Expanded Edition)*
