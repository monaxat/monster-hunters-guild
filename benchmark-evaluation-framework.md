# AI Agent Benchmark --- Evaluation Framework

## Purpose

This document describes the **ideal evaluation framework** for the AI
agent development benchmark.

It defines what a comprehensive benchmark should evaluate and what a
mature implementation should aim to measure. It is a target model, not a
finalized measurement specification.

The practical methodology for collecting, validating, normalizing, and
storing metrics should be designed separately. That work requires
additional decisions about instrumentation, task boundaries, human time
tracking, issue classification, cost attribution, and evaluation
procedures.

## Evaluation Principles

The benchmark should evaluate the overall value of an agent's work, not
just how quickly it produces code or how many tokens it consumes.

A useful evaluation should:

-   Measure the quality and completeness of the delivered result.
-   Account for human effort required to supervise, review, and repair
    the work.
-   Capture the time and financial cost of reaching an accepted result.
-   Distinguish minor defects from issues requiring experienced
    specialists.
-   Evaluate how independently and consistently an agent can work.
-   Consider whether the result can be maintained and extended.
-   Use consistent tasks and acceptance criteria when comparing agents.

No single metric should determine the overall ranking. Results should
first be presented as a multidimensional scorecard. Any aggregated score
should be introduced only after the weighting methodology has been
defined and justified.

## 1. Human Involvement

Measures the amount of human effort required to guide an agent and turn
its output into an accepted result.

Potential metrics:

-   **Active Human Time:** Time spent actively interacting with the
    agent or working on its output.
-   **Review Time:** Time spent inspecting and validating the result.
-   **Correction Time:** Human time spent correcting or completing the
    result.
-   **Intervention Count:** Number of times a person must intervene to
    unblock, redirect, or correct the agent.
-   **Clarification Count:** Number of times requirements or
    instructions must be clarified or repeated.
-   **Handoff Effort:** Effort required to understand the agent's
    current state and continue its work.

Human waiting time and agent execution time should be distinguished from
active human work.

## 2. Issues and Resolution Complexity

Measures the defects, omissions, and other problems discovered during or
after an agent's work.

Issues should be classified by severity:

  -----------------------------------------------------------------------
  Level                   Severity                Description
  ----------------------- ----------------------- -----------------------
  1                       Minor                   Cosmetic or negligible
                                                  defect with little
                                                  practical impact.

  2                       Low                     Straightforward issue
                                                  with a limited scope
                                                  and simple resolution.

  3                       Medium                  Issue requiring
                                                  codebase understanding
                                                  or non-trivial
                                                  debugging.

  4                       High                    Complex issue requiring
                                                  experienced engineering
                                                  judgment or specialist
                                                  knowledge.

  5                       Critical                Severe architectural,
                                                  security,
                                                  data-integrity, or
                                                  operational problem.
  -----------------------------------------------------------------------

Potential metrics:

-   **Issue Count by Severity:** Number of issues in each severity
    category.
-   **Weighted Issue Cost:** Combined issue impact, accounting for
    severity and resolution effort.
-   **Diagnosis Time:** Time required to identify the cause of an issue.
-   **Resolution Time:** Time required to resolve an issue and verify
    the fix.
-   **Required Expertise:** Approximate skill level needed to diagnose
    and resolve the issue.
-   **Regression Count:** Number of new issues introduced while fixing
    existing ones.
-   **Recurring Issue Rate:** Frequency with which the same class of
    issue appears across tasks or runs.

A raw issue count is insufficient. A large number of trivial issues may
be less costly than one architectural defect that requires a senior
specialist.

## 3. Execution Time

Measures how long the agent takes to complete work and how that time is
distributed across the workflow.

Potential metrics:

-   **Planning Time:** Time spent analyzing requirements and preparing
    an implementation plan.
-   **Implementation Time:** Time spent producing the implementation.
-   **Testing Time:** Time spent running checks and validating the
    result.
-   **Fixing Time:** Time spent addressing discovered defects.
-   **Agent Active Time:** Time during which the agent is actively
    processing the task.
-   **Total Elapsed Time:** Wall-clock time from task start to accepted
    completion.
-   **Time per Accepted Task:** Time required to deliver a task that
    satisfies its acceptance criteria.

Elapsed time and active processing time should be reported separately.
Parallel work, tool latency, and human review can otherwise make
comparisons misleading.

## 4. Financial Cost and Resource Consumption

Measures the direct and indirect resources consumed to produce an
accepted result.

Potential metrics:

-   **Input Tokens:** Tokens submitted to the model.
-   **Output Tokens:** Tokens generated by the model.
-   **Cached Tokens:** Tokens served through provider caching, where
    applicable.
-   **Tool Calls:** Number and cost of external tool operations.
-   **API Cost:** Direct model usage cost.
-   **Additional Service Cost:** Cost of external services or
    infrastructure used by the agent.
-   **Retry and Rework Cost:** Additional cost caused by failed
    attempts, corrections, and repeated execution.
-   **Cost per Accepted Task:** Total attributable cost of delivering an
    accepted task.

Prices, model versions, and provider billing rules should be recorded
because they can change over time.

## 5. Output Quality

Measures whether the delivered result satisfies the requirements and is
useful in practice.

Potential dimensions:

-   **Requirement Coverage:** How completely the implementation
    addresses the stated requirements.
-   **Functional Correctness:** Whether implemented features behave as
    expected.
-   **Content Quality:** Accuracy, clarity, relevance, tone, and
    consistency of generated content.
-   **Design Consistency:** Compliance with the visual identity and
    interface specifications.
-   **Code Quality:** Readability, structure, modularity, and adherence
    to project conventions.
