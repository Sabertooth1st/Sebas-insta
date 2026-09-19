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
- `.nojekyll` — empty on purpose. It tells GitHub Pages to serve these files as
  they are instead of running Jekyll over them first. Leave it there.

The page is built around one thing: the before and after, then the plan that
produced it. Everything else on the page is secondary to those two.

### Page photos vs. post photos

Two sets, and they are not interchangeable:

| | For | Why |
| --- | --- | --- |
| `before.jpg`, `after.jpg` | The web page | Plain 2:3 crops, no text. The page lays them out side by side and captions them in HTML, so they stay sharp and readable at any width. |
| `assets/before-after.jpg` | An Instagram feed post — **and the page's link preview** | 1080×675, captioned **177 KG / TODAY**. The text is baked in because a feed post has to carry its own meaning. `index.html` points `og:image` at this file, so renaming it silently breaks the preview on every shared link. |
| `assets/before-after-story.jpg` | An Instagram story | 1080×1920, the same pair at story size. |
| `assets/progress-three-stage.jpg` | A feed post — check the crop first | 1620×675, three stages — 177 kg, along the way, today. The middle frame is the one that makes it look survivable rather than magic. At 2.4:1 it is wider than Instagram's 1.91:1 feed limit, so post it as a carousel or a story, or re-crop, or it gets cut. |

Do not put the captioned versions on the page body: the page already captions
them in HTML, and you would get the label twice. The one exception is
`og:image`, which has to be a wide captioned composite — a 2:3 portrait gets
cropped to unreadable by the preview cards in WhatsApp and iMessage.

## What is still outstanding

| Where | What it needs |
| --- | --- |
| The guide | The Gumroad link, replacing the card's `href="#signup"` |
| Presets | Parked in a comment until the guide has launched, then its Gumroad link |
| TikTok / YouTube | Parked in a comment below the email link. Uncomment a block once its URL exists |
| Mailing list | A form endpoint — see below |
| GitHub Pages | Not switched on yet — see *Putting the page online* |

Nothing on the page points anywhere dead, so it is safe to publish as it
stands. Search `index.html` for `EDIT ME` and `EDIT THESE FIRST` to find the
copy worth revisiting.

## Arming a thing for sale

Both cards work the same way. Each carries `data-pending`, and while that
attribute is there the card hides its price and its button, shows a line
pointing at the mailing list instead, and refuses to be tapped.

To put something on sale, make two edits to that card:

1. Replace `href="#signup"` with the real checkout URL.
2. Delete `data-pending`.

The card refuses to go live until step 1 is a real `http(s)` link, whatever you
do to `data-pending` — the script checks the `href` itself. So a half-finished
edit shows the not-on-sale card rather than a **Get it** button that 404s.

The price and the **Get it** button appear on their own. That is the whole
change — there is nothing else to switch on.

**When the launch week ends**, change the card's price in `index.html` to the
full price and update `product/README.md` to match. Nothing does this for you,
and until you do the card undercharges against Gumroad.

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

**Read this part before you pick, because the two options are not
interchangeable and the difference bites on launch day.**

- **Formspree** — the drop-in. Sign up, make a form, copy the endpoint that
  looks like `https://formspree.io/f/abcdwxyz`. Addresses arrive by email and
  export to CSV. **It cannot send email to the list.** It collects addresses;
  it is not a mailing tool. If you use it, launch day means exporting a CSV and
  importing it somewhere else under time pressure.
- **Buttondown** or **MailerLite** — twenty minutes more setup, and you can
  actually mail the list, which is the entire point of collecting it. **These
  will not work by swapping the `action` alone.** The page's script posts JSON,
  which is Formspree's shape; Buttondown expects form-encoded data and
  MailerLite needs an API key, so both fail silently and the visitor just sees
  "That didn't send." Use their own embed snippet in place of the whole
  `<form class="signup">` block instead.

`content/14-day-plan.md` has you emailing the list on day 10, so pick one that
can send.

For Formspree, in `index.html` find:

```html
<form class="signup" id="signup" action="" method="POST">
```

and put the endpoint inside the empty `action=""`. The script notices on its own
and starts posting to it. A hidden honeypot field already filters most bots.

Whichever you pick, **send yourself one real address and confirm it arrives**
before day 1. If the endpoint is wrong the page says nothing is switched on and
carries on looking fine, so a silent failure here costs you the whole fortnight.

## Editing the page

In order of what matters:

1. **The before and after.** Replace `before.jpg` and `after.jpg` to change it.
   They are shown at 2:3 and cropped to fill, so tall photos work best. Pick
   two shots of the same kind — both full body, both mirror selfies — because
   it is the likeness that makes the difference read. Do not pair a dark
   outdoor shot with a bright indoor one; that invites the reader to credit
   the lighting instead of the work. If either file is missing the whole block
   hides itself rather than showing a broken image.
2. **The bio line and the plan card.** The two pieces of copy that decide
   whether anyone scrolls.
3. **"What it took".** The list of rules, in his own words. It is what makes
   the card above believable, which is why it sits directly under it.
4. **The links.** There is a parked TikTok/YouTube block inside a comment at
   the end of the `Elsewhere` list — copy one of those whole
   `<a class="link">…</a>` blocks for a new link. Change the `href`, the
   `data-track` name, the icon and the two lines of text. Delete
   `data-placeholder` to make it live; leave the attribute on and it shows a
   dashed **set me** pill and cannot be tapped.

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
