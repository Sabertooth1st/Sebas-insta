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
- `assets/` — the captioned versions, for posting to Instagram rather than for
  the page. See below.
- `product/README.md` — what is for sale, at what price, and why none of it is
  in this repository.
- `content/14-day-plan.md` — what to post, in what order, and when the product
  goes live.

The page is built around one thing: the before and after, then the plan that
produced it. Everything else on the page is secondary to those two.

### Page photos vs. post photos

Two sets, and they are not interchangeable:

| | For | Why |
| --- | --- | --- |
| `before.jpg`, `after.jpg` | The web page | Plain 2:3 crops, no text. The page lays them out side by side and captions them in HTML, so they stay sharp and readable at any width. |
| `assets/before-after.jpg` | An Instagram feed post | 1080×675, captioned **177 KG / TODAY**. The text is baked in because a feed post has to carry its own meaning. |
| `assets/before-after-story.jpg` | An Instagram story | 1080×1920, the same pair at story size. |
| `assets/progress-three-stage.jpg` | A feed post | 1620×675, three stages — 177 kg, along the way, today. The middle frame is the one that makes it look survivable rather than magic. |

Do not put the captioned versions on the page: the page already captions them,
and you would get the label twice.

## What is still outstanding

| Where | What it needs |
| --- | --- |
| The plan | The Gumroad link, replacing `PUT_THE_GUIDE_LINK_HERE` |
| Presets | The Gumroad link, replacing `PUT_THE_PRESETS_LINK_HERE` |
| TikTok / YouTube | Parked in a comment below the Instagram link. Uncomment a block once its URL exists |
| Mailing list | A form endpoint — see below |
| GitHub Pages | Not switched on yet — see *Putting the page online* |

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

The prices live in two places: the card in `index.html` and the list in
`product/README.md`. Change one, change the other. They drifted apart once
already.

## Putting the page online

This repository is **public**, so GitHub Pages serves it free. That is the whole
reason nothing paid is allowed in here — see `product/README.md`.

1. Repo **Settings** → **Pages**.
2. Under **Source**, pick **Deploy from a branch**.
3. Pick the repo's default branch, folder `/ (root)`. Save.
4. A minute later it is live at `https://sabertooth1st.github.io/Sebas-insta/`.

That URL is what goes in the Instagram bio, and every push to that branch
updates it within a minute.

If the repository is ever made private, GitHub Pages stops serving it unless you
are on a paid plan. Cloudflare Pages is the free way round that: dash.cloudflare.com
→ **Workers & Pages** → **Create** → **Pages** → **Connect to Git**, framework
preset **None**, empty build command, output directory `/`. The URL looks like
`https://sebas-insta.pages.dev`.

A custom domain is a nicer link and costs about $10 a year — worth doing, but not
before there is something to sell.

> The page's link-preview tags (`og:url`, `og:image`) hardcode the
> `sabertooth1st.github.io` address. If you host somewhere else, update those two
> lines in `index.html` or shared links will preview the wrong thing.

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
