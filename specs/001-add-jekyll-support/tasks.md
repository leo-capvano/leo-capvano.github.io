# Tasks: Add Jekyll Support to GitHub Pages Website

**Input**: Design documents from `/specs/001-add-jekyll-support/`
**Prerequisites**: plan.md ✓, spec.md ✓, research.md ✓, data-model.md ✓, quickstart.md ✓

**Tests**: No automated tests — per Constitution Principle V, acceptance is manual owner validation only.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2, US3)
- All file paths are relative to the repository root

---

## Phase 1: Setup

**Purpose**: Install Ruby dependencies and establish the local Jekyll runtime.

- [X] T001 Create `Gemfile` at repository root declaring `source "https://rubygems.org"` and `gem "github-pages", group: :jekyll_plugins`
- [ ] T002 Run `bundle install` to resolve gems and generate `Gemfile.lock` (commit both files)

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Create the site-wide Jekyll configuration that all pages depend on.

**⚠️ CRITICAL**: No user story work can begin until `_config.yml` exists — pages without this file cannot resolve the theme, URL, or social links.

- [X] T003 Create `_config.yml` at repository root with all required fields: `title`, `author`, `description`, `email`, `baseurl`, `url`, `theme: minima`, `minima.social_links` (github: leo-capvano, linkedin: leo-capuano), and `exclude` list containing `specs/`, `.specify/`, `.opencode/`, `Gemfile`, `Gemfile.lock`, `README.md`

**Checkpoint**: Foundation ready — `_config.yml` established, user story implementation can now begin.

---

## Phase 3: User Story 1 — Site Owner Enables Jekyll (Priority: P1) 🎯 MVP

**Goal**: Transform the bare-Markdown GitHub Pages site into a Jekyll-powered site with a consistent visual theme (header, footer, typography) on every page.

**Independent Test**: Push the branch, wait for the GitHub Pages build, and visit `https://leo-capvano.github.io`. The site should render with the minima theme rather than raw Markdown. The site title, author name, and social links should appear in the header/footer.

### Implementation for User Story 1

- [X] T004 [US1] Add YAML front matter block at the very top of `index.md` (before the `# Leo Capuano` heading): `layout: default` only — no `title` field to avoid duplicate headings with the existing Markdown `<h1>`
- [X] T005 [P] [US1] Create `404.md` at repository root with front matter (`layout: default`, `title: "Page Not Found"`, `permalink: /404.html`) and body content: heading `# 404 — Page Not Found`, a short message, and a `[Return to the homepage](/)` link

**Checkpoint**: User Story 1 complete — Jekyll-powered site with minima theme, persistent header/footer, and custom 404 page. Fully testable by visiting the GitHub Pages URL.

---

## Phase 4: User Story 2 — Site Owner Migrates Existing Content (Priority: P2)

**Goal**: Ensure all existing portfolio content (bio, Featured Projects, All Projects, Technology Overview, Contact sections) is preserved and renders correctly after the Jekyll migration — zero content regression.

**Independent Test**: Run `bundle exec jekyll serve` locally and compare the rendered homepage section-by-section against the current raw `index.md`. All headings, links, tables, and in-page anchor navigation must be present and correctly formatted.

### Implementation for User Story 2

- [X] T006 [US2] Audit all content sections in `index.md` (About / Bio, Featured Projects, All Projects, Technology Overview, Contact) for Markdown validity: confirm headings use `#`/`##`/`###` syntax, tables use pipe notation, code spans use backticks — fix any syntax that would break minima's rendering
- [X] T007 [P] [US2] Verify every external GitHub project link in `index.md` uses an absolute URL (`https://github.com/...`) that will survive Jekyll's link processing without rewriting
- [X] T008 [US2] Verify in-page anchor link syntax in `index.md` (e.g. "Jump to: About" navigation links) uses lowercase, hyphenated fragment IDs that match minima's auto-generated heading anchors (e.g. `[About](#about)` for `## About`); update any mismatched fragments

**Checkpoint**: User Story 2 complete — all existing portfolio content preserved, correctly formatted, and all links functional in the Jekyll-rendered site.

---

## Phase 5: User Story 3 — Site Owner Adds New Pages (Priority: P3)

**Goal**: Verify that Leo can publish a new page by creating a single Markdown file with front matter — no changes to `_config.yml` or any other global file required.

