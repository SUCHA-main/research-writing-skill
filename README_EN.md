# Research Writing Assistant

> This repository is a public fork of [Norman-bury/research-writing-skill](https://github.com/Norman-bury/research-writing-skill). The original project, skill system, and version 3.1.0 are maintained by 旬常 (GitHub: Norman-bury). This fork preserves the original attribution and MIT license and only maintains fork-specific documentation and installation guidance. See [NOTICE.md](NOTICE.md).

Upgrade "paper writing" from one-off chat sessions into a trackable, recoverable, and reusable engineering-style collaboration workflow.  
This Skill is designed for undergraduates, graduate students, and early-stage researchers with a clear goal: fewer detours, less rework, and more time spent on research that truly matters.

## What This Is

This is not a prompt pack that only polishes sentences. It is a modular research writing collaboration workflow.
Before starting any task, it aligns goals and constraints through a brainstorming process to confirm paper type, research background, methods, and chapter structure, then routes to the appropriate skill module based on your discipline and task type.

If you are working on a thesis, a course project paper, or a submission draft, this Skill can support process, documentation, and write-back while reducing dependence on single-session memory. It does not automatically guarantee paper quality or correctness.

## Core Capabilities

- **Brainstorming**: 7-round Q&A to confirm paper type, discipline, title, research background, methods, chapter structure
- **End-to-end collaboration**: From topic development, body writing, and figure generation to pre-submission self-review, executed with stage gates
- **Natural expression and information fidelity**: Called “De-AI writing” in the original project; it does not treat polishing as compression and preserves research objects, data scope, method conditions, metric meanings, and conclusion boundaries
- **Figure support**: Python handles reproducible data figures, while Gemini and similar image tools handle prompts for flowcharts, architecture diagrams, and conceptual figures
- **Discipline-specific writing support**: Routed modules for engineering, social sciences, medicine, and law
- **Literature review support**: Integration of English-language search and Chinese literature organization
- **LaTeX template support**: Generate a LaTeX project from a provided institution or journal template; compilability must be verified locally
- **Environment setup and troubleshooting**: Guidance for Miniconda, virtual environments, and plotting dependencies

## Supported Platforms

This Skill uses a directory-based design and provides configuration or installation guidance for the following platforms. Discovery behavior and compatibility still depend on each platform version:

| Platform | Configuration |
|----------|---------------|
| Claude Code | `.claude-plugin/plugin.json` |
| Cursor | `.cursor-plugin/plugin.json` |
| Codex | `.codex/INSTALL.md` |
| OpenCode | `.opencode/INSTALL.md` |
| Gemini CLI | `GEMINI.md` |
| Others | `AGENTS.md` |

## What You Get

By default, Skill outputs are project files — not finished Word documents.

| Output Type | Default Format | Notes |
|---|---|---|
| Written body | `.md` / plain text / `.tex` | Suitable for version control and further processing |
| Chapter files | `chapters/*.md` | One file per chapter |
| LaTeX project | `chapters/*.tex` + `main.tex` | Template-based draft; verify by compiling locally |
| Figure scripts | `.py` | Reproducible figure generation logic |
| Prompt assets | `.md` | Reusable templates for translation, polishing, and de-AI-ification |

## De-AI Writing Boundaries

“De-AI writing” here only means natural expression and information fidelity. It does not mean evading AI detection or academic-integrity review. Unless the user explicitly asks for a shorter version, the Skill should not remove facts, data, limiting conditions, or explanatory sentences. Research objects, data ranges, sample definitions, method conditions, metric meanings, experiment boundaries, conclusion limits, and domain-specific terms should remain intact. Language edits serve natural expression, clear logic, and stable wording.

Paper prose should stay in continuous paragraphs instead of becoming a stack of bullet points, and it should not rely on bold or italic styling to create emphasis. The writing avoids mechanical transitions such as "first", "second", "finally", "in addition", and "in conclusion", and it also avoids empty framing phrases such as "it is worth noting that" or "it should be pointed out that". If the original text is complete and naturally ordered but slightly wordy, the safer edit is a light cleanup rather than cutting useful information for the sake of looking concise.

## Important Boundaries (Read First)

1. The Skill does not automatically generate or write directly to `.docx` files by default.  
2. The Skill does not open Word and apply formatting on your behalf — you will need to copy manually or use a conversion tool.  
3. The Skill can generate plain-text paragraphs ready to paste into Word, but final styling (heading levels, headers/footers, table of contents, reference fields) must be handled in Word.  
4. The rules explicitly prohibit fabricated references, data, and results, but every output still requires verification and every citation must be traceable.
5. The Skill does not replace supervision, peer review, statistical or methodological review, and it does not guarantee acceptance.
6. Do not use the Skill to fabricate evidence or evade academic-integrity checks.

## Installation

### Option 1: Direct Download

Download the repository, extract it, and copy `research-writing-skill/` into your paper writing directory.

### Option 2: Git Clone

```bash
git clone https://github.com/SUCHA-main/research-writing-skill.git
cd research-writing-skill
```

To follow the original project, visit the [upstream repository](https://github.com/Norman-bury/research-writing-skill).

### Platform-specific Installation

- **Codex**: See `.codex/INSTALL.md`
- **OpenCode**: See `.opencode/INSTALL.md`
- **Others**: Place the entire directory in your paper project root

The optional tools have separate dependencies: `scripts/scholar_search.py`
requires `requests`, and `scripts/pdf_parser.py` requires `PyMuPDF`. They are not
required by the skill integrity check; install them in an isolated Python
environment before running the tools.

## Upstream Figure Examples

For data-driven result figures, the Skill can generate Python scripts first, then the figures are rendered locally. The two upstream examples below illustrate output formats such as training curves and metric comparisons; they do not establish reproducible data or evaluation results for this fork.

<p align="center">
  <img src="img/python-miou-comparison.png" alt="Local Python figure example: validation mIoU comparison" width="48%">
  <img src="img/python-training-loss-comparison.png" alt="Local Python figure example: training loss comparison" width="48%">
</p>

For flowcharts, model architecture diagrams, and mechanism figures, `figures-diagram` can first generate the prompt, and then the prompt can be used with Gemini or another image-generation tool. The two images below are prompt-generated examples inherited from upstream.

<p align="center">
  <img src="img/gemini-federated-calibration-diagram.png" alt="Gemini-generated diagram example: federated calibration workflow" width="48%">
  <img src="img/gemini-mask2former-decoder-diagram.png" alt="Gemini-generated diagram example: Mask2Former decoding mechanism" width="48%">
</p>

## Standard Collaboration Workflow (Recommended)

1. **Brainstorming**: Say "I want to write a paper", the Skill will guide you to confirm paper type, title, research background, etc.
2. **Chapter planning**: After confirming chapter structure, the Skill creates framework in `chapters/`
3. **Chapter writing**: Write chapter by chapter, one file per chapter
4. **Figure generation**: When data figures are needed, the Skill generates Python scripts
5. **Self-review**: Use the peer-review skill for pre-submission review
6. **Delivery**: Manually migrate to Word/LaTeX for final formatting

## Quality Gates

Medium or full-paper tasks should go through `skills/paper-orchestration/` first, with a persistent task packet and a capability-use audit in `plan/progress.md`. Introduction and Related Work require `refs/evidence-map.md` or `plan/evidence-map.md` before drafting. Experiment and Results sections require `plan/experiment-protocol.md`, `tables/table-schema.md`, and `figures/data-manifest.md`.

Common checks:

```powershell
powershell -ExecutionPolicy Bypass -File scripts/check_skill_integrity.ps1
powershell -ExecutionPolicy Bypass -File scripts/research_quality_gate.ps1 -ProjectPath <paper-project>
```

## Skill Map

| Scenario | Skill |
|---|---|
| Entry and routing | `skills/using-research-writing/` |
| Medium/full-paper orchestration | `skills/paper-orchestration/` |
| Brainstorming | `skills/brainstorming-research/` |
| Evidence-driven Introduction/Related Work | `skills/evidence-driven-writing/` |
| Chapter writing | `skills/writing-chapters/` |
| Experiment and results planning | `skills/experiment-results-planning/` |
| LaTeX output | `skills/latex-output/` |
| General writing standards | `skills/writing-core/` |
| Humanities / social science writing | `skills/writing-humanities/` |
| Medical / biology writing | `skills/writing-medical/` |
| Law writing | `skills/writing-law/` |
| Literature review | `skills/literature-review/` |
| Translation / polishing / de-AI | `skills/prompts-collection/` |
| Pre-submission self-review | `skills/peer-review/` |
| Statistical analysis | `skills/statistical-analysis/` |
| Python figures | `skills/figures-python/` |
| Flowcharts / architecture diagrams | `skills/figures-diagram/` |
| Environment setup and troubleshooting | `skills/environment-setup/` |

## LaTeX Template Usage

If you have a LaTeX template from your institution or journal:

1. Place template files (`.cls`, `.sty`, `.tex`, etc.) in `latex-templates/` directory
2. Tell the AI "use my LaTeX template"
3. The AI will parse template structure and generate corresponding `.tex` chapter files

See `latex-templates/README.md` for details.

## Delivering Markdown to Word

### Option A: Manual Copy (Default Recommendation)

1. Ask the Skill to output a "plain-text paragraph version" (avoiding Markdown markers)
2. Copy the body in your editor and paste it into Word
3. Apply your institution's template styles in Word (headings, body text, captions)
4. Manually check equations, references, figure/table numbers, and cross-references

### Option B: Pandoc Conversion (Optional)

If Pandoc is installed locally, first confirm that the command is available:

```bash
pandoc --version
```

The simplest conversion is:

```bash
pandoc draft.md -o draft.docx
```

If you already have a Word style template from your institution or journal, use it as a reference document:

```bash
pandoc draft.md --reference-doc=template.docx -o draft.docx
```

Pandoc handles format conversion and style inheritance, but it does not replace final manual checking. After conversion, check heading levels, figure and table numbers, equations, references, headers, footers, and table-of-contents fields.

## FAQ

### Why are the default outputs not Word files?

Research collaboration needs text assets that are trackable, reusable, and version-controlled. Markdown is better suited for iterative work. Word is appropriate for final delivery, so it is handled as the last step.

### Can it generate the final submittable version for me?

It can produce content close to a final draft, but your institution's template, table of contents fields, page numbers, reference fields, and formatting details should still be finalized in Word.

### Will this Skill fabricate references?

The rules explicitly prohibit fabricated references and data, but rules alone do not replace verification. Check each DOI, author, title, year, data source, and cited passage against the original source.

## Repository Structure

```text
research-writing-skill/
├── SKILL.md                    # Main entry (legacy platform compatible)
├── AGENTS.md                   # General agent configuration
├── GEMINI.md                   # Gemini CLI configuration
├── CHANGELOG.md                # Version history
├── .claude-plugin/             # Claude Code configuration
├── .cursor-plugin/             # Cursor configuration
├── .codex/                     # Codex configuration
├── .opencode/                  # OpenCode configuration
├── hooks/                      # Session start scripts
│   ├── session-start
│   ├── hooks.json
│   └── hooks-cursor.json
├── img/                        # README example images
├── skills/                     # Skill modules directory
│   ├── using-research-writing/
│   ├── paper-orchestration/
│   ├── brainstorming-research/
│   ├── evidence-driven-writing/
│   ├── writing-chapters/
│   ├── experiment-results-planning/
│   ├── latex-output/
│   ├── literature-review/
│   ├── figures-python/
│   ├── figures-diagram/
│   ├── peer-review/
│   ├── statistical-analysis/
│   ├── verification/
│   ├── environment-setup/
│   ├── prompts-collection/
│   ├── writing-core/
│   ├── writing-humanities/
│   ├── writing-medical/
│   └── writing-law/
├── latex-templates/            # User LaTeX templates directory
├── modules/                    # Legacy modules (kept for compatibility)
├── templates/                  # Code templates
├── plan-template/              # Plan templates
└── scripts/                    # Utility scripts
```

## Version

- Version: 3.1.0
- Updated: 2026-05-10
- Maintenance goal: Stable workflow, traceable content, deliverable outputs, multi-platform support
