# Mr Mushakk — Mandal Explorer

Production application with email OTP, admin-only server-side mandal CRUD, photos, Google Maps navigation, nearby search, visit plans, favourites, visited tracker, and open-app reminders. No AI or transport schedules.

## Setup
1. `npm install`
2. Configure environment variables `BREVO_API_KEY`, `BREVO_SENDER_EMAIL`, `SESSION_SECRET` (at least 32 random characters), and `ADMIN_EMAIL` (the email allowed to manage mandals). Optional `DATA_DIR` (persistent disk directory), `PORT`, `CORS_ORIGIN`. Do **not** commit secrets.
3. `npm test && npm run build && npm start`
4. Open `http://localhost:3001` and sign in with email OTP. Only `ADMIN_EMAIL` sees the Data Manager.

## Deployment
Deploy this **Node Express app** on Render, not as a static-only Netlify site. Build: `npm install && npm run build`; Start: `npm start`. Set env vars in Render dashboard. `DATA_DIR` MUST point to a persistent disk for mandal edits and photos to survive redeploy/restart. Without a persistent disk, Render's ephemeral filesystem may lose new mandals and uploaded photos. If using a static frontend on another origin, configure reverse proxy to the API or deploy together on Render.

## Important limitations
- Visitor favourites, plans, visited state and reminders live in that browser's local storage, not synced across devices.
- Reminders are only displayed while the page is open.
- Nearby search requires HTTPS (or localhost), geolocation permission and mandal latitude/longitude.
- The seed mandals are unverified listings; verify locations and festival status before publishing.
- Google Maps opens externally; no Maps API key needed.
- Session tokens expire after 7 days; login again when expired.
