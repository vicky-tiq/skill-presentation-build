# Producing the deck — four channels

All four are in use. Pick by what happens to the deck *after* the talk, not by what is quickest to generate.

**Before committing to a channel, check it is actually available in this session** — MCP servers drop out, need re-auth, or are not connected. If the chosen channel is unavailable, say so and offer the next-best one rather than silently substituting.

The input to every channel is the same: the **section map from Step 3**, expanded to one slide per idea. Never one slide per section — a 20-minute talk with three sections is not three slides.

---

## Gamma

**Pick it when:** fastest path to a presentable deck, the user will keep editing online, or the deliverable is a shareable link.

- `generate` for a single deck from a prompt; `generate_multi_page_gamma` for longer multi-section decks; `generate_from_template` when a house template exists.
- Generation is asynchronous — poll `get_generation_status` until it completes before reporting a URL.
- `get_themes` first if brand matters; pick the closest theme rather than fighting the default.
- `export_gamma` produces PDF or PPTX afterwards, so Gamma is also a reasonable route *to* a .pptx if online editing is wanted as well.

Feed it the section map as structured outline text — headline plus the one idea per slide — not a wall of prose. Gamma expands prose into padding.

---

## .pptx file

**Pick it when:** it must open in PowerPoint or Keynote, be emailed, be uploaded to a client portal, or be handed to an event organiser who will run it from their laptop.

- Use the `pptx` skill. It handles creation, templates (.potx), layouts, and speaker notes.
- Put the speaker script into the **notes pane**, and still deliver the standalone script file — presenters rehearse from the file and present from the notes.
- If the venue supplies a template, use theirs; ask for the .potx rather than eyeballing their colours.
- Check the file opens and the fonts survive before calling it delivered. Fonts that exist only on this machine will substitute on theirs.

---

## HTML Artifact

**Pick it when:** layout control matters, the deck should live at a stable shareable URL, or it will be presented from a browser.

- Load the `artifact-design` skill before writing the page, then publish with the `Artifact` tool.
- One `<section>` per slide, fixed aspect ratio (16:9), keyboard arrow navigation, and a visible slide counter. Presenting means the speaker cannot fumble.
- Give it a real name at publish time (`AI in Action — SME Workshop`), not a generic one, and update in place at the same URL on later passes.
- It must still read at phone width — people open the link afterwards on their phone.
- Charts follow the `dataviz` skill.

---

## Canva / Adobe Express

**Pick it when:** a designer or the marketing team will take it further in the tool they already work in.

- **Adobe Express:** call `create_visual_design_express_skill` first and follow the playbook it returns — the design is authored as self-contained HTML, validated with `html_export_readiness_skill`, then imported via `export_html_to_express` into a native Express document. Run the readiness check immediately before *every* export, including retries.
- **Canva:** use the Canva plugin skills (`canva:edit-design`, `canva:brand-check`, `canva:implement-feedback`). Canva is strongest for taking an existing design and adapting it, weakest as a from-nothing generator.
- Either way, hand over a deck that is structurally finished. Designers should be adjusting type and imagery, not discovering that slide 7 contains three separate ideas.

---

## Common to every channel

- Apply the user's brand via the `brand-context` skill. Do not invent colours or fonts.
- Minimum 30pt type, whatever the channel. Check at the size the room will see.
- Agenda slide near the front, summary slide near the end.
- Section divider slides help the audience feel the transitions that the script is already speaking.
- A slide the speaker would need to read aloud is a failed slide — move that text into the script.
- If there is a demo, put a static fallback of the demo *into the deck* (screenshots or an embedded recording), so a dead connection does not end the talk.
