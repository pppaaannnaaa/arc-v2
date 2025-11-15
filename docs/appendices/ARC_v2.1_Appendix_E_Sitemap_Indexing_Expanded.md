# Appendix E — ARC Sitemap & AI Indexing Specification

## E.1 Overview

The **ARC Sitemap** is an optional companion artifact that provides AI agents and crawlers with a machine-friendly index of ARC-annotated pages.  
Its purpose is to accelerate ingestion, reduce crawling cost, and supply pre-computed summaries or snapshots to agents that prefer deterministic inputs over live crawling.

This appendix defines a recommended sitemap format, usage guidelines, validation schema, and best practices for secure and reliable AI indexing.

---

## E.2 Why an ARC Sitemap?

- **Faster ingestion:** Provide AIs with pre-parsed ARC summaries to avoid repeated DOM parsing.  
- **Deterministic data:** Reduce ambiguity by supplying canonical `ai-summary` fields.  
- **Reduced load:** Offload crawler work by publishing structured representations.  
- **Version control:** Track changes and allow AIs to fetch delta updates only.  

Use the sitemap when you control the content pipeline (CMS, static site generator, or backend) and want to provide an authoritative AI-friendly feed.

---

## E.3 Recommended Sitemap Formats

ARC supports multiple formats depending on publisher preference: **JSON**, **JSON-LD**, and **YAML**. JSON is the recommended default for machine consumption.

### E.3.1 JSON — Example

```json
{
  "arc_sitemap_version": "2.1",
  "site": "https://example.com",
  "generated_at": "2025-11-09T08:00:00Z",
  "pages": [
    {
      "url": "https://example.com/signup",
      "lastmod": "2025-11-08T12:00:00Z",
      "ai_indexable": true,
      "ai_summary": "Signup page for AquaGrow; collects email and password for onboarding.",
      "ai_tags": ["signup","onboarding","user-account"],
      "ai_checksum": "sha256:af3c...",
      "ai_snapshot": {
        "page": "signup",
        "title": "Create Your Account",
        "sections": [
          { "name": "registration_form", "fields": ["email","password"], "intent": "register_user" }
        ]
      }
    }
  ]
}
```

### E.3.2 JSON-LD — Example

```json
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "ARC Sitemap",
  "url": "https://example.com/arc-sitemap.json",
  "distribution": [
    {
      "@type": "DataDownload",
      "encodingFormat": "application/json"
    }
  ]
}
</script>
```

### E.3.3 YAML — Example

```yaml
arc_sitemap_version: "2.1"
site: "https://example.com"
generated_at: "2025-11-09T08:00:00Z"
pages:
  - url: "https://example.com/signup"
    lastmod: "2025-11-08T12:00:00Z"
    ai_indexable: true
    ai_summary: "Signup page for AquaGrow; collects email and password for onboarding."
    ai_tags: ["signup","onboarding","user-account"]
    ai_checksum: "sha256:af3c..."
```

---

## E.4 Sitemap Fields — Definitions

| Field | Type | Required | Description |
|:--|:--:|:--:|:--|
| `url` | string | yes | Canonical URL of the page. |
| `lastmod` | date-time | recommended | ISO-8601 last modification timestamp. |
| `ai_indexable` | boolean | yes | Whether the page may be ingested by AI agents. |
| `ai_summary` | string | recommended | Short human/A1-readable summary of the page. |
| `ai_tags` | array[string] | optional | Topics or categories for quick filtering. |
| `ai_checksum` | string | optional | Content checksum (e.g., `sha256:`) to detect changes. |
| `ai_snapshot` | object | optional | Pre-parsed ARC JSON snapshot for deterministic ingestion. |
| `crawl_priority` | number (0-1) | optional | Priority hint for crawlers; 1 highest. |
| `auth_required` | boolean | optional | Whether the page requires authentication to view. |
| `robots_directive` | string | optional | e.g., `noindex`, `nofollow` — crawler instruction. |

---

## E.5 Publishing & Hosting the Sitemap

- Place the sitemap at a well-known URL, for example: `https://example.com/arc-sitemap.json` or `/.well-known/arc-sitemap.json`.  
- Add an entry to `robots.txt` to indicate the sitemap location:  
  ```txt
  Sitemap: https://example.com/arc-sitemap.json
  ```
- Support conditional requests (ETag/If-Modified-Since) for efficient crawler behavior.  
- Offer gzip compression for large sitemaps.

