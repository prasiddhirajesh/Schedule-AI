Your 24/7 Agentic AI Receptionist
Quick Overview (What it does):
Appointment Ace captures calls/texts, understands intent, checks live availability, and books directly—then confirms and follows up. It’s built as an agentic, tool-using AI with a polished frontend for owners and a lightweight embeddable widget for customers.

Core Value (Why it matters):
Small service businesses lose money to missed calls and “phone tag.” Appointment Ace eliminates that friction with autonomous scheduling and an owner-facing dashboard that shows exactly what the AI is doing—in real time.

Frontend First: UX & Product Surface
-Primary surfaces
-Customer Widget (Web & Mobile-responsive):
  Embeddable on any website; supports voice (WebRTC/Twilio Client) & chat (text).
-Inline availability picker, service selector, and contact capture.
-Live “typing/speaking” feedback; graceful fallbacks for low bandwidth.
-Owner Dashboard (Ops Console):
Today view (timeline of bookings, no-shows, reschedules).
Calendar view (day/week/month) with drag-drop edits that propagate to Google Calendar.
Conversation viewer (transcripts/audio snippets) with PII masking toggles.
Rules & Policies editor (business hours, buffers, services, durations, prices).
Analytics (lead capture rate, conversion, peak times, top services).

Frontend tech highlights (bulleted)
Framework & UI
Next.js (React 18) for SSR/ISR and app-router; Vercel deploy.
Tailwind CSS + shadcn/ui for accessible, consistent components.
Framer Motion for micro-interactions; Radix UI primitives for a11y.
State & Data


React Query (TanStack) for server cache + optimistic updates.


Zustand for local UI state (modals, toasts, ephemeral form state).


Forms & Validation


react-hook-form + Zod schemas (client & server parity).


Realtime


WebSockets/Server-Sent Events for live booking status & agent actions.


Twilio Client (WebRTC) for in-browser calling; fall back to PSTN.


Auth & Security


Clerk/Auth0 for session management; RBAC (Owner, Staff).


CSP, Helmet, httpOnly cookies, and token-scoped tool access.


Observability


Sentry (errors), PostHog (product analytics), OpenTelemetry tracing.


Why this frontend matters
Converts more leads with zero-friction voice/chat entry.


Gives owners trust & control (see what the AI did, amend instantly).


Keeps ops smooth with real-time state and offline-safe flows.



System Architecture (High level)
Flow
User (call/SMS/web chat) → Twilio ingress


Voice Assistant → text intent


LangGraph agent (state machine) plans → tools


Tools: Google Calendar (check/create), business rules


LLM (GPT-4) crafts confirmations & clarifications


ElevenLabs TTS (if voice) → Twilio response


Events streamed to Frontend (WebSockets/SSE) → UI updates


Owner Dashboard reads from a Graph/API layer that exposes conversations, events, rules, and analytics—all reflected live.

Tech Stack (Bulleted with brief notes)
Frontend
Next.js (React 18) — SSR/ISR for speed and SEO; app router for modularity.


Tailwind CSS + shadcn/ui + Radix — fast, accessible, consistent UI.


React Query + Zustand — robust data + lightweight local state.


react-hook-form + Zod — type-safe forms; identical validation client/server.


WebSockets/SSE/Live Voice control platforms  — live agent state, booking confirmations, analytics ticks.


Twilio Client (WebRTC) — browser calling; audio device management.


Sentry + PostHog — quality + product insight.


Backend & AI Orchestration
FastAPI — Python API surface; lightweight, async-ready.


LangChain + LangGraph — agent state machine (gather → check → confirm → book).


OpenAI GPT-4 / Gemini 2.5 / LLMs — NLU/NLG and tool-aware reasoning.


OpenAI Whisper — speech-to-text (accurate, robust accents/noise).


ElevenLabs — natural TTS for voice responses.


Google Calendar API — availability, booking, rescheduling.


Infra & DevEx
Railway.app (API) + Vercel (frontend) — fast deploys.


PostgreSQL (RDS/Neon) — bookings, rules, transcripts metadata.


Redis — short-lived sessions, rate limiting, idempotency locks.


OpenTelemetry — end-to-end traces across agent steps.


GitHub Actions — CI/CD, type checks, tests, deploy gates.



Frontend Architecture (How pieces fit)
App layout: /dashboard (owner), /widget (embeddable), /auth, /settings.


Data model hooks: useBookings(), useConversations(), useAvailability(), useRules().


Realtime channel: useLiveAgentStream() hydrates toasts, banners (“Booked: 2:30 PM – Water Heater Repair”), and updates calendar instantly.


Error model: typed API errors → UI toasts + form field hints; retries with exponential backoff via React Query.


A11y: focus traps, ARIA roles, keyboard shortcuts; high-contrast theme toggle.


Performance: route-level code split, image/asset optimization, Speculative Prefetch on common owner flows.



Agentic Behavior (What users see in UI)
Intent detected → “Looking for Thursday afternoon…”


Tool use emitted → “Checking calendar…”


Options rendered → selectable chips (2:00, 2:30, 3:00).


Confirmation → ticket with iCal link + SMS.


Owner Dashboard updates live: booking card appears; click-through to convo.



Security & Privacy (Customer-trust basics)
Data minimization in widget; PII masking in transcripts by default.


Scoped tokens for each tool (Calendar per-location/per-staff).


Audit log in dashboard (who/what/when for bookings & edits).



Roadmap (Frontend-heavy milestones)
Self-serve theme/brand kit: logo, colors, voice persona, greeting scripts.


Inline payments & deposits: Stripe Elements in the booking flow.


CRM syncs: HubSpot timeline embed; owner sees touchpoints inline.


Owner-side “AI coach” panel: suggested rules (buffers, durations) from analytics.


Multi-location & staff routing: skills + availability matching in UI.



Demo Story (How to pitch it live)
Open website with floating widget → start a voice chat.


Ask for “tomorrow after 2 PM; faucet repair, 45 minutes.”


Show live chips for times; choose one → instant confirm.


Flip to Owner Dashboard: booking appears; drag to 3:00 PM → SMS reschedule fires.


Open Conversation viewer: transcript + audio; show Rules editor tweak (add 15-min buffer) → refresh calendar options.# Schedule-AI
