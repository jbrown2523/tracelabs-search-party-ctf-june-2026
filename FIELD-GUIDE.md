# Solo OSINT Field Guide for Trace Labs Search Party CTFs

This guide expands on the workflow described in the main [event write-up](README.md). It documents techniques I used during the June 2026 Trace Labs Global OSINT Search Party CTF without including case names, identifiers, findings, or evidence.

The objective is not to collect the largest possible amount of information. The objective is to produce relevant, reproducible, and responsibly collected intelligence that can survive review.

## Operating Boundaries

Trace Labs investigations concern real missing people. Before opening a search engine, establish the boundaries:

- Use passive, publicly accessible sources.
- View but do not engage.
- Do not contact, follow, message, call, tag, react to, or otherwise interact with anyone connected to a case.
- Do not attempt password resets, access private groups, use breached data, impersonate people, or perform active scanning.
- Do not pursue persons of interest.
- Escalate urgent, sensitive, location-related, or uncertain activity to a Trace Labs coach.
- Preserve uncertainty instead of turning a plausible lead into an unsupported claim.

Tools change. These boundaries do not.

## The Investigation Loop

I used the following loop for each case:

```text
Define question
    |
Collect public leads
    |
Validate identity and relevance
    |
Preserve direct evidence
    |
Submit, escalate, or reject
    |
Record coverage and choose the next question
```

Every search should answer a defined question. Examples:

- Does the subject have a validated public profile?
- Does a candidate username appear on another platform?
- Is there a directly supported education or employment record?
- Does an archived page preserve a useful historical identifier?
- Does a claimed relationship have explicit public support?

Without a question, tool use becomes an unfocused sweep that produces noise faster than intelligence.

## Tool-Purpose Matrix

This matrix describes the role each tool family played. A result from a discovery tool was always validated directly before it was treated as evidence.

| Tool or technique | Best use | What it can establish | What it does not establish |
|---|---|---|---|
| Search engines and query operators | Initial discovery and focused pivots | Indexed pages, documents, profiles, and references | That a search snippet is current, complete, or submission-ready |
| Platform-native search | Public profiles, posts, groups, and visible connections | Direct platform content and stable profile context | Identity from a matching display name alone |
| WhatsMyName | Username enumeration across platforms | Candidate accounts using the same username | That every reported hit exists or belongs to the subject |
| Lullar and IDCrawl | Candidate account and name discovery | Potential profiles and indexed references | Independent identity validation |
| Wayback Machine and Archive.org | Historical pages and deleted-link context | Archived content, old identifiers, and historical links | That archived content remains accurate or subject-controlled |
| Google Lens | Broad visual and exact-image discovery | Reused images, visually similar content, and indexed copies | Identity from a lookalike result |
| TinEye | Exact and modified image matching | Reuse history and exact-image matches | Comprehensive facial recognition or all web copies |
| Yandex Images | Additional visual-match coverage | Alternative image matches and visual leads | Identity without independent tie-backs |
| Local metadata inspection | Inspect preserved originals without uploading them | Embedded EXIF, software, timestamps, and file properties | That a platform-generated or edited timestamp proves subject activity |
| Jimpl and Metadata2Go | Secondary metadata checks when appropriate | Readable embedded metadata | That absent metadata means an image is false |
| PullPush | Public Reddit submission and comment discovery | Indexed Reddit activity tied to a validated input | Identity when the username itself is unvalidated |
| Google Maps and other map providers | Geography and route context | Location relationships and visual comparisons | That the subject was at a location |
| Direct screenshots and SHA-256 hashes | Evidence preservation | What was observed and whether the saved file later changed | That the underlying claim is correct without analysis |

## Search Query Patterns

Use placeholders and adapt the query to the specific intelligence question. Do not treat a search-result snippet as final evidence.

### Establish the Identity Surface

```text
"<full name>" -missing -police -news
"<known alias>" "<known location>"
"<full name>" site:<platform-domain>
"<full name>" "<school or employer>"
"<username>"
"<email address>"
```

Excluding common case-reporting terms can reveal older or independently published material. The exclusions are a discovery aid, not a reason to ignore official context.

### Search for Relationships

