# Gent Draw (/docs/features/draw)



Gent Draw is an Excalidraw-based drawing board inside agent chat. It is for the moments where a screenshot, rough diagram, annotated idea, or hand-drawn layout says more than a paragraph.

You can draw, paste images, drop image files, reopen previous drawings, export the board, or send the whole drawing to the agent as a single PNG attachment.

## What Draw is good for [#what-draw-is-good-for]

* Annotating screenshots before asking an agent to fix a UI
* Sketching a screen layout or state machine
* Drawing arrows over an error, trace, or design reference
* Combining pasted images with hand-written notes
* Sending one compact visual brief instead of many separate files

## Opening Draw [#opening-draw]

In agent chat, use the drawing control in the composer. Gent opens a full drawing modal with an Excalidraw canvas and a small toolbar.

The toolbar includes:

| Control | What it does                                                         |
| ------- | -------------------------------------------------------------------- |
| Cancel  | Close the modal without sending                                      |
| History | Reopen saved drawings                                                |
| Export  | Save the current board as a PNG                                      |
| Send    | Export the current board as a PNG and attach it to the agent message |

## Pasting and dropping images [#pasting-and-dropping-images]

Draw supports image-heavy workflows:

* Paste an image from the clipboard
* Pick image files from disk
* Drag and drop image files into the canvas

Supported image types include PNG, JPG, JPEG, GIF, WebP, SVG, and BMP. Images become Excalidraw image elements, so you can draw around them, resize them, and annotate them before sending.

## Sending to the agent [#sending-to-the-agent]

When you click **Send**, Gent exports the current board as `image/png`, writes a temporary file, closes the drawing modal, and attaches that one PNG to the agent message.

This keeps the chat input simple: the agent receives one visual artifact that contains the sketch, pasted images, arrows, labels, and annotations together.

## Autosave and history [#autosave-and-history]

Draw autosaves non-empty scenes and stores a thumbnail for history. Use the History control to reopen previous drawings, continue editing them, or delete old entries.

Autosave stores the Excalidraw scene data so reopening a drawing keeps editable elements, not just a flat screenshot.

## Exporting without sending [#exporting-without-sending]

Use **Export** when you want to save the drawing locally but not send it to the agent. Gent writes a PNG to the location you choose.

## Draw vs Canvas [#draw-vs-canvas]

| Surface     | Best for                                                                       |
| ----------- | ------------------------------------------------------------------------------ |
| Gent Draw   | Human sketches, annotations, pasted screenshots, and visual prompts            |
| Gent Canvas | Agent-generated HTML, charts, prototypes, demos, and interactive web artifacts |

Use Draw when the human needs to communicate visually. Use [Canvas](/docs/features/canvas) when the agent needs to render something visual.
