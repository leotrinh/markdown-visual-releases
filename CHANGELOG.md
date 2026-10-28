# Changelog

Changes sit under Unreleased until a build is released; the release then gives them a version and date. Phases 1-7 are tracked in `plans/260917-0502-markdown-visual-v1/plan.md` and are not back-filled here.

## [Unreleased]

## [1.0.9] - 2026-10-27

### Changed
- GitHub in About opens the releases page (`leotrinh/markdown-visual-releases`).
- The installer version checks GitHub for updates at most once a day, 8 seconds after launch; Check for Updates still checks at once.
- When the app is installed both from the Microsoft Store and with the installer, it says so once and suggests keeping only one.

### Fixed
- Links did nothing: Buy me a coffee and GitHub in About, links in the preview, and every other link to a website or an email address. The permission that lets the app open them was written in a shape the app could not read, so every open was refused silently.
- A link that cannot be opened now says why in a notice, instead of doing nothing.

## [1.0.8] - 2026-10-13

### Added
- A Welcome document opens once, the first time this version runs: a short tour, a preview of what Markdown looks like in the app, what the app does and does not send, and a link to support the author. Close it like any tab; it does not come back, and it stays out of Recent and the sidebar.

### Changed
- The Welcome screen names its support link plainly ("Buy me a coffee") instead of hiding it behind the author's name.
- The privacy notes say what the update check sends; they still claimed there was none.
- The Microsoft Store version no longer offers updates itself: Check for Updates opens the app's page in the Store, which installs updates.

### Fixed
- Download & Install could fail with "The process cannot access the file because it is being used by another process (os error 32)": the downloaded installer was started while the app still held it open.

## [1.0.7] - 2026-10-12

### Changed
- Microsoft Store package for the 1.0.6 features (New File, New Folder, sidebar follows the opened file); the app itself is unchanged since 1.0.6.

## [1.0.6] - 2026-10-09

### Added
- New File: a button in the sidebar's Files toolbar and `Ctrl+N` create a Markdown file in the open folder; New File… in the tree's context menu creates one in that folder, or next to that file. The save dialog opens there with `Untitled.md` suggested, and the new file opens in a tab. A file that is already open in a tab is never emptied.
- New Folder: a button next to New File and New Folder… in the tree's context menu put a name field at the top of the folder; Enter creates the folder, Escape cancels. A name Windows cannot use, or one that exists already, is refused with the reason under the field.

### Fixed
- Opening a file from another folder shows that folder in the sidebar. Before, the tree stayed on the folder restored from the last session (often Downloads) whatever file was opened. Files already open stay in their tabs, and a file inside the folder the tree already shows leaves it where it is.

## [1.0.0 – 1.0.5]

Shipped across 1.0.0 to 1.0.5; these entries were not split by version when they were released.

