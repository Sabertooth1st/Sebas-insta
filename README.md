# sebastianuzice

The landing page behind the Instagram bio link, and the plan for what gets posted.

## What is here

- `index.html` — the page people land on when they tap the bio link. It holds the
  links and, once there is one, the thing being sold.
- `content/14-day-plan.md` — what to post, in what order, and when the product goes live.

## Putting the page online

GitHub Pages hosts it free and gives a real URL for the bio:

1. Repo **Settings** → **Pages**.
2. Under **Source**, pick **Deploy from a branch**.
3. Branch `main`, folder `/ (root)`. Save.

A minute later it is live at `https://sabertooth1st.github.io/Sebas-insta/`, and that
is what goes in the Instagram bio. Every push updates it.

A custom domain is a nicer link and costs about $10 a year. Worth doing, but not
before there is something to sell.

## Editing the page

Everything meant to be changed sits near the top of `index.html` or is marked with a
comment. In order of what matters:

1. The name, handle and bio line.
2. The paid slot — the bordered card. Its `href` points at the checkout. Delete the
   whole block until there is a product, because an empty card that goes nowhere
   costs more trust than it earns.
3. The links below it.

Add a square photo to the repo as `avatar.jpg` and it appears automatically. Without
one, the page hides the slot rather than showing a broken image.

## Taking payment

Gumroad is the fastest way to start: free to open, hosts the file and the checkout,
and takes a cut per sale. Stripe is cheaper per sale but you have to build the
checkout, so it is worth moving to later, not now.

Whichever it is, the account has to be created by hand. Once the product link
exists, it goes in the paid slot.
