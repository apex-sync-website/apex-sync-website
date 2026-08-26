# Creator Protection implementation and launch gate

## Changed artifacts

- `index.html`
  - Added desktop Creator Protection nav destination.
  - Added an accessible mobile navigation owner instead of leaving links desktop-only.
  - Added Creator Protection to the existing “What We Do” list.
- `creator-protection/index.html`
  - Dedicated indexable landing page and creator intake frontend.
- `../research/apex-creator-protection-design-study-20260825.md`
  - Research synthesis, experience contract, and anti-pattern gate.

## White-label and SEO claim boundary

The public page must not use provider brand names or imply that Apex supplies protection technology. Apex may describe general creator risks, invite creators to seek protection, collect applications, screen initial fit, communicate status, and coordinate introductions.

The page explicitly states that Apex does **not** provide detection, claiming, removal, monetization, Content ID, or DRM technology. Independent third parties provide any protection services under their own criteria and terms. Automated QA fails if rendered copy contains `Creator Shield` or `Enfinity`, or if the required role disclaimers disappear.

Do not publish market-size statistics—including the proposed `$9 billion` privacy-market claim—without a primary source defining the market, currency, measurement period, and methodology.

## Intake transport owner

The landing page has one transport configuration point:

```js
const INTAKE_ENDPOINT = '';
```

An empty value is intentionally fail-closed. A valid form will show an honest configuration message and will **not** send or store creator data.

The approved production endpoint must:

1. Accept JSON via `POST`.
2. Validate all required fields server-side.
3. Reject or ignore `company_website` honeypot submissions.
4. Preserve `submission_id` and return it in JSON.
5. Enforce deduplication/idempotency on `submission_id`.
6. Append to the canonical website-intake table, not an outreach/source tab.
7. Store the supplied Pacific timestamp, source/referrer, UTM values, and consent version.
8. Return a non-2xx status on any uncommitted write.
9. Keep Google credentials and private tokens server-side.

## Payload schema

- `submission_id`
- `submitted_at_pt`
- `referrer`
- `utm_source`
- `utm_medium`
- `utm_campaign`
- `consent_version`
- `creator_name`
- `contact_name`
- `email`
- `country`
- `primary_channel`
- `primary_platform`
- `content_category`
- `youtube_url` (optional)
- `tiktok_url` (optional)
- `instagram_url` (optional)
- `facebook_url` (optional)
- `rights_control`
- `existing_provider`
- `infringement_url` (optional)
- `notes` (optional)
- `consent`

## Local deterministic form test

Serve the site locally and open:

`/creator-protection/?test_mode=1`

Mock success activates only on `localhost` or `127.0.0.1`. It never sends data and returns a visible local-test receipt.

## Verification checklist

- [ ] Direct route returns 200.
- [ ] Homepage desktop nav opens Creator Protection.
- [ ] Homepage mobile menu opens, closes, supports Escape, and links correctly.
- [ ] Original homepage `#ecosystem`, `#about`, and `#contact` links still work.
- [ ] Landing-page mobile menu opens, closes, supports Escape, and links correctly.
- [ ] No horizontal overflow at 1440×900, 1024×768, 390×844, and 320×568.
- [ ] One H1 and logical headings.
- [ ] SEO title and description describe access/intake without presenting Apex as the technology provider.
- [ ] Rendered copy contains no provider brand names.
- [ ] Explicit Apex/independent-provider responsibility boundary is present.
- [ ] No unsourced market-size statistic is published.
- [ ] Keyboard-only path reaches every link, disclosure, field, radio, checkbox, and submit control.
- [ ] Reduced-motion mode removes continuous/reveal motion dependencies.
- [ ] Empty required submission presents summary and per-field errors.
- [ ] Errors clear after correction.
- [ ] Unconfigured production transport sends no request and claims no success.
- [ ] Local test mode returns a stable receipt and sends no request.
- [ ] Browser console has no errors.
- [ ] Production endpoint write is verified by exact canonical Sheet tab/row and Submission ID.
- [ ] Production smoke test is completed after deployment.

## Canonical operations workbook discovered

`Creator Shield — Canonical Outreach Operations (2026)`  
Spreadsheet ID: `1aaAOH56YFCRpxBG0608rzhHx57oWKTzNQOBi_rxz19s`

The dedicated source owner now exists:

- Tab: `11_WEBSITE_INTAKE`
- Sheet ID: `1499290544`
- Columns: `A:AA` (27 fields)
- Frozen header: row 1
- Initial data rows: empty

Verified readback on August 25, 2026 PT. Do not write website applications into `01_SOURCE_REGISTRY`, `02_RAW_IMPORT`, `03_CREATORS`, or outreach-event tabs by approximation. Production transport must append to this exact tab and return the page-generated Submission ID.
