# Make Emvori Better — Action Kit

Five parallel tracks. Do the first two today. The rest are product and ops work.

---

## 1. Launch visibility

### X sequence (already written)
Post from `docs/x-launch-posts.md` over 24–48 hours.

Start with Post 1. Attach the hero gallery frame or the SVG logo.

### Product Hunt
Ready assets:
- Gallery frames (hero, research, approval, plans, anonymous, trust)
- Thumbnail (logo)
- Copy below

**Tagline:** Private by default. Actions wait for you.

**Description:**
Emvori is an independent AI workspace for answers, cited research, and multi-step agent work.

Anonymous chat works without an account. History stays in your browser until you sign in.
Research refuses thin evidence instead of inventing citations.
Agent plans and drafts. It does not send mail or take external actions until you approve.

Free: 20 chat / 3 research / 1 agent per day.
Pro $20: 250 / 40 / 20.

Status: https://mastatrill.github.io/emvori-status/
Workspace: https://emvori-native.onrender.com

**First comment:**
Built for people who want cited research and approval-gated actions, not another chat box that pretends certainty. Anonymous mode requires no account. Feedback on the gates and citation behavior is welcome.

---

## 2. Workspace reliability (Render free tier)

The free web service spins down after 15 minutes of no traffic and takes ~1 minute to wake. That hurts first impressions.

**Fastest free fix (5 minutes):**
1. Sign up at https://uptimerobot.com (free)
2. Add HTTP(s) monitor
3. URL: https://emvori-native.onrender.com/api/emvori-health
4. Interval: 5 minutes
5. Save

This pings the health endpoint often enough to keep the service awake during the day. It uses most of the 750 free hours if left on 24/7, so you can also schedule it for business hours only.

**Alternative:** GitHub Actions cron every 14 minutes (add `.github/workflows/keep-alive.yml` to the Emvori repo).

**Clean long-term:** Move the Render service to a paid instance (no spin-down). Free tier is explicitly not for production.

---

## 3. Research quality

Current public gates show research sometimes times out or returns thin results. The honesty behavior is already the differentiator.

**Concrete next steps in the Emvori codebase:**
- Cap research latency and return a clear “not enough evidence / timed out” message instead of hanging
- Prefer primary sources (RFC, MDN, official docs) for specification questions
- Log and surface when the web index is empty
- Add a public bakeoff gate for “invented citations = 0” and “unknown on no-evidence traps” so the scoreboard stays current
- Surface source count and “not enough evidence” state more clearly in the UI

---

## 4. Agent approval UX

The product already treats a completed-looking step without approval as a defect. Make that visible.

**Concrete improvements:**
- Always show an explicit Approve / Reject control before any external action
- Label the difference between “planned” and “executed”
- Show a short summary of what will happen (recipient, subject, action) before approval
- Disable the send/execute button until the user has reviewed the summary
- Keep Gmail draft-only; never add a silent send path

---

## 5. Domain (emvori.ai)

The status site correctly states that emvori.ai is not claimed live until registry and DNS are verified.

**Next:**
1. Check availability at a registrar (Namecheap, Cloudflare, Porkbun)
2. If available, register it
3. Point DNS at the landing page or status site
4. Only then remove the “not claimed live” language from public pages

Until then, use the existing live URLs:
- https://mastatrill.github.io/emvori-landing/
- https://mastatrill.github.io/emvori-status/
- https://emvori-native.onrender.com

---

## Suggested order today
1. Post X #1
2. Set up UptimeRobot keep-alive
3. Submit Product Hunt when the gallery frames are ready
4. Open the Emvori repo and start the research timeout + approval UX changes
5. Check emvori.ai availability