```text
"<full name>" cousin
"<full name>" brother
"<full name>" sister
"<full name>" friend
"<full name>" "<candidate relative name>"
```

A relationship should be supported by explicit wording, a validated network connection, or another strong tie-back. Shared surnames and platform suggestions are weak leads.

### Search for Historical Records

```text
"<full name>" filetype:pdf
"<full name>" school
"<full name>" college
"<full name>" employee
"<username>" archive
site:web.archive.org "<username or domain>"
```

PDFs, community newsletters, event programs, and archived personal pages can preserve useful historical context that no longer appears on current social platforms.

## Identity Validation Ladder

Identity confidence should rise through evidence, not repetition. Ten copied pages repeating the same unsupported claim are still one weak source.

### Weak

- Matching name
- Matching display name
- Matching or similar username
- Visual resemblance
- Platform-generated suggestion
- Search-result snippet

Weak indicators are useful for discovery but are not enough for a normal submission.

### Moderate

- Same uncommon username on two public platforms
- Consistent location and age range
- Matching face plus consistent biographical context
- Candidate profile linked from a relevant public page
- Consistent school, employer, or community connection

Moderate evidence may justify deeper validation or coach review.

### Strong

- Candidate profile cross-linked from an already validated account
- Explicit self-identification
- Multiple independent tie-backs across face, geography, network, and biography
- Direct public source explicitly supporting the claimed relationship or record
- Archived and current sources that independently converge on the same identity

Strong identity validation still does not prove every claim made on the profile.

## Username Enumeration Workflow

Username enumeration is fast and noisy. I treated enumeration results as leads only.

1. Start with a validated or case-supplied username.
2. Run it through a username-enumeration service.
3. Open each candidate directly.
4. Confirm that the page actually represents an account, not an error page, anti-bot response, or generic platform route.
5. Compare public identity indicators such as display name, image, geography, biography, and cross-links.
6. Reject candidates without an independent tie-back.
7. Record both validated results and false positives.

Common false positives:

- A site returns HTTP 200 for nonexistent usernames.
- An anti-bot or login page is mistaken for a profile.
- A username belongs to an unrelated person.
- A profile existed historically but has no reliable tie to the subject.
- An aggregator repeats a candidate without exposing the underlying source.

## Reverse-Image Workflow

Different reverse-image services index different material. I used more than one service when an image question mattered.

1. Use the clearest available public reference image.
2. Search the original image before using screenshots or crops.
3. Repeat with a tightly cropped face or distinctive area when appropriate.
4. Compare exact matches separately from visual lookalikes.
5. Open the original source behind any promising result.
6. Validate the result using non-visual tie-backs.
7. Record negative searches to avoid repeating them.

Important limitations:

- A lookalike is not an identity match.
- A reverse-image result may only lead back to known case coverage.
- Platform compression and cropping can prevent exact matches.
- No result does not prove the image is unique.
- Image timestamps may describe editing, caching, or publication rather than capture or subject activity.

## Metadata Review

Metadata inspection can answer narrow questions, but it rarely replaces identity validation.

I preferred local inspection of preserved public files where possible. Useful fields can include:

- GPS coordinates
- Original capture time
- Camera make and model
- Editing software
- Author or copyright fields
- File dimensions and format

Treat metadata carefully:

- Social platforms commonly strip EXIF.
- A software or edit timestamp may describe publication processing.
- A downloaded image may have been regenerated by a content-delivery network.
- Missing metadata is a negative result, not proof of manipulation.
- Metadata should be corroborated before it supports a substantive claim.

## Archive Workflow

Archives were useful for recovering historical context, old identifiers, and links to unavailable profiles.

1. Search the exact URL in the Wayback Machine.
2. Search related domain paths and known historical variants.
3. Review archived navigation pages for linked profiles or usernames.
4. Preserve useful archived pages locally.
5. Record the archive capture date separately from the date of the page's underlying content.
6. Treat unavailable images or contaminated pages cautiously.

Archived pages may contain copied, outdated, or unrelated content. Attribute each claim to the specific page and supporting evidence rather than trusting an archived site as a whole.

## Public Documents and Community Records

Public documents can provide stronger identity and relationship evidence than social-profile guesses. Useful document types include:

- School and college publications
- Graduation and award lists
- Community newsletters
- Sports rosters
- Event programs
- Public organizational documents
- Historical club, band, or project pages

