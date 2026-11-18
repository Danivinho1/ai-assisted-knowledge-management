# How the JSON was built with Claude Code

The formatting JSON was not written in one pass. It went through several iterations, each driven by a concrete problem seen in the live list.

## Process

1. **Describe the target visually.** Start from a mockup or screenshot and list the elements: badges, card sections, colors and their meaning.
2. **Generate a first version.** Ask for a JSON that uses SharePoint's formatting schema, with one input per column and explicit names.
3. **Test in the real list.** Paste it, take a screenshot and compare it with the mockup.
4. **Diagnose from the symptom.** Feed the exact symptom back: "card renders blank", "only the title shows", "date is one day off". Each symptom pointed to a specific cause.
5. **Isolate the cause.** When a complex card rendered blank, a minimal version with only the proven expressions was created. Then pieces were added back one at a time.
6. **Lock the names.** Internal column names were verified from the list settings and every reference was updated in one pass.
7. **Validate before delivery.** Every JSON is parsed and checked for unbalanced parentheses before it goes to the user.

## Iterations that mattered

| Version | Problem found | Change |
|---|---|---|
| v0.1 | Cards showed only the title | Column names did not match the internal names |
| v0.2 | Blank card after the full version | Split into a full card and a minimal fallback |
| v0.3 | Date one day off | Changed the column to date-only format |
| v0.4 | Text centered, footer fields stuck together | Left alignment and explicit spacing |

## Prompt patterns that worked

- **Give the exact symptom and the screenshot.** "The card shows only the title and the chip reads 'Sin vigencia'" leads to a targeted fix; "it doesn't work" does not.
- **Ask for one change at a time** when the output is a formatting schema. A large rewrite hides which part failed.
- **Ask for a fallback.** A minimal version that is known to work makes debugging faster.
- **Request validation.** Asking the model to check structure and balance catches errors before they reach the list.

## What the AI did not do

- It did not connect to SharePoint. Every test was run by hand in the browser, and the screenshots were the feedback loop.
- It did not decide the data model. The categories, tactics and validity rules came from the analysts' process.
