## 2026-07-03 - Task: Remove frontend external navigation links and default fal entry
### What was done
- Removed frontend GitHub, release, support, feedback, and About-page navigation entry points.
- Rendered Markdown links as plain text so generated or help content cannot open external pages.
- Removed the default fal.ai provider entry from the provider selector while keeping old fal task/config compatibility.
- Added documentation for the frontend no-external-navigation policy.
### Testing
- `npm install`
- `npm run build`
- `npm test`
- `rg -n -S 'href=|target="_blank"|window\.open|https://github.com|github.com|ifdian|star-history|cooksleep|useVersionCheck|latestRelease\.url|关于' src -g '!*.test.ts'` -> no frontend link hits.
### Notes
- `src/components/Header.tsx`: changed the app title to plain text and removed the GitHub release update link path.
- `src/components/HelpModal.tsx`: removed the bottom GitHub profile link.
- `src/components/SupportPromptModal.tsx`: replaced external sponsor/feedback links with a local dismiss button.
- `src/components/MarkdownRenderer.tsx`: renders Markdown anchors as text spans instead of clickable links.
- `src/components/SettingsModal.tsx`: removed the About tab/page and default fal.ai option from provider choices.
- `src/hooks/useVersionCheck.ts`: removed the now-unused GitHub release check hook.
- `src/lib/apiProfiles.ts`: removed fal from default provider ordering.
- `src/lib/apiProfiles.test.ts`: updated provider-order expectation for the hidden fal default.
- `src/store.ts`: removed the `about` settings tab type.
- `docs/frontend-navigation-policy.md`: documented the no-external-navigation behavior and fal compatibility boundary.
- Rollback: before commit, run `git checkout -- src/components/Header.tsx src/components/HelpModal.tsx src/components/MarkdownRenderer.tsx src/components/SettingsModal.tsx src/components/SupportPromptModal.tsx src/hooks/useVersionCheck.ts src/lib/apiProfiles.ts src/lib/apiProfiles.test.ts src/store.ts docs/frontend-navigation-policy.md progress.md`; after commit, revert the published commit.
