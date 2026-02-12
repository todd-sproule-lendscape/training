# Operating Lease Training

A companion learning website for operating lease accounting, covering lessor accounting under IFRS 16 and ASC 842.

**Live site:** https://kennywonglendscape.github.io/training/

## Lessons

1. **What is an Operating Lease?** - Operating vs finance lease distinction, classification criteria, lessor accounting overview, RIAD vs EIR comparison
2. **Income Recognition** - Straight-line rental income (IFRS 16 S81, ASC 842-30-25-11), 30/360 day count convention, RIAD processing scenarios, variable payments, modifications, collectibility
3. **Depreciation & Initial Direct Costs** - Straight-line depreciation, useful life, IDC amortisation, RIAD daily rate allocation (TrackStraightLineAmount), UK/US tax overview
4. **Revenue Table & Configuration** - Revenue table structure, ALIR/ALCR output records, operating lease columns, charge-accounting-types configuration

## Interactive Features

- **Quiz** - 20 questions (multiple-choice + calculation) in a page-by-page format grouped by lesson, with per-lesson score breakdown and personalised feedback
- **Calculator** - Straight-line lease calculator with depreciation/NBV schedule and Chart.js visualisation
- **Progress Tracking** - localStorage-based lesson completion and quiz score history
- **Password Protection** - Front-end password gate using SHA-256 hashing (see below)

## Password Protection

The site is protected by a simple front-end password gate. Users must enter a shared password before accessing any content. Login state is stored in `localStorage`.

**Default password:** Ask your administrator for the shared password.

### Changing the Password

1. Open a browser console (F12) and run:
   ```js
   crypto.subtle.digest('SHA-256', new TextEncoder().encode('YOUR_NEW_PASSWORD'))
     .then(buf => console.log(Array.from(new Uint8Array(buf)).map(b => b.toString(16).padStart(2,'0')).join('')));
   ```
2. Copy the hex string printed in the console.
3. In `js/main.js`, replace the `PASSWORD_HASH` value in the `Auth` object with the new hex string.

### Disabling Password Protection

1. Remove the `<!-- Auth guard -->` `<script>` tags from the `<head>` of every HTML file.
2. On `index.html`, remove the `#login-section` div and the `style="display:none"` from `#site-content`.
3. Optionally remove the `Auth` object from `js/main.js`.

> **Note:** This is front-end-only obfuscation, not strong security. A technically inclined user could bypass it. For production security, use server-side authentication or hosting-level access controls.

## Tech Stack

HTML + CSS + JavaScript (no build tools). Bootstrap 5 and Chart.js loaded via CDN. Deployed directly to GitHub Pages.

## Local Development

Open `index.html` directly in a browser, or run a local server:

```
python -m http.server 8000
```

Then visit http://localhost:8000
