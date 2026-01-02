# Research Log — Analysis of nederlandseloteriij.nl

**Typosquatting & Infrastructure Assessment**

---

## 1. Context

During routine use of search engines (Google and DuckDuckGo), the domain  
**`nederlandseloteriij.nl`** (containing an additional _“i”_) appeared among search results strongly resembling references to the legitimate **Nederlandse Loterij**.

Given the visual similarity, the regulated context of online gambling, and the high level of public trust associated with the brand, the domain was flagged as a potential **typosquat** warranting closer OSINT analysis.

---

## 2. Initial Reconnaissance: WHOIS & Infrastructure

### 2.1 WHOIS Data

WHOIS queries returned the following information:

- **Domain:** `nederlandseloteriij.nl`
    
- **Registration date:** 11 November 2025
    
- **Status:** Active
    
- **Nameservers:**
    
    - `phil.ns.cloudflare.com`
        
    - `naomi.ns.cloudflare.com`
        
- **Registrar:** Internet Domain Service BS Corp.
    
- **Registrant name:**  
    _Staats loterij B.V. (part of Nederlandse Loterij)_
    
- **Administrative / technical contact (email):**  
    A string that resolves to the generic label **“email”** when copied.
    

**Interpretation:**

- The listed email address is **non-functional**, consistent with **WHOIS obfuscation** implemented by the registrar or WHOIS service.
    
- The use of a well-known organisation as registrant is **not verifiable** and likely **misleading**.
    
- This combination suggests **intentional concealment of the true actor**.
    

---

### 2.2 Hosting & Infrastructure

- DNS and hosting are routed via **Cloudflare**:
    
    - origin IP address concealed
        
    - CDN, TLS and baseline security enabled
        
- HTTPS is correctly configured
    

**Interim conclusion:**  
The infrastructure is professionally configured and deliberately shielded, consistent with a purposeful setup rather than an experimental or test site.

---

## 3. Certificate Transparency (CT) Analysis

### 3.1 Findings via crt.sh

Certificate Transparency logs reveal multiple certificates issued for  
`nederlandseloteriij.nl`:

- Issuers:
    
    - **Google Trust Services (WE1)**
        
    - **Sectigo Public Server Authentication CA DV E36**
        
- **Not Before:** 11 November 2025
    
- **Not After:** February 2026
    
- Certificates include:
    
    - the apex domain
        
    - wildcard-style entries (`*.nederlandseloteriij.nl`)
        

Both **precertificates** and **leaf certificates** are present.

---

### 3.2 Interpretation

- Certificates are:
    
    - valid;
        
    - not revoked;
        
    - temporally consistent with domain registration.
        
- Multiple issuers likely reflect:
    
    - re-issuance;
        
    - testing or migration;
        
    - normal TLS lifecycle behaviour.
        

**Key observation:**  
CT timestamps align with the WHOIS registration date and provide **no indication of prior or hidden activity** before November 2025.

---

## 4. Wayback Machine & Archiving

### 4.1 Context

- The domain did **not** exist in the Wayback Machine prior to the investigation.
    
- Initial archives were **manually created by the researcher**.
    
- The domain has only been active since **11-11-2025**.
    

---

### 4.2 Temporal Observations

Since the first archive capture:

- no observable content changes;
    
- no malware injections;
    
- no sudden redirects or payload alterations.
    

**Interim conclusion:**  
The site exhibits stable and consistent behaviour and does not currently appear to have entered a later malicious phase.

---

## 5. Functional & Content Analysis

### 5.1 Structure & Content

The site:

- is built as a **modern React / Next.js web application**;
    
- is fully localised for a Dutch audience;
    
- includes:
    
    - links to **legitimate subdomains** of nederlandseloterij.nl;
        
    - articles and blog-style content **hosted locally on the typosquat domain**.
        

**Key observation:**  
Local hosting of articles appears deliberate, likely to prevent broken links or inconsistencies should content on the legitimate site change.

---

### 5.2 Age Verification Popup

The site displays an **18+ age verification prompt**:

- appears after a short delay;
    
- stores acceptance locally via `localStorage`;
    
- does not trigger redirects or external network requests.
    

**Interpretation:**

- No indicators of malicious behaviour.
    
- Likely implemented to:
    
    - limit legal exposure;
        
    - comply with gambling regulations;
        
    - reinforce perceived legitimacy.
        

---

## 6. JavaScript & Code Analysis

### 6.1 Analysed Components

- Next.js application chunks
    
- Layout, header and footer
    
- Cookie and age-verification components
    
- Navigation and form logic
    

### 6.2 Findings

- No evidence of:
    
    - obfuscated malware;
        
    - credential harvesting;
        
    - suspicious external endpoints.
        
- Present:
    
    - SEO-oriented metadata;
        
    - indexation-focused content structure;
        
    - standard analytics hooks.
        

**Interim conclusion:**  
The codebase supports a **content- and affiliate-oriented web application model**.

---

## 7. Traffic & Tracking

### 7.1 Typosquat Domain

The typosquat domain likely measures:

- visitor counts;
    
- on-site behaviour;
    
- SEO performance.
    

This is plausibly achieved via first-party analytics (e.g. Cloudflare Web Analytics).

---

### 7.2 Legitimate Target Subsites

Outbound links include parameters such as `_gl` and `_gcl_au`:

- These belong to **legitimate Nederlandse Loterij infrastructure**.
    
- They are **not accessible or controllable** by the typosquat operator.
    
- Conversion tracking benefits the legitimate organisation, not the typosquat actor.
    

**Conclusion:**  
The typosquat operator benefits **indirectly via traffic capture**, not via downstream analytics or conversions.

---

## 8. Final Assessment

- `nederlandseloteriij.nl` is a **recently registered typosquat domain**.
    
- The site is:
    
    - technically professional;
        
    - content-consistent;
        
    - legally defensive in design.
        
- No evidence of **active malicious behaviour** was identified.
    
- The most plausible objectives are:
    
    - SEO traffic interception;
        
    - reputational free-riding;
        
    - affiliate or referral traffic generation.
        
- The infrastructure allows for **future escalation**, but **no current indicators** suggest this has occurred.
    

---

## 9. Reflection & Potential Next Steps

- Template detection and reuse across similar domains
    
- Clustering analysis of comparable typosquats
    
- Ongoing monitoring for content or redirect changes
    
- Consideration of notification to brand owner or regulator
