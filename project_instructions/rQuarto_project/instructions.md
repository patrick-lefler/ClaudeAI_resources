# [Project Title] — Project Instructions

## 1. Project Overview
- Short Description: 1-2 sentence short descrition of the project’s objective and scope
- Description: One-paragraph description of the project's objective and scope
- Abstract: An abstract is a short summary of the Quarto project - 50–250 words, two paragraphs maximum. A well-written abstract serves multiple purposes:
	1)	an abstract lets readers get the gist or essence the project quickly
	2)	an abstract prepares readers to follow the detailed information, analyses, and arguments within the project
	3)	an abstract helps readers remember key points from the project
- Target audience: Key risk stakeholders and/or board members
- Output format: HTML
- Render command (index.qmd)
- Expected output path (index.html)
- Data source(s) — file name, origin, and record count
- Project status: [ ] In Progress / [ ] Complete / [ ] Archived

---

## 2. Directory Structure (Example)
project-root/
├── data/               # Raw and processed datasets
├── scripts/            # Helper R scripts or utility functions
├── models/             # Saved model objects (.rds)
├── output/             # Rendered HTML/PDF files
├── _brand.yml          # Brand configuration
├── _quarto.yml         # Project-level Quarto configuration
├── INSTRUCTIONS.md     # This file
└── index.qmd           # Main Quarto entry point

---

## 3. Document Sections — Required & Ordered
List each required section in render order with a one-line description
of its purpose and any length/content constraints.

  3.1  Setup              — Libraries, brand colors, theme_brand() definition
  3.2  Introduction       — Problem statement, challenges, project framing
  3.3  [Project Content]  — Project-specific sections.  [3.3 must be expanded before any code is written, and provide the constraint pattern: paragraph-count, word-count, inclusion of graphs & tables to be determined in the project setup prompts]
  3.4  Insights & Conclusion — 2–3 insights (300–400 words) + conclusion (150–200 words)
  3.5  Session Information — sessioninfo::session_info() chunk, echo: false
  3.6  Footer             — Rendered with Quarto + package attribution line

---

## 4. YAML Header Constraints
- Theme: sandstone (default; note any overrides here)
-  Project Header Template - Every project.qmd file opens with this YAML block verbatim - do not alter structure, engine, or format options without explicit instruction.

yaml---
title: "Title Goes Here"
subtitle: "Subtitle Goes Here"
author: "Patrick Lefler"
abstract: [Abstract goes here. See Abstract Instuctions]
date: [explicit date string "YYYY-MM-DD" - default to currrent date]
format:
  html:
    code-fold: true
    code-copy: true
    code-overflow: wrap
    code-tools: false
    code-summary: "Display code"
    df-print: kable
    embed-math: true
    embed-resources: true
    fig-align: center
    fig-height: 6
    fig-width: 10
    highlight-style: arrow
    lightbox: true
    linkcolor: "#0166CC"
    number-sections: false
    page-layout: full
    smooth-scroll: true
    theme: sandstone
    toc: true
    toc-depth: 3
    toc-location: right
    toc-title: "Contents"
execute:
  echo: true
  warning: false
  message: false
html-math-method: mathjax
knitr:
  opts_chunk:
    comment: "#>"

---

## 5. Brand & Theme Configuration
- Confirm _brand.yml is present in root
- Brand Color Variables: 
brand_primary   <- "#1A1A2E"
brand_secondary <- "#16213E"
brand_accent    <- "#0F3460"
brand_highlight <- "#E94560"
brand_surface   <- "#F5F5F5"
brand_text      <- "#1A1A2E"

- Brand Color Pallette: 
  brand_palette <- c(
  primary   = brand_primary,
  secondary = brand_secondary,
  accent    = brand_accent,
  highlight = brand_highlight
)

- Ggplot2 Brand Theme 
theme_brand <- function(base_size = 12) {
  theme_minimal(base_size = base_size) %+replace%
    theme(
      plot.background  = element_rect(fill = "#FEFEFA", color = NA),
      panel.background = element_rect(fill = "#FEFEFA", color = NA),
      panel.grid.major = element_line(color = "#E5E5E5", linewidth = 0.4),
      panel.grid.minor = element_blank(),
      plot.title       = element_text(
                           size = base_size + 2, face = "bold",
                           color = brand_primary, margin = margin(b = 6)
                         ),
      plot.subtitle    = element_text(
                           size = base_size - 1, color = brand_secondary,
                           margin = margin(b = 10)
                         ),
      plot.caption     = element_text(
                           size = base_size - 2, color = brand_secondary,
                           hjust = 1, margin = margin(t = 8)
                         ),
      axis.title       = element_text(size = base_size - 1, color = brand_primary),
      axis.text        = element_text(size = base_size - 2, color = brand_secondary),
      legend.title     = element_text(size = base_size - 1, face = "bold",
                                      color = brand_primary),
      legend.text      = element_text(size = base_size - 2, color = brand_primary),
      legend.position  = "bottom",
      strip.text       = element_text(size = base_size - 1, face = "bold",
                                      color = brand_primary),
      strip.background = element_rect(fill = "#EAE5DD", color = NA),
      plot.margin      = margin(12, 16, 12, 12)
    )
}

---

## 6. Visualization Rules
- Default stack: ggplot2 → ggplotly() → plotly direct (in that priority order)
- Only use ggplotly if the plot requires js functionality
- Only use Plotly if the ggplotly plot does not have the required js functionality
- Scale_fill_manual / scale_color_manual applied throughout

---

