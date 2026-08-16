# CRISPY. — Premium Burger Ordering App
Live URL:
https://crispy-onebite-infinitecraving.netlify.app/

A cinematic, fully functional food-ordering web app for the fictional chicken-burger brand **CRISPY.**

Built with **React 19**, **Tailwind CSS v4** and **Framer Motion** — no backend, everything runs client-side.

## Run it

```bash
npm install
npm run dev      # local dev server
npm run build    # production build
```

## The experience

### Opening — the burger assembly intro (home only, first visit)
A ~4s cinematic sequence: near-black screen → "CRAFTING THE CRAVE" → bottom bun rises from below →
crispy chicken drops hard (squash/stretch + crumb burst + screen vibration) → sauce glides in,
spreads and drips → cheese drops soft with a stretch and shine → three lettuce pieces land light →
top bun descends gently with a tiny bounce → completion pulse, particle burst, shadow expansion,
light sweep → camera pushes in as the assembled burger crossfades into the real hero burger →
headline reveals blur-to-sharp ("ONE BITE. INFINITE CRAVINGS.") → the burger settles into its
normal floating animation.

- Physics are per-ingredient: chicken heavy, cheese soft, sauce fluid, bun solid.
- Skippable (Skip button / Escape / auto), **plays only once** — `localStorage` key
  `crispy_intro_seen_v1` skips it on later visits (and `prefers-reduced-motion` skips it always).
- To watch it again: clear that localStorage key (or open an incognito tab).

### Home (`#/`) — a premium food advertisement
- **3D hero burger** — a true turntable built from the seven real burger-layer images at
  different depths (`preserve-3d` + `translateZ`), **continuously rotating on the Y axis**,
  tilting toward your mouse in real time, floating gently with steam + floating crumbs +
  synced ground shadow. Front/back layer copies keep the burger un-mirrored while spinning.
  A "360° BURGER" hint sits below the stack — text never touches the burger (3-zone layout:
  headline left, burger center, flavor info right; stacked on mobile).
- **3D motion throughout the home page** — words tilt in 3D (Brand Statement), the Signature
  burger and the Cravings Collection cards respond to the cursor with springy 3D tilt, the
  MADE TO BE CRAVED parallax rotates typography and burger in 3D on scroll, and the FinalCTA
  burger sways in perspective.
- **Cinematic hero** — 3-zone layout: `CRISPY CHICKEN EXPERIENCE` label, giant headline
  (`ONE BITE. INFINITE CRAVINGS.`) and CTAs on the left, the floating AI-generated burger
  center (gentle float, subtle rotation, scale breathing, soft shadow, red glow, floating
  crumbs, faint steam — text NEVER touches the burger), small supporting content on the right.
  Stacks heading → burger → description → CTA on mobile. `SCROLL TO TASTE ↓` indicator.
- **Brand statement** — CRISPY. JUICY. BOLD. revealing word by word on scroll.
- **Signature burger** — large showcase with image parallax, stars, feature list, price,
  ADD TO CART (real cart) and a customize shortcut (opens the product modal).
- **Why CRISPY** — editorial split rows for THE CRUNCH / THE SAUCE / THE BUN with big imagery
  and ghost numerals — not generic cards.
- **THE CRAVINGS COLLECTION** — the 4 best-sellers with the full product-card experience.
- **Cinematic parallax** — full-screen MADE TO BE CRAVED. with a burger partially outside the
  viewport; typography, image and background light all move with scroll.
- **Final CTA** — READY FOR THE FIRST BITE? with the burger peeking up from the bottom edge.

### Flavor (`#/flavor`) — the story of the taste
- **Flavor hero** — FLAVOR IN EVERY LAYER. with a slowly floating burger.
- **The Layers** — a scroll-driven exploded burger (top bun → sauce → lettuce → cheese →
  crispy chicken → sauce → bottom bun); layers separate vertically as you scroll, labels
  appear on alternating sides, never over the burger. Static exploded diagram on mobile.
- **Taste Journey** — 01 THE CRUNCH → 04 THE FINISH, blur-to-sharp scroll reveals on a timeline.
- **Flavor Meter** — segmented editorial meters (CRUNCH 10, SPICE 7, CREAMINESS 8,
  JUICINESS 10) that fill when they enter the viewport.
- **The Signature Kick** — sauce visual with a slowly morphing molten blob.
- **Final statement** — CRISPY. JUICY. MELTY. BOLD. IRRESISTIBLE. appearing one by one,
  then *Taste is the memory you keep.* + EXPLORE MENU.

### E-commerce (unchanged)
Menu with search/filters/sort/favorites → product customization modal with live pricing →
cart drawer + cart page (localStorage-persisted) → checkout (demo payments, validation) →
animated order confirmation. Free delivery over Rs 1,500, 5% tax, toasts, cart badge.

## Architecture

```
src/
  data/products.js        product catalog + option groups
  lib/cart.js             line building, pricing, selection defaults
  lib/router.jsx          hash router with page transitions + anchor scrolling
  lib/storage.js          sandbox-safe localStorage/sessionStorage helpers
  context/StoreContext.jsx
                          cart · favorites · toasts · drawer/modal state · menu state · orders
  components/             Hero, BurgerIntro (assembly sequence), BrandStatement,
                          SignatureShowcase, WhyCrispy, CravingsCollection,
                          CinematicParallax, FinalCTA, FlavorPage (+ its sections), Navbar,
                          MenuPage, ProductCard, ProductModal, CartDrawer, CartPage,
                          CheckoutPage, ConfirmationPage, Toasts, …
  assets/layers/          AI-generated burger layer sprites (top-bun, bottom-bun, lettuce,
                          cheese, chicken-fillet, sauce-ribbon, sauce-drizzle) + sauce visuals
```

- **State:** React Context for cart, favorites, search, filters, checkout, order state
- **Persistence:** `localStorage` for cart, favorites and the last order (sandbox-safe —
  the app still works in-memory where storage is blocked)
- **No real payments** — the card form is a validated demo only
- `prefers-reduced-motion` respected, film grain, embers, steam, parallax, page transitions
- Fully responsive with touch-sized controls; the hero burger always has breathing room

All branding, copy and imagery are fictional and AI-generated — no affiliation with any real
restaurant chain.