---

## E.6 Access Control & Privacy

- Honor `ai_indexable: false` for pages that must not be indexed by AIs.  
- Do not include sensitive snapshots in public sitemaps; instead, mark `auth_required: true` and provide authenticated API endpoints for partners.  
- Use `ai_tags` and `ai_context` in snapshots to annotate sensitivity (e.g., `sensitive`, `personal`).  
- Provide a machine-readable policy at `/.well-known/arc-policy.json` describing retention, access, and approved AI consumers.

---

## E.7 Crawler Etiquette & Rate Limits

- Provide a suggested rate limit in the sitemap's metadata, e.g., `"crawl_rate": "1/s"`.  
- Encourage polite crawling: respect `robots.txt`, use an identifiable `User-Agent`, and support conditional requests.  
- Offer a developer contact (e.g., `ai-crawl-contact` field) for crawl coordination in enterprise contexts.

---

## E.8 Versioning & Delta Feeds

- Include `arc_sitemap_version` at top-level to avoid parsing errors across versions.  
- For large sites, provide delta feeds (`/arc-sitemap-deltas/YYYY-MM-DD.json`) containing only changed pages since a given timestamp.  
- Use `ai_checksum` to detect changed content server-side before re-supplying snapshots.

---

## E.9 Validation Schema (JSON Schema Draft-07 compatible)

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "ARC Sitemap Schema v2.1",
  "type": "object",
  "required": ["arc_sitemap_version","site","generated_at","pages"],
  "properties": {
    "arc_sitemap_version": { "type": "string" },
    "site": { "type": "string", "format": "uri" },
    "generated_at": { "type": "string", "format": "date-time" },
    "pages": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["url","ai_indexable"],
        "properties": {
          "url": { "type": "string", "format": "uri" },
          "lastmod": { "type": "string", "format": "date-time" },
          "ai_indexable": { "type": "boolean" },
          "ai_summary": { "type": "string" },
          "ai_tags": { "type": "array", "items": { "type": "string" } },
          "ai_checksum": { "type": "string" },
          "ai_snapshot": { "type": "object" },
          "crawl_priority": { "type": "number", "minimum": 0, "maximum": 1 },
          "auth_required": { "type": "boolean" },
          "robots_directive": { "type": "string" }
        }
      }
    }
  }
}
```

---

## E.10 Example Generator (Python snippet)

```python
import hashlib, json, datetime
from urllib.parse import urljoin

def page_checksum(content: str) -> str:
    return "sha256:" + hashlib.sha256(content.encode("utf-8")).hexdigest()

def build_arc_entry(url, html_content, snapshot=None, indexable=True):
    return {
        "url": url,
        "lastmod": datetime.datetime.utcnow().isoformat()+"Z",
        "ai_indexable": indexable,
        "ai_summary": snapshot.get("summary") if snapshot else None,
        "ai_tags": snapshot.get("tags") if snapshot else [],
        "ai_checksum": page_checksum(html_content),
        "ai_snapshot": snapshot
    }

# Example usage
entry = build_arc_entry("https://example.com/signup", "<html>...</html>", snapshot={"page":"signup","summary":"Create account"}, indexable=True)
print(json.dumps(entry, indent=2))
```

---

## E.11 Best Practices for AI Consumers (Crawlers & Agents)

- Respect `ai_indexable` and `auth_required`. Do not index pages marked non-indexable.  
- Prefer `ai_snapshot` if present to avoid re-parsing DOM. Use checksum to decide whether to refresh.  
- When snapshots are absent, fetch the page and parse `data-ai-*` attributes directly.  
- Keep a local cache and implement conditional GETs to minimize bandwidth usage.  
- Validate incoming sitemap against the schema before ingestion.

---

## E.12 Security Considerations

- Ensure sitemaps do not expose PII inadvertently. Use `auth_required` for restricted pages.  
- Implement access controls for enterprise or partner-only AI indexing endpoints.  
- Monitor sitemap access and anomalous crawl patterns; provide rate-limited API tokens if needed.

---

## E.13 Closing Notes

The ARC Sitemap is optional but highly recommended for sites aiming for robust AI integration. It provides a pragmatic balance between live crawling and authoritative, server-provided semantics that AI systems can rely on.

---

*End of Appendix E — ARC Sitemap & AI Indexing Specification*
