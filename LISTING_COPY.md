# Atlassian Marketplace Partner Listing Copy — External Share, Guest Access & Link Expiry Guard for Confluence

## App Identity
- **App Name**: External Share, Guest Access & Link Expiry Guard for Confluence
- **App Key**: `com.evidencepair.confluence.link.guard`
- **App ID**: `ari:cloud:ecosystem::app/26e2e52e-6bae-47e6-983a-ef0309e06fec`
- **Vendor**: EvidencePair LLC
- **Category**: Security & Compliance / Document Management / Administration
- **Runs on Atlassian Badge Eligibility**: **100% Eligible** (Native Forge `nodejs24.x`, Zero Remotes, Zero Forge SQL/KVS, Zero Data Egress)

---

## Tagline / Summary
> Time-boxed external share leases, 1-click SHA-256 lockdown & guest access audit radar.

---

## Full Marketplace Description

### Eliminate Forgotten External Share Links & Unmonitored Guest Access in Confluence Cloud

Enterprise Confluence spaces routinely accumulate forgotten external share links, unrevoked vendor review pages, and over-permissive guest access on sensitive security runbooks and internal policies.

**External Share, Guest Access & Link Expiry Guard for Confluence** gives Confluence administrators and page owners time-boxed external share leases (`7/14/30` days), 1-click cryptographic SHA-256 external lockdowns, automated label governance (`external-share-locked` / `external-lease-active`), and a global exposure audit radar—built 100% on Atlassian Forge (`nodejs24.x`) with **zero external servers** and **zero data egress**:

1. **Time-Boxed External Share Lease & SHA-256 Lockdown Seal (`confluence:contentBylineItem`)**:
   - Inspect live page exposure (`INTERNAL LOCKED`, `EXTERNAL LEASE ACTIVE`, `EXPIRED SHARE — QUARANTINED`) directly from the Confluence page byline.
   - Grant a temporary external review lease or execute an immediate **1-Click External Lockdown**, recording a deterministic **Web Crypto SHA-256 signature** (`accountId|pageId|exposureState|expiryTimestamp|action`) in Confluence Content Property `linkGuardState` (`<32 KB`) and syncing `external-share-locked` or `external-lease-active` labels.
2. **External Share & Guest Governance Policy Engine (`confluence:spaceSettings`)**:
   - Configure space-wide maximum external share lease durations (`7`, `14`, or `30` days) and automatic anonymous/guest lockdown rules in Space Property `linkGuardPolicy` (`<32 KB`).
3. **Global Exposure Radar, 1-Click Bulk Lockdown & SOC 2 CSV Export (`confluence:globalPage`)**:
   - Audit space permissions and page leases across Confluence, revoke expired external shares in 1 click with SHA-256 audit logging, and export a signed SOC 2 / ISO 27001 access control CSV report.

---

## Version Highlights (Highlights 1–3)

### Highlight 1: Time-Boxed External Share Leases & 1-Click SHA-256 Page Lockdown
Control page exposure directly from the Confluence byline (`INTERNAL LOCKED`, `EXTERNAL LEASE ACTIVE`, `EXPIRED SHARE — QUARANTINED`). Grant temporary external review leases or trigger an immediate 1-Click External Lockdown backed by a tamper-evident SHA-256 signature (`accountId|pageId|exposureState|expiryTimestamp|action`) in Confluence v2 Content Properties (`<32 KB`).

### Highlight 2: Space External Share & Guest Access Governance Policy Engine
Enforce maximum external share lease durations (`7`, `14`, or `30` days), automatic expired-share quarantine, and anonymous/guest access lockdown rules in Space Settings (`linkGuardPolicy`). Syncs `external-share-locked` and `external-lease-active` labels via Confluence REST API v1.

### Highlight 3: Global Exposure Audit Radar, 1-Click Bulk Lockdown & SOC 2 CSV Export
Scan Confluence spaces for anonymous access, guest permissions, and expired external share leases from an Onest-styled radar dashboard. Revoke expired shares in 1 click (`external-share-locked`) and export a cryptographically signed RFC-4180 CSV access control report for SOC 2 and ISO 27001 audits.
