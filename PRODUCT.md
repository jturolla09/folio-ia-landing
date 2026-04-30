# Product

## Register

brand

## Users

Health-conscious Brazilians, roughly 30–50 years old, who do regular labs (annual checkups, ongoing cholesterol/thyroid/vitamin monitoring) and accumulate scattered PDFs across multiple labs (Fleury, Sabin, Dasa, Hermes Pardini). They lose track of past results, can't easily compare trends, and arrive at appointments without history. They are not patients of a chronic disease cult, not biohackers, not quantified-self optimizers — just adults who want their own health archive to actually exist somewhere.

Context of use: at home, on a phone, after receiving an exam by email or WhatsApp from a lab. Sometimes preparing for a doctor's appointment.

Job to be done: "Stop losing my exams. Have them in one place. Bring my history to the doctor without thinking about it."

## Product Purpose

Folio AI is a personal health archive. Users upload exam PDFs or photos; AI extracts the biomarker values; the app stores, organizes chronologically, and visualizes trends. Users can export or share a clean history with a doctor.

Explicitly not a diagnostic tool. Folio does not interpret results, suggest medication, flag risk, or give medical advice. The product line is held strictly: organization, not interpretation. This shapes copy, iconography, and tone — visual cues that imply medical authority are off-limits.

Success looks like: a user with three years of scattered lab PDFs ends up with a single timeline they can pull up in two taps before a checkup.

## Brand Personality

Modern-tech, product-confident. Linear / Stripe / Raycast applied to personal health. Crisp, technical, expert — not warm-for-warmth's-sake, not clinical-corporate, not wellness-aspirational.

Three-word personality: **precise, calm, owned.** ("Owned" as in: this archive belongs to the user, not to a hospital or insurer.)

Voice: direct, no health jargon, no fear-mongering, no hype. Portuguese-first (pt-BR). Sentences short. Verbs active. Numbers when they help, never as decoration.

Emotional goal: the relief of "finally, someone built the obvious thing." Quiet competence.

## Anti-references

- **Generic blue-SaaS health landing.** The training-data reflex: hero-blue gradient, three step cards, dark features section, hero metric pills, identical icon-card grids, gradient-text accents. This is the single biggest trap for this product because the category invites it. If a critic could guess the design from the category name alone, it has failed.
- **Wellness / biohacker dashboards.** Whoop, Levels, Oura aesthetic. Dark neon, data-as-identity, optimization-cult vibe. Too intense for a personal archive, alienates the actual audience.
- **Hospital / insurance corporate sites.** Stock doctor photography, sterile teal-and-white, bureaucratic. Cold and authoritative in the wrong way.
- **Diagnostic-AI startup framing.** Any visual or copy cue that implies the product reads, judges, or recommends. No "AI insights," no "your health, decoded," no warning-pill counts as a hero feature.

## Design Principles

1. **Archive, not advice.** Every visual decision should reinforce that this is a calm filing cabinet, not a diagnostic tool. No alert-driven UI, no judgment colors as decoration, no medical-authority cues.
2. **Earned blue, or none.** The category reflex is blue. If blue stays, it has to be a specific, owned blue used with restraint — not a gradient hero + blue features + blue CTA stacking on itself. Otherwise pick a different anchor.
3. **Show the actual product.** This product is screens of clean data. The landing should feel like the app feels — not like a generic SaaS marketing page bolted on top.
4. **Brazilian without cliché.** pt-BR copy is the baseline. Visual Brazilianness, if any, comes through restraint and precision (modernist), not green-yellow or tropical motifs.
5. **Quiet competence over enthusiasm.** No exclamation points. No "🚀". The voice of someone who has built this carefully and trusts the user to recognize that.

## Accessibility & Inclusion

- WCAG 2.1 AA as the floor. Contrast 4.5:1 for body text, 3:1 for large text and UI components.
- Respect `prefers-reduced-motion` — disable scroll-reveal animations, pulses, and any decorative motion when set.
- Mobile-first reality: a non-trivial share of the audience will arrive on mid-range Android. Keep the landing light, fonts loadable, layout stable.
- Forms must be operable by keyboard alone. Error messages must be specific and actionable (not "algo deu errado").
- Portuguese as the primary language; English is not a target on this surface.
