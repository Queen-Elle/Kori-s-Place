# Kori's Place

A website for a UK hair business where clients can browse hairstyles, pick a date and time, and book an appointment online.

**Status:** front end complete. Bookings go to the stylist on WhatsApp until the booking server is connected (`apiUrl` in `book.html`). The server, with the database and Stripe deposits, is in a separate repository, `koris-place-api`.

## Features

- **Home:** introduction, "how it works" steps, and featured styles
- **Services:** hairstyle catalogue with photos, prices, durations and category filters
- **Book:** choose a style, date and time, then enter contact details. It checks opening days, the booking window and taken slots, and sends the request to the stylist on WhatsApp
- **Work with us:** enquiry page for weddings, events and group bookings, sent to the stylist on WhatsApp
- **Contact:** WhatsApp, email, Instagram, location and opening hours, plus a message form that opens WhatsApp with the message ready to send
- Responsive layout with a mobile menu, built for phones first
- Plain HTML, CSS and JavaScript. No build step and no dependencies

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home page |
| `services.html` | Hairstyle catalogue |
| `book.html` | Booking form |
| `work.html` | Weddings, events and group enquiries |
| `booking-confirmed.html` | Page shown after a deposit is paid (needs the server) |
| `admin.html` | Kori's private bookings page, opened with her password (needs the server, not linked from the site) |
| `contact.html` | Contact details and message form |
| `images/` | Logo files and style photos (create this folder next to the pages) |

## Run it locally

Open `index.html` in a browser. Keep all the pages in the same folder.

## Set it up for the business

Each page has a settings block at the top of its `<script>`. Fill these in before going live:

1. **WhatsApp number** in `book.html` (`BOOKING.whatsapp`), `contact.html` (`CONTACT.whatsapp`) and `work.html` (`WORK.whatsapp`). Use digits only, with the country code and no `+` or leading 0. UK example: `07123 456789` becomes `447123456789`.
2. **Contact details** in `contact.html` (`CONTACT`): email, Instagram and TikTok usernames, location, opening hours. The footer's "Get to know us" and "Contact us" links lead to the contact page, and "Work with us" leads to `work.html`.
3. **Hairstyles and prices** in `services.html` (`STYLES`, `ADDONS`): name, category, description and prices. A price can be a number, a range `[low, high]`, `{ from: n }` or `null` (shows "Price on request"). `options` lists sizes or variants with their own ranges. The same style ids, options and add-ons are in `book.html` (`STYLES`, `ADDONS`), and `index.html` has `FEATURED`, so keep them matching.
4. **Booking server address:** `apiUrl` in `book.html`, and `API_URL` in `booking-confirmed.html` and `admin.html`. Leave them empty to keep using WhatsApp.
5. **Opening times** in `book.html` (`BOOKING.weeklySlots`): start times for each weekday, where 0 is Sunday. An empty list means closed. Also set `leadDays` and `horizonDays` for how far ahead people can book.

### Logo

The logo files are in `images/`: `logo.png` (full logo, white background), `logo-soft.png` (same, softened to match the site's off-white, used on the home page), `logo-mark.png` (the head only, used in the header and footer), and the browser tab icons `favicon.png`, `favicon-48.png` and `apple-touch-icon.png`. To change the logo, replace these files and keep the same names. The logo has a white background and dark lettering, so it is shown on a light background instead of directly on the black.

### Adding style photos

1. Create an `images` folder next to the HTML files.
2. Save each photo named after its style id, for example `images/knotless-braids.jpg`.
3. `.jpg`, `.jpeg`, `.png` and `.webp` all work. A style with no photo shows "Photo coming soon".

To use a different file name, set `image: "images/my-photo.png"` on that style. Portrait photos (taller than wide) work best, because the photo box shows the top of each picture.

## Roadmap

- [x] Custom backend (Node.js, Express and PostgreSQL) to store bookings, so taken slots update automatically and double bookings are prevented (built, see `koris-place-api`; to be deployed)
- [x] Online deposit with Stripe, with the price calculated on the server and a booking marked paid only after Stripe confirms the payment (built, to be tested with real keys)
- [x] Booking confirmation page
- [x] Simple password-protected page for the stylist to see her bookings (`admin.html`)
- [ ] A notification to the stylist for each new booking
- [ ] Custom domain and hosting

## Security note

Never commit payment keys. Stripe secret keys and database credentials belong in the server's environment variables, never in these pages. Only publishable keys can appear in front-end code.

## Tech

HTML, CSS and vanilla JavaScript. Planned: a Node.js and Express backend with PostgreSQL, and Stripe for payments.
