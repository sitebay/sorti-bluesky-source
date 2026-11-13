# Remix this maintained Bluesky source

## Identity and scope

This is the SiteBay-maintained source fork at
[sitebay/sorti-bluesky-source](https://github.com/sitebay/sorti-bluesky-source).
The maintenance branch `sorti/remix-8fe5fcb` starts from the complete public
[bluesky-social/social-app source at `8fe5fcb69755160fc913adf8f6cf76318c92b608`](https://github.com/bluesky-social/social-app/tree/8fe5fcb69755160fc913adf8f6cf76318c92b608),
package `bsky.app` version **1.138.0**. Bluesky Social PBC and its contributors
own the upstream application. SiteBay maintains the adaptation instructions;
this is not an official Bluesky product or support channel.

The initial maintenance change appends a README section and adds this guide
and `SORTI_SOURCE.json`. Application code, all upstream files and modes,
dependency locks, GitHub workflows and notices remain unchanged. Select the
exact maintenance commit, not a moving branch name, when importing a source.
`SORTI_SOURCE.json` records the base tree, source inventory digest, toolchain,
notice hashes and the deliberately limited change scope.

This is a complete source foundation. It is not an installed Sorti app, a
permission to use a Bluesky account, a tested integration bridge, or a
redistribution-ready branded application. Build and runtime acceptance belong
to the exact selected source and their own recorded checks.

## Source and asset ownership

Read [LICENSE](LICENSE), [ASSETS.md](ASSETS.md), [NOTICE.md](NOTICE.md) and the
original [forking guidelines](README.md#forking-guidelines) before adapting
or distributing the application. The MIT license covers the source code;
it does not cover every asset in this tree.

For an application you will distribute, replace the commissioned artwork in
`assets/illustrations/`, supply an authorized UI icon set for `assets/icons/ui/`
and the corresponding embedded glyphs, and replace Bluesky and Attie brand
assets. Replace or remove the community artwork and product imagery that
`ASSETS.md` identifies as not licensed for downstream use. Third-party brand
marks require their own appropriate basis. Keep the separate notices for the
permissively licensed fonts and flag icons. The upstream asset guide names
the exact paths and rights holders; do not infer broader rights from a
successful source download or build.

Give the adaptation its own name, branding, support links, analytics and error
reporting. A source-only maintenance fork intentionally retains the original
upstream tree for review; that does not make its existing artwork appropriate
for a new public product. Keep the original notices with source and exports.
Do not add private account data, credentials, environment files, browser state,
installed dependencies or user-supplied game assets to this repository.

## Source map

| Source | Responsibility |
| --- | --- |
| `src/view/com/posts/FollowingEmptyState.tsx` | Following-feed empty state and original Search/Feeds navigation |
| `src/view/com/posts/CustomFeedEmptyState.tsx` | Custom-feed empty state and original feedback/analytics behavior |
| `src/view/com/util/EmptyState.tsx` | Shared empty-state presentation |
| `src/alf/`, `src/components/` | ALF themes, layout, typography and shared interaction primitives |
| `src/screens/`, `src/features/` | Current locations for new screens and features |
| `src/Navigation.tsx`, `src/routes.ts` | Original routing and navigation contracts |
| `src/state/queries/`, `src/state/session/`, `src/state/persisted/` | Network data, accounts, sessions and persistence |
| `src/locale/` | Localization sources and generated catalogs |
| `assets/`, `ASSETS.md`, `NOTICE.md` | Asset custody and the actual licensing boundaries |
| `package.json`, `pnpm-lock.yaml`, `pnpm-workspace.yaml`, `patches/` | Reproducible toolchain and upstream dependency policies |
| `docs/build.md`, `docs/testing.md`, `AGENTS.md` | Upstream development and verification instructions |
| `sorti.import.json`, `sorti/` | Actual reviewed Sorti bridge and handoff, only after an import creates them |

Read the selected files before changing them. Use the existing ALF and
component primitives, localization boundaries and accessibility labels. New
screens and features follow the locations in `AGENTS.md`; the existing empty
state example below stays in its real current owner. Preserve platform-specific
file resolution and original service/data contracts.

## Setup, build and run

At this source pin, `package.json` requires **Node >=24.22.1**. Its
`devEngines.runtime` selects Node `^24.22.1` and
`devEngines.packageManager` pins **pnpm 11.28.5**. There is no top-level
`packageManager` field. Retain the declared pnpm version, lockfile, workspace
policies and patches rather than generating another package manager's lockfile.

Read the current upstream instructions first. The ordinary commands from the
actual app checkout are:

```sh
pnpm install --frozen-lockfile
pnpm run typecheck:web
pnpm run lint
pnpm run test --runInBand
pnpm run build-web
pnpm web
```

Use the repository scripts, not ad hoc invocations of the underlying test or
formatting tools. The install script runs the source's lexicon generator and
`intl:compile-if-needed`. `AGENTS.md` reserves direct `intl:extract` and
`intl:compile` commands for the upstream translation workflow; do not run them
manually to paper over a build failure. Preserve the normal prerequisite
behavior and report a real failure if the selected source cannot build.

This version's `build-web` uses Expo's Metro web export with graph optimization,
tree shaking and source maps, then `scripts/post-web-build.js`. The latter
validates JavaScript entrypoints, prepares the web templates/static files and
resolves the emitted Inter font paths. Its optional Sentry upload runs only
when the authorized Sentry credential is supplied. A local build needs no
borrowed Sentry, Bluesky, cloud or account credentials. Keep build output local
until its original publication review.

Run development servers on an available port without replacing another
project's process. The browser build and web development server do not require
an iOS or Android toolchain. Native builds and the upstream mock environment
follow `docs/build.md` and `docs/testing.md` separately. Record actual Node,
pnpm, source commit, command, exit status and artifact hash for each executed
check. Merely listing these commands does not claim that they passed.

## One concrete customization

In your owned adaptation, rewrite the Following-feed empty-state invitation
in `src/view/com/posts/FollowingEmptyState.tsx` in the adaptation's voice.
Keep its `Trans` boundary and the existing **Find accounts to follow** and
**Discover new custom feeds** controls. Preserve their original Search/Feeds
navigation and accessibility labels. Use the source's established localization
workflow for the changed message.

Inspect that exact state in light and dark themes, narrow and wide layouts,
with keyboard focus and screen-reader labels. Exercise both original
navigation controls and return to the same account/feed state. This design
change does not require posting, following, messaging or changing a real
account. Do not replace the app with a wrapper page that merely changes its
title.

## Extension and source boundaries

| Intended change | Original owner and constraint |
| --- | --- |
| Copy, layout and theme | Actual app components, ALF and localization; preserve navigation and accessibility |
| Feed composition or workflow | Original feed components, queries and state; retain authorization, pagination, cache and user data unless deliberately migrated |
| Service or account model | Separately reviewed integration and persistence migration; source access grants no account access |
| Asset replacement | Actual owned/licensed replacement bytes, their provenance and the declared asset paths |
| Sorti companion tools | The actual reviewed import bridge and app/API owners; no direct private-store reads or inherited credentials |

A new source feature must not leave live routes pointing at removed screens.
Keep account mutations with the original authenticated account and service
owner. A Sorti bridge exposes only implemented, reviewed tools; a catalog row
or app title cannot grant posting, upload, credential or repository access.

## Git, immutable delivery and Sorti admission

Keep source, adaptation changes, README, this guide, dependency pins and
provenance in the maintained Git repository. For this branch, the complete
source and root guides travel together at one immutable commit. Object storage
can deliver permitted content-addressed archives and build artifacts bound to
that source and their digests. An S3 object URL does not replace source history,
permissions or the workspace binding.

The current ordinary Sorti repository owner selects one complete hosted Git
snapshot. A recipe-only repository cannot stand in for this application, and a
loose `REMIX.md` URL does not grant source admission. This upstream tree is
90,837,171 bytes before maintenance docs, exceeding the 64 MiB code/reference
seed budget. Use the original complete imported-web-app repository workflow;
do not drop assets to fit an unrelated seed lane or raise a guard to obtain a
catalog listing.

For an actual import, select the original account/team and repository, review
its exact immutable commit, and preserve root guides and notices. Let the
original importer create the real descriptor, supported bridge and
`sorti/README.md` / `sorti/REMIX.md` handoff. Those generated paths do not exist
merely because this guide mentions them. Run the imported app's actual
build/conformance commands and test its original preview before accepting a
runtime or publishing it. Do not rewrite an older accepted snapshot.

## Save compatibility, interruption and maintenance

Preserve sessions, drafts, feed preferences, cookies, IndexedDB and local
storage during presentation changes. Do not clear user data to make a refresh
look successful. A persistence change needs the original supported migration
and verification against existing state.

When a Forge mission, source operation or build is interrupted, recover the
same app, source revision, candidate and operation receipt. Reconcile an
unknown result before resubmitting. A reload must not silently fork another
app, start another build or discard the current draft. Check the actual saved
result and reopen the same accepted version.

Remix creates a new authorized app identity with the real parent source.
Improve keeps the existing owned app identity, accepted history and user data.
Existing imported apps can receive these guides through an ordinary reviewed
source edit; they do not need an invented parent or forced global publication.

Upstream updates are explicit source changes. Select and inspect the new
commit, retain all notices, update the source map/toolchain/provenance, and
repeat the relevant build and runtime checks. Do not silently follow moving
`main` or reuse a build receipt from another source version. Source capture,
web build, imported bridge, authenticated behavior, native device acceptance,
asset replacement and publication are separate results.
