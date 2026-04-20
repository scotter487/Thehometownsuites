# The Hometown Suites — Website

Static HTML/CSS website for [thehometownsuites.com](https://thehometownsuites.com). No build tools or dependencies required — open `index.html` in any browser.

---

## Waitlist Form

The waitlist form is located in the **"Stay Connected"** section at the bottom of the page (`#contact`). It collects interest from prospective guests before the property opens in summer 2026.

### Fields

| Field | Type | Required | Purpose |
|---|---|---|---|
| Your Name | Text input | Yes | Identifies the submission |
| Email Address | Email input | Yes | Used to follow up when bookings open |
| I'm interested in | Dropdown select | No | Captures suite vs. office interest |
| Anything else? | Textarea | No | Free-form notes (stay length, arrival date, questions) |

### How It Works

The form currently uses **client-side only** handling — there is no backend or third-party service connected yet.

When the user clicks **"Join the Waitlist"**, the `handleSubmit` function in `index.html` runs:

1. `e.preventDefault()` stops the browser from navigating or reloading the page.
2. The form element is hidden (`display: none`).
3. A success message (`#successMsg`) is shown in its place confirming the submission.

```js
function handleSubmit(e) {
  e.preventDefault();
  document.querySelector('.contact__form').style.display = 'none';
  document.getElementById('successMsg').style.display = 'flex';
}
```

No data is currently sent or stored anywhere. The success state is cosmetic until a backend is wired up.

### Connecting a Backend

To make the form functional, replace the `handleSubmit` logic with one of the following approaches:

**Option A — Fetch to your own API endpoint:**
```js
async function handleSubmit(e) {
  e.preventDefault();
  const data = Object.fromEntries(new FormData(e.target));
  await fetch('/api/waitlist', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data),
  });
  document.querySelector('.contact__form').style.display = 'none';
  document.getElementById('successMsg').style.display = 'flex';
}
```

**Option B — Third-party form service (e.g. Formspree, Netlify Forms, EmailJS):**

Replace `action="#"` in the `<form>` tag with your service's endpoint URL and update or remove `handleSubmit` per the service's instructions. Most services require no custom JS.

---

## Files

| File | Description |
|---|---|
| `index.html` | Full single-page site — markup, inline JS |
| `styles.css` | All styles — color variables, layout, responsive breakpoints |

## Colors

The design is built around `#2D495E` with a complementary gold accent.

| Variable | Value | Usage |
|---|---|---|
| `--primary` | `#2D495E` | Nav, section backgrounds, icons |
| `--primary-dark` | `#1E3344` | Hero background, footer |
| `--accent` | `#C9A96E` | Buttons, labels, highlights |
| `--bg` | `#F8F5F0` | Main page background |
