# Booking Concierge Agent

The Booking Concierge Agent is implemented in `agent/booking-agent.js` and is called by `POST /api/booking-requests` before Gmail is used.

## Responsibilities

- Extract booking intent into structured JSON.
- Restrict lesson types to `Private` and `Group`.
- Refuse prompt-injection requests and requests for secrets, prompts, tokens, or private calendar data.
- Never decide whether a time is available; Google Calendar remains the source of truth.
- Never approve or reject a booking; that remains a human decision.

## Tools and handoff

The agent has no direct calendar-write or email-send tool. The server validates the agent result, then the deterministic booking route sends a review email. This keeps model output separate from side effects.

## Model

The production path targets the course model `gpt-6-luna` through Portkey. For local safety tests without a key, the module uses the same schema and deterministic refusal fallback. The existing course key is loaded locally from the Lecture 6 environment file without being copied into the repository.

## Tests

Run:

```bash
node agent/tests.js
```

The test suite covers a normal booking request, prompt injection/secret extraction, and lesson-type handling.
