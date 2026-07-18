# Phone booking form (deploy to a PUBLIC repo)

`index.html` is the mobile web form for arming bookings. It reads/writes
`requests.json` in the **private** `tennis-bot-requests` repo via the GitHub API,
using a fine-grained token the user saves once in their phone browser.

## Deploy

Free-tier GitHub Pages needs a **public** repo, and the booking data is private, so:

1. Put `index.html` in a **public** repo (a new one, or a page in your existing
   `psc-sun` Pages site).
2. Enable GitHub Pages for it (Settings → Pages → deploy from branch).
3. Open the Pages URL on the phone and add it to the home screen.

The form's code is public but contains **no data and no credentials** — everything is
fetched at runtime with the user's token.

## Token (per phone, one-time)

Create a **fine-grained personal access token**:
- Resource owner: your account
- Repository access: **only** `tennis-bot-requests`
- Permissions: **Contents → Read and write**
- Expiry: ~90 days (rotate when it lapses)

Paste it into the form's token field. It's stored in that browser's `localStorage`
only. Because it's scoped to `tennis-bot-requests` alone, an extracted token can edit
booking requests but never the bot code or secrets.

## Editing users / presets

The form's user and preset lists are constants in the `CFG` block near the top of
`index.html` (they change rarely). If you add a user or a court preset in the bot's
`config.json`, mirror the name here.
