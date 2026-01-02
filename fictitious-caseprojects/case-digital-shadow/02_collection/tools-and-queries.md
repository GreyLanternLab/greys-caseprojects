# Tools & Example Queries

This document lists the tools and example queries used during the fictional OSINT investigation.
All tools were applied passively and without interaction.

---

## 🌐 Website & Domain

**Tools:**  
whois, dig, nslookup, crt.sh, Censys, SecurityTrails, DNSDB-lite, BuiltWith, Wappalyzer, Wayback Machine

### WHOIS (registration & privacy)

```bash
whois glam-ops.net
```

Output: registration date, registrar, privacy shielding
Pivot: registrant email (if visible), registrar, timing of registration

DNS & Mail Authentication
```
dig +short A glam-ops.net
dig TXT glam-ops.net
dig MX glam-ops.net
```
Output: hosting, SPF/DMARC, mail infrastructure
Pivot: IP → ASN / hosting provider
Missing SPF/DMARC = potential risk indicator

SSL / Certificate Transparency

crt.sh search: glam-ops.net

Output: historical certificates, subdomains
Pivot: subdomains → additional infrastructure paths

Technology Fingerprint

BuiltWith / Wappalyzer on https://glam-ops.net

Output: CMS, frameworks, trackers
Pivot: generic builders or templates (disposable-site indicator)

Archives

Wayback Machine search: glam-ops.net

Output: first capture, content changes
Pivot: site age vs “fast deployment” narrative

## 📧 Contact Points (Email / Phone / WhatsApp)

Tools:
Search engines, dig, email syntax validators (syntax only)

Email String (Exact Match)
```
"apply@glam-ops.net"

```
Output: reuse on other sites or platforms
Pivot: copy-paste recruitment networks

Email Domain with Keywords
```
"glam-ops.net" AND ("apply" OR "contact" OR "portfolio")
```
Output: alternative contact routes
Pivot: geographic or platform spread

Mail Authentication
```
dig MX glam-ops.net
dig TXT glam-ops.net
```
Output: professional mail setup or disposable configuration

Phone Number (Exact)
```
"+254700000999"
```
Output: reuse on classifieds or social platforms
Pivot: VOIP providers, regional clustering

⚠️ No calls, no messages, no interaction.


## 📱 SOCMINT
Handle & Bio Search
```
site:instagram.com "glam_opps"
```
Output: profile age, links, WhatsApp presence
Pivot: alternative handles

Cross-Platform Overlap
```
"glam_opps" OR "GlamOpps" ("model" OR "agency")
site:twitter.com OR site:tiktok.com
```
Output: duplicated branding or language
Pivot: syndication patterns


## 🖼️ Image Analysis

Tools:
Google Images, TinEye, InVID, Forensically, ExifTool

Reverse Image Search

Upload images to Google Images or TinEye

Expected output:
Stock usage, first appearance

Possible pivots:
Template or reused assets

EXIF Metadata (if available)
```
exiftool image.jpg
```
Output: camera/app, timestamps
Pivot: absence is not suspicious, but documented

⚠️ No facial recognition on real persons.

## ✍️ Text & Language
Exact Sentence Matching
```
"fast-track selection" "video interview" "deployment within 2–3 weeks"
```
Output: copy-paste recruitment scripts
Pivot: multilingual variants

Semantic Variants
```
("accommodation provided" OR "housing included")
("experience not required" OR "no experience needed")
```
Output: content farms or ad networks
Pivot: regional reuse


## 🏢 Entities & Registrations

Tools:
OpenCorporates, national business registries, OpenSanctions, Google Maps, NGO reports

Company Name
```
"GlamOpps" "Glam Opps" "GlamOpps Agency"
site:opencorporates.com
```
Output: registrations, name variants
Pivot: directors / UBOs (where public)

Reviews & Address
```
"GlamOpps" reviews
site:maps.google.com
```
Output: fake reviews or missing address
Pivot: address mismatch


## 🌍 Context & Corroboration

Compare with UNODC, IOM and US TIP reports on recruitment patterns

Build timelines and node diagrams (Mermaid, draw.io, Gephi)

Identify inconsistencies and corroborating signals
