# Prompt for Gemini: create the AfroIndie Founder Google Form

Paste the block below into Gemini (or the "Create with AI" ✨ box inside
Google Forms itself, which uses Gemini) to generate the form. The field
order, types, and option wording match `index.html` exactly — keep the
option text unchanged if Gemini offers to "improve" the wording, since the
site's submission code sends these exact strings.

---

```
Create a Google Form for event registration with these exact specs:

Title: AfroIndie Founder — Webinar Registration

Description: Register for AfroIndie Founder, a 3-day hands-on virtual
experiment for indie builders, themed "Now That You Can Build." Friday to
Sunday, Sept 18–20, 2026. Virtual via Google Meet. 44 slots only.

Add these questions, in this exact order, with these exact types and exact
option text:

1. Short answer — "Full name" — required

2. Short answer — "Email" — required — turn on response validation for
   email format

3. Short answer — "Social handle(s)" — not required — description text:
   "X, Instagram, LinkedIn — whatever you're on"

4. Paragraph — "What have you built, or are you currently building?" —
   required — description text: "A weekend project, an MVP, a side hustle —
   anything counts."

5. Checkboxes — "Topics you're most interested in" — not required — options,
   in this order:
   - Ideation & Refining Ideas
   - Building & Launching Fast
   - Growth: 0 to 500 Users
   - Business Models & Unit Economics
   - Fundraising (Preseed & Seed)
   - Burn Rate, Runway & Profitability

6. Multiple choice — "Interested in a community of actual AI builders?" —
   required — options exactly: Yes, No

Settings:
- Turn off "Collect email addresses" (email is already a question above)
- Turn off "Limit to 1 response"
- Link responses to a new Google Sheet
- Confirmation message: "You're in! Keep an eye on your inbox — your Google
  Meet link and a short pre-event note are coming before Sept 18–20, 2026."
```

---

## After the form is created

Get its pre-fill link and send it over so the site's `CONFIG` object in
`index.html` can be wired to it — see the "Connecting the Google Form"
section in `README.md` for the exact steps.
