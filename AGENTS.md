# Repository Guidelines

## Project Structure & Module Organization
Repo root hosts the Vite + React 19 app. `index.tsx` hydrates `App.tsx`, which assembles feature slices such as `Content.tsx`, `SideControls.tsx`, and `Prompt.tsx`. Jotai atoms sit in `atoms.tsx`; shared hooks, helpers, and type aliases live in `hooks.tsx`, `utils.tsx`, and `Types.tsx`. Palette data, prompt templates, and sample image URLs centralize in `consts.tsx`. Styling relies on Tailwind utilities with `index.css` handling global resets. Keep `metadata.json` aligned with any AI Studio deployment changes.

## Build, Test, and Development Commands
Run `npm install` with the active Node LTS. Day-to-day commands:
```
npm run dev      # hot-reload dev server; requires GEMINI_API_KEY in .env.local
npm run build    # production bundle + type check in dist/
npm run preview  # serve the built artifact for final QA
```
Prefer `npm run build` before every commit or PR; it is the fastest regression detector available today.

## Coding Style & Naming Conventions
Use TypeScript with 2-space indentation and semicolons. Components and files are PascalCase (`ExampleImages.tsx`), hooks start with `use`, and atoms end with `Atom`. Keep state mutations in `atoms.tsx`, move derived data or math into `utils.tsx`, and keep `App.tsx` limited to orchestration. Favor Tailwind utilities over bespoke CSS; if you must touch global styles, add a brief comment.

## Testing Guidelines
No automated test script exists yet; when adding logic, introduce Vitest + React Testing Library next to the module (`Component.test.tsx`). Unit-test `utils.tsx`, prompt builders, and hooks with mocked atoms. For UI flows, capture manual QA steps in the PR (e.g., “Select `segmentation-masks`, upload custom image, observe palette change”). Target smoke coverage for any new reducer-like hook before merging.

## Commit & Pull Request Guidelines
History follows Conventional Commits (`feat:`, `fix:`, `chore:`). Keep subjects under 72 chars, describe scope (`feat(prompt): tighten defaults`), and squash locally if a change spans multiple WIP commits. PRs should include a short summary, linked issue, screenshots for UI tweaks, `npm run build` output, and explicit mention of manual test cases. Request review from another agent before merging to main.

## Security & Configuration Tips
Never commit `.env.local`; it must declare `GEMINI_API_KEY`. Remote sample images are fetched at runtime, so avoid adding bulky binaries to git. If a feature needs extra secrets or scopes, document them here and in `metadata.json`, and gate usage through env variables.