Workflow:

1. Search the exact name with `filetype:pdf` and relevant context.
2. Open the underlying document rather than relying on the indexed snippet.
3. Confirm the section, organization, location, and date surrounding the name.
4. Check whether another source independently ties the person to that context.
5. Preserve the document and record the exact page containing the evidence.
6. Separate what the document explicitly states from conclusions inferred from it.

A document can be authentic while the identity match remains wrong. A common name on a roster still needs contextual validation.

## Relationship and Network Validation

Social graphs can reveal useful family, friend, school, work, and community connections, but platform suggestions are not evidence of a relationship.

Strong relationship indicators include:

- Explicit public wording such as a person identifying someone as a relative
- Repeated meaningful interaction over time
- Independent community or historical records naming both people
- Cross-linked profiles with consistent identity context
- A validated profile directly linking to another public profile

Weak relationship indicators include:

- Shared surname
- Appearing in a platform's suggested-people section
- A single reaction or generic comment
- Being present in the same large group
- An inferred relationship without explicit support

When documenting a relationship, state the narrowest claim supported by the source. Evidence that two people knew each other does not automatically establish friendship, family relationship, or current contact.

## Geography and Map Review

Map tools were most useful for understanding whether a location, route, or geographic claim was plausible. They were not proof that the subject was present.

When a legitimate location question exists:

1. Identify the exact claim being tested.
2. Compare place names, distances, routes, and surrounding geography.
3. Use multiple map providers when imagery or coverage differs.
4. Compare stable visual features such as road layout, building position, signage, and terrain.
5. Record which features match and which remain uncertain.
6. Escalate potentially current or exact-location findings to a coach.

Avoid converting geographic plausibility into subject movement. A road connecting two places proves the route exists, not that a person traveled it.

## Timeline and Activity Claims

Claims about activity after a person went missing require especially careful handling.

Potentially misleading timestamps include:

- Content-delivery network `Last-Modified` headers
- Image regeneration or resizing dates
- Archive capture dates
- Page update dates
- Reposts of older content
- Editing-software timestamps
- Platform migration or cache timestamps

Before treating a timestamp as subject activity, ask:

- Does the timestamp belong to the original content or a generated derivative?
- Is the action attributable to the subject rather than a platform, relative, or other account?
- Is the content original, reposted, tagged, or automatically resurfaced?
- Can the observation be reproduced from the direct source?
- Does the claim require immediate coach review?

If attribution is unclear, preserve the observation as a technical lead and explicitly state that it does not prove subject activity.

## Direct Sources and Search Snippets

I used the following source-strength order:

```text
Direct public source
    >
Archived direct source
    >
Independent corroborating source
    >
Aggregator or index
    >
Search-result snippet
```

Search snippets and aggregators are excellent discovery tools. They become weak evidence when the underlying page is inaccessible, changed, or no longer supports the snippet.

If the underlying source cannot be reproduced:

- Preserve the lead.
- Attempt an archive lookup.
- Search for independent corroboration.
- Mark the limitation.
- Do not present the snippet as stronger than it is.

## Evidence Preservation

For each serious lead, preserve a minimal evidence package:

```text
Lead ID
Direct source URL
Capture time
Specific claim
Why it matters
Identity tie-backs
Confidence and uncertainty
Screenshot or saved public source
SHA-256 hash of preserved files
Disposition: submit, coach review, reject, or monitor
```

On Windows PowerShell, a preserved file can be hashed with:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath ".\evidence-file.png"
```

Hashing does not prove that the source or claim is true. It proves whether the preserved file remains unchanged after capture.

Prefer stable, direct URLs in submissions. Temporary content-delivery URLs and tokens may expire.

A consistent filename pattern also made evidence easier to review:

```text
<case-code>_<source>_<short-description>_<capture-date>.<extension>
```

The public write-up does not include the event's evidence files or case codes. The pattern is shown only as a reusable organizational technique.

## Lead Review Template

```markdown
# Lead Review

## Claim

What specific fact might this source establish?

## Direct Source

- URL:
- Captured:
- Public and passive:

## Identity Tie-Backs

- Tie-back 1:
- Tie-back 2:

