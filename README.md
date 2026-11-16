# Kori's Place

A website for a UK hair business where clients can browse hairstyles, pick a date and time, and book an appointment online.

**Status:** front end complete, with booking requests sent over WhatsApp. Online payment and the booking database are planned and not built yet (see [Roadmap](#roadmap)).

## Features

- **Home:** introduction, "how it works" steps, and featured styles
- **Services:** hairstyle catalogue with photos, prices, durations and category filters
- **Book:** choose a style, date and time, then enter contact details. It checks opening days, the booking window and taken slots, and sends the request to the stylist on WhatsApp
- **Contact:** WhatsApp, email, Instagram, location and opening hours, plus a message form that opens WhatsApp with the message ready to send
- Responsive layout with a mobile menu, built for phones first
- Plain HTML, CSS and JavaScript. No build step and no dependencies

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home page |
| `services.html` | Hairstyle catalogue |
| `book.html` | Booking form |
| `contact.html` | Contact details and message form |
| `images/` | Style photos (create this folder next to the pages) |

## Run it locally

Open `index.html` in a browser. Keep all the pages in the same folder.

## Set it up for the business

Each page has a settings block at the top of its `<script>`. Fill these in before going live:

1. **WhatsApp number** in `book.html` (`BOOKING.whatsapp`), `contact.html` (`CONTACT.whatsapp`) and `index.html` (`SOCIAL.whatsapp`). Use digits only, with the country code and no `+` or leading 0. UK example: `07123 456789` becomes `447123456789`.
2. **Contact details** in `contact.html` (`CONTACT`): email, Instagram username, location, opening hours.
3. **Hairstyles** in `services.html` (`STYLES`): name, category, price in pounds, duration and description. The same style ids and names are in `book.html` and `index.html` (`STYLES` and `FEATURED`), so keep them matching.
4. **Opening times** in `book.html` (`BOOKING.weeklySlots`): start times for each weekday, where 0 is Sunday. An empty list means closed. Also set `leadDays` and `horizonDays` for how far ahead people can book.

### Adding style photos

1. Create an `images` folder next to the HTML files.
2. Save each photo named after its style id, for example `images/knotless-braids.jpg`.
3. `.jpg`, `.jpeg`, `.png` and `.webp` all work. A style with no photo shows "Photo coming soon".

To use a different file name, set `image: "images/my-photo.png"` on that style. Portrait photos (taller than wide) work best, because the photo box shows the top of each picture.

## Roadmap

- [ ] Custom backend (Node.js, Express and PostgreSQL) to store bookings, so taken slots update automatically and double bookings are prevented
- [ ] Online payment with Stripe, with the price calculated on the server and a booking marked paid only after Stripe confirms the payment
- [ ] Booking confirmation page and a notification to the stylist for each new booking
- [ ] Simple password-protected page for the stylist to see upcoming bookings
- [ ] Custom domain and hosting

## Security note

Never commit payment keys. Stripe secret keys and database credentials belong in the server's environment variables, never in these pages. Only publishable keys can appear in front-end code.

## Tech

HTML, CSS and vanilla JavaScript. Planned: a Node.js and Express backend with PostgreSQL, and Stripe for payments.
