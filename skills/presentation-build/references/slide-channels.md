# Producing the deck — choosing a channel

The input to every channel is the same: the **section map from Step 3**, expanded to one
slide per idea. Never one slide per section — a 20-minute talk with three sections is not
three slides.

**Before committing to a channel, check it is actually available in this session** — MCP
servers drop out, need re-auth, or are connected under a different account than expected.
If the chosen channel is unavailable, say so and offer the next-best one rather than
silently substituting.

Pick by what happens to the deck *after* the talk, not by what is quickest to generate.

| Channel | Pick it when | Lands as |
|---|---|---|
| **Native slides MCP** | Fast themed deck without leaving the conversation | A hosted deck + speaker notes |
| **Gamma** | Fastest good-looking deck that will keep being edited online | A Gamma link |
| **.pptx** | Must open in PowerPoint/Keynote, be emailed, handed to an organiser | A file |
| **Google Slides** | The team lives in Workspace and will co-edit or comment | A Drive link |
| **Figma Slides** | The deck is a design artefact; designers will own it | A Figma file |
| **Canva / Adobe Express** | Marketing will take it further in their own tool | An editable design |
| **HTML Artifact** | Layout control matters, or it needs a stable shareable URL | A web page |
| **Lark Slides** | No API — build the .pptx, user imports it by hand. See the Lark section | A .pptx + steps |

---

## Native slides MCP

**Pick it when:** a themed, presentable deck is wanted immediately and nothing downstream
requires a specific file format.

- `create_slides` — pass **all slides in one call**, `presentation_id: ""` on the first
  call, then the returned id on every later call in the same conversation.
- **`talktrack` is the speaker-notes field.** Put the section's spoken content there so the
  script and the deck stay attached. Still deliver the standalone script file.
- Editing one slide: resend **only that slide**, same `slidenum`, `force_edit: true`, same
  `presentation_id`. Resending the whole deck, or omitting `force_edit`, appends duplicates.
- Twelve layouts. Map them to the section map rather than picking at random:
  `title_and_subtitle` for **section dividers** — these are exactly the transition points
  already written into the map; `title_and_two_columns` for the first content slide;
  `quadrant_grid` / `data_table` / `timeline_horizontal` / `phase_roadmap` where the content
  genuinely has that shape; `metric_rings` only for real 0–100 percentages.
  `title_and_body` at most **once**, for the conclusion.
- Eighteen themes via `theme_id` (pass it in `create_slides`, not a separate `apply_theme`
  call). Pick the theme closest to the user's brand; do not fight the defaults.

---

## Gamma

**Pick it when:** fastest path to a presentable deck, the user will keep editing online, or
the deliverable is a shareable link.

- `generate` for a single deck; `generate_multi_page_gamma` for longer multi-section decks;
  `generate_from_template` when a house template exists.
- Generation is asynchronous — poll `get_generation_status` until it completes before
  reporting a URL.
- `get_themes` first if brand matters.
- `export_gamma` produces PDF or PPTX afterwards, so Gamma is also a route *to* a file when
  online editing is wanted as well.

Feed it the section map as structured outline text — headline plus the one idea per slide —
not prose. Gamma expands prose into padding.

---

## .pptx file

**Pick it when:** it must open in PowerPoint or Keynote, be emailed, uploaded to a client
portal, or run from an event organiser's laptop.

- Use the `pptx` skill. It handles creation, templates (.potx), layouts, speaker notes.
- Put the script into the **notes pane**, and still deliver the standalone script file —
  presenters rehearse from the file and present from the notes.
- If the venue supplies a template, use theirs; ask for the .potx rather than eyeballing
  their colours.
- Fonts that exist only on this machine will substitute on theirs. Check before delivering.

**.pptx is also the master for Google Slides** — see below.

---

## Google Slides

**Pick it when:** the audience or the team lives in Google Workspace, several people will
comment or co-edit before the talk, or the presenter will open it from Drive on the day.

There is **no Google Slides content API connected here.** The Drive MCP can create a *blank*
presentation (`create_file` with `mimeType: application/vnd.google-apps.presentation`) but
cannot lay slides out inside it. Do not promise a populated deck by that route.

The working path is **build the .pptx first, then let Drive convert it**:

1. Build the deck with the `pptx` skill as above.
2. `create_file` with `title`, `base64Content` (the .pptx bytes, base64) and
   `contentMimeType: application/vnd.openxmlformats-officedocument.presentationml.presentation`.
3. Leave `disableConversionToGoogleType` **unset** — conversion to native Google Slides is
   the default and is the entire point. Setting it true parks a .pptx in Drive instead.
4. `parentId` to drop it in the right folder if the user names one.

Then:

- **Open the converted deck and look at it.** Conversion moves type and spacing; a layout
  that was tight in PowerPoint can overflow in Slides. Keep the .pptx as the master and
  re-convert after edits rather than maintaining two copies.
- Speaker notes survive the conversion.
- Sharing is a separate, deliberate step. `share_file` publishes it to other people —
  **ask the user first, every time**, and confirm who the audience is. Never widen access
  because a document or a calendar invite implied it.

---

## Figma Slides

**Pick it when:** the deck is a design artefact — it must match components or a design
system already in Figma, or designers will own it after you hand it over.

