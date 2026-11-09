# Security: External Share, Guest Access & Link Expiry Guard

Updated 9 November 2026

How the Atlassian Marketplace app **External Share, Guest Access & Link Expiry Guard**, made by EvidencePair LLC, handles data, what protects it, how we handle vulnerabilities, and which certifications apply. What the app stores is listed in full in its [privacy policy](./PRIVACY_POLICY.md).

## Data handling

- **Forge only.** The app runs on Atlassian Forge (`nodejs24.x`) on Atlassian infrastructure.
- **No egress.** The manifest declares no external permissions and no remote services. The app makes requests only to your site's Confluence REST API, and it loads no analytics, error-reporting services or external assets.
- **No storage of its own.** The app keeps its data in Confluence on your site: a space property (`linkGuardPolicy`), a page property (`linkGuardState`) and two page labels (`external-share-locked`, `external-lease-active`). It uses no Forge storage or Forge SQL, and EvidencePair has no copy.
- **Requests run as the user.** Every request the app makes to Confluence runs as the person using its screens, so Confluence applies that person's own permissions. The app makes no requests as itself, and it has no scheduled jobs, triggers or background tasks.
- **What it does not do.** The app does not read or change Confluence's page restrictions, space permissions, public links or guest access. A lockdown or lease is a record in the page property plus a label on the page. Settings such as locking expired leases and blocking anonymous and guest access are saved with the space's policy; the app does not act on them. A lease that passes its expiry time shows as expired, and nothing changes until someone runs a lockdown.
- **Saves are not checked.** The app does not check Confluence's reply when it saves a property or changes a label. If Confluence refuses a save, for example because the person cannot edit the page, the app's screen can still show the change until it is reloaded.
- **Permissions it asks for.**
  - `read:page:confluence`: read a page's ID, title, space and version, the list of pages in a space, and the `linkGuardState` property.
  - `write:page:confluence`: save the `linkGuardState` property on a page.
  - `read:space:confluence`: read a space's `linkGuardPolicy` property.
  - `write:space:confluence`: save a space's `linkGuardPolicy` property.
  - `read:label:confluence`, `write:label:confluence`: add and remove the app's two labels on a page. Confluence asks for both scopes to add a label. The app does not read labels.
  - `read:content-details:confluence`: declared but unused. No request the app makes needs it.
- **What the hashes are.** Each `linkGuardState` record carries a SHA-256 hash of its account ID, page ID, state, expiry time and action. It does not cover the page title, note, lease length or time of the change. The app recomputes the hash each time it reads the record and shows "TAMPER DETECTED" when it does not match. The radar's CSV report ends with a SHA-256 hash of the viewer's account ID, the export time and the report's rows. The app's screens call these signatures and seals. They are not digital signatures: anyone who can edit a page could change its record and recompute the hash.

## Encryption

The app stores nothing outside your Confluence site and sends nothing outside Atlassian's platform. Encryption in transit and at rest is provided by Atlassian as part of your site, as described in the [Atlassian Trust Center](https://www.atlassian.com/trust). The app adds no encryption of its own.

## Vulnerability management

- **Reporting.** Email security@evidencepair.com. Tell us the app, what you found and how to reproduce it. Please do not test against sites you do not own. We acknowledge every report within one business day.
- **Response.** EvidencePair adopted a written security incident response plan on 12 October 2026. It covers triage, containment, investigation, notification of Atlassian and affected customers, and recovery.
- **Dependencies.** The app's npm dependencies are pinned in its lockfile. Atlassian maintains and patches the Forge runtime.
- **Bug bounty.** We do not run a bug bounty programme.

## Certifications

EvidencePair holds no security certifications, and the app has had no independent penetration test or external audit. The infrastructure the app runs on is Atlassian's, and Atlassian's own certifications cover it: see the [Atlassian Trust Center](https://www.atlassian.com/trust).
