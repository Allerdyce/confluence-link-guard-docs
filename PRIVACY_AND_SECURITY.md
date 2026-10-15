# Privacy Policy, Data Residency & Security Statement — External Share, Guest Access & Link Expiry Guard for Confluence

**Effective Date**: October 15, 2026  
**Publisher**: EvidencePair LLC  
**App Key**: `com.evidencepair.confluence.link.guard`  
**App ID**: `ari:cloud:ecosystem::app/26e2e52e-6bae-47e6-983a-ef0309e06fec`

---

## 1. Zero Data Egress & Architecture Statement ("Runs on Atlassian")

**External Share, Guest Access & Link Expiry Guard for Confluence** executes 100% inside Atlassian's managed Forge Cloud runtime (`nodejs24.x`) and declares **zero external remote endpoints (`remotes:`)** and **zero external egress permissions**.

- **0 Bytes External Storage**: EvidencePair LLC does not operate any external servers, databases, or telemetry endpoints that receive customer data from External Share, Guest Access & Link Expiry Guard for Confluence.
- **100% Native Confluence Space & Content Property Storage (<32 KB Enforced)**:
  - Space-level external share and guest governance policies are stored exclusively inside your Confluence instance's **Space Properties** (`/wiki/api/v2/spaces/{spaceId}/properties`, key `linkGuardPolicy`).
  - Page-level external share leases and SHA-256 lockdown records are stored exclusively inside your Confluence instance's **Page Content Properties** (`/wiki/api/v2/pages/{pageId}/properties`, key `linkGuardState`).
  - Page labels (`external-share-locked` and `external-lease-active`) are stored exclusively as native Confluence content labels (`/wiki/rest/api/content/{pageId}/label`).
  - Zero Forge SQL and Zero Forge KVS storage are used.

---

## 2. Data Residency & Compliance Inheritance

Because External Share, Guest Access & Link Expiry Guard for Confluence stores 100% of its policy configurations and page lockdown/lease signatures within native Confluence Space and Page Properties:
- **Automatic Data Residency**: All app data automatically resides in the exact geographic region (US, EU, AU, DE, SG, CA, UK, JP, etc.) configured for your host Confluence Cloud product under Atlassian Data Residency.
- **Lifecycle & Deletion**: All app properties are automatically included in standard Confluence Cloud backups and are permanently deleted when the host page, space, or property is deleted by your administrator.

---

## 3. Privacy Policy (GDPR / CCPA / SOC 2 / ISO 27001 Alignment)

### Personal Data Processed
To provide cryptographic attribution on page external share lease grants and lockdown events, the app records:
- **Atlassian Account ID (`accountId`)** of the user granting a lease or locking down a Confluence page.
- **ISO-8601 UTC Expiry Timestamp (`expiryTimestamp`)**, exposure state (`INTERNAL_LOCKED`, `EXTERNAL_LEASE_ACTIVE`, or `EXPIRED_SHARE_QUARANTINED`), and governance action (`action`).
- **Stores Personal Data Declaration**: No external PII (such as names, emails, or phone numbers) is stored or exported outside the Atlassian Cloud host tenant.

### How Data Is Used
- Processed solely within the Atlassian Forge runtime to compute and verify a deterministic SHA-256 integrity signature (`accountId|pageId|exposureState|expiryTimestamp|action`).
- Never transmitted outside your Atlassian Cloud tenant, never sold, and never shared with third parties.

### Data Subject Rights (Access, Rectification, Erasure)
Space and organization administrators have full read/write/delete control over all app properties via standard Confluence REST API v2 endpoints:
- `GET` / `PUT` / `DELETE /wiki/api/v2/spaces/{spaceId}/properties/{propertyId}` (`linkGuardPolicy`)
- `GET` / `PUT` / `DELETE /wiki/api/v2/pages/{pageId}/properties/{propertyId}` (`linkGuardState`)

---

## 4. Security Contact
Security inquiries or vulnerability reports may be submitted to **EvidencePair LLC** at `support@titlecovenant.com`.
