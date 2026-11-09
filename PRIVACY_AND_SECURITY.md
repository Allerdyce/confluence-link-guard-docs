# Data Residency & Security Summary — External Share, Guest Access & Link Expiry Guard

> The app's privacy policy is [PRIVACY_POLICY.md](./PRIVACY_POLICY.md), and its security documentation (data handling, encryption, vulnerability management and certifications) is [SECURITY.md](./SECURITY.md). This page is the architecture summary.

**Updated**: 9 November 2026  
**Publisher**: EvidencePair LLC  
**App Key**: `com.evidencepair.confluence.link.guard`  
**App ID**: `ari:cloud:ecosystem::app/26e2e52e-6bae-47e6-983a-ef0309e06fec`

---

## 1. Zero Data Egress & Architecture Statement ("Runs on Atlassian")

**External Share, Guest Access & Link Expiry Guard** executes 100% inside Atlassian's managed Forge Cloud runtime (`nodejs24.x`) and declares **zero external remote endpoints (`remotes:`)** and **zero external egress permissions**.

- **0 Bytes External Storage**: EvidencePair LLC does not operate any external servers, databases, or telemetry endpoints that receive customer data from External Share, Guest Access & Link Expiry Guard.
- **100% Native Confluence Space & Content Property Storage (<32 KB Enforced)**:
  - Space-level external share and guest access policies are stored exclusively inside your Confluence instance's **Space Properties** (`/wiki/api/v2/spaces/{spaceId}/properties`, key `linkGuardPolicy`).
  - Page-level external share leases and SHA-256 lockdown records are stored exclusively inside your Confluence instance's **Page Content Properties** (`/wiki/api/v2/pages/{pageId}/properties`, key `linkGuardState`).
  - Page labels (`external-share-locked` and `external-lease-active`) are stored exclusively as native Confluence content labels (`/wiki/rest/api/content/{pageId}/label`).
  - Zero Forge SQL and Zero Forge KVS storage are used.
- **Requests run as the user**: every Confluence request the app makes runs as the person using it, so Confluence applies that person's permissions. The app reads and changes no page restrictions, space permissions, public links or guest access.

---

## 2. Data Residency & Lifecycle

Because External Share, Guest Access & Link Expiry Guard stores 100% of its policy configurations and page lockdown/lease records within native Confluence Space and Page Properties and page labels:
- **Data Residency**: All app data is stored with the rest of your Confluence site's data, in your site's data residency location.
- **Lifecycle & Deletion**: The app deletes nothing itself and has no uninstall step. Its properties and labels stay until someone deletes them, or until the page or space they belong to is permanently deleted.

---

## 3. Personal Data

### Personal Data Processed
To attribute page external share lease grants and lockdown events, the app records:
- **Atlassian Account ID (`accountId`)** of the user granting a lease or locking down a Confluence page, and (`updatedBy`) of the user who last saved a space's policy.
- **ISO-8601 UTC Expiry Timestamp (`expiryTimestamp`)**, exposure state (`INTERNAL_LOCKED` or `EXTERNAL_LEASE_ACTIVE`), and governance action (`action`).
- **Page title** (`pageTitle`), copied from Confluence. A page title can contain personal data.
- The app does not look up or store names, email addresses or phone numbers.

### How Data Is Used
- The account ID is shown in the page byline and in the radar's CSV report, and is one input to the record's SHA-256 hash (`accountId|pageId|exposureState|expiryTimestamp|action`).
- Never transmitted outside your Atlassian Cloud tenant, never sold, and never shared with third parties.

### Access, Correction & Deletion
People with permission to edit a page can read, change or delete its `linkGuardState` property, and space administrators can do the same for `linkGuardPolicy`, through Confluence REST API v2:
- `GET` / `PUT` / `DELETE /wiki/api/v2/spaces/{spaceId}/properties/{propertyId}` (`linkGuardPolicy`)
- `GET` / `PUT` / `DELETE /wiki/api/v2/pages/{pageId}/properties/{propertyId}` (`linkGuardState`)

The app does not take part in Atlassian's personal data reporting. See [PRIVACY_POLICY.md](./PRIVACY_POLICY.md) for what happens when an account is closed.

---

## 4. Security Contact
To report a security issue, email `security@evidencepair.com`. We acknowledge every report within one business day. EvidencePair holds no security certifications; see [SECURITY.md](./SECURITY.md). For support, see <https://evidencepair.com/support/>.
