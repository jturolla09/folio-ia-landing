---
name: folio-email-reminder
description: >-
  Draft and prepare re-engagement / reminder emails to Folio AI's existing user
  base, in pt-BR, brand voice. Reads a recipients list (CSV path or pasted),
  generates a personalized pt-BR email, and creates Gmail drafts (review before
  send). Use when the user says "email my users", "send a reminder to my user
  base", "re-engage beta users", or "draft the user newsletter".
---

# Folio AI — user reminder / re-engagement email

Brand voice (PRODUCT.md / DESIGN.md): pt-BR, calm, precise, short sentences, no
hype, no exclamation marks, no rocket emoji. **Archive, not advice.**

## Inputs you need

1. **Recipients** — a CSV with at least `email`, optionally `nome` (first name).
   Ask the user for the path (e.g. `marketing/users.csv`) or to paste the list.
   The user base lives in Supabase — they export it to CSV. Never invent
   addresses.
2. **Goal of the email** — pick or confirm: re-engagement ("você tem exames
   parados?"), new-feature announcement, or gentle "suba seu primeiro exame"
   nudge for sign-ups who never uploaded.

## LGPD + deliverability guardrails (state these, don't skip)

- Only email people who are **existing users / opted in**. Existing-user
  reminders rest on the existing relationship; pure cold marketing needs a legal
  basis. When unsure, ask.
- Every email MUST include: a clear sender identity, the reason they're getting
  it ("você se cadastrou no Folio AI"), and a working **descadastrar / opt-out**
  line. Honor opt-outs.
- Personal Gmail is fine for a **small** list (tens, low hundreds) and has a
  ~500/day cap and weak deliverability. For a real campaign (hundreds+),
  recommend a proper ESP popular in Brazil — **Brevo** (ex-Sendinblue),
  **Resend**, or Mailchimp — with SPF/DKIM on the folio domain. Offer to format
  the same copy as an ESP-ready HTML template.

## Procedure

1. Load recipients. Dedupe. Validate addresses. Report the count and ask for
   confirmation before creating any drafts.
2. Write ONE email: subject (pt-BR, < 50 chars, no hype), a short plain-text
   body + a clean HTML version, personalized with `{{nome}}` when present.
   Include the opt-out line and the app link https://folio-ia.app.
3. For each recipient (or in batches), create a Gmail draft with `create_draft`
   (personalized `to`, subject, body, htmlBody). Do NOT send — there is no send
   tool here by design; the user reviews drafts and sends.
   - For a large list where individual drafts are impractical, instead produce a
     single ESP-ready HTML template + a CSV merge field guide, and tell the user
     to import it into Brevo/Resend.
4. Summarize: how many drafts created (or template produced), and the exact
   next step to send.

## Sample subject lines (pt-BR, on brand)

- "Seus exames continuam esperando"
- "Aquele PDF do laboratório ainda está perdido?"
- "Um lugar só para o seu próximo exame"

## Guardrails

- Never send automatically. Drafts only (review gate).
- Never email addresses not in the provided opted-in list.
- Always include the opt-out line. Keep it honest and calm — no urgency tricks.
