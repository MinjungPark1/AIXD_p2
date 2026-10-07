# Shiftwise — interactive mobile prototype

A class-project prototype for hourly workers coordinating multiple jobs. The home page presents the live app inside an iPhone-style frame. The full responsive app is also available at `app.html`.

## Run locally

Install Node.js 20 or newer, then run from this folder:

```sh
npm start
```

Open **http://localhost:8080**. There are no packages to install, API keys, backend services, or build steps. Serve the files over HTTP; do not double-click the HTML files because ES modules require an HTTP origin.

## Upload to GitHub

1. Extract `Shiftwise_GitHub_Ready.zip`.
2. Create your own empty GitHub repository.
3. Upload the contents of the extracted `shiftwise` folder, including `dist`, `package.json`, `server.mjs`, `verify.mjs`, and this README. Keep the folder structure.

If you use Git locally, create an empty repository on GitHub, then run these commands inside the extracted folder. Replace the placeholder URL with your repository URL:

```sh
git init
git add .
git commit -m "Add Shiftwise mobile prototype"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

Uploading source to a GitHub repository does not by itself publish a website. For static hosting, publish the contents of **dist/** as the website root; every runtime asset uses relative paths, including the iframe, so project subdirectories are supported. No Sites account or platform-specific project identity is included in the downloadable package.

## Present the demo

- **Start guided demo** restores fictional state and begins the five-step walkthrough inside the phone.
- Use **Maya / Jordan / Alex** above the phone to switch roles. Jordan opens available shifts; Alex opens the coverage inbox.
- Follow the actual in-app controls: resolve conflict → publish request → volunteer → manager review → approval.
- **Try a scenario** opens overlap, travel-gap, unknown-buffer, blocked-volunteer, multiple-volunteer, and empty-calendar scenarios.
- **Reset demo** asks before clearing local fictional changes.
- **Open full app** displays the original responsive layout outside the phone frame.
- The screen inside the phone scrolls independently. On small devices the surrounding page stacks vertically.

## Implemented features

- Private combined schedules; workplace UI excludes other workers’ private job data.
- Week and agenda views, private shift add/edit/delete, directional travel buffers, and private contact reminders.
- Overlap/travel checks, explicit overnight dates, and ambiguous/nonexistent daylight-saving validation.
- Coverage preview, volunteer confirmation, manager approval, cancellation, rejection, withdrawal, expiration, changed-shift invalidation, event history, save retry, and duplicate-action guards.
- Fictional state persists in browser localStorage across the framed and full-app views on the same origin.

**Job applications and pay tracking are not implemented in this version.** The PRD was left unchanged at the user's request.

## Source map

| File | Purpose |
| --- | --- |
| `dist/index.html` | iPhone-style demonstration page |
| `dist/showcase.css` | Phone frame and presentation layout |
| `dist/showcase.mjs` | Outside-frame controls and origin-checked communication |
| `dist/app.html` | Full responsive application entry point |
| `dist/app.mjs` | Role views, forms, guided demo, scenarios, persistence |
| `dist/style.css` | Application styling and embedded mobile layout |
| `dist/engine.mjs` | Deterministic schedule and coverage rules |
| `dist/favicon.svg` | Shiftwise mark |
| `server.mjs` | Dependency-free local static preview |
| `verify.mjs` | Scheduling and interaction smoke checks |

To change phone dimensions, edit `.phone` in `dist/showcase.css`. To change fictional schedules, edit `seed()` in `dist/engine.mjs`, then reset demo data. Google Fonts are optional remote styling resources; system sans-serif fallbacks work without them.

## Validation

```sh
npm run check
npm test
```

Checks cover scheduling rules, ownership, private-data rendering, full guided demo, approval integrity, daylight-saving cases, and failed-save retry. They are logic and DOM-independent rendering checks, not full browser visual testing. Browser visual QA was unavailable during this build.

## Prototype limitations

All people, employers, and actions are fictional. No messages, real invitations, payroll actions, integrations, or external roster changes occur. Role switching demonstrates perspectives; it is not authentication. All fictional role data exists locally, and the UI privacy boundaries are not production authorization. Browser tabs do not provide production-grade transactional concurrency. A real service needs a secure backend, authenticated workplace membership, permissions, transactional approvals, and operating-policy validation.

Calendar week view covers 8 AM–10 PM; agenda and details display full times. Qualification is seeded as Barista and staffing checks require manager confirmation. Onboarding is a mock invitation under My jobs → Review setup & privacy. Local data is not synced to other browsers or devices. No Apple assets, affiliation, or native iOS functionality are implied by the device frame.
