# tk-mime

A reference Haskell project **and** a `stack` template for quick-starting new
projects with a complete, known-good VSCode toolchain:

- **GHC 9.8.4** via Stackage **`lts-23.28`**
- **HLS 2.14.0.0** — code highlighting, completions, hover
- **hlint** diagnostics + "apply hint" code actions (via HLS)
- **fourmolu** formatting
- `stack test`
- **step-debugging** via `phoityne-vscode` + `haskell-debug-adapter`

## Quick-start a new project from the template

```powershell
stack new <project-name> https://raw.githubusercontent.com/byth3p0und/tk-mime/main/templates/budget-haskell.hsfiles
cd <project-name>
stack build
code .
```

The generated project ships with a pinned `stack.yaml` and
`.vscode/{settings,launch,tasks}.json`, so HLS + hlint work on open and **F5**
debugs the executable. See [templates/README.md](templates/README.md) for the
one-time per-machine prerequisites (HLS, the phoityne extension, and the
`ghci-dap`/`haskell-debug-adapter` executables).

## Why `lts-23.28` / GHC 9.8.4

hlint bundled inside HLS works on GHC 9.6 / 9.8 / 9.12 but is **missing from the
ghcup HLS build for GHC 9.10.3** (which `lts-24.x` maps to). Pinning `lts-23.28`
keeps hlint working alongside the latest HLS.
