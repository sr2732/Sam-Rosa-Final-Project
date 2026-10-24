# Move with Sam Rosa

Move with Sam Rosa is a Pilates website with a Google Calendar availability browser, a Booking Concierge Agent, Gmail booking-review notifications, approval/rejection workflow, and testimonial submission.

## Run locally

1. Install Node.js 18+.
2. Create `.env` one level above this repository or in this folder. The app checks both locations.
3. Add Google OAuth values from Google Cloud and the course `PORTKEY_API_KEY`.
4. Run `npm install`.
5. Run `npm run build`.
6. Run `npm start`.
7. Open `http://localhost:3001`.

## Required environment

See `.env.example`. Required values are `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REDIRECT_URI`, `GOOGLE_CALENDAR_ID`, `PILATES_EMAIL`, and `PORTKEY_API_KEY`.

The first Google authorization is completed at `http://localhost:3001/auth/google`. The calendar account must authorize Calendar read access and Gmail send access. The client-facing app reads Google free/busy data; it does not invent availability.

## Agent

`agent/booking-agent.js` is the Booking Concierge Agent. It targets course model `gpt-6-luna` through Portkey, returns structured booking intent, validates `Private`/`Group`, and refuses prompt-injection or secret-extraction requests. It never writes to the calendar or sends email directly. `node agent/tests.js` runs the safety tests.

## Important production notes

The approval links must use the deployed HTTPS URL, not localhost. Local JSON storage is for the class demonstration; production should use a database. Before submission, run the fresh-clone dry run, capture screenshots, verify the public URL, and check that no `.env`, OAuth token, or local data file is committed.
