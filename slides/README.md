# Breaking Agents in Dublin — talk deck

A self-contained reveal.js deck for a 15-minute talk on breaking LLM agents
(AgentBreaker) and defending them (AgentArmor). Design language matches
[muhammadmurtuza.com](https://muhammadmurtuza.com): Geist + Geist Mono, warm
near-black, a single orange accent.

## Run it

Any static server works — reveal needs `http://`, not `file://`, for the
speaker-notes and hash routing to behave.

```bash
npx serve .
# or
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

- **Present:** arrow keys / click to advance. Fragments appear on click, so you
  control when each point lands — nothing is on screen before you say it.
- **Speaker view:** press **S** — notes, timer, and next-slide preview. Every
  slide's notes carry its `[mm:ss]` budget; they sum to **15:00**.
- **Overview:** press **Esc**.
- **PDF export:** open `http://localhost:8000/?print-pdf` and print to PDF from
  the browser. `pdfSeparateFragments` is off, so each slide prints once with all
  fragments shown.

## Screenshots

These are **real** captures from Lakera's Agent Breaker (`play.lakera.ai/agent-breaker`),
pulled from live winning runs — nothing generated or mocked. Each case slide shows the
challenge on the left and the exploit landing (Score 100) on the right. To re-capture or
swap, drop a PNG into `assets/` with the matching name; it loads automatically.

Case studies run in a deliberate difficulty order (normal chat → memory → MCP tool → document),
and each slide shows the **recon story**: the earlier failed/low-scoring payload, then the
winning one. File names keep the original capture numbering.

| Slide | App (challenge slug)                     | Channel / technique                | Files |
|-------|------------------------------------------|------------------------------------|-------|
| 04    | CorpConnect Messenger (`email_tool_invocation`) | A normal chat box — forged tool output / identity spoof | `case-02-challenge.png`, `case-02-score.png` |
| 05    | MindfulChat (`chatapp_refuse`)           | Its memory — memory-log poisoning  | `case-04-challenge.png`, `case-04-score.png` |
| 06    | OmniChat Desktop (`mcp_chat_poisoning`)  | A tool it trusts (MCP) — tool-description poisoning | `case-01-challenge.png`, `case-01-score.png` |
| 07    | Clause AI (`legal_TI_exfiltration`)      | A document it reads — indirect injection | `case-03-challenge.png`, `case-03-score.png` |

`assets/defense-vault.jpg` is the vault-door photo behind the "defensive turn" slide
(free-license, Unsplash). Case images sit in window chrome at a fixed height,
`object-fit: contain`, so nothing is cropped.

## Structure

```
index.html      all 18 slides, reveal config, screenshot auto-loader
css/deck.css    design tokens + components (window chrome, statement slide, footer)
assets/         your screenshots go here
```

## The 13 slides

1. Title · 2. **Chatbot vs Agent** (the whole problem, explained plainly: one answers, one acts) ·
3. Attack surface ("if it reads it, you can poison it") · **4–7. Four case studies** with the recon
story, in difficulty order: normal chat / identity spoof (CorpConnect) → memory poisoning
(MindfulChat) → MCP tool poisoning (OmniChat) → document injection (Clause AI) · 8. The pattern
(a format beats a command) · 9. **The defensive turn** (vault-door photo: stop asking the model to
guess) · 10. AgentArmor — three locks · 11. Three takeaways · 12. **Ethics question**
(big: "If it will act for anyone, who is it really working for?") · 13. Close / CTA.

Pacing guide in the notes still sums to ~15:00, with the tighter front half leaving more room for
the case studies and Q&A.

## Editing notes

- **One accent rule:** orange is for a single word per headline (wrap it in
  `<strong>`), the `$` prompt, eyebrows, and scores. Don't put two oranges in
  competition on one slide.
- **Type scale:** 120 / 64 / 40 / 32 / 24px — never smaller. Set as CSS vars in
  `deck.css`.
- **Glow:** each `<section>` has `data-glow="tl|tr|bl|br|c"` to move the orange
  radial into a different corner so the deck doesn't feel static.
- **The content is a scaffold.** It's grounded in the real AgentBreaker playbook,
  but swap the install commands, handles, and case specifics for your actual runs
  before presenting.

## Going fully offline

The deck pulls reveal.js and fonts from pinned CDNs. For a no-wifi room, vendor
them locally:

```bash
npm i reveal.js@5.1.0
# copy node_modules/reveal.js/dist + plugin into ./vendor, repoint the <link>/<script>
# tags, and self-host the two Geist fonts (download the woff2 from Google Fonts).
```