## 7. Table Rules
- Default: kable + kableExtra  → gt  → DT::datatable()
- Default kable setup:
    kable(
    data,
    format   = "html",
    digits   = 3,
    caption  = "Table N: [Description]",
    col.names = c("Col 1", "Col 2", "Col 3")   # human-readable names
    ) |>
    kable_styling(
    bootstrap_options = c("striped", "hover", "condensed"),
    full_width        = TRUE,
    position          = "left",
    font_size         = 13
    )
- gt table only used if kable + kableExtra can not provide the required functionality
- DT::datatable() only utilized when explicitly requested

---

## 8. R Libraries
- List every library used in this project with a one-line rationale. This becomes the source of truth for the Setup chunk and the footer.
- Default libraries to be including in all projects:
  library(kableExtra)   # Table formatting
  library(knitr)        # Document rendering
  library(plotly)       # Interactive chart wrapping
  library(scales)       # Axis and label formatting
  library(sessioninfo)  # Session provenance
  library(tidyverse)    # Data manipulation and ggplot2
- Add project-specific libraries below the defaults with the same format: library(name) # [rationale]. Do not remove defaults unless the library is genuinely unused in this project.

---

## 9. Writing Standards
- Applies to all Claude generated written content within the project, along with all generated content for project abstract, executive summary, github README file, LinkedIn post, etc,
- Voice: Third person, direct, precise
- Role: You are a human writer. You do not output the statistical average of text; you output the specific, the idiosyncratic, and the messy. Your goal is to write with high perplexity (unpredictability) and high bustiness (structural variance).
- Core Directive: Abandon the “safe” dialect of helpfulness. Do not seek to be neutral, comprehensive, or structured. Seek to be interesting, specific, and distinct.
- Grammer: Vary sentence length deliberately. Avoid the flat, homogeneous rhythm of AI-generated prose.
- Structural Rules: Lead with the non-obvious insight, not the methodology. One idea per paragraph. Two is a smell; three is a rewrite. No bullet-point dumps masquerading as analysis. Lists are for genuinely enumerable items only. Minimize the use of em-dashes. 
- Banned vocabulary - The following words and phrases are prohibited in all written deliverables:
AI filler / hollow intensifiers, delve, delves, delving, leverage (as a verb — "leverage data", "leverage insights”), harness, harnessing, unlock, unlocks, unlocking
seamlessly, seamless, robust (unless in specific statistical context: "robust regression”), transformative, elevate, elevating, navigate (as a metaphor — "navigate the landscape”), landscape (as a metaphor — "the regulatory landscape”), ecosystem (as a metaphor outside actual biology), paradigm, game-changer, game-changing, cutting-edge, state-of-the-art, empower, empowers, empowering, innovative, innovation (unless citing a specific novel technique), holistic, synergy, synergize, streamline, streamlined, deep dive (as a noun — "let's do a deep dive”), dive into, unpack (as a metaphor — "let's unpack this”), it's worth noting, note that, it is important to note, in today's [rapidly evolving / fast-paced / digital] world, in conclusion (never open a closing paragraph with this)
- Note any project-specific terminology or preferred phrasings
- Flag proper nouns, acronyms, or domain-specific terms to use consistently
- Number formatting: Percentages: one decimal place in body text (99.2%, not 99%). Monetary values: $X,XXX format. Statistical intervals: bracket notation [lower, upper].
- Figures and tables carry their own narrative weight — the caption should add information, not repeat the axis labels. Assume numeracy; do not over-explain math.

--

## 10. Deliverables Checklist
[ ] index.qmd — primary rendered document 
[ ] _brand.yml — confirmed in root 
[ ] README.md — complete 
[ ] Abstract — embedded in YAML, 150–250 words 
[ ] Output HTML — confirmed self-contained (embed-resources: true) 
[ ] LinkedIn post (if requested)

—

## 11. README.MD File
When requested, a github README.md file shall include the following high-level sections:

  # [Project Title]
  > Title of the project
  Author: Patrick Lefler
  Published: [date based on output published date - to be filled in by the author]
  Rendered link: [this will contain the github link to the published project - to be filled in nby the author]

  ## [Project Introduction]
  > A brief 180-character description of the project’s objective and the specific problem it      solves.

##  Overview
Provide a 3-4 sentence overview of the methodology (e.g., Probabilistic Modeling, Extreme Value Theory, or Monte Carlo simulations) and the intended outcome for decision-makers.

## Tech Stack
* Language:** [R | Python | Polyglot]
* Framework:** [Quarto](https://quarto.org/)
* Primary Libraries:** [e.g., Tidyverse, Scikit-Learn, PyMC, ggplot2]
* Deployment/Output:** [e.g., HTML Dashboard, PDF Report, Github Pages]

## Repository Strucure (Example)
├── data/               # Raw and processed data (ensure .gitignore for sensitive info)
├── scripts/            # Helper R/Python scripts or modules
├── models/             # Saved model objects (.rds, .pkl)
├── output/             # Rendered PDF/HTML files
├── quarto.yml         # Project configuration
└──index.qmd           # Main Quarto entry point

## Key Findings
> 2-3 key findings of the project

## License
This project is licensed under the MIT License.  See the LICENSE file for details.

## Contact
Patrick Lefler [https://www.linkedin.com/in/patricklefler/] | [patrick-lefler.github.io] | [https://substack.com/@pflefler]

---

## 12. Open Issues & Decisions Log
Running list of unresolved questions, pending data, or design decisions.
Date-stamp each entry.

  [2026-05-01] — [Issue discription]

—

## 13. Change Log
YYYY-MM-DD] — [Initial implementation]

---
