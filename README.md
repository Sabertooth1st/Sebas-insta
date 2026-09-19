# sebastianuzice

The landing page behind the Instagram bio link, and the plan for what gets posted.

## What is here

- `index.html` — the page people land on when they tap the bio link. One file:
  markup, styles and script all live in it, so there is no build step and
  nothing to install. Open it in a browser and what you see is what gets
  published.
- `before.jpg`, `after.jpg` — the transformation pair at the top of the page.
  Both come from the sets he labelled himself (AT 177KG and CURRENTLY), and
  both are gym mirror selfies in the same pose, so the comparison is like for
  like. Neither is edited.
- `avatar.jpg` — the profile photo, with `avatar-placeholder.svg` as its fallback.
- `content/14-day-plan.md` — what to post, in what order, and when the product goes live.

The page is built around one thing: the before and after, then the plan that
produced it. Everything else on the page is secondary to those two.

## What is still outstanding

| Where | What it needs |
| --- | --- |
| The plan | The Gumroad link, replacing `PUT_THE_GUIDE_LINK_HERE` |
| Presets | The Gumroad link, replacing `PUT_THE_PRESETS_LINK_HERE` |
| TikTok / YouTube | Parked in a comment below the Instagram link. Uncomment a block once its URL exists |
| Mailing list | A form endpoint — see below |

Nothing on the page points anywhere dead, so it is safe to publish as it
stands. Search `index.html` for `EDIT ME` to find the copy worth revisiting.

## Arming a thing for sale

Both cards work the same way. Each carries `data-pending`, and while that
attribute is there the card hides its price and its button, shows a line
pointing at the mailing list instead, and refuses to be tapped.

To put something on sale, make two edits to that card:

1. Put the real checkout URL in `href`.
2. Delete `data-pending`.

The price and the **Get it** button appear on their own. That is the whole
change — there is nothing else to switch on.

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

1. **The before and after.** Replace `before.jpg` and `after.jpg` to change it.
   They are shown at 2:3 and cropped to fill, so tall photos work best. Pick
   two shots in the same pose and the same kind of place — it is the likeness
   that makes the difference read. If either file is missing the whole block
   hides itself rather than showing a broken image.
2. **The bio line and the plan card.** The two pieces of copy that decide
   whether anyone scrolls.
3. **"What it took".** The list of rules, in his own words. It is what makes
   the card above believable, which is why it sits directly under it.
4. **The links.** There is a `COPY ME` block in the comments to paste for a new
   one. Put the real URL in `href` and delete `data-placeholder` to make a link
   live; leave the attribute on and it shows a dashed **set me** pill and
   cannot be tapped.

The colours are the tokens at the top of the `<style>` block. `--brand` drives
the icons and focus rings; `--accent` drives the buttons. Light and dark are
both handled already.

## Taking payment

Gumroad is the fastest way to start: free to open, hosts the file and the
checkout, handles receipts and sales tax, and takes a cut per sale. Stripe is
cheaper per sale but you have to build the checkout, so it is worth moving to
later, not now.

The account has to be created by hand — it needs a real name, email and bank
details. Once a product is published, its link goes in the matching card.

## Adding analytics later

Every link already reports its own clicks, but only if an analytics script is on
the page. Add Plausible or Google Analytics to `<head>` and the clicks start
showing up with no other change — that is how you learn which link deserves the
bio.
