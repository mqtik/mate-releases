# Gent Canvas (/docs/features/canvas)



Gent Canvas gives agents a real web surface next to the conversation. When an agent needs to show something visual, it can call the built-in `mate-canvas` MCP tool and render a self-contained HTML document in the Canvas panel.

This is the web-agent surface in Gent: the agent writes the page, Gent renders it, and you can keep iterating without leaving the chat.

## What Canvas is for [#what-canvas-is-for]

Use Canvas when the output should be seen, touched, or inspected as a rendered web artifact:

* Interactive prototypes and one-off UI mockups
* Charts, dashboards, and data visualizations
* Diagrams and system maps
* Games, simulations, and small tools
* HTML/CSS/JS demos that benefit from live iteration

Canvas is not an image viewer. If an agent creates a PNG, SVG, JPEG, logo, screenshot, or icon file, it should attach or reference the file directly instead of opening it in Canvas.

## Starting with `/canvas` [#starting-with-canvas]

Type `/canvas` followed by what you want:

```text
/canvas build a responsive pricing table with annual/monthly toggle
```

Gent rewrites that into a focused instruction for the agent:

1. Create a complete self-contained HTML file in the current working directory
2. Put CSS and JavaScript inline
3. Use CSS custom properties for important colors, fonts, and spacing
4. Call `mcp__mate-canvas__show` with the generated file

The Canvas panel opens beside the chat when the tool call completes.

## File mode and auto-reload [#file-mode-and-auto-reload]

Canvas supports inline HTML, but Gent prefers file mode for iterative work. The agent writes a file such as `canvas-a1b2c3d4.html`, then calls the show tool with:

```json
{
  "file": "canvas-a1b2c3d4.html",
  "title": "Pricing table"
}
```

Follow-up `/canvas` messages are applied to the same file when possible. The panel auto-reloads after edits, so the agent does not need to call the show tool again for every tiny change.

## Library support [#library-support]

Canvas can load browser libraries from CDNs when the HTML needs them. Good fits include:

| Need               | Examples                      |
| ------------------ | ----------------------------- |
| 3D scenes          | Three.js, Babylon.js          |
| Charts             | D3, Chart.js, Plotly, ECharts |
| Maps               | Leaflet, MapLibre GL          |
| Animation          | GSAP, anime.js, Lottie        |
| Audio              | Tone.js, Howler.js            |
| Games and sketches | Phaser, p5.js, Matter.js      |
| Diagrams           | Mermaid, JointJS              |
| Editors            | Monaco Editor, CodeMirror     |

Agents should pin CDN versions instead of using `latest`, for example `three@0.160.0`.

## Canvas vs Web Preview [#canvas-vs-web-preview]

Canvas and Web Preview solve different problems:

| Surface     | Use it when                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------- |
| Gent Canvas | The agent is generating a self-contained web artifact directly in chat                              |
| Web Preview | You already have a dev server running on localhost and want to view it from Gent or a paired device |

For app development, a common flow is: ask the agent to sketch an idea in Canvas, then move the real implementation into your project and use [Web Preview](/docs/features/web-preview) to test the running app.

## Constraints [#constraints]

* Canvas has no backend, database, filesystem access, or server-side API
* Everything must run in the browser
* External dependencies should load from versioned CDN URLs
* The current Canvas panel is attached to the current chat and replaces the previous Canvas artifact for that conversation

## Related [#related]

* [Agent Chat](/docs/features/agent-chat)
* [Web Preview](/docs/features/web-preview)
* [Gent Draw](/docs/features/draw)
