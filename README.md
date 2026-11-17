# AI Agent Development Benchmark

## Project Overview

**The Wyrm Hunters** is a benchmark project for evaluating AI agents
designed to assist with software development.

The project provides a realistic website brief and a set of supporting
specifications. It is intended to test how well different agentic AI
systems can interpret requirements, organize content, plan
implementation work, and build a coherent web application.

This is not primarily a benchmark of coding speed. The focus is on how
effectively an agent can work with an incomplete but structured product
brief and turn it into a consistent implementation.

## What This Project Evaluates

The benchmark focuses on several areas:

-   **Content generation:** creating website copy that follows the
    brief, maintains a consistent tone, and fits the intended audience. 
-   **Content organization:** structuring information into appropriate
    pages, sections, components, and data models.
-   **Implementation planning:** breaking feature requests into clear,
    practical implementation plans with dependencies and priorities.
-   **Requirements interpretation:** understanding the project
    documentation, identifying constraints, and avoiding unsupported
    assumptions.
-   **Consistency:** keeping the visual identity, terminology, content,
    and technical decisions aligned across the application.
-   **Feature implementation:** translating requirements and
    implementation plans into working frontend functionality.

The project can be used to compare different agents, models, prompts,
and development workflows.

## Scope and Benchmark Approach

The initial benchmark uses prepared visual assets rather than requiring
agents to generate images or icons.

This keeps the first evaluation focused on software-development tasks:
interpreting specifications, generating and organizing content, planning
features, and implementing the website. It also reduces variability
caused by image-generation models and makes comparisons between coding
agents more meaningful.

AI-generated visual content is a separate potential benchmark task. It
can be introduced later to evaluate image and icon generation, prompt
interpretation, visual consistency, and how generated assets are
integrated into the application.

## Project Documentation

The repository contains the following project specifications:

`technologies.md` - Technical requirements, recommended technologies, architecture considerations, and implementation guidelines.

`description.md` - The website brief written from the client's perspective. Describes the website, its purpose, content, and required sections.

`description-visual-identity.md` - The visual identity specification, including the color palette and service icon style.

`asset-preparation-plan-specification.md` - Requirements for assets preparationd and outputs

### Visual Asset Specifications

The following files describe the visual assets used by the website:

  -----------------------------------------------------------------------
  File                                Description
  ----------------------------------- -----------------------------------
  `description-logo.md`               Visual direction and requirements
                                      for the guild logo.

  `description-hunters.md`            Visual descriptions and art
                                      direction for the guild's hunters.

  `description-clients.md`            Visual descriptions and art
                                      direction for client testimonial
                                      portraits.
  -----------------------------------------------------------------------

These documents define the intended appearance and help keep visual
assets consistent with the overall identity of The Wyrm Hunters.

## Suggested Benchmark Workflow

An agent can be evaluated through a sequence of tasks:

1.  Read and interpret all project documentation.
2.  Summarize the requirements and identify any ambiguities or conflicts.
3.  Propose a website architecture and organize the required content.
4.  Create an implementation plan for the main website and its features.
5.  Analyze the source visual assets in raw-assets/ and prepare an asset-preparation plan. The directory contains source portraits of clients and hunters, the guild logo, the favicon source image, and a composite image containing the five service icons. The agent should inspect the actual files, identify the required transformations, document the proposed output assets, and submit the plan for user review before modifying the files. See  asset-preparation-plan-specification.md for the expected plan structure and asset-specific requirements.
6.  Implement the website according to the specifications.
7.  Review the result for functional completeness, responsive behavior,
    accessibility, and consistency with the brief.
8.  Record issues, assumptions, and deviations from the requirements.

For a fair comparison, agents should receive the same documentation and
task instructions. Evaluation criteria and any additional constraints
should also remain consistent.

## Project Status

This repository is intended to serve as a reusable benchmark scenario.
The documentation defines the target website and its constraints;
individual benchmark runs can use different AI agents and workflows to
produce and evaluate implementations.
