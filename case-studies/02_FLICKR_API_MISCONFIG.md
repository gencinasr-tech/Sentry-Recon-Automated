# 📸 Case Study: Cross-Environment API Misconfiguration & User Enumeration

**Date:** January 2026
**Target:** Flickr (Staging Environment)
**Status:** ⚪ Disclosed (Closed as Informative)

## 📝 Executive Summary
During a subdomain reconnaissance phase, I identified a development endpoint (**Staging API**) that improperly accepted **Production API Keys**. This misconfiguration allowed an unauthenticated attacker to perform API Reflection (listing internal methods) and User Enumeration (resolving emails to internal User IDs) on the staging environment using public production credentials.

Although the vendor accepted the technical validity of the finding, they classified the impact as low/informative. I am publishing this research for educational purposes with sensitive data redacted.

---

## 🛠️ Technical Breakdown

### 1. Discovery & Reconnaissance
Using passive enumeration techniques, I identified a live staging API endpoint exposed to the internet.

By analyzing network traffic on the main production site, I extracted the public **Production API Key** used by the web client.

### 2. Vulnerability: Cross-Environment Credential Reuse
The core issue was a lack of isolation between environments. The Staging API validated requests using the Production database's API keys.

* **Production Key:** `56b24a...[REDACTED]`
* **Staging Endpoint:** `api.staging.[TARGET].com`

Sending a test request to Staging with the Production key resulted in a successful response (`"stat": "ok"`), confirming that both environments shared the authentication backend.

### 3. Information Disclosure (API Reflection)
Leveraging the reflection methods, the API disclosed a comprehensive list of available commands, including administrative methods that are typically restricted or hidden in production environments.


### 4. Impact: User Enumeration / PII Leak
I demonstrated that it was possible to resolve private email addresses to public profiles and internal User IDs using specific API methods on the staging server.

**Proof of Concept (Redacted):**
```bash
curl "[https://api.staging](https://api.staging).[TARGET].com/services/rest/?method=flickr.people.findByEmail&api_key=[REDACTED_PROD_KEY]&find_email=[TARGET_EMAIL]&format=json&nojsoncallback=1"
```

{
  "user": {
    "id": "[REDACTED_NSID]",
    "nsid": "[REDACTED_NSID]",
    "username": { "_content": "[REDACTED_USERNAME]" }
  },
  "stat": "ok"
}

---

### 🖼️ Evidence / Evidencias

**1. API Method Reflection:**

> *Screenshot showing `flickr.reflection.getMethods` exposing internal administrative methods on the staging environment.*

**2. PII Leak Proof of Concept:**

> *Screenshot confirming the resolution of a private email address to a specific User ID (Sensitive data redacted).*

## 📉 Resolution & Lessons Learned

**Reported to:** Flickr Bug Bounty (HackerOne)
**Status:** Closed as *Informative* (Risk accepted / Low impact according to vendor).

**🎓 Pentester's Takeaway:**
This case highlights the importance of **Environment Isolation**. Development and Staging environments are often the "soft underbelly" of an organization. Even if Production is secure, a Staging endpoint reusing Production credentials (API Keys) can become a valid vector for Information Disclosure and User Enumeration. Always check if keys from the main site open doors in subdomains.