### Added
- Editor: each document opens as Preview, Split or Editor (`Ctrl+1/2/3`) with a resizable split. CodeMirror 6 gives Markdown highlighting, search, and an undo history that survives tab and mode switches.
- Save (`Ctrl+S`) and Save As (`Ctrl+Shift+S`) write through a temporary file next to the original, so a failed save never truncates it. Each file keeps its own line endings and BOM.
- Conflict handling: a file changed on disk after it was opened is not overwritten (Reload from Disk / Keep My Version); a file deleted meanwhile shows as missing with Save As / Close; read-only files open read-only; files that are not UTF-8 are refused instead of opening empty.
- Unsaved-changes safety: a dot on unsaved tabs, a confirmation before closing one, and a single review dialog listing every unsaved file when the window closes.
- Status bar with line, column, line ending, encoding and saved state; banners for external change, missing file, save errors, read-only and large files.
- Large files are checked before they are read: over 20 MB asks first, over 100 MB is refused.
- A file that cannot be opened (not UTF-8, too large, unreadable) shows a dismissible notice with the file name and the reason.
- Each document keeps its scroll position when you switch tabs or between Preview, Split and Editor.
- Open Folder works: `Ctrl+Shift+O`, the button on the welcome screen and one in the top bar choose the folder shown in the sidebar. `Ctrl+O` and a top-bar button open files from any screen; before, only the welcome screen could.
- Sidebar: a Refresh button, and the tree also refreshes after Save As, so a new file shows up. A folder that is empty, that has no Markdown, that is gone or that cannot be read says so instead of showing nothing. The tree works from the keyboard (Tab, arrow keys, Enter, the context-menu key).
- Reveal in Explorer in the tree's context menu shows the file in the system file manager; a failed Copy Path or Reveal says so.
- Recent files and folders are remembered across restarts. The welcome screen and the sidebar's Recent tab list them; click one to open it, × to forget it.
- The last session comes back at launch: the open files, their view modes, the active tab, and the sidebar's folder. Settings → Startup turns this off. A file named at launch opens after them and stays in front; a file that has since disappeared is reported once.
- The window remembers its size, position and whether it was maximized.
- `Alt+Left` / `Alt+Right` go back and forward through the tabs you focused, `Ctrl+Tab` / `Ctrl+Shift+Tab` cycle the tabs, `Ctrl+W` closes the current tab.
- When the tabs do not fit, a menu at the end of the tab bar lists all of them, and the active tab scrolls into view.
- The window title names the active file, with a dot in front while it has unsaved changes.
- Search workspace content: the field in the top bar (`Ctrl+Shift+F`) lists the lines of the workspace's Markdown files that hold what you type, best matches first, as they are found. Case does not matter; every word must appear in the file; "quotes" mean an exact phrase; one character only searches the open document. `Up`/`Down` choose, `Enter` opens the match (`Ctrl+Enter` keeps the list open), `Escape` closes the list and then clears the field. The file opens at the matching line, in the editor or the preview, whichever the tab shows. Text you have edited but not saved is searched as it is on screen, not as it is on disk. Files that `.gitignore` or the default excludes hide, files that are not UTF-8 and files over 20 MB are skipped.
- The app follows the disk. A file that changes outside the app is reloaded when you have no unsaved edits (the scroll position and caret stay, and "X updated on disk." shows for 3 seconds); with unsaved edits you get the "changed on disk" banner and your text is never overwritten; a file that is deleted keeps its tab with the "missing on disk" banner, and if it comes back the tab picks it up. The sidebar shows files and folders created, renamed or deleted in the folders it has open, without Refresh. The app's own saves cause none of this. Only the open files and the sidebar's open folders are watched, not whole folders below them. A change the system fails to report is caught when the window regains focus, or within 30 seconds.