-   **Accessibility:** Compliance with the project's accessibility
    expectations.
-   **Responsive Quality:** Correct behavior across supported screen
    sizes and devices.
-   **Test Coverage and Reliability:** Quality of automated checks and
    confidence in the implementation.

Quality should be evaluated against explicit acceptance criteria.
Automated checks can verify objective properties, while expert or human
review may be needed for design, content, and maintainability.

## 6. Autonomy

Measures how independently an agent can complete work without
sacrificing correctness.

Potential metrics:

-   **Autonomous Completion Rate:** Share of tasks completed without
    human intervention.
-   **Self-Detection Rate:** Share of the agent's own defects that it
    identifies before submission.
-   **Self-Correction Rate:** Share of detected defects that it
    successfully resolves independently.
-   **Clarification Quality:** Whether the agent asks useful questions
    when requirements are genuinely ambiguous.
-   **Decision Quality:** Whether the agent makes reasonable decisions
    within the authority and constraints given to it.
-   **Unjustified Assumption Count:** Number of unsupported assumptions
    that affect the implementation.

Autonomy should not reward an agent for silently guessing, ignoring
uncertainty, or making unauthorized changes.

## 7. Maintainability and Extensibility

Measures the long-term usefulness of the produced implementation.

Potential dimensions:

-   **Architectural Alignment:** Compliance with the agreed architecture
    and technical constraints.
-   **Modularity:** Separation of concerns and clarity of component
    boundaries.
-   **Duplication:** Unnecessary repetition in code or content.
-   **Technical Debt:** Shortcuts or design decisions likely to increase
    future maintenance effort.
-   **Extensibility:** How easily the implementation can accommodate new
    requirements.
-   **Handoff Readiness:** How easily another developer or agent can
    understand and continue the work.

A useful way to evaluate maintainability is to assign a follow-up change
to a different agent or developer and observe the effort and issues
involved.

## 8. Consistency

Measures whether the agent preserves decisions and conventions
throughout the project.

Potential dimensions:

-   **Requirements Consistency:** Whether implementation decisions
    remain aligned with the project brief.
-   **Visual Consistency:** Whether layouts, colors, typography, and
    visual assets follow the same design system.
-   **Content Consistency:** Whether terminology, tone, facts, and
    descriptions remain coherent across sections.
-   **Technical Consistency:** Whether the same architectural and coding
    conventions are applied throughout the codebase.
-   **Cross-Task Consistency:** Whether later tasks preserve decisions
    made during earlier tasks unless a change is justified.

## 9. Reproducibility

Measures how stable the agent's performance is across repeated runs.

Potential metrics:

-   **Quality Variance:** Variation in output quality across repeated
    executions of the same task.
-   **Time Variance:** Variation in execution time.
-   **Cost Variance:** Variation in resource consumption and financial
    cost.
-   **Completion Variance:** Variation in whether the agent successfully
    completes the task.
-   **Behavioral Consistency:** Whether the agent follows comparable
    reasoning and implementation patterns under equivalent conditions.

This category is particularly relevant for systems with
non-deterministic model behavior or multi-agent orchestration.

## 10. Overall Economic Efficiency

The benchmark should ultimately help estimate the real cost of obtaining
an accepted result.

One possible derived metric is **Total Cost of Ownership per Accepted
Task (TCO)**:

`TCO = API Cost + Tool Cost + Additional Service Cost + Human Labor Cost`

Human labor cost can be estimated as:

`Human Labor Cost = Σ (Time spent by each role × Hourly rate for that role)`

Different roles may have different rates. For example, a task requiring
three hours of senior engineering review should not be treated as
equivalent to three hours of routine junior-level review.

TCO should be considered alongside quality, completion rate, and risk. A
low-cost result that fails acceptance criteria is not an efficient
result.

## 11. Recommended Evaluation Priorities

A mature benchmark may eventually cover all categories. The following
priorities provide a practical direction for development.

  -----------------------------------------------------------------------
  Category                Core metrics            Priority
  ----------------------- ----------------------- -----------------------
  Human Involvement       Active human time,      Essential
                          review time,            
                          intervention count      

  Issues                  Issue count by          Essential
                          severity, resolution    
                          time, required          
                          expertise               

  Execution Time          Total elapsed time,     Essential
                          time per task,          
                          implementation time     

  Financial Cost          Token usage, API cost,  Essential
                          cost per accepted task  

  Output Quality          Requirement coverage,   Essential
                          functional correctness  

  Autonomy                Autonomous completion   Recommended
                          rate, self-correction   

  Maintainability         Code quality,           Recommended
                          architectural           
                          alignment,              
                          extensibility           

  Consistency             Design, content, and    Recommended
                          technical consistency   

  Reproducibility         Quality, time, and cost Later stage
                          variance across runs    

  Economic Efficiency     TCO per accepted task   Later stage
  -----------------------------------------------------------------------

## 12. Relationship to the Measurement Methodology

This framework describes **what should be evaluated**. It does not
prescribe exactly **how data must be collected**.

A separate measurement specification should define:

-   Task lifecycle and precise start/end boundaries.
-   How human active time and waiting time are recorded.
-   How interventions and clarifications are counted.
-   Issue reporting, severity assignment, and resolution tracking.
-   How required expertise is classified.
-   How token usage, tool calls, and financial costs are collected.
-   How quality criteria are scored and who evaluates them.
-   How repeated runs and environmental differences are handled.
-   How results are stored, aggregated, and compared.
-   How missing, estimated, or unverifiable measurements are reported.

The measurement methodology should be designed before using these
metrics for formal agent rankings. Until then, this document should be
treated as the target evaluation model for the benchmark.
