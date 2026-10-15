# Note-taking Slides

A minimal, single-file HTML meeting deck with a notes panel beside the slides.

The idea is simple: **show the discussion material and take notes in the same window**. Notes are saved automatically in browser local storage while you type. At any point, **Download meeting record (.md)** exports one Markdown file containing both the slide content and your notes.

![Template preview](assets/template-preview.png)

## Why this exists

I wanted something lighter than a normal presentation for small research and project meetings:

- a visible agenda on the left;
- one focused discussion slide at a time;
- a notes box on the right;
- no timer or presenter clutter;
- automatic browser autosave;
- a portable Markdown record at the end of the meeting.

Everything runs locally in the browser. There are no external JavaScript or CSS dependencies.

## Quick start

1. Download or copy [`template.html`](template.html).
2. Rename the copy for your meeting, for example `2026-10-18-project-review.html`.
3. Open it in a text editor.
4. Edit the `MEETING` object and `SLIDES` array near the top of the `<script>` block.
5. Open the HTML file in your browser.
6. Take notes in the right-hand panel during the meeting.
7. Click **Download meeting record (.md)** when you want a portable record.

The notes are also saved continuously in browser local storage, so moving between slides does not lose them.

## Editing a meeting

The content is deliberately data-driven. Most meetings only require editing these two blocks:

```js
const MEETING = {
  title: 'Project Review Meeting',
  subtitle: 'Decisions, updates and open questions',
  date: '18 October 2026',
  exportFile: 'project-review-meeting-record.md'
};

const SLIDES = [
  {
    id: 'decision',
    time: 5,
    title: 'Key decision',
    subtitle: 'Start with the question that most needs input.',
    context: 'Short background for the discussion.',
    items: [
      {
        title: 'What should we decide today?',
        text: 'The concrete question to discuss.'
      }
    ]
  }
];
```

Each slide needs a unique `id`. The `id` is also used to associate browser-saved notes with that slide.

## Available slide elements

### Discussion questions

```js
items: [
  { title: 'Question one', text: 'Supporting detail.' },
  { title: 'Question two', text: 'Supporting detail.' }
]
```

### Updates

Useful for information the other person should know but does not need to decide.

```js
updates: [
  'The analysis is complete.',
  'The collaborator has confirmed their role.'
]
```

### Option cards

Useful when you want reactions to one or two possible designs.

```js
items: [{
  title: 'Which approach looks more useful?',
  text: 'These are illustrative rather than final.',
  ideas: [
    { label: 'Option A', title: 'Focused', text: 'Narrower and faster.' },
    { label: 'Option B', title: 'Broader', text: 'More complete but more complex.' }
  ],
  foot: 'Possible dimensions to vary: scope · timing · cost.'
}]
```

### Comparison table

```js
difference: [
  ['Scope', 'Existing approach', 'Our approach'],
  ['Evidence', 'Single source', 'Multiple sources']
]
```

## Notes and autosave

Notes are written to **browser local storage** as you type. They are not cookies and they are not sent anywhere.

The local-storage key includes the HTML file path, so different meeting files should normally keep separate notes. Browser handling of `file://` local storage can vary, so the Markdown export is the durable copy to keep after the meeting.

The exported record includes, for each slide:

1. slide title and context;
2. updates, options, comparisons and discussion questions;
3. your notes from the meeting.

This makes the exported `.md` useful as a meeting note rather than just a dump of handwritten remarks.

## Keyboard shortcuts

- `→` / `Page Down`: next slide
- `←` / `Page Up`: previous slide

Shortcuts are disabled while the notes box is active, so arrow keys behave normally while typing.

## Files

- [`template.html`](template.html) — reusable self-contained template
- [`assets/template-preview.png`](assets/template-preview.png) — preview used in this README

## Design philosophy

This is intentionally not a full presentation framework. It works best for short meetings where slides are there to structure a conversation rather than deliver a talk. Keep each slide to a small number of questions and put the most important discussion first.
