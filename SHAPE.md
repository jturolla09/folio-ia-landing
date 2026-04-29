# Shape Brief: folio-ia-landing rebuild (CONFIRMED 2026-04-29)

## 1. Feature Summary
Waitlist landing for Folio AI — personal health-exam archive. Converts health-conscious 30–50yo Brazilians into early-access signups while killing the "generic blue SaaS" reflex of the current page.

## 2. Primary User Action
Sign up for the waitlist with email. Everything else exists to make that decision feel obvious for the right person and uninteresting for the wrong one.

## 3. Design Direction
**Color strategy:** Drenched. One owned cobalt-indigo carries 60–70% of vertical surface. Working anchor `oklch(0.32 0.18 264)`. Pale cream type on cobalt. ONE complementary warm-cream accent for CTA hover and one type moment. NOT generic SaaS blue.

**Theme scene:** A 41-year-old marketing manager in Rio, on her phone in her kitchen on a weekday morning, holding a coffee, about to forward another lab PDF to herself, pausing to read this page instead. Warm-natural light, mood "finally, someone made this." Cobalt anchors it as serious, owned.

**Anchor references:** Linear marketing (committed color, type-precision, screenshots-as-hero) + Arc browser launch pages (product imagery as the page, restrained chrome). NOT Stripe (too neutral). NOT Klim (too type-foundry).

**Typography:** Replace Bricolage Grotesque + Plus Jakarta Sans (both reflex-reject). Default to **General Sans** (ITF, free) — single committed sans, weights 400/500/600/700, tightened tracking on display sizes. Fallback `system-ui`.

## 4. Scope
Production-ready. Replaces `index.html` end-to-end. Real waitlist form (Formspree + Turnstile preserved). Motion respects `prefers-reduced-motion`.

## 5. Layout Strategy
Strict 12-column grid as voice. Visible as alignment, not decoration. Asymmetric placements within it.

**Three-section editorial scroll:**
1. **Hero (drenched cobalt, full viewport).** Headline columns 1–7, display weight tight tracking. Waitlist form columns 1–5. ONE iPhone columns 8–12, held still, no rotation. Trust line as quiet inline strip. Subtle 1–2% noise texture on cobalt.
2. **Story scroll (alternating bands).** Three typeset moments. Beat 1 cobalt: "Você recebe um exame por WhatsApp." Beat 2 warm off-white full-bleed metrics screenshot built in HTML. Beat 3 cobalt: "Você leva o histórico para o consultório." Each beat one viewport tall on desktop.
3. **Footer-CTA combined cobalt band.** Headline, repeated form, security/LGPD as one inline line, legal links. No separate footer.

**Cuts:** features grid, "Como funciona" cards, security cards, dark navy band, emoji-logo strip, "Demo em breve" placeholder, three-phone rotation, glassmorphism nav.

## 6. Key States
- Default; `prefers-reduced-motion` (no entrance motion)
- Form: empty, invalid email (warm-red border, no shake), Turnstile pending ("Aguarde…"), success (inline replacement: "Você está na lista. Avisamos quando o acesso for liberado."), error (specific by failure mode, not "Algo deu errado")
- Mobile: single column, alternation preserved
- Slow connection: cobalt paints first, font-display swap

## 7. Interaction Model
Page load: staggered hero reveal, 450ms ease-out-quart. No bounce. Reduced-motion skips. Scroll: no parallax; one subtle translate-up reveal per beat. Form submit: inline state transition, no modal/toast. Nav: solid cobalt, hairline rule when scrolled. CTA hover swaps to warm-cream fill / cobalt text. No translateY card lifts (no cards). Skip-to-content link.

## 8. Content Requirements
- **Brand:** "Folio AI" everywhere (kill `folio.ia`)
- **Headline:** "Seus exames, em um lugar só."
- **Subhead:** "Você sobe um PDF, a gente extrai os valores, e seu histórico fica organizado para a próxima consulta."
- **Trust line:** "Criptografado. Conforme LGPD. Gratuito durante a beta."
- **Final CTA label:** "Quero meu arquivo de saúde."
- **Removed:** "Resultado em segundos", "47 pessoas já na lista", "Demo em breve", emoji "logos" of OpenAI/Supabase/Lovable
- **Bans:** zero em dashes, zero exclamation points, zero emoji-as-iconography in body

## 9. Open-Question Defaults (confirmed by user)
- Font: General Sans
- Metrics screenshot: built in HTML (not captured image)
- "47 na lista": dropped
- Privacy/terms pages: untouched for now

## Asset Regeneration

When the app UI changes significantly, regenerate the phone mockup screenshots and the metrics panel screenshot used on the landing page.

1. From inside the `folio-ia/` directory, run:
   ```bash
   npx skillfish add payolajoker/ai-agent-setting imagegen
   ```
2. Use the installed `imagegen` skill to capture updated screenshots of the app (phone mockup views and the metrics panel).
3. Optionally replace the HTML-built mockups in `index.html` with real app captures if the fidelity is worth the tradeoff.
