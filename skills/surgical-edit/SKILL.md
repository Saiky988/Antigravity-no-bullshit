Surgical Edit
This skill governs how to make small, precise, controlled changes to an existing codebase. It complements codebase-first investigation, task discipline, anti-AI-code patterns, human UI principles, and natural writing guidelines.
The core idea is simple: change exactly what is necessary to accomplish the task, while preserving everything that does not need to change.
The purpose is not to minimize line count at all costs. A surgical edit can involve multiple files or a substantial change when the task genuinely requires it. The goal is controlled change, not artificially small diffs.
1.  Identify the exact change
Before editing, determine:
•  What behavior must change
•  What behavior must remain unchanged
•  Where that behavior is implemented
•  What code actually needs modification
•  What files are directly involved
Do not start by rewriting the surrounding system.
2.  Find the narrowest correct integration point
Prefer the smallest existing integration point that naturally owns the behavior.
•  Existing component → modify the component
•  Existing handler → modify the handler
•  Existing service → modify the service
•  Existing utility → extend the utility
•  Existing config → update the config
Do not create a new layer simply because it feels cleaner.
3.  Preserve surrounding code
When changing one part of a file, leave unrelated code alone. Do not automatically:
•  Reorder imports
•  Rename nearby variables
•  Reformat the whole file
•  Rewrite adjacent functions
•  Change unrelated comments
•  Restructure surrounding logic
•  Modernize syntax
•  Replace working patterns
A focused task should produce a focused change.
4.  Do not rewrite to implement
If an existing function is mostly correct and only one part needs changing, modify that part.
Bad approach: Rewrite the entire function, rewrite related helpers, reorganize the file, introduce abstraction, update imports, "clean up" everything.
Preferred: Identify the required change, modify the required logic, preserve everything else.
5.  Preserve existing control flow when possible
Do not replace working control flow without a reason. For example, do not turn a simple if (...) into a new abstraction, state machine, helper chain, or strategy pattern just because it appears more structured. Change the existing flow if it already fits the task.
6.  Preserve existing APIs
Do not change function signatures, route paths, request formats, response formats, component props, exported names, event names, or database contracts unless the task requires the API change.
If an API change is required, identify the affected callers and update them deliberately. Do not silently break consumers.
7.  Preserve data flow
Understand the existing data flow before modifying it. When possible, keep:
input → existing processing → existing state/data → existing output
and modify only the necessary step. Do not introduce a second source of truth for a value that already has one.
8. Avoid duplicate implementations
Before adding a new function, helper, component, service, or utility, check whether the repository already has something that performs the same job. Prefer modifying or reusing the existing implementation when appropriate.
Do not create formatDate(), formatDateValue(), formatDateString(), and dateFormatter() for behavior that already has one established implementation.
9. Do not duplicate state
If existing state already represents the required information, use it. Avoid adding originalValue, displayValue, cachedValue, derivedValue, or temporaryValue when the new state can be derived from existing data. Additional state should have a real reason to exist.
10. Keep patches local
If the requested behavior belongs to one module, prefer keeping the implementation within that module. Do not spread a small change across unrelated utilities, global configuration, shared components, multiple services, or new infrastructure unless the existing architecture genuinely requires it.
11. Respect local formatting
Do not cause unrelated formatting churn. If the repository uses semicolons, no semicolons, single quotes, double quotes, specific indentation, or specific import ordering—follow it. Do not reformat an entire file to satisfy personal preference.
12. Avoid opportunistic cleanup
While editing, you may notice ugly code, old naming, duplicated logic, unused comments, outdated syntax, possible refactors, or unrelated bugs. Do not automatically fix them. Ask: Is this necessary for the requested change? If not, leave it alone.
13. Do not mix unrelated refactors
Avoid commits or diffs that contain requested feature plus cleanup, renaming, formatting, dependency updates, and architecture changes unless those changes are actually required. Keeping changes focused makes them easier to review, debug, revert, and understand.
14. Change the minimum behavior surface
Consider how many parts of the system your change affects. Prefer modifying one component over touching component → shared utility → global state → API → configuration when both can correctly solve the task. The fewer unrelated boundaries crossed, the lower the regression risk.
15. Be careful with shared code
Shared utilities and components have a larger blast radius. Before modifying them, check who uses them, whether behavior is relied upon elsewhere, whether the change can remain local, and whether a new optional behavior is actually necessary. Do not change global behavior to solve a local problem unless intended.
16. Avoid unnecessary compatibility layers
Do not add fallback code, aliases, wrappers, adapters, or compatibility shims unless there is a real compatibility requirement. Avoid wrapping newFunction(...) around oldFunction(...) only because changing the original call site feels inconvenient. If the old interface should actually remain supported, then a compatibility layer may be appropriate.
17. Preserve existing behavior by default
Treat existing behavior as intentional unless the task explicitly changes it. When adding a feature, existing behavior + new requested behavior is usually preferable to replace existing behavior + new behavior + new architecture. Do not "improve" behavior that was not part of the request.
18. Make edits in dependency order
When a change spans multiple files, make the dependency chain clear. For example:
type / contract → implementation → caller → UI
or:
database → service → route → frontend
Do not randomly edit files and discover integration problems afterward.
19. Verify immediately after meaningful changes
After a significant edit: inspect the changed code, check syntax and types if applicable, run the relevant test or build check, verify the requested behavior, and check for accidental changes. Do not wait until the end of a large chain of edits to discover a simple mistake.
20. Review the diff
Before considering the task finished, review what actually changed. Look for:
•  Unrelated file changes
•  Accidental formatting
•  Deleted behavior
•  Renamed symbols
•  Unnecessary imports
•  Unused variables
•  Debug code
•  Temporary comments
•  Duplicated logic
•  Unexpected API changes
•  Generated files changed accidentally
The diff is often more informative than the final result alone.
21. Prefer reversible changes
When two correct approaches exist, prefer the one that is easier to understand, easier to test, easier to revert, and less invasive. Do not introduce irreversible architectural changes for a small requirement.
22. Don't optimize prematurely
Do not introduce caching, memoization, batching, concurrency, lazy loading, custom data structures, or other optimization techniques unless the task requires them or the existing implementation clearly has a measured or known performance problem. Correctness and integration come first.
23. Don't make a change broader because it is technically possible
The fact that you can improve something does not mean you should.
•  Fixing one button does not require redesigning the page
•  Adding one endpoint does not require rewriting the API layer
•  Fixing one query does not require replacing the database abstraction
•  Adding one field does not require migrating every related model
•  Changing one CSS rule does not require redesigning the stylesheet
Keep the blast radius proportional to the requirement.
24. Know when to stop
Once the requested behavior works, required integration is complete, relevant checks pass, no regression was introduced, and the diff is explainable—stop. Do not continue modifying code simply because more improvements are possible.
Change Decision
Before modifying a piece of code, classify the change:
•  Required: Directly necessary to complete the requested task. Do it.
•  Necessary: Not explicitly stated, but required for the requested behavior to work correctly or safely. Do it.
•  Supporting: A small related change needed because of an existing dependency or integration boundary. Do it when justified.
•  Optional: Would improve the code but is not needed for the task. Do not silently include it.
•  Unrelated: Does not contribute to the requested result. Leave it alone.
When a Larger Change Is Correct
Do not confuse "surgical" with "tiny." A larger change is appropriate when:
•  The existing implementation cannot support the requirement
•  The architecture genuinely requires coordinated changes
•  An API contract must change
•  A migration is required
•  A security or correctness issue affects multiple callers
•  The feature naturally spans multiple modules
•  Preserving the old implementation would create duplicated or broken behavior
When a larger change is necessary:
1.  Explain why the broader change is required
2.  Identify the affected boundaries
3.  Change only those boundaries
4.  Preserve unrelated behavior
5.  Verify the complete path
The goal is controlled scope, not arbitrary minimalism.
----
Special Cases
Existing bug discovered
If an unrelated bug is discovered: do not automatically fix it. Mention it if it materially affects the requested task. Fix it only if leaving it would break the requested behavior or your own change. Do not turn a feature task into a bug-fixing session.
Existing bad code
Do not refactor bad code merely because you noticed it. If the requested task can safely be completed without restructuring it, leave it alone. If the bad structure directly prevents the requested change, make the smallest structural adjustment that solves the problem.
Generated files
If a generated file changes as a consequence of editing its source, follow the repository's existing generation workflow. Do not manually edit generated output unless the project expects that. Avoid unrelated generated-file churn.
Formatting
Do not use formatting tools in a way that creates large unrelated diffs. If formatting is required by the repository's workflow, run it appropriately. Otherwise, keep formatting changes local.
Surgical Edit Workflow
Locate → Inspect → Identify integration point → Define exact change
→ Edit locally → Verify → Review diff → Stop
At each step, ask: Can this be done without changing anything else? If yes, prefer that approach.
Self-Review
Before finishing, ask:
•  Did I modify only code relevant to the task?
•  Did I preserve unrelated behavior?
•  Did I preserve existing APIs and contracts?
•  Did I reuse existing implementations where appropriate?
•  Did I avoid duplicate state and logic?
•  Did I avoid unnecessary abstractions?
•  Did I avoid opportunistic cleanup?
•  Did I avoid formatting churn?
•  Did I avoid changing shared behavior unnecessarily?
•  Did I verify the actual changed path?
•  Did I inspect the final diff?
•  Can I explain why every changed line exists?
•  If the change is large, can I explain why the larger scope was necessary?
•  Is there anything in the diff that I would remove if reviewing someone else's PR?
If a changed line cannot be justified by the task, its dependencies, or verification, reconsider it.
Important constraints
This skill must not be interpreted as:
•  Always producing tiny diffs
•  Avoiding multiple-file changes
•  Refusing necessary refactors
•  Refusing architecture changes when required
•  Preserving broken behavior at all costs
•  Avoiding tests
•  Avoiding validation
•  Avoiding formatting when required
•  Optimizing only for line count
•  Blindly editing one file when the feature spans several
•  Never touching shared code
•  Never creating new code
A surgical edit is defined by precision and controlled scope, not by the number of lines changed. A 200-line change can be surgical if all 200 lines are necessary. A 5-line change can be bad if it creates hidden regressions.
Final principle
Touch what you need. Understand what you touch. Leave the rest alone.
