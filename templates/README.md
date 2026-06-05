# budget-haskell stack template

A custom `stack` template that quick-starts a new Haskell project with the full
working toolchain already wired up: code highlighting, **fourmolu** formatting,
**hlint** diagnostics + code actions, tests, and **step-debugging** — all on the
known-good versions (GHC 9.8.4 / Stackage `lts-23.28` / HLS 2.14.0.0).

## Create a new project

```powershell
stack new <project-name> C:\Code\versioned\GitHub\byth3p0und\tk-mime\templates\budget-haskell.hsfiles
cd <project-name>
stack build
code .
```

That's it. The generated project already contains a pinned `stack.yaml`
(`lts-23.28`) and `.vscode/{settings.json,launch.json,tasks.json}`, so opening it
in VSCode gives you HLS + hlint immediately, and **F5** debugs the executable.

Author/copyright/github fields are filled from your stack config
(`%APPDATA%\stack\config.yaml` → `templates.params`).

## One-time, per-machine prerequisites

These are installed globally and only need doing once (already done on this
machine):

- **ghcup** providing **HLS 2.14.0.0** and **stack 3.7.1** (stack manages its own
  GHC 9.8.4 — there is intentionally no ghcup-managed GHC).
- VSCode extensions: `haskell.haskell`, `justusadam.language-haskell`,
  `phoityne.phoityne-vscode` (the debugger UI).
- Debug adapter executables on PATH (in `%APPDATA%\local\bin`):

  ```powershell
  stack install --resolver lts-23.28 haskell-dap ghci-dap haskell-debug-adapter
  ```

## Why these versions

hlint shipped *inside* HLS works on GHC 9.6 / 9.8 / 9.12 but is **missing from the
ghcup HLS build for GHC 9.10.3**. `lts-24.x` maps to GHC 9.10.3, so the template
pins `lts-23.28` (GHC 9.8.4) to keep hlint working with the latest HLS. Do not
bump the snapshot to `lts-24.x` without checking that HLS regained the hlint
plugin for that GHC.

## Editing the template

`budget-haskell.hsfiles` is a single file; each embedded file starts with a
`{-# START_FILE <path> #-}` marker. `{{name}}` and the
`{{author-name}}`/`{{copyright}}`/`{{github-username}}` fields are Mustache
placeholders substituted at `stack new` time.
