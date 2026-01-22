# 📸 Case Study: Cross-Environment API Key & PII Leak on Flickr

**Executive Summary:**
During automated reconnaissance, I identified a Staging API endpoint that improperly accepts Production API keys. This misconfiguration allowed for full API method reflection and unauthorized access to sensitive methods, resulting in a PII (Personally Identifiable Information) leak where email addresses could be resolved to user profiles.

---

## 🛠️ Technical Details / Detalles Técnicos

- **Vulnerability:** Cross-Environment Configuration / Broken Access Control
- **Attack Vector:** Public API Key -> Staging Endpoint -> Method Reflection -> PII Leak
- **Impact:** Information Disclosure, PII Leakage (Email to User correlation), Potential Data Loss (via administrative methods).

### 1. Reconnaissance (The Discovery)
My automation script (`bb-check`) identified a live staging endpoint returning 200 OK:
`https://api.staging.flickr.com/services/rest/`

### 2. Exploitation (The Exploit)
By extracting a public API Key from the main production website and replaying it against the staging endpoint, I confirmed the environments shared authentication backends but lacked proper authorization scopes on staging.

**Step 1: API Reflection**
Using `flickr.reflection.getMethods`, the API disclosed a full list of administrative and internal methods not typically available to public keys.

**Step 2: PII Leak (Proof of Concept)**
Using the `flickr.people.findByEmail` method, I was able to resolve an email address to a specific user ID and username, bypassing privacy controls.

**Request:**
`GET /services/rest/?method=flickr.people.findByEmail&api_key=[PROD_KEY]&find_email=[REDACTED]`

**Response:**
```json
{
  "user": {
    "id": "155114775@N08",
    "nsid": "155114775@N08",
    "username": { "_content": "Crazycactiguy" }
  },
  "stat": "ok"
}
