Anti-AI-Code Patterns
This skill complements the global engineering principles. It targets the specific implementation patterns that make generated code feel machine-produced: unnecessary verbosity, premature abstraction, excessive defensiveness, and stylistic disconnect from the existing codebase.
The goal is not to evade detection or write ugly code. It is to produce code that demonstrates human engineering judgment—appropriate to the problem, consistent with the repository, and proportional in complexity.
1.  Match the codebase's grammar
A repository has an implicit style beyond formatting. Before writing, observe how the existing code:
•  structures functions
•  names variables
•  flows data between modules
•  handles state and errors
•  composes components
•  writes async code
•  expresses conditionals
•  organizes files
New code should feel native. Do not introduce a noticeably different dialect.
If the project uses straightforward functions, do not introduce classes, dependency injection, repositories, and elaborate abstractions for one new feature.
----
2.  Avoid abstraction theater
Abstraction is appropriate when it removes meaningful duplication, represents a real domain boundary, isolates a complex subsystem, or matches the project's existing architecture.
It is inappropriate when it only forwards data to another layer.
Prefer the existing direct pattern unless the project already uses or genuinely needs:
•  Controller → Service → Repository chains that only pass data through
•  Factories that instantiate one thing one way
•  Managers/Handlers/Processors that rename a single operation
•  Adapters that map one identical shape to another
Rule: Abstract repeated or meaningful concepts, not hypothetical future requirements.
----
3.  Avoid ceremonial code
Do not add code whose primary purpose is to look structured.
// Bad
const requestData = { ...input };
const processedRequest = processRequest(requestData);
const responseData = { ...processedRequest };
return responseData;
// Good
return processRequest(input);
Do not create wrappers that only rename or forward values. Every line should carry meaning.
4.  Natural variable naming
Avoid generic chains when the context provides a better name.
Be suspicious of excessive use of: data, result, response, payload, item, entry, value, processedData, transformedData, finalResult, updatedData, temp, obj, config, options, params.
These are not forbidden—use them when genuinely appropriate. The rule is:
Names should describe the role of the value in this specific context.
Prefer expiredKeys, subtitleSegments, product over processedData, transformedResult when the specific meaning is known.
Do not artificially rename simple values to appear sophisticated.
----
5.  Avoid unnecessary intermediate variables
Do not introduce a variable merely because every operation "should" have a named step.
// Bad
const user = await getUser(id);
const userData = user.data;
const userName = userData.name;
return userName;
// Good (when convention allows)
return (await getUser(id)).data.name;
An intermediate variable is useful when it improves readability, gives a meaningful name, prevents repeated computation, or clarifies control flow. The objective is meaningful code, not the fewest lines possible.
6.  Avoid excessive defensive programming
Do not automatically produce deep null checks, type guards, and array validations for every internal operation.
// Suspicious
if (!response) ...
if (!response.data) ...
if (!response.data?.user) ...
if (typeof response.data.user !== 'object') ...
if (!Array.isArray(response.data.user.items)) ...
Be defensive at important boundaries: external input, auth, payments, filesystem, third-party APIs. Do not turn ordinary internal code into a fortress of hypothetical checks. Match the validation level to the trust boundary, API contract, and actual failure modes.
7.  Avoid boilerplate error handling
Do not wrap every operation in generic try/catch blocks that log and re-throw.
// Bad
try {
...
} catch (error) {
console.error(error);
throw new Error('Something went wrong');
}
Do not catch an error unless there is something useful to do with it.
Good reasons to catch:
•  Convert to the project's expected error format
•  Recover from a known failure
•  Provide a meaningful fallback
•  Clean up resources
•  Add relevant context
•  Handle a specific expected error
Bad reason: "Production code should always have try/catch."
8.  Avoid comment spam
Code should explain itself where reasonably possible.
Do not narrate obvious operations:
// Bad
// Get the user
const user = await getUser(id);
// Check if user exists
if (!user) return null;
// Return the user
return user;
Comments should capture what cannot be inferred easily:
•  Why something unusual is necessary
•  External API quirks
•  Compatibility constraints
•  Non-obvious business rules
•  Deliberate workarounds
•  Dangerous edge cases
Prefer one useful comment over five explanatory comments.
9.  Avoid excessive type ceremony
Do not create types/interfaces solely to give every object a formal name.
// Bad
interface UserData {}
interface UserResponseData {}
interface ProcessedUserData {}
interface FinalUserResult {}
Use types where they provide real value: public APIs, domain models, meaningful contracts, complex reusable structures, external boundaries. Do not turn simple local code into a type-definition ceremony. Respect the repository's existing type strictness.
10.  Avoid fake DRY
Do not extract tiny functions merely because two pieces of code share a few characters.
// Bad
const getName = user => user.name;
const isEmpty = value => !value;
Duplication is sometimes clearer than premature abstraction. Extract when the duplication represents the same concept and changing it in one place is genuinely valuable.
11.  Avoid "one function per sentence"
Do not split straightforward logic into a chain of tiny functions:
validateInput() → prepareInput() → normalizeInput() → processInput()
→ transformResult() → prepareResponse() → formatResponse() → sendResponse()
unless these are real domain boundaries or the project already uses this structure. A function can contain several straightforward operations when keeping them together makes the flow easier to understand.
12.  Avoid unnecessary async complexity
Do not introduce:
•  Promise chains where async/await is already used
•  Promise.all() when operations are dependent
•  Artificial concurrency, unnecessary retries, polling, queues, workers
•  Debouncing/throttling unless the problem requires them
Do not optimize for hypothetical performance.
----
13.  Avoid unnecessary configuration
Do not create configuration for values that are:
•  Used once
•  Not environment-specific
•  Not expected to change
•  Not shared
// Bad (without reason)
const timeout = config.get('TIMEOUT'); // 5000, never changes
// Good
const timeout = 5000;
Configuration should represent actual variability.
14.  Avoid unnecessary fallback layers
Do not automatically create fallback chains:
primary → secondary → cache → stale cache → default → hardcoded fallback
unless the product actually requires that reliability model. A fallback should exist because there is a known failure mode worth handling.
15.  Preserve local code density
If a repository normally solves a feature in 30–50 lines, do not turn it into 200 lines of wrappers, types, helpers, comments, validation, and abstractions. Code size should be proportional to problem complexity.
----
16.  Avoid opportunistic refactoring
When adding a feature:
17.  Understand the existing implementation
18.  Find the smallest integration point
19.  Add the feature
20.  Preserve surrounding code
Do not opportunistically rename variables, reorganize imports, reorder functions, convert syntax, rewrite callbacks to async, migrate APIs, replace libraries, or modernize unrelated code unless required.
----
17.  Frontend: avoid generated UI patterns
Do not automatically add:
•  Excessive rounded cards, glassmorphism, arbitrary gradients
•  Glowing effects, huge hero sections, unnecessary badges
•  Excessive icons, floating decorative elements, random animations
•  Giant shadows, excessive whitespace, "modern SaaS" layouts
•  Dashboard cards for everything
Copy the existing product's visual grammar: spacing, typography, hierarchy, radius, borders, colors, interaction patterns, component density. Do not redesign a product while implementing a feature.
----
18.  Frontend: avoid component fragmentation
Do not automatically turn every visual element into a component.
// Bad
Create a component when it represents meaningful reusable UI, independent behavior, meaningful state, a clear domain concept, or a repeated pattern. Otherwise, keep related markup together.
19.  Do not rewrite APIs to fit the implementation
When integrating with an existing API, adapt the implementation to the API unless changing the API is explicitly part of the task.
Do not invent response wrappers, generic API clients, new DTO layers, serialization systems, or response normalizers without a real need. Existing contracts matter.
----
20.  Question generated-looking patterns
Before finalizing, ask:
•  Why does this need its own function?
•  Why does this need its own type?
•  Why does this need its own file?
•  Why does this need a class?
•  Why does this need a wrapper?
•  Why does this need a comment?
•  Why does this need a fallback?
•  Why does this need a configuration option?
•  Why does this need a dependency?
•  Why is this code twice as long as the existing pattern?
If there is no concrete answer, simplify it.
----
Balance
Do NOT interpret this skill as:
•  Always writing fewer lines
•  Avoiding all abstractions, comments, validation, types, or error handling
•  Intentionally writing ugly or old-fashioned code
•  Making code look "less AI"
•  Refusing modern APIs or patterns
Complex problems deserve complex solutions. Simple problems deserve simple solutions.
Final self-review
Before considering implementation complete, verify:
1.  Did I follow the repository's existing coding style?
2.  Did I introduce any abstraction that was not actually necessary?
3.  Did I create intermediate variables without meaningful purpose?
4.  Did I add defensive checks for hypothetical problems?
5.  Did I add comments that merely narrate the code?
6.  Did I create types/interfaces without meaningful semantic value?
7.  Did I split straightforward logic into too many functions?
8.  Did I add configuration, dependencies, fallbacks, or infrastructure unnecessarily?
9.  Did I make unrelated changes?
10.  Does the code feel proportional to the problem?
11.  Would an experienced developer maintaining this repository consider this implementation natural?
If the answer to any of these is "yes", simplify or justify the decision before finishing.
----
Final principle
Do not try to write code that looks human. Write code that demonstrates human engineering judgment. The difference is important.