- Markdown help: `F1` or the Help icon opens a drawer beside the document (over its right edge in a narrow window). `F1` or × closes it, and so does `Escape` while focus is in it; focus goes back to where it was unless you moved on, for example to the editor after Insert. Search finds how a piece of syntax is written, how it looks, and what to press; each card has Copy, and Insert writes the snippet at the caret (after a selection, which stays) while the active document shows the editor. Images show their syntax only. The last section lists every keyboard shortcut, with Cmd instead of Ctrl on macOS. About has its own (i) icon.
- Snippet completion in the editor: `Ctrl+Space` lists Markdown snippets (headings, bold, italic, strikethrough, inline code, code block, link, image, lists, task list, quote, table, rule) and typing narrows the list. Typing `#`, `>`, `-`, `1.`, `|`, `[`, `![` or an opening backtick where it starts a construct offers that construct's snippets by itself, never inside a code block; a space closes the list. `Tab` moves through a snippet's fields (a link's text, then its address). Nothing opens for ordinary typing.
- `/` moves focus to the sidebar's file filter (opening the sidebar first) unless you are typing in a field or the editor; `Ctrl+,` opens Settings.
- Windows installer (`pnpm release:build`): install for the current user only or for all users, with a Start menu shortcut and an optional desktop one; the installer, its uninstaller and their pages carry the Markdown Visual icon and colours, and the publisher, copyright and homepage are filled in. It is not code-signed yet, so SmartScreen may ask for **More info**, then **Run anyway**.
- The installer adds Markdown Visual to **Open with** for `.md`, `.markdown`, `.mdown` and `.mkd`, and **Open in Markdown Visual** to the right-click menu, and never makes it your default Markdown app. Uninstalling removes exactly those entries from where they were written and keeps your Markdown files and, unless you tick **Delete the application data**, the app's settings and history.
- A second Windows distribution channel, Microsoft Store MSIX, alongside the direct-download installer (not published yet): `pnpm msix:prepare` / `msix:build` / `msix:sign` / `msix:verify` package, sign and smoke-test the MSIX from the same Tauri build; when the app runs as a Store-installed MSIX the direct-download updater is disabled (the Store manages updates instead). See `docs/microsoft-store-msix.md`.

- Crash recovery: while a document has unsaved changes, a copy of its text is kept on the device (the first 5 seconds after the first edit, then at most every 30 seconds). After a crash or a power cut the next launch lists the files and offers **Restore** or **Discard** for each, or **Restore all** / **Discard all**; closing the prompt keeps the copies for next time. A restored file is unsaved text again; if the file changed on disk meanwhile you get the usual "changed on disk" banner instead of an overwrite, and a file that was deleted is written back to its old path. The copies are removed when you save, close the tab, reload from disk or choose Discard All on exit. They are plain text, on this device only: **Settings, Recovery** turns them off and removes any left, and a file over 8 MB gets none.
- A screen that says "Markdown Visual hit a problem", shows the error and offers Reload replaces a blank window if the app's own interface fails. Your files are not touched.
- The project is MIT-licensed (`LICENSE`), with a privacy statement (`docs/privacy.md`), a security model (`docs/security.md`), the release procedure and the MVP acceptance list with its evidence (`docs/release.md`), and measured performance numbers (`docs/benchmarks.md`). The README has its screenshot, the shortcut list and the roadmap.

### Changed
- Typing in Split view on a long document no longer freezes the window. A 500 KB document took 180 ms per key to reach the screen (2 frames a second); it now takes 19 ms, like a short one. Three causes, each found by measuring: the preview parsed the whole document again for every change of the editor's text, the preview was drawn after every 120 ms of typing however long the document, and the browser re-measured the whole preview each time the editor changed. A document of 20 KB or more is now drawn once typing pauses (0.07 to 1.5 s later, depending on its length); shorter ones follow every change as before. Drawing a long document still takes as long as it did (about 1 s at 250 KB): see `docs/benchmarks.md`.
- The window can no longer be asked to open arbitrary paths with their default program (`opener:allow-open-path` is gone: nothing used it). Opening a link in the browser and Reveal in Explorer keep their permissions (checked in the running app: the window's calls to them pass the permission check, and `open_path`, `plugin:fs` and `plugin:shell` are refused).

### Fixed
- The launcher icons are RGBA PNGs now. The RGB ones made the macOS and Linux builds panic in `tauri::generate_context!`; the Windows build never noticed.
- Task lists show their checkboxes in the preview, ticked for `[x]`; before, `- [ ]` and `- [x]` looked the same. The boxes are read-only, and the Help drawer's Task list card shows its result again.
- Typing in the sidebar's file filter lagged in a folder of thousands of files: with 5 000 files a key took 160 to 200 ms. The field now shows keys at once and the tree follows 100 ms after the last key, and rows that are off screen are not laid out, so a key takes about 40 ms.
- A link in a document can no longer take the app window away: links to other file types, `//host` addresses and query-only links are inert (clicking says so) and the window refuses any navigation off the app page. Before, such a link replaced the whole app with a blank page or a website.
- `#heading` links scroll to the heading; Markdown links with spaces (`my%20notes.md`) or a `#section` open the file; local images with spaces in their name load; remote images show a "blocked" placeholder instead of a broken picture.
- Headings, table headers, links and code in the preview are readable in the dark theme.
- Dialogs take keyboard focus when they open, keep Tab inside, and hand focus back when they close; Save is the default in the unsaved-changes prompts.
- Launching the app with a Markdown file (double-click, "Open with", command line) opens it; before, nothing opened because the request was sent before the window was ready. A second launch brings the window forward, opens its files, and understands relative paths.
- Dropping a file that is not Markdown says so instead of doing nothing, and dropping more than 200 files says how many were skipped.
- The About dialog's GitHub button opens this project's repository instead of the GitHub home page, and credit links open in the system browser.
- In the dark theme the scrollbars and other native controls are dark too.
- The sidebar no longer vanishes when the window is narrower than 980 px: the toggle in the top bar decides, at every width the window can have.
- The sidebar lists only folders and Markdown files (not images, text files or `.gitignore`), hides what `.gitignore` excludes inside a Git repository, shows hidden folders such as `.github`, and no longer stalls the window while it reads a large folder.
- File paths no longer show the Windows `\\?\` prefix (root tooltip, Copy Path). Copy Relative Path no longer treats `C:\docs2` as inside `C:\docs`, and "Go to parent folder" from `C:\docs` goes to `C:\` instead of listing the app's working directory.
- The toolbar and every other icon button were drawn at about 10 px instead of 16 px, because the browser's own button padding squeezed the icon; they looked small and dim, most of all in dark mode. They now keep their size.
- Button tooltips are readable in dark mode (dark text on a light box; before, dark text on a dark box), and each button shows one tooltip instead of two, since the browser's own hover label is gone.
- The placeholder in the search and filter fields takes the theme's grey instead of the browser's, so it stays legible in dark mode (3.3 to 3.9:1 before, above 5:1 now).

### Developer
- Phase 12 (hardening): `cargo fmt --check` joins CI and the workspace is formatted; `deny.toml` and `pnpm audit:cargo|licenses|npm` with `supply-chain.yml` (on dependency changes and weekly) audit licenses and known vulnerabilities (no vulnerability in either tree; six informational notices inside Tauri's own dependencies are ignored with a reason each); `cross-platform.yml` (weekly and by hand, not required for a merge) installs Tauri's Linux libraries and runs the whole workspace and the frontend on macOS and Ubuntu (not yet run since the fix); the workspace crates are `publish = false`. `pnpm check:wiring` also fails on a granted capability nothing uses, `pnpm check:platform-bounds` on any `dangerouslySetInnerHTML` in `src/`, ESLint forbids `console.log` and `.info`, and the production bundle drops `console.debug|info|log`.
- `fixtures/markdown-project/` (a workspace with every kind of file, including a 500 KB one and a `node_modules` that must stay hidden) and `fixtures/kitchen-sink.md` (every feature and every hostile input) are read by `fixture_project.rs` and `kitchen-sink.test.tsx`; `src/lib/tauri/csp.test.ts` pins the content security policy and `preview-containment.test.ts` pins the containment rule. `pnpm bench` adds `bench:io` (open, save, list, scan) to `bench:search`; results go to the git-ignored `benchmarks/results/`. The real-window checks of `docs/release.md` (CSP enforcement from page code, the hostile document in WebView2, crash recovery end to end, typing and drawing times) were run against the release exe; they are scripts outside the repository.
- `contracts/recovery.json` is the shared sample of the recovery payload (Rust and TypeScript both test it). The recovery store writes through the same atomic replace as a save and reads defensively: a damaged, misnamed or stale file is skipped and never stops a launch.
- `pnpm check:wiring` (also run in CI) fails on Tauri commands that are not registered, plugin permissions that are not granted (every file under `src/lib/tauri`, not only `client.ts`), and modules nothing imports except through unwired scaffolds; `pnpm check:platform-bounds` also catches `cfg(windows)`, `cfg(unix)`, `cfg_attr` and `cfg!()`.
- `contracts/ipc-documents.json` is the shared sample of the document IPC payloads; Rust and TypeScript tests both check against it.
- `package.json` is the single source of the version (and repository URL): `tauri.conf.json` points at it, the window title gets it at startup, and `pnpm brand:check` fails if `Cargo.toml` disagrees.
- The minimum Rust version is 1.88, what the locked dependency tree needs. CI tests the OS-agnostic crates on Windows, Ubuntu and macOS.
- Removed code nothing called: the composition root, the picker/opener/app-store ports and their stub adapters, the open-document use case, and the never-invalidated directory cache.
- `contracts/content-search.json` holds the search's parse rules, its matching cases and its wire payloads; the Rust engine, its TypeScript twin (used for unsaved text) and the wire types are all tested against it. `pnpm bench:search` builds workspaces of 100, 1 000 and 10 000 files in a temporary folder and times the search (release build; results go to the git-ignored `benchmarks/results/search.json`). A search stops the moment a newer one starts, and every batch, summary and error carries the run's `generation`, so an older run cannot change what the newer one shows.
- Saved state goes through one gateway (`src/lib/tauri/kv-store.ts`): settings in `app-settings.json`, recents and the session in `app-state.json` with a `schemaVersion`. A section that is missing or not the shape its reader expects is ignored, so a damaged file costs the history, not the launch. The frontend owns persistence; the Rust `AppStore` port stays removed.
- Listing and scanning a workspace share one walker (default excludes, `.gitignore`, hidden folders kept) and run on the blocking pool like the document adapter.
- `pnpm install` works on a fresh clone under pnpm 11: build approvals are `allowBuilds` in `pnpm-workspace.yaml`, because pnpm 11 ignores the old `onlyBuiltDependencies` key and failed with `ERR_PNPM_IGNORED_BUILDS`. CI takes the pnpm version from `packageManager` alone and no longer calls the deleted placeholder-icons script.
- `src/styles/contrast.test.ts` measures the theme tokens and every stylesheet rule that sets both a text and a background colour, in both themes, against 4.5:1; the four older pairs that miss it are listed in the test and that list cannot grow.
- File watching: the `FileWatcher` port takes the whole watch set per call (`watch_paths`), `NotifyFileWatcher` (`notify` 8) reports settled bursts as `fs://changes { paths, overflow }` (`contracts/fs-watch.json`), and `core/disk` decides per tab and per folder from the file's stamp. `mdv-infrastructure/tests/file_watcher.rs` runs it against the real filesystem. Reloading from disk now keeps the editor's scroll position and caret, overlapping loads of one folder in the tree are latest-wins, opening a folder always lists it again (a closed folder is not watched), a folder whose listing failed recovers on the next change, and when more than three notices show, information goes before errors. Sending the same watch request again registers every folder afresh; the disk is rechecked on focus and every 30 s because Windows can lose changes without saying so.
- One list of keyboard shortcuts (`core/shortcuts/shortcut-map.ts`): the window bindings, the top bar's tooltips and the Help drawer's list all read it, and a test presses every listed combination. A bare printable key such as `/` never fires from a text field or the editor.
- Help content is bundled (`features/help/help-data.ts`) and its rendered examples use the app's own preview (`MarkdownPreview` takes `compact`; given its own text it no longer follows the active tab, which made every example re-render on each commit while typing). The snippet catalog is one list for completion and Insert; the stub applier and the old shortcut catalog are gone.
- The sidebar filter is a component of its own (`app/FilterField.tsx`: what is typed, committed to the store 100 ms after the last key), so a key redraws the field alone; tree rows use `content-visibility: auto` with a one-line placeholder (the scroll height, the rows under a scroll position and keyboard focus were compared with and without it). Measured in the release exe on a folder of 5 000 files: 156–200 ms to the next frame per key before, about 40 ms after; the cost was the browser drawing the rows, not React, and typing in the editor beside the tree was never affected.
- `pnpm check:wiring` no longer stops silently when `scripts/wiring-scaffolds.txt` lists nothing (grep exits 1 on an empty list); the list is empty now that completion, snippets and help are wired. `--font-mono`, `--shadow-color`, `--help-w` and `--z-drawer` are design tokens; `copyToClipboard` is shared by the tree menu and the Help drawer.
- ESLint ignores the Cargo workspace's `target/` folder (the config named a `src-tauri/target` that does not exist), so `pnpm lint` no longer fails after `pnpm tauri build` leaves compressed assets there.
- Installer: `pnpm release:build` runs `tauri build`, checks that the generated NSIS script includes `src-tauri/installer/shell-integration.nsh` and registers no association through the template, and writes `SHA256SUMS.txt` beside the installer. `bundle.fileAssociations` stays unset on purpose: the Windows template makes the app the default `.md` handler, ignores `rank` and leaves the executable path unquoted. `pnpm brand:check` also guards the install mode (`both`), the publisher and homepage, the installer images, the hook's extensions (equal to `SUPPORTED_EXTS`) and the shell-context restore that keeps an all-users uninstall in HKLM. CI compiles the installer on every push, and `release.yml` (manual, or a bare `x.y.z` tag) keeps the release installer and its sums as workflow artifacts. What has not been run is in `docs/architecture.md`; open decisions are in `docs/tech-debt.md`.
- `pnpm icons` also writes 48 and 512 px PNGs and the installer's 24-bit BMPs. The Rust cache in CI now uses the action's default workspace; it pointed at `target`, which holds no `Cargo.toml`.
- The sanitizer keeps `<input>` only as a task list's checkbox: the schema requires an `li` ancestor and the default schema forces `type="checkbox"` and `disabled`; raw HTML still never survives the sanitizer. The schema now `satisfies` hast-util-sanitize's `Schema`, so a mistyped key fails `pnpm typecheck`. Tests run hand-built trees through the schema and render task lists through the preview; `preview.css` draws the box with the theme's tokens, because the browser's own disabled box made ticked and unticked barely differ in the light theme.