- **Load the `figma-create-new-file` skill before calling `create_new_file`** — the tool
  requires it. Then `create_new_file` with `editorType: "slides"`, a `fileName`, and a
  `planKey`.
- The `planKey` comes from `whoami`. Call it first and **read the seats**, do not grab the
  first plan in the list: a **View seat cannot receive a new file.** Only offer teams where
  the seat is Full, and if more than one qualifies, ask which.
- `whoami` also returns the connected handle and email. **Check it is the account the user
  expects.** (Observed 2026-09-15: the Figma connection on this machine is authenticated as
  a different person's account from the user's own — creating a deck there puts the work in
  someone else's drafts. Confirm before creating anything.)
- Populate and edit through `use_figma`, loading the `figma-use` / `figma-use-slides` skills
  first.

Strongest when the deck must look designed and stay editable by designers. Weakest when the
presenter needs to run it offline or hand a file to an event organiser — export to PDF for
that, or build the .pptx instead.

---

## Lark — no API, but a real manual path

**You cannot build a Lark Slides deck programmatically.** Do not offer it as an automated
channel. Verified 2026-09-15:

- The connected Lark MCP covers **Bitable, Contacts, Docx, IM and Wiki only** — no slides
  tool, and no Drive upload tool, so the "build a .pptx and convert it on upload" trick that
  works for Google Slides has no entry point.
- Lark's open API has no Slides namespace, and the Drive file-type list recognises
  `doc`, `sheet`, `mindnote`, `bitable`, `file`, `docx`, `folder` and `shortcut` —
  **`slides` is not a type the API knows about.**

### The manual path that does work

Lark Slides imports PowerPoint. So **build the .pptx with the `pptx` skill, hand the user
the file, and give them these steps** — verified against the Lark help centre, 2026-09-15:

**From a local .pptx:** open any Lark document → hover the **+** icon in the upper-right
corner → **Upload or Import** → **Import as Docs** → choose the import format
**Microsoft PowerPoint**.

**From a .pptx already in Lark Drive:** open the PPTX → hover the **···** icon in the
upper-right corner → **Import as Slides**.

Limits that will bite:

- Maximum import size **600 MB**.
- **Files in Wiki or My Document Library cannot be converted.** Move the file to **Drive**
  first. Worth saying up front — this team keeps a lot in Wiki.
- Import fidelity is **not documented**. Assume fonts, animations and embedded objects can
  shift, and tell the user to open the imported deck and look at it before presenting. Keep
  the .pptx as the master.
- Going the other way (Lark Slides → export), **charts, boards, comments and video covers
  cannot be exported.** So a deck that gets rebuilt inside Lark Slides with native charts
  will not round-trip cleanly back to a file.

### What Lark *is* good for in this skill

1. **The script and section map as a Lark Doc.** `docx_v1_document_create` then
   `docx_v1_documentBlock_batchUpdate`. For an internal Lark team this is often the more
   useful half of the output: the section map is a table people can comment on, and the
   speaker script is a document the presenter rehearses from.
2. **Announcing the finished deck in the Lark group.** `im_v1_message_create` posts the
   link (Gamma, Drive, Figma, Artifact) into the chat where the audience already is.
   Posting a message is **sending on the user's behalf** — confirm the chat and the wording
   with them first, every time.

---

## Canva / Adobe Express

**Pick it when:** a designer or the marketing team will take it further in the tool they
already work in.

- **Adobe Express:** call `create_visual_design_express_skill` first and follow the playbook
  it returns — the design is authored as self-contained HTML, validated with
  `html_export_readiness_skill`, then imported via `export_html_to_express` into a native
  Express document. Run the readiness check immediately before *every* export, retries
  included.
- **Canva:** use the Canva plugin skills (`canva:edit-design`, `canva:brand-check`,
  `canva:implement-feedback`). Canva is strongest at adapting an existing design, weakest as
  a from-nothing generator.

Either way, hand over a deck that is **structurally** finished. Designers should be adjusting
type and imagery, not discovering that slide 7 contains three separate ideas.

---

## HTML Artifact

**Pick it when:** layout control matters, the deck should live at a stable shareable URL, or
it will be presented from a browser.

- Load the `artifact-design` skill before writing the page, then publish with `Artifact`.
- One `<section>` per slide, fixed 16:9, keyboard arrow navigation, visible slide counter.
  Presenting means the speaker cannot fumble.
- Give it a real name at publish time (`AI in Action — SME Workshop`), not a generic one,
  and update in place at the same URL on later passes.
- It must still read at phone width — people open the link afterwards on their phone.

---

## Common to every channel

- Apply the user's brand via the `brand-context` skill. Do not invent colours or fonts.
- Any chart follows the `dataviz` skill.
- Minimum 30pt type, whatever the channel. Check at the size the room will see.
- Agenda slide near the front, summary slide near the end.
- Section divider slides let the audience *feel* the transitions the script already speaks.
- A slide the speaker would need to read aloud is a failed slide — move that text into the
  script.
- If there is a demo, put a static fallback of it **into the deck** (screenshots or an
  embedded recording), so a dead connection does not end the talk.
- **Sharing a deck with other people is always a separate step the user approves** — links,
  Drive permissions, Figma invites, published Artifacts. Build first, ask, then share.
