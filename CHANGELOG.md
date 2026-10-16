# Changelog

All notable changes to PlatyPeer in this repository.

## Unreleased

### Mapped No/Unclear report sentences for every checklist item (`43a14cb`)
- Every checklist item (67 across 8 lists) now carries pre-written `no` / `unclear`
  report sentences, e.g. No → "The authors did not use an external test
  dataset, so generalisability beyond the development cohort is untested.",
  Unclear → "Whether the authors used an external test dataset was not
  clearly stated."
- The optional note is appended to the mapped sentence.
- The composer shows a live **Report preview** that follows the selected
  question, answer and note.
- Re-answering in Second Read regenerates the mapped sentence, unless the
  sentence was hand-edited (hand edits always win).
- Removed the superseded `assets/ai-checklist-template.json`, which shadowed
  the new sentence files; checklists load only from `assets/checklists/`.

### Answer buttons not changing color — fixed (`977a275`)
- The First Read answer buttons carried `data-ckans` while the highlight CSS
  targeted `[data-a]`, so the pressed state never painted. The attribute was
  added; Yes/No/Unclear/N-A now show green/red/amber/grey.

### Checklist composer feedback and hardening (`013186e`)
- Live status line under the composer, e.g.
  `Selected iAIMS I1 · Answer No · Weight MINOR → joins the report as MINOR`,
  so every tap gives unmistakable text feedback beyond button color.
- `render()` hardens state first (`ensureState()`), so no odd stored review
  shape can silently break button wiring.
- Tapping Add before questions finish loading shows a notice instead of
  silently doing nothing.

### First Read checklist redesign (`889bf79`)
- AI Checklist composer moved to the bottom of First Read behind a big
  on/off toggle (**Do you need AI Checklist?**), persisted, off by default.
- Checklist selection is a dropdown (iAIMS Checklist — RECOMMENDED, plus
  TRIPOD+AI, CLAIM 2024, CONSORT-AI/SPIRIT-AI, DECIDE-AI, STARD-AI, MI-CLAIM,
  TRIPOD-LLM); full item sets bundled in `assets/checklists/`.
- Question selection is a searchable card list with a detail panel instead
  of a dropdown.
- Answer (Yes/No/Unclear/N-A) and Weight (Major/Minor, suggestion only,
  overridable) on separate labeled rows.
- Taps update in place — no full re-render, so focus and typed notes survive.
- Composer has its own Line/Section/Note inputs mirroring the general
  capture form, so checklist and general comments feel like one thing and
  produce identical comment cards.

### AI Checklist merged into First Read — 5 steps (`a6a02c3`)
- Six stations became five: Invite → First read → Second read → Report →
  AI polishing. The standalone AI Checklist step is gone.
- One unified comment object: class (Major/Minor), core (Yes/No, max 3),
  line (number or General), section (paper sections or General), plus
  checklist linkage (list, question, description, Yes/No/Unclear/N-A answer,
  optional note).
- Removed the 1–5 scale. Only **No/Unclear** answers become report sentences
  inside Major/Minor; Yes/N-A stay in the reads and never export.
- Checklist severity is a suggestion the reviewer can override.
- Comment cards are popup-style with entrance animation and an **×** button
  (animated delete) on every card.
- Per-review Delete in My Reviews now requires typing **DELETE**, like
  Clear review.
- Legacy `notes[]` convert to comment objects on load; old 1–5 answers are
  archived to history (fresh start, no score migration). Old `.pltpy`
  files still import.
- `.pltpy` format bumped to v2 (`checklists_used`); Report/PDF/TXT group
  No/Unclear sentences under Major/Minor with checklist code chips.
- Landing page (`index.html`) and dashboard (`dashboard.html`) updated
  from six stations to five.

### My Reviews fixes (`dac506d`)
- Deleted reviews no longer reappear as empty shells; the list refreshes
  in place.

### Start screen (`466461a`)
- New Review vs Continue Previous Review (`.pltpy` select/drop) start
  screen.