## Relevance

Why would this help the investigation?

## Limitations

What remains uncertain or unsupported?

## Disposition

- Submit
- Coach review
- Reject
- Monitor
```

## Submission Quality Gate

Before submitting, I checked:

- Is the source public and passively collected?
- Is this the direct source rather than a search result?
- Does the evidence support the exact wording of the claim?
- Is the subject or relationship adequately validated?
- Is the information new and relevant?
- Is the selected category appropriate?
- Are uncertainty and limitations explicit?
- Does the screenshot show the evidence with enough context?
- Have sensitive details been minimized?
- Should this be escalated to a coach instead of submitted normally?

If any answer was unclear, the lead needed more work or a narrower claim.

## Rejection Log

Rejected leads should be preserved without retaining unnecessary personal information.

| Lead | Reason rejected | Evidence checked | Revisit condition |
|---|---|---|---|
| Candidate profile A | Matching name only | Direct profile and public biography | Revisit only if an independent tie-back appears |
| Candidate username B | Anti-bot page reported as account | Direct page validation | Do not revisit unless the platform behavior changes |
| Historical record C | Underlying page inaccessible | Search snippet and archive check | Revisit if direct or archived proof becomes available |
| Image result D | Visual lookalike only | Reverse-image result and source page | Revisit only with non-visual corroboration |

Recording why a lead failed is more useful than simply deleting it. It prevents repeated work and shows that the candidate was considered deliberately.

## Exhaustion Matrix

An exhaustion matrix makes it easier to decide when to stop searching a weak path.

| Search family | Inputs tested | Outcome | Status |
|---|---|---|---|
| Exact-name web | Name and known variants | Known sources and collisions only | Exhausted for current indexing |
| Username search | Validated handles and likely variants | Candidate accounts reviewed | Partial or exhausted |
| Social platforms | Relevant public platforms | Profiles validated or rejected | Partial or exhausted |
| Archives | Exact URLs, domains, and identifiers | Captures preserved or absent | Exhausted where accessible |
| Reverse image | Original and selected crops | Exact matches, noise, or no result | Exhausted for tested images |
| Metadata | Preserved originals | Useful fields or negative result | Exhausted |

Use precise status language:

- `Checked`: The named input was reviewed.
- `Exhausted where accessible`: The meaningful public routes were covered, but inaccessible or private sources remain.
- `Not applicable`: No validated input exists for the tool.
- `Blocked`: Access failed and no rule-compliant workaround was attempted.

Avoid claiming that the entire internet or every possible tool has been exhausted.

## Solo-Investigator Time Management

A solo investigator cannot search every path. I would use this rhythm in a future event:

### Initial Sweep

- Spend a short, fixed period establishing a baseline for every case.
- Identify which cases provide validated footholds.
- Rank cases by likely usefulness, not only potential points.

### Focused Sprints

- Choose one intelligence question.
- Search for a fixed period.
- Rank the resulting leads.
- Validate only the strongest candidates.
- Package submissions together.

### Stop Conditions

Pause or abandon a path when:

- The only support is a matching name or username.
- Repeated searches return the same known sources.
- The underlying evidence cannot be accessed or corroborated.
- A tool requires prohibited, private, paid, or uncertain access.
- The claim would exceed what the source proves.
- Further work would consume time better spent on a stronger lead.
- The lead may reveal urgent or highly sensitive information that requires a coach.

## Tools and Methods I Deliberately Did Not Use

Choosing not to use a tool can be part of responsible tradecraft.

I did not:

- Access breached credentials or leaked personal data.
- Attempt password resets or account recovery.
- Join private groups or interact with accounts.
- Use active network-scanning tools without a relevant, permitted subject-controlled technical identifier.
- Treat paid biometric search as automatically appropriate.
- Upload sensitive evidence to unnecessary third-party services.
- Submit platform-generated timestamps as proof of subject activity without corroboration.
- Infer identity from a matching name, username, or face alone.

## Final Principle

Discovery creates possibilities. Validation creates intelligence.

A useful OSINT submission should allow another reviewer to understand:

1. What was found.
2. Where it came from.
3. Why it is connected.
4. What it proves.
5. What it does not prove.
6. Why it may help.

That standard matters more than the number of tools used.
