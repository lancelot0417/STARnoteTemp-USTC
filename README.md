# STARnoteTemp

This is an updated STAR analysis note template

## What Changed

- Use `main.tex` as the primary entry point.
- Move reusable package and compatibility settings to `starsetup.tex`, mirroring
  the `ustcthesis` pattern of keeping document structure separate from setup.
- Split the note body into files under `chapters/`.
- Use `\include{chapters/...}` and write top-level content files with
  `\chapter{...}` so chapter files can be reused more directly with USTC thesis
  projects.
- Add `chapters/02_floats_and_math.tex`, a removable USTC-style writing guide
  with examples for figures, subfigures, booktabs tables, table notes,
  `siunitx` numerical columns, equations, aligned equations, and algorithms.
- Add `usercommands.tex` for project-specific shorthand commands that should be
  shared by STAR note and thesis chapter files.
- Add `bib/references.bib` and enable `natbib` with `unsrt`.
- Replace deprecated `subfigure` with `subcaption`, and add USTC-style shared
  packages such as `bicaption`, `threeparttable`, `longtable`, `algorithm2e`,
  `siunitx`, and `booktabs`.
- Keep `starrefblk.sty` and `starnote.cls` as template files.
- Do not include the old `starphysics.sty` macro collection by default; users
  should define only the project-specific shorthand commands they need.
- Make the title page robust when `STAR-logo-base-red.pdf` is not present locally.
- Fix the note-version typo in `starnote.cls`.
- Add an explicit `\draftversion{...}` hook; leave it unset for a clean note.

## Recommended Use

Start from `main.tex`, edit the metadata block, then write each major top-level
content file under `chapters/` with `\chapter{...}`. In this STAR note template,
`\chapter` is mapped to a STAR-note section; in `ustcthesis`, the same command
remains a thesis chapter. Put project-specific references in `bib/references.bib`
and figures under `figures/`.

For best portability between this template and `ustcthesis`, keep physics content
inside `chapters/`, keep template-specific title/cover metadata in `main.tex`,
and avoid putting document-class-specific commands inside chapter files.

## Custom Commands

Put your own shorthand commands in `usercommands.tex`. Do not put project-local
macros inside `chapters/*.tex`, `starnote.cls`, or `starsetup.tex` unless they
are truly template-level commands. This keeps the same chapter files usable in
both this STAR note template and `ustcthesis`.

The template intentionally does not include the old `starphysics.sty` macro
collection. If an existing note depends on legacy STAR particle shorthands, copy
only the commands you actually use into `usercommands.tex`.

For thesis reuse, copy `usercommands.tex` into the thesis project and load it
from `ustcsetup.tex` or from the thesis main preamble after the common packages:

```tex
\input{usercommands}
```

For symbols that may be used in normal text, define them with `\ensuremath`.
For example:

```tex
\newcommand{\pT}{\ensuremath{p_{\mathrm{T}}}}
\newcommand{\sNN}{\ensuremath{\sqrt{s_{_{\mathrm{NN}}}}}}
\newcommand{\myObservable}{\ensuremath{R_{\mathrm{AA}}^{\mu\mu}}}
\newcommand{\myCollisionSystem}{Au+Au collisions at \sNN\ = 200 GeV}
```

Avoid short names that conflict with existing commands, such as redefining `\pp`
for proton-proton collisions when it is already used for a pion-pair shorthand.

## Figures, Tables, and Equations

The file `chapters/02_floats_and_math.tex` is included as a practical example.
It demonstrates the patterns most often needed in STAR analysis notes:

- single figures and two-panel figures with `subcaption`;
- publication-style tables with `booktabs`;
- table notes with `threeparttable`;
- aligned numerical columns with `siunitx`;
- numbered equations and multi-line aligned equations;
- short procedural blocks with `algorithm2e`.

Delete this chapter from `main.tex` when the examples are no longer needed.
