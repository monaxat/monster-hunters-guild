# Asset Preparation Plan --- Specification

## Purpose

This document defines the expected contents of an AI-generated
asset-preparation plan for The Wyrm Hunters website.

The agent must inspect the source files in `raw-assets/`, determine what
needs to be changed, and propose a clear, actionable plan. The plan must
be presented to the user for review and approval **before any source
assets are modified or final assets are generated**.

This document defines the expected analysis and deliverables. It does
not prescribe every implementation detail in advance: the agent should
inspect the actual files and recommend suitable dimensions, formats,
quality settings, and processing steps based on their intended use.

## Source Asset Inventory

The `raw-assets/` directory contains the original visual assets, grouped by type:
  
`clients/` - Client testimonial portraits. - Inspect, optimize, and convert portraits to WebP.

`hunters/` - Guild hunter portraits  Inspect, optimize, and convert portraits to WebP.

`logo/`- Guild logo source image, currently 1024px - Determine suitable display dimensions,  resize, and convert to WebP.

`favicon/` - Favicon source image in  PNG format . Remove unnecessary whitespace, resize, and generate appropriate favicon files.

`icons/` - One PNG image containing all five service icons. Separate the icons into individual files, identify each icon, optimize, and convert to WebP.

-----------------------------------------------------------------------

The agent must verify the actual directory and file names rather than
assume that the inventory above exactly matches the filesystem. If files
are missing, duplicated, unexpected, or stored in a different structure,
the plan must report that.

## Expected Plan Structure

The generated plan should be clear enough for a developer or another
agent to execute without repeating the initial investigation.

### 1. Source Inventory

For every source file, record:

-   Current path and filename.
-   File format.
-   Pixel dimensions.
-   Aspect ratio.
-   File size.
-   Transparency/alpha channel, if present.
-   Intended role on the website.
-   Visible issues or uncertainty.

Group the inventory by asset category. Do not infer image properties
from filenames alone.

### 2. Proposed Transformations

For each source file or logical asset, specify:

-   What needs to be changed and why.
-   Proposed output format.
-   Proposed output dimensions or size variants.
-   Proposed quality/compression settings, where relevant.
-   Whether transparency must be preserved.
-   Proposed output path and filename.
-   Any manual review or user decision required.

Avoid arbitrary resizing or recompression. Recommendations should be
based on actual source dimensions and intended display contexts.

### 3. Asset-Specific Requirements

#### Client and hunter portraits

-   Inspect all portraits in the respective source folders.
-   Preserve the original composition and square aspect ratio.
-   Convert the portraits to WebP.
-   Preserve sufficient visual quality for testimonial cards, team
    sections, and larger responsive layouts where applicable.
-   Recommend dimensions based on actual source sizes and expected
    display sizes.
-   Do not crop faces or alter the artwork unless the source itself
    requires correction and the plan explicitly identifies it.

#### Guild logo

-   Inspect the current logo source, expected to be 1024 px.
-   Determine appropriate display dimensions for the website,
    considering header, footer, and other possible uses.
-   Recommend one optimized asset or multiple variants if the use cases
    justify them.
-   Convert to WebP while preserving transparency if the source contains
    it.
-   Ensure downscaling does not make important heraldic details
    unreadable.
-   Do not redesign or otherwise alter the logo.

#### Favicon

-   Inspect the PNG source and identify unnecessary transparent or blank
    margins around the actual emblem.
-   Recommend a crop that keeps the emblem visually centered and
    preserves its intended shape.
-   Determine suitable favicon dimensions and output formats.
-   Include conventional favicon deliverables needed by the website,
    such as a multi-size `favicon.ico` and/or appropriately sized PNG
    files. Recommend additional platform-specific assets only when
    justified.
-   Check that the result remains recognizable at small sizes,
    especially 16×16 and 32×32 pixels.
-   Do not stretch the image or crop important parts of the emblem.

#### Service icons

-   Inspect the composite PNG containing five icons.
-   Propose how to split it into five separate image files.
-   Identify each icon and map it to the corresponding service category
    using the visual identity documentation:
    -   Monster Elimination
    -   Escort & Protection
    -   Tracking & Investigation
    -   Relic Recovery
    -   Emergency Response
-   Specify the crop boundaries or explain how they will be determined.
-   Check whether the source contains separators, margins, shadows, or a
    shared background that should be excluded or preserved.
-   Ensure all five output icons have consistent canvas dimensions,
    visual scale, and alignment.
-   Preserve transparency where appropriate.
-   Optimize dimensions for their actual UI usage and convert the
    individual icons to WebP.
-   If the icon-to-category mapping or crop boundaries are ambiguous,
    flag the uncertainty for user review instead of guessing.

### 4. Proposed Output Structure

Recommend a clean output directory structure. For example:

``` text
public/
  assets/
    portraits/
      clients/
      hunters/
    branding/
      logo.webp
    icons/
      monster-elimination.webp
      escort-protection.webp
      tracking-investigation.webp
      relic-recovery.webp
      emergency-response.webp
```

Favicon files may be placed in the public root or another location
appropriate to the chosen framework and build configuration.

The example is a proposal, not a mandatory path. The agent should align
the final structure with the project architecture described in
`technologies.md`.

### 5. Validation Checklist

The plan must state how the prepared assets will be checked:

-   All expected source assets are accounted for.
-   Original files remain unchanged.
-   Output files open correctly and use the intended formats.
-   Image dimensions and aspect ratios are correct.
-   Transparency is preserved where required.
-   Portraits and logo retain sufficient visual quality.
-   Favicon is centered, properly cropped, and recognizable at small
    sizes.
-   All five service icons are separated and correctly identified.
-   Icon dimensions, visual scale, and alignment are consistent.
-   File sizes are appropriate for web delivery.
-   Output filenames and paths are consistent and predictable.

### 6. Risks, Assumptions, and Questions

The agent must explicitly list:

-   Uncertain source files or asset mappings.
-   Proposed crops that may remove meaningful content.
-   Format limitations or transparency concerns.
-   Decisions that affect the website implementation.
-   Questions that require user input.

Do not silently make subjective or destructive decisions.

## Review and Approval Workflow

1.  Inspect `raw-assets/` and the relevant project documentation.
2.  Produce the source inventory.
3.  Analyze each asset group and identify required transformations.
4.  Prepare the complete asset-preparation plan, including proposed
    output paths.
5.  Present the plan to the user, highlighting assumptions and decisions
    that need approval.
6.  Wait for user review and approval.
7.  Apply the approved transformations.
8.  Validate the generated files against the approved plan.
9.  Report the final output paths, dimensions, formats, file sizes, and
    any deviations.

The agent must not overwrite or delete original source assets. Prepared
files should be written to a separate output location.

## Expected Final Deliverables

After approval and execution, the agent should provide:

-   The approved asset-preparation plan.
-   A mapping from every source file to its generated output file(s).
-   The prepared optimized assets.
-   A short validation report with dimensions, formats, and file sizes.
-   A list of unresolved issues or deviations from the approved plan.

## Scope Boundaries

This task is about analyzing, preparing, optimizing, and organizing
existing visual assets.

It does not include generating new artwork, redesigning the logo,
changing character appearances, or inventing replacement icons. Those
activities should be handled as separate tasks and evaluated
independently.
