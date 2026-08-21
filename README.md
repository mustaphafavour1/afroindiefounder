# AfroIndie Founder — Registration Page

A single-page, non-scrolling registration site for the AfroIndie Founder webinar
(Fri–Sun, Sept 18–20, 2026 · virtual via Google Meet · 44 slots).

It's one static file — `index.html` — with no build step and no dependencies
besides two Google Fonts (Fredoka for the display wordmark, Poppins for
everything else). Open it directly in a browser, or deploy it as-is.

## Preview locally

```bash
# from this folder
npx serve .
# or just open index.html directly in a browser
```

## Deploying (Vercel)

This is a static site, so Vercel needs zero config — import the repo and
deploy. `index.html` at the root is served automatically.

## Connecting the Google Form

The page collects everything in its own branded form, then submits it
silently in the background to a Google Form via that form's `/formResponse`
endpoint (a hidden iframe catches the response so the visitor never leaves
the page or sees Google's UI). The data lands in the Google Form's
responses / linked Sheet exactly like a normal submission.

**The wiring lives in one place:** the `CONFIG` object inside the
`<script>` tag near the bottom of `index.html`:

```js
var CONFIG = {
  actionUrl: "https://docs.google.com/forms/d/e/REPLACE_WITH_FORM_ID/formResponse",
  entries: {
    name: "entry.REPLACE_NAME",
    email: "entry.REPLACE_EMAIL",
    socials: "entry.REPLACE_SOCIALS",
    building: "entry.REPLACE_BUILDING",
    topics: "entry.REPLACE_TOPICS",
    community: "entry.REPLACE_COMMUNITY"
  }
};
```

To wire it up once the Google Form exists:

1. Open the Google Form in edit mode.
2. Click the **⋮** overflow menu (top right) → **Get pre-filled link**.
3. Fill each field with a recognizable placeholder (type the field's own
   name into it) so it's obvious which is which, then click **Get link**.
4. Click **Copy link**.
5. Send that link over (to Claude, or paste it here yourself) — it contains
   every field's `entry.<id>`, plus the form ID for the `/formResponse` URL
   (same ID as in the link, with `/viewform` swapped for `/formResponse`).

Easiest path: just paste the pre-filled link back into the chat and it'll be
mapped into `CONFIG` directly. Doing it by hand is also fine — each
`entry.NNNNNNNN=...` in the link's query string corresponds to one field, in
the order the fields appear on the form.

**Important:** the Google Form's "Topics" checkbox options and the "Interested
in a community…" choice options must match the site's option text
*exactly* (see `GOOGLE_FORM_PROMPT.md`), or the submitted values won't line
up with a defined option in the form.

## Form fields

| Site field | Google Form question type | Required |
|---|---|---|
| Full name | Short answer | Yes |
| Email | Short answer (email validation) | Yes |
| Social handle(s) | Short answer | No |
| What have you built / are building | Paragraph | Yes |
| Topics of interest | Checkboxes (6 options) | No |
| Interested in an AI-builder community | Multiple choice (Yes / No) | Yes |

The "what have you built" field is required on purpose — the flyer frames
proof of having tried to build something as the actual ticket in.

## Files

- `index.html` — the entire site (markup, styles, submission logic)
- `GOOGLE_FORM_PROMPT.md` — a ready-to-paste prompt for Gemini (or Google
  Forms' own "Create with AI" panel) to generate the matching Google Form
