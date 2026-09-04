No AI Writing
This skill prevents AI-generated writing from sounding generic, inflated, overly polished, corporate, or disconnected from the actual project. It applies to project-facing writing: READMEs, documentation, comments, JSDoc, commit messages, changelogs, release notes, error messages, UI copy, configuration descriptions, API documentation, developer notes, TODOs, CLI output, and inline explanations.
The goal is not to make writing intentionally bad, informal, or "look less AI." The goal is to make writing specific, useful, proportional, technically accurate, consistent with the repository, natural for the context, and written for the actual reader.
1.  Write for the actual reader
Before writing, determine who will read it.
•  README → someone trying to understand or use the project
•  API docs → developer consuming the API
•  Code comment → future maintainer
•  Error message → actual user or developer debugging
•  Commit message → project history
•  Changelog → user/developer interested in changes
Do not write generic explanations that nobody needs.
2.  Match the project's existing writing style
Inspect nearby documentation before creating new documentation. Match existing terminology, capitalization, heading style, sentence style, technical vocabulary, level of detail, tone, and formatting.
If the repository uses short practical notes, do not introduce polished corporate documentation. If the repository has detailed technical docs, do not suddenly write cryptic one-liners. Existing project style takes precedence over generic documentation conventions.
3.  Avoid generic AI introductions
Avoid unnecessary openings:
•  "Welcome to..."
•  "In this comprehensive guide..."
•  "This powerful solution..."
•  "In today's fast-paced world..."
•  "This project aims to..."
•  "Whether you're a beginner or an experienced developer..."
•  "Let's dive into..."
•  "This documentation will walk you through..."
•  "At its core..."
•  "Designed with scalability and performance in mind..."
Unless the project genuinely needs such wording. Start with useful information.
4.  Don't oversell the project
Do not invent marketing language. Avoid unsupported claims: powerful, blazing fast, next-generation, production-ready, enterprise-grade, highly scalable, robust, seamless, revolutionary, optimized, secure, lightweight—unless the repository actually provides evidence.
Describe what the project does instead of praising it.
Bad: A powerful next-generation API solution designed for seamless scalability.
Better: API for generating and managing temporary download links.
5.  Be specific instead of impressive
Prefer concrete facts.
Bad: The system provides a robust and flexible architecture for handling various operations.
Better: Requests are handled by Express routes, with Redis used for short-lived cache entries.
Specific writing is usually more useful than polished writing.
6.  Do not explain obvious code
Comments should explain why, not restate what the code already says.
Bad:
// Get the user
const user = await getUser(id);
Better:
// Keep deleted users out of the cache until the next refresh.
const user = await getUser(id);
If the code is already obvious, no comment may be better.
7. Avoid comment narration
Do not narrate every operation:
// Check if user exists
// If user exists
// Get user's data
// Return user's data
Code should communicate straightforward operations itself. Comments are for context, constraints, decisions, or non-obvious behavior.
8. Avoid unnecessary JSDoc/docstrings
Do not generate documentation for every function simply because the language allows it. Avoid JSDoc that only repeats the function signature:
/**
•  Gets a user by ID.
•  @param {string} id The user ID.
•  @returns {Promise<User>} The user.
*/
when the function and types already make this obvious. Use JSDoc/docstrings when they provide information that the code cannot communicate clearly.
9. README proportionality
A README should contain what a user needs to understand and use the project. Typical useful sections may include: what it is, requirements, installation, configuration, usage, API/commands, development, limitations, license.
Do not automatically generate every possible section. Do not create giant feature matrices, fake roadmaps, unnecessary architecture diagrams, badges everywhere, repeated explanations, "philosophy" sections nobody asked for, or speculative future plans.
The size of the README should roughly match the complexity of the project.
10. Don't fabricate documentation
Never document behavior that has not been verified. Do not invent endpoints, parameters, environment variables, configuration options, CLI flags, supported platforms, performance numbers, dependencies, compatibility, architecture, or future features.
If something is unclear, inspect the code. If it cannot be verified, say so or leave it undocumented.
11. Use real examples
When examples are useful, make them match the actual project. Do not generate generic placeholder examples when the repository already contains real usage.
Prefer npm run build if that is the actual command, rather than inventing npm run example. Examples should be copyable whenever possible.
12. Keep technical writing direct
Prefer:
Requires Node.js 20 or newer.
over:
In order to ensure proper compatibility and functionality, users are required to have Node.js version 20 or newer installed on their system.
Prefer:
The token expires after 10 minutes.
over:
Tokens are designed to remain valid for a predefined period of 10 minutes before becoming invalid.
Do not inflate simple statements.
13. Avoid repetition
Do not explain the same thing in README, comments, API docs, examples, and changelog unless each context genuinely needs it. Say it once where it is most useful.
14. Error messages should help
Error messages should tell the user what actually went wrong and, when useful, what they can do next.
Avoid "An unexpected error occurred while processing your request." when the actual problem is known.
Prefer "Invalid API key." or "File not found: config.json." Do not write error messages like essays.
15. UI copy should sound like UI copy
Avoid turning interface text into documentation.
Bad: Please be advised that you are required to enter a valid email address in order to continue with the registration process.
Better: Enter a valid email address.
Buttons should generally be actions: Save, Delete, Retry, Continue, Copy, Cancel. Avoid unnecessary phrases such as "Click here to...", "Please proceed by...", "Kindly..." unless the product's tone specifically calls for them.
16. Commit messages should describe the change
Do not generate dramatic commit messages.
Bad: Implement comprehensive improvements to enhance the overall robustness and scalability of the authentication architecture.
Better: Fix auth token refresh. Or: Add retry for supplier requests.
Follow the repository's existing commit style if one exists.
17. Changelogs should describe actual changes
Do not turn every change into marketing copy.
Bad: Experience an exciting new generation of performance improvements!
Better:
•  Add request retry for supplier API
•  Fix expired link response
•  Update mobile navigation
Only mention changes that actually happened.
18. Avoid fake precision
Do not invent exact numbers simply because documentation looks better with them. Do not claim "50% faster," "99.99% uptime," "supports 10,000 requests/sec," or "reduces memory usage by 30%" unless those numbers were actually measured.
19. Avoid unnecessary emojis and decoration
Do not automatically add emojis, badges, decorative separators, excessive bold text, ASCII art, or motivational slogans. Use them only when they fit the existing project.
20. Don't rewrite existing writing unnecessarily
When modifying documentation: preserve useful existing wording, update only what changed, don't rewrite the entire README for one feature, don't change tone without a reason, don't "polish" unrelated sections.
A documentation change should be treated like a code change: modify the relevant part and leave working content alone.
21. Don't turn TODOs into essays
TODOs should be short and actionable.
Good: // TODO: retry failed supplier requests
Bad: // TODO: Consider implementing a comprehensive retry mechanism that could potentially improve the resilience of supplier requests under various network failure conditions in the future.
22. Don't generate documentation just because you can
Not every change needs a README update, new comments, JSDoc, a changelog entry, or a new documentation page. Only update writing when the task or project convention requires it.
23. Preserve technical honesty
Writing must reflect actual implementation.
•  Experimental → call it experimental
•  Beta → call it beta
•  Mocked → call it mocked
•  Incomplete → call it incomplete
•  Local-only → say so
•  Unsupported → say so
Do not make unfinished functionality sound production-ready.
24. Separate facts from suggestions
Do not present recommendations as existing behavior.
Bad: The API automatically retries failed requests and provides fallback providers. (when that is only an idea)
Better: The API currently sends each request to the configured provider.
If suggesting a future improvement, label it clearly as a suggestion.
25. Final writing review
Before finalizing project-facing writing, ask:
•  Is every claim supported by the actual project?
•  Is this information useful to the intended reader?
•  Did I match the repository's existing writing style?
•  Did I add unnecessary introduction or explanation?
•  Did I oversell anything?
•  Did I invent any behavior, API, configuration, or numbers?
•  Did I repeat information unnecessarily?
•  Could this be shorter without losing useful information?
•  Did I rewrite unrelated existing content?
•  Does this sound like something an experienced developer would actually write for this project?
If a sentence exists mainly to make the document sound polished, remove it.
Important constraints
This skill must not be interpreted as:
•  Always writing as little as possible
•  Banning detailed documentation
•  Banning professional writing
•  Banning polished prose
•  Banning README structure
•  Banning comments
•  Banning JSDoc
•  Banning changelogs
•  Banning marketing copy when marketing copy is actually required
•  Intentionally making writing informal or sloppy
•  Intentionally introducing grammar mistakes
•  Trying to make text "undetectable as AI"
Detailed writing is appropriate when the subject requires it. The rule is useful detail, not decorative detail. Professional writing is good. Artificially inflated writing is not.
Preferred mindset
Use this hierarchy:
Actual project facts
→ Reader needs
→ Existing writing style
→ Clear and direct wording
→ Necessary detail
→ Stop
Not:
Task
→ Generate giant documentation
→ Add sections
→ Add explanations
→ Add marketing language
→ Add examples
→ Add badges
→ Add roadmap
→ Rewrite everything
Final principle
Write what the project needs to say, for the person who needs to read it, and nothing more.
