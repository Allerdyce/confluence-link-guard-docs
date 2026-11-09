# Privacy policy: External Share, Guest Access & Link Expiry Guard

Updated 9 November 2026

This policy describes the Atlassian Marketplace app **External Share, Guest Access & Link Expiry Guard** ("the app"), made by EvidencePair LLC ("EvidencePair", "we"). EvidencePair's company privacy policy, which covers our website and email you send us, is at <https://evidencepair.com/privacy/>.

## In short

- The app runs on Atlassian Forge, inside your Confluence site. It declares no external egress and no remote services, and it makes requests only to your site's Confluence API.
- It keeps its data in Confluence itself, as a space property, a page property and two page labels. That data is never sent to EvidencePair.
- The only personal data it stores itself is the Atlassian account ID of the person who made the latest change to a page's lease or lockdown, or to a space's policy. It also copies page titles into its records, and a title can contain personal data.

## What the app stores

**One space property, `linkGuardPolicy`, per space whose policy someone saves in space settings:**

- the space's ID, and a space key field, which this version always sets to the fixed value `MFS` whatever the space;
- the policy: the longest lease allowed (7, 14 or 30 days), the list of lease lengths on offer, the on/off settings for locking expired leases and for blocking anonymous and guest access, and the names of the two labels;
- the Atlassian account ID of the person who last saved it, and when;
- the size of the record in bytes.

**One page property, `linkGuardState`, per page where someone grants a lease or locks the page down, one page at a time or in a bulk lockdown:**

- the page's ID, title and space ID;
- the Atlassian account ID of the person who took the action, and when;
- the page's state (locked or lease active), the action, the lease length in days and the expiry time;
- a short note that the app writes itself, such as "Time-boxed 7-day external review lease granted". The app's screens have no field for typing a note;
- a SHA-256 hash of the account ID, page ID, state, expiry time and action, which lets the app tell whether those values have changed since they were saved. The hash adds no information of its own;
- the size of the record in bytes.

Each new action on a page overwrites that page's record, and each save of a policy overwrites the space's. Each record therefore holds only the latest account ID.

**Two page labels, `external-share-locked` and `external-lease-active`.** Each time the app saves a page's record, it adds one of these labels to the page and removes the other.

The app does not look up names, email addresses or profiles.

The radar (the app's global page) builds a CSV report each time it opens and shows it on screen for copying. The app does not save the report. It lists each page's ID, title and state with the account ID from its record, and ends with the account ID of the person viewing it.

## What the app reads from Confluence

- The page the byline item is opened on: its ID, title, space ID and version number, and its `linkGuardState` property.
- The `linkGuardPolicy` property of the space the byline item or space settings page is opened in.
- When someone saves a lease or lockdown, the `linkGuardPolicy` property of one fixed space: the space with ID 262148, a value set in the app's configuration. The app does not read the page's own space policy at that point. If your site has no space with that ID, or the person cannot view it, the app uses its default policy.
- On the radar, up to 50 pages of that same fixed space: each page's ID, title and version number, and its `linkGuardState` property. The global page belongs to no space, so this version always scans the space with ID 262148. If your site has no space with that ID, the list is empty.

It does not ask Confluence for page content, comments, attachments, restrictions or permissions.

## Where the data lives

Space properties, page properties and labels are part of your Confluence site's data. Atlassian stores them with the rest of your site, in your site's data residency location, under Atlassian's own security and privacy commitments. The app has no storage of its own: it uses no Forge storage and no Forge SQL, and EvidencePair runs no servers in its path.

## Who can see it

Confluence shows a page property to anyone who can view the page, through Confluence's REST API. The app's byline item also shows the account ID in a page's record to anyone who opens it on that page. Anyone who can view a page can therefore see who last granted it a lease or locked it down. Confluence shows a space property to anyone who can view the space, so anyone who can view a space can read its policy, including the account ID of the person who saved it. The labels show on the page.

The app asks Confluence for everything as the person using it. The radar and its CSV report therefore show only pages that person can view.

Confluence's permissions also decide who can change this data. Saving a page property or changing a page's labels needs permission to edit the page. Saving a space property needs space administrator permission.

## Retention and deletion

The app keeps the properties and labels until someone deletes them. It has no retention setting, deletes nothing, runs nothing on a schedule, and has no uninstall step. When a lease passes its expiry time, the app shows it as expired; it does not delete the record. A page's property and labels are removed when the page is permanently deleted, and a space's property when the space is. Anyone who can edit a page can delete its `linkGuardState` property through Confluence's REST API and remove its labels. A space administrator can delete the space's `linkGuardPolicy` property in the same way. Do this before uninstalling if the data must go.

## Account closure

The app does not take part in Atlassian's personal data reporting. When an Atlassian account is closed, its account ID stays in any `linkGuardState` or `linkGuardPolicy` record where that person made the latest change. It stays until someone makes a newer change there, or the property, page or space is deleted.

## Platform logs

The app writes nothing to the Forge platform's logs. Atlassian's platform can still record errors it sees while the app runs, such as an unhandled error and its message ([Atlassian: view app logs](https://developer.atlassian.com/platform/forge/view-app-logs/)).

## Email and support

If you email us, our [company privacy policy](https://evidencepair.com/privacy/) describes how we handle that email, and the current restrictions on where our apps may be used. For help with the app, see <https://evidencepair.com/support/>.

## What we never do

We do not sell personal data or use it for unrelated advertising or AI training. The app's data stays in your Confluence site and never reaches us.

## Changes to this policy

The date at the top changes when this policy does. Every version is kept in this repository's history.

## Contact

hello@evidencepair.com
