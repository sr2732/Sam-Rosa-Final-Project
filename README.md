# Move with Sam Rosa

Move with Sam Rosa is a Pilates website with a Google Calendar availability browser, a Booking Concierge Agent, Gmail booking-review notifications, approval/rejection workflow, and testimonial submission. It demonstrates how an independent instructor can build an integrated booking and testimonial portal without a separate booking-platform subscription.

Live app: https://sam-rosa-final-project.onrender.com

Project artifacts:

- `report.html` — final project report
- `slides.html` — Reveal.js presentation
- `agent/` — Booking Concierge Agent and safety tests

## Run locally

1. Install Node.js 18+.
2. Clone this repository and enter its directory.
3. Copy `.env.example` to `.env`.
4. Add your own Google OAuth values and Portkey key to `.env`; never commit that file.
5. Run `npm install`.
6. Run `npm run build`.
7. Run `npm start`.
8. Open `http://localhost:3001`.
9. For local Google Calendar/Gmail access, open `http://localhost:3001/auth/google` once and complete authorization.

## Required environment

See `.env.example`. Required values are `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REDIRECT_URI`, `GOOGLE_CALENDAR_ID`, `PILATES_EMAIL`, and `PORTKEY_API_KEY`.

The calendar account must authorize Calendar read access and Gmail send access. The client-facing app reads Google free/busy data; it does not invent availability. For the public deployment, set `GOOGLE_REDIRECT_URI` to `https://sam-rosa-final-project.onrender.com/auth/google/callback` in the host environment and register that exact URI with Google.

## Agent

`agent/booking-agent.js` is the Booking Concierge Agent. It targets course model `gpt-6-luna` through Portkey, returns structured booking intent, validates `Private`/`Group`, and refuses prompt-injection or secret-extraction requests. It never writes to the calendar or sends email directly. `node agent/tests.js` runs the safety tests.

## Important production notes

Approval links use the deployed HTTPS URL in production. The demonstration uses JSON persistence; a production version should use managed storage. Do not commit `.env`, OAuth tokens, booking data, testimonial data, or API keys.
