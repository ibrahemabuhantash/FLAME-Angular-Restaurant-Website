# FLAME — Fire Grilled Burgers

A fictional restaurant ordering portfolio project based on [FLAME Figma](https://www.figma.com/design/cx6ZtRuvwwKBDuwvw6VCj2). Angular 20.3, TypeScript, standalone components, Angular Router, Reactive Forms, signals, CSS custom properties and local storage.

## Run (Windows / VS Code)

Install Node.js 22.12+ within the 22.x series. Open the folder containing package.json in VS Code, then run:

```sh
npm install
npm start
```

Open http://localhost:4200. Use `npm start -- --port 8080` if you prefer port 8080.

```sh
npm test
npm run build
```

Production output: `dist/flame-restaurant/browser`. Vercel and Netlify configuration files are included for SPA navigation. On Vercel use Angular preset, Node 22.x, `npm run build`, and the output folder above.

## Pages
- `/` homepage and featured items
- `/menu` category filtering and quick add
- `/menu/:id` item details, quantity and recipe
- `/cart` multiple products, update, remove, empty state, price summary
- `/checkout` customer form, pickup/delivery selection and conditional address, fee and totals, demo cash payment only
- `/confirmation` in-memory demonstration receipt (refreshing it does not recreate an order)
- `/about`, `/contact` (demo contact validation), and not-found page

## Business rules and security
- Prices match the three Figma menu items: 5.50, 4.75 and 2.25 JD. Calculations use integer fils. The illustrative delivery fee is 1.50 JD, pickup is free. The design does not specify a delivery fee, so this was added as a demo assumption. No extra taxes are modeled; this is not a production menu.
- Separate recipe options stay as separate cart lines; identical options merge. Quantities are limited to 99 per line. Local Storage stores only item IDs, recipe and quantities, with validation on read. Checkout/customer data is not saved or transmitted. Valid checkout clears the cart and creates a local, in-memory demo receipt. Phone validation assumes Jordanian mobile prefixes 077/078/079.
- Food assets use the original SVG source authored in the previous Figma construction step because temporary Figma asset URLs were inaccessible. Exact exported geometry at every breakpoint has not been verified. Responsive implementation adapts some spacing and control heights for usability.

## Verification status
- Ten dependency-free Node tests passed (cart math, variants, limits, storage data parsing, categories and fees).
- TypeScript source syntax was checked, but the full Angular build, Angular template type checking and browser interactions have not been verified: the environment could not resolve registry.npmjs.org. Run `npm install`, `npm run build` and exercise the following flows on your device before publishing.

## Manual QA checklist
- Open pages at 390, 768 and 1440px. Check overflow, layout and keyboard navigation.
- Filter Burgers, Chicken and Sides; open each item's details and quick-add to the cart.
- Add different items, change quantities, remove lines, refresh and verify restoration.
- With empty cart, confirm checkout is blocked. With items, validate required name and phone, then switch to delivery and check address validation and 1.50 JD fee. Return to pickup and verify fee zero.
- Submit valid demo order, verify receipt and cleared bag. Try the contact form with invalid and valid values. Refresh deep links after deployment.
- Ensure the site is labeled as a fictional concept. No backend, payment processor, restaurant or real order exists.
