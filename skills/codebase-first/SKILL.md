Codebase First
This skill governs how to approach an existing codebase before making changes. It complements the global engineering principles and specialized skills for code quality and UI.
The core idea is simple: understand the codebase before deciding how to change it.
This prevents common AI-agent mistakes: immediately generating architecture, creating duplicate utilities, guessing APIs, rewriting existing files, or building features without understanding how the project currently works.
These guidelines are practical and proportional. They do not create a rigid mandatory process for trivial changes.
1.  Inspect before implementing
Before making meaningful changes, inspect the relevant part of the repository. Understand:
•  Where the feature currently lives
•  Which files participate in the flow
•  Existing components, utilities, and services
•  Current data flow
•  Existing API patterns
•  Relevant configuration
•  Nearby code that performs similar work
Do not inspect the entire repository when the task only affects a small area.
2.  Start from the task, then trace outward
Identify the smallest part of the codebase related to the request. Trace outward only when necessary:
•  Component → parent/state
•  Route → controller/service
•  Service → API/database
•  Feature → shared utilities
•  Page → layout/navigation
Avoid broad repository exploration without a reason.
3.  Search before creating
Before creating a new component, utility, helper, hook, service, API endpoint, type/interface, configuration, style, or dependency—search the repository for existing equivalents.
A duplicate implementation is usually worse than reusing an existing one.
4.  Learn local patterns
When modifying an existing feature, identify how nearby code handles similar problems. Prefer local examples over generic knowledge.
•  If three existing pages fetch data the same way, follow that pattern.
•  If existing components manage loading state locally, do not introduce a new global state solution.
•  If APIs follow a particular response structure, preserve it.
•  If styles use a particular convention, follow it.
5.  Understand data flow before changing it
For feature work involving data, determine:
source → transformation → state → UI/output
Do not change one layer blindly without understanding how the surrounding layers interact. Avoid creating new transformations when an existing one already provides the required shape.
6. Identify the integration point
Before writing code, determine where the requested behavior naturally belongs. Prefer:
•  Modifying the existing component over creating a parallel component
•  Extending the existing service over creating another service
•  Adding to an existing route over inventing another route
•  Using an existing utility over creating another helper
The best integration point is usually the smallest one that fits the existing architecture.
7. Respect the repository as the source of truth
Do not assume:
•  Framework conventions
•  API formats
•  Folder structures
•  Naming schemes
•  State management
•  Authentication flow
•  Database structure
•  Styling system
•  Build tooling
Inspect the repository and use what actually exists.
8. Do not trust assumptions
If something is unclear, investigate the codebase before guessing.
•  Don't assume an API returns { data: ... }
•  Don't assume authentication is handled by middleware
•  Don't assume a component is reusable
•  Don't assume a utility is safe to replace
•  Don't assume a dependency is available
•  Don't assume a route follows conventional REST patterns
Use evidence from the repository.
9. Follow dependency direction
Understand existing boundaries before introducing new imports or relationships. Avoid creating unnecessary coupling:
•  UI importing database logic
•  Low-level utilities importing high-level application modules
•  Unrelated features depending on each other
•  Circular dependencies
Do not restructure architecture merely to satisfy an isolated task.
10. Preserve working boundaries
Existing modules often have intentional responsibilities. Do not move code between layers unless the task requires it. Do not merge files, split files, rename directories, or reorganize modules simply because another structure looks cleaner.
11. Check configuration before adding configuration
Before introducing environment variables, config files, feature flags, build options, constants, or scripts—search for existing configuration mechanisms. Use them instead of inventing another configuration path.
12. Check dependencies before adding dependencies
Inspect package manifests and existing imports before installing anything. Prefer:
existing dependency > platform API > standard library > small local implementation > new dependency
Only add a dependency when it provides meaningful value.
13. Understand generated/build files
Before editing generated files, determine whether they are source-controlled outputs or generated artifacts. Prefer modifying the source and regenerating the output when appropriate. Do not manually edit generated files unless the project intentionally treats them as source.
14. Understand tests and validation
Before implementing a non-trivial change, look for relevant tests, test conventions, lint configuration, type checking, build commands, and validation scripts. Follow the repository's existing validation approach. Do not invent a testing framework or test architecture for one task.
15. Read enough, not everything
Codebase-first does not mean reading every file. Read enough to answer:
•  What already exists?
•  Where does this change belong?
•  What patterns should I follow?
•  What behavior must I preserve?
•  What is the smallest safe change?
Once those questions are answered, implement.
16. Stop investigating when the path is clear
Do not keep exploring the repository just to appear thorough. If the relevant architecture is understood and the integration point is clear, start implementing. Discovery should reduce uncertainty, not become a substitute for implementation.
17. When requirements conflict with the codebase
If the user's request clearly requires changing existing behavior, follow the explicit request.
If the request is ambiguous, prefer the implementation that:
•  Fits existing patterns
•  Changes the least
•  Preserves compatibility
•  Avoids unnecessary architecture
Do not silently reinterpret the task into a different feature.
18. Before creating new architecture
Pause when the proposed solution requires introducing:
•  A new service layer
•  Manager/controller abstraction
•  Repository pattern
•  Global state
•  Event system
•  Plugin system
•  Generic framework
•  Large utility layer
•  Configuration architecture
First verify that the existing codebase actually needs it. Most small feature requests should not require architectural expansion.
19. Change only what you understand
Do not make broad edits to files or systems whose behavior you have not inspected. If a change requires touching unfamiliar code, inspect that code first. Avoid "while I'm here" modifications.
20. Final codebase-first review
Before finishing, ask:
•  Did I inspect the relevant existing implementation?
•  Did I search for existing equivalents before creating anything?
•  Did I follow local patterns?
•  Did I identify the correct integration point?
•  Did I verify actual APIs/data shapes instead of guessing?
•  Did I preserve existing behavior and boundaries?
•  Did I avoid unnecessary architecture?
•  Did I avoid unnecessary dependencies/configuration?
•  Did I touch only relevant files?
•  Did I investigate enough without wasting time?
•  Is the final change smaller because I understood the codebase?
Important constraints
•  Do not require repository-wide analysis for trivial tasks.
•  Do not force a fixed number of files to inspect.
•  Do not make agents spend excessive time planning.
•  Do not forbid creating new components, services, or utilities when they are genuinely needed.
•  Do not treat existing code as automatically correct.
•  Do not preserve bad architecture merely because it already exists.
•  Do not replace explicit user requirements with existing conventions when the two intentionally conflict.
•  Do not turn this into a generic software architecture lecture.
Workflow
Locate → Inspect → Search → Understand → Integrate → Implement → Verify
Final principle
The repository is the context. Read it before inventing around it.
