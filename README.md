# sebastianuzice

The landing page behind the Instagram bio link, and the plan for what gets posted.

## What is here

- `index.html` — the page people land on when they tap the bio link. One file:
  markup, styles and script all live in it, so there is no build step and nothing
  to install. Open it in a browser and what you see is what gets published.
- `avatar-placeholder.svg` — the neutral photo shown until a real one exists.
- `content/14-day-plan.md` — what to post, in what order, and when the product goes live.

## What is still a placeholder

The page is safe to publish as it stands: nothing on it points anywhere dead.
Search `index.html` for `EDIT ME` to find what is worth filling in. A link left
mid-edit is drawn with a dashed border and a **set me** pill and refuses to do
anything if a visitor taps it, so a half-finished page never misdirects anyone.

| Where | What it needs |
| --- | --- |
| Photo | A square photo saved in this repo as `avatar.jpg` (600×600 is plenty) |
| TikTok / YouTube / Work with me | Parked in a comment below the Instagram link. Uncomment a block once its URL or address exists |
| Paid slot | The Gumroad link, replacing `PUT_THE_GUMROAD_LINK_HERE` |
| Before / after | Two photos of the same shot saved as `presets-before.jpg` and `presets-after.jpg` |
| Mailing list | A form endpoint — see below |

## Putting the page online

This repository is private, and GitHub Pages only serves private repositories on
a paid plan. Two free ways round that:

**Make the repository public, then use GitHub Pages.** Nothing here is secret,
so this is the simplest route.

1. Repo **Settings** → **General** → **Danger Zone** → **Change visibility** → public.
2. **Settings** → **Pages** → Source: **Deploy from a branch**.
3. Pick the repo's default branch, folder `/ (root)`. Save.
4. A minute later it is live at `https://sabertooth1st.github.io/Sebas-insta/`.

**Or keep it private and use Cloudflare Pages.** Free on private repos, and
faster.

1. Sign in at dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages**
   → **Connect to Git**, and pick this repository.
2. Framework preset: **None**. Leave the build command empty and the output
   directory as `/`.
3. Deploy. The URL looks like `https://sebas-insta.pages.dev`.

Whichever it is, that URL goes in the Instagram bio, and every push updates it
within a minute. A custom domain is a nicer link and costs about $10 a year —
worth doing, but not before there is something to sell.

## Turning on the email form

The form is real, but it deliberately refuses to send anywhere until an endpoint
is set. Better a visible "not switched on yet" than an address disappearing into
nothing.

Pick one, all free to start:

- **Formspree** — fastest. Sign up, make a form, copy the endpoint that looks like
  `https://formspree.io/f/abcdwxyz`. Addresses arrive by email and export to CSV.
- **Buttondown** or **MailerLite** — more setup, but you can actually mail the
  list afterwards, which is the entire point of collecting it.

Then in `index.html` find:

```html
<form class="signup" id="signup" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```

and replace the `action` value with the endpoint. The script notices on its own
and starts posting to it. A hidden honeypot field already filters most bots.

## Editing the page

In order of what matters:

1. The name, handle and bio line, at the top of the `<body>`.
2. The paid slot — the bordered card at the top. It is already filled in for
   the preset pack. One thing is missing: create the product on Gumroad, then
   replace `PUT_THE_GUMROAD_LINK_HERE` with the link it gives you. Nothing else
   changes — the price and the **Get it** button appear on their own. Until
   then the card shows "not on sale yet", points at the mailing list and
   refuses to be tapped, so the page is safe to put live before the checkout
   exists.

   The before-and-after pair is what actually sells presets. Save the same
   photo edited and unedited as `presets-after.jpg` and `presets-before.jpg`
   (portrait crop). The block hides itself until both are there.
3. The links. There is a `COPY ME` block in the comments to paste for a new one.
   Put the real URL in `href` and delete `data-placeholder` to make a link live.

The colours are the tokens at the top of the `<style>` block. `--brand` drives
the icons and focus rings; `--accent` drives the buttons. Light and dark are both
handled already.

## Taking payment

Gumroad is the fastest way to start: free to open, hosts the file and the
checkout, handles receipts and sales tax, and takes a cut per sale. Stripe is
cheaper per sale but you have to build the checkout, so it is worth moving to
later, not now.

The account has to be created by hand — it needs a real name, email and bank
details. Once the product is published, its link goes in the paid slot and the
page starts selling.

## Adding analytics later

Every link already reports its own clicks, but only if an analytics script is on
the page. Add Plausible or Google Analytics to `<head>` and the clicks start
showing up with no other change — that is how you learn which link deserves the
bio.
