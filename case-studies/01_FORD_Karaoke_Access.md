# 🚗 Case Study: Broken Access Control on Pre-Launch Infotainment System

**Executive Summary:**
During a routine automated reconnaissance session targeting Ford assets, I identified a misconfigured S3 Bucket exposing internal configuration files. Analysis of these files revealed URLs for "Pre-Launch" (Staging) environments. Pivoting to these environments allowed me to discover a third-party application (Karaoke) that was fully accessible without authentication.

---

## 🛠️ Technical Details / Detalles Técnicos

- **Vulnerability:** Broken Access Control / Improper Authentication
- **Attack Vector:** Information Disclosure (S3 Bucket) -> Pivoting -> IDOR/BAC
- **Impact:** Financial Loss (free premium service), Information Leakage.

### 1. Reconnaissance (The Discovery)
My automation script ('bb-check') flagged new subdomains and files in a public S3 Bucket ('wonka-dev'). Upon analyzing the exposed XML and JSON configuration files, I located a specific config file ('v2.6.json') listing vehicle application endpoints.

**Key finding in JSON:**
\\\json
{
  "id": "com.ford.wonka.stingraykaraoke",
  "url": "https://karaoke-car-player-prod-ford-prelaunch.REDACTED.com",
  "category": "Audio"
}
\\\

### 2. Exploitation (The Exploit)
The URL pointed to a 'prelaunch' environment. Accessing it via a standard web browser revealed:
1.  The web application loaded without requesting credentials.
2.  Upon accepting the disclaimer, full access to the music dashboard was granted.
3.  **Proof of Concept:** I was able to play full premium songs (copyrighted content) and generate "Passenger" QR codes.

### 🖼️ Evidence / Evidencias

**1. Access to Dashboard (No Auth required):**
> *Screenshot showing the music player interface loaded without login.*
![Dashboard](./dashboard.png)

**2. Premium Content Playback:**
> *Screenshot confirming playback of copyrighted songs.*
![Player](./music-player.png)

## 📉 Resolution & Lessons Learned

**Reported to:** Ford VDP (HackerOne)
**Status:** Closed as *Informative* (Third-party asset risk accepted).

**🎓 Pentester's Takeaway:**
This case highlights the criticality of Supply Chain Security. Even without a monetary bounty, this exercise validated the reconnaissance methodology: Automation detected the leak -> Manual analysis found the URL -> Curiosity found the logic flaw.