**Independent Test**: Create the file, run `bundle exec jekyll serve`, and confirm the new page is accessible at its expected URL and shares the minima theme with the homepage.

### Implementation for User Story 3

- [X] T009 [P] [US3] Create `about.md` at repository root with front matter (`layout: page`, `title: "About"`, `permalink: /about/`) and placeholder body content to demonstrate the new-page publishing capability (owner can replace content later)

**Checkpoint**: User Story 3 complete — new pages are publishable by creating a single Markdown file. No global configuration changes required (FR-006).

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Local preview validation and final commit.

- [ ] T010 [P] Run `bundle exec jekyll serve` and validate the local site against the quickstart.md Step 5 acceptance checklist: theme renders, all content sections present, footer social links appear, anchor navigation works, and `http://localhost:4000/nonexistent` serves the custom 404 page
- [ ] T011 Stage all new and modified files (`Gemfile`, `Gemfile.lock`, `_config.yml`, `index.md`, `404.md`, `about.md`) and create a conventional commit: `feat: add Jekyll support with minima theme and custom 404`

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Phase 1 (bundle install must complete first)
- **User Stories (Phases 3–5)**: All depend on Phase 2 completion (`_config.yml` must exist)
  - US1 (P1): No dependency on US2 or US3
  - US2 (P2): Logically depends on US1 (front matter must exist on `index.md` to render it through Jekyll for comparison), but content audit tasks can begin in parallel with T004/T005
  - US3 (P3): Depends on US1 (Jekyll must be functional to test new pages)
- **Polish (Phase 6)**: Depends on all user story phases complete

### User Story Dependencies

- **User Story 1 (P1)**: Starts after Phase 2 — no dependency on US2 or US3
- **User Story 2 (P2)**: Starts after Phase 2 — content audit (T006–T008) can run concurrently with US1 implementation in different files
- **User Story 3 (P3)**: Starts after Phase 2 — `about.md` (T009) is in its own file and can run in parallel with T004/T005

### Within Each User Story

- Foundational config (`_config.yml`) before any page-level work
- Front matter on `index.md` before content audit (pages must go through Jekyll to observe rendering)
- Core implementation before final validation

### Parallel Opportunities

- **T004 + T005**: Different files (`index.md` vs `404.md`) — run in parallel
- **T005 + T009**: Different files (`404.md` vs `about.md`) — run in parallel
- **T006 + T007**: Different concerns in the same file, but T007 is read-only link check — can overlap review
- **T010**: Runs after all implementation tasks

---

## Parallel Example: User Story 1

```bash
# T004 and T005 can be written simultaneously (different files):
Task: "Add front matter block to index.md"         # file: index.md
Task: "Create 404.md with permalink /404.html"     # file: 404.md

# T005 and T009 can also be written simultaneously:
Task: "Create 404.md"                              # file: 404.md
Task: "Create about.md for US3 verification"       # file: about.md
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (Gemfile + bundle install)
2. Complete Phase 2: Foundational (`_config.yml`) — **CRITICAL, blocks everything**
3. Complete Phase 3: User Story 1 (front matter on `index.md` + `404.md`)
4. **STOP and VALIDATE**: Run `bundle exec jekyll serve`; confirm minima theme renders; push and verify live GitHub Pages URL
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Jekyll runtime ready
2. Add User Story 1 → Jekyll site live with theme → **Push, validate live URL (MVP!)**
3. Add User Story 2 → Content audit complete → **Confirm zero content regression**
4. Add User Story 3 → `about.md` created → **Confirm new pages publish without config change**
5. Each story adds value without breaking previous stories

---

## Notes

- No automated tests — owner validates manually (`bundle exec jekyll serve` locally, then the live GitHub Pages URL)
- `layout: default` on `index.md` is intentional — prevents minima's `page` layout from injecting a duplicate `<h1>` above the existing Markdown heading
- `Gemfile.lock` must be committed — ensures reproducible local builds; GitHub Pages ignores it during its own build
- `specs/`, `.specify/`, `.opencode/` must appear in `_config.yml` `exclude:` list — without this, Jekyll publishes spec artefacts as site pages
- `permalink: /404.html` on `404.md` is mandatory — GitHub Pages only serves a custom 404 when it finds a file at exactly `/404.html`
- [P] tasks = different files, no blocking dependencies between them
- Commit after Phase 2 checkpoint and again after the final Polish phase at minimum
