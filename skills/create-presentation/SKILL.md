---
name: create-presentation
description: Create a PowerPoint or PDF presentation with SlideForge from a topic, a brief, or project files, then hand the user a download link. Use when the user asks for slides, a deck, or a presentation.
---

# Create a presentation with SlideForge

## Trigger

The user asks for a presentation, slide deck, or slides, for example "make a
10-slide deck on our Q3 roadmap" or "turn this README into a pitch deck".

## Workflow

1. Work out the brief before calling any tool:
   - Topic: one or two sentences. If the deck is about this project, read
     the relevant files (README, docs, changelog) and summarize them into the
     topic. Don't paste whole files.
   - Number of slides (default 8 if the user didn't say).
   - Tone, audience and language, only if the user mentioned them.
2. Optional: call `list_templates` if the user asks for a particular look.
3. Call `generate_presentation` with the brief. It returns a
   `presentation_id` right away; the deck is built in the background.
4. Call `check_presentation_status` every 5-10 seconds until `status` is
   `completed` or `failed`. A deck usually takes one to three minutes. Tell
   the user it's in progress rather than waiting silently.
5. Call `export_presentation` with `format` `pptx` (default), `pdf`, or
   `images`, and give the user the link. It expires after a few minutes, so
   export again if they ask later.

## When a tool returns an error

- **Free trial needed:** the message includes a secure checkout link for a
  $0, 7-day trial. Show the link exactly as given and explain it costs
  nothing today. Once the user says they've finished, call
  `generate_presentation` again.
- **Out of slides:** say so and suggest a smaller deck, or point them to
  https://www.slideforge.io/pricing. `get_account` shows the balance.
- **`failed` status:** offer to try again, ideally with a shorter or clearer
  topic.

## Output

- One or two lines on what was created (title, slide count).
- The download link.
