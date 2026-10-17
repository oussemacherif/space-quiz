# Copilot instructions

## Project structure and architecture

The quiz is a self-contained static web page in `index.html`: markup, styles, question data, and application logic all live in that file. It runs directly in a browser from the filesystem and has no build step, package manager, server, or external runtime dependencies.

The JavaScript question array is the source of quiz content. The rendering and interaction flow is managed by the page's state (`current`, `score`, `selected`, and `locked`) and the functions `renderQuestion`, `selectAnswer`, `checkAnswer`, `showResult`, and `restartQuiz`. Keep question count and score/progress/result displays consistent with the question data when changing the quiz.

The CSS uses custom properties in `:root` for the light palette and overrides them under `prefers-color-scheme: dark`. Responsive layout and reduced-motion handling are in the same stylesheet. Preserve these behaviors when adjusting visuals or animations.

## Commands and verification

There are no build, test, or lint commands configured in this project. To run the app, open `index.html` directly in a browser; no server is required.

For a browser smoke test, verify that number keys 1–4 select an answer, Enter checks and advances, correct answers update the score, incorrect answers show red feedback and identify the right answer, progress advances, and the final screen shows the score and reaction. Also verify replay resets the quiz.

## Interaction and UI conventions

- Answer options are created from the question data in `renderQuestion`; keep answer selection and feedback state synchronized with the visible buttons and score.
- The answer buttons support both pointer selection and keyboard shortcuts. Enter checks a selected answer, then advances after feedback; keep this two-step behavior intact.
- Progress is exposed as an ARIA progress bar, answer choices are buttons, and feedback uses a live region. Preserve these accessible semantics when changing the DOM.
- The page supports narrow viewports, system light/dark preference, and reduced-motion preference. Keep the quiz centered in its narrow column and retain those responsive and preference-aware styles.
