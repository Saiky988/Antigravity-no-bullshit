Human UI
This skill guides frontend and UI work in an existing codebase. It complements the global engineering principles and anti-AI-code patterns with specific guidance for visual and interactive implementation.
The goal is not to make interfaces "look less AI" artificially. It is to produce UI that feels like it was designed and implemented by a thoughtful human product developer who understands the existing product, its users, and its constraints.
1.  Understand the existing visual language first
Before designing or building anything new, inspect existing pages, components, and styles. Reuse established spacing, typography, colors, radii, shadows, borders, icons, layouts, and interaction patterns. Do not introduce a new visual language unless explicitly asked.
2.  Avoid generic AI-generated UI
Do not apply decorative patterns blindly:
•  Excessive gradients
•  Random glassmorphism
•  Excessive rounded cards
•  Excessive shadows
•  Decorative blobs
•  Unnecessary glowing effects
•  Arbitrary animations
•  Excessive icons
•  Huge hero sections for simple products
•  "Modern SaaS" styling applied without context
•  Dashboard-card-everything layouts
•  Excessive badges and pills
•  Meaningless visual decoration
3.  Design with hierarchy
Every element should have a reason to exist. Establish clear visual hierarchy. Primary actions should be obvious. Secondary information should remain secondary. Avoid making everything visually important.
4.  Prefer real product UI over showcase UI
Optimize for usability, not screenshots. UI should feel like part of a real application that people use repeatedly. Avoid designs that look impressive in a mockup but become annoying during actual use.
5.  Preserve existing components
Reuse existing buttons, inputs, modals, cards, navigation, tables, tabs, and other components. Do not create near-duplicates just because a slightly different version is needed. Extend existing components when appropriate.
6.  Avoid component fragmentation
Do not turn every tiny visual element into its own component. Keep simple UI local when it is only used once. Extract components when reuse, complexity, or maintainability actually justifies it.
7.  Spacing and sizing
Use the project's existing spacing scale. Avoid arbitrary values unless necessary. Do not add excessive padding simply to make interfaces feel "premium." Keep density appropriate to the product.
8.  Typography
Respect the existing font system. Avoid excessive font weights, sizes, uppercase labels, letter spacing, or dramatic headings. Text hierarchy should come from intentional sizing, weight, and spacing rather than decoration.
9.  Color
Reuse the existing palette. Do not invent additional accent colors casually. Avoid using color merely to decorate. Reserve strong colors for meaningful states, emphasis, or actions.
10.  Animation and interaction
Animation should communicate state, hierarchy, or continuity. Avoid animation for decoration. Avoid animating everything on page load. Prefer subtle transitions when appropriate. Respect reduced-motion preferences when the project supports accessibility requirements.
11.  Responsive design
Treat mobile as a real layout, not a shrunken desktop. Inspect how existing responsive layouts work. Reflow content intentionally. Do not simply hide difficult elements to make a layout fit. Consider touch targets, navigation, overflow, text wrapping, and viewport constraints.
12.  Mobile navigation
Use the project's established navigation pattern. If mobile requires a different navigation structure, design it intentionally. Do not blindly add bottom tabs, hamburger menus, or drawers just because they are common patterns.
13.  Forms and inputs
Keep forms clear and predictable. Labels, placeholders, validation, disabled states, loading states, and errors should have consistent behavior. Do not add unnecessary helper text or visual decoration.
14.  Empty, loading, and error states
Design real states instead of leaving blank space. Keep messages concise and useful. Do not use giant illustrations or decorative empty-state compositions unless they fit the product.
15.  Tables, lists, and data-heavy UI
Prioritize readability and scanning. Do not turn every row into a large card. Preserve information density when the product needs it. Use visual emphasis intentionally.
16.  Accessibility
Preserve semantic HTML where practical. Maintain keyboard accessibility. Use visible focus states where appropriate. Ensure controls have meaningful labels. Do not rely solely on color to communicate state.
17.  Don't redesign without permission
If the task is to add or fix something, do not redesign surrounding UI. Do not change established spacing, colors, navigation, or component behavior unless required. A bug fix is not a design refresh.
18.  Don't "polish" everything
Avoid unsolicited micro-interactions, hover effects, transitions, shadows, gradients, icons, and visual tweaks. Only polish what improves the requested experience.
19.  UI implementation should match the codebase
Follow existing CSS architecture, utility classes, component conventions, naming, and file structure. Do not introduce a new styling system for one component. Do not add dependencies for trivial visual effects.
20.  Handle imperfect requirements naturally
If requirements are incomplete, infer from existing UI before inventing something. Prefer the most conservative design consistent with the product. Do not fill ambiguity with generic SaaS patterns.
21.  Visual consistency beats theoretical best practice
An existing design convention should generally be preserved even if another pattern is more fashionable. Consistency across the product matters more than isolated perfection.
22.  Avoid unnecessary UI states
Do not invent loading, confirmation, tooltip, modal, onboarding, or animation states unless the interaction actually needs them. At the same time, do not omit states that are required for a real usable flow.
23.  Keep UI proportional
Simple functionality should have simple UI. Important functionality can receive stronger hierarchy. Do not build a complex visual system around a small feature.
24.  Final UI review
Before finishing frontend work, mentally review:
•  Does this look like it belongs in the existing product?
•  Did I reuse existing components and patterns?
•  Did I introduce unnecessary decoration?
•  Did I make everything into a card?
•  Did I add gradients, glows, glass, or animations without a reason?
•  Is the hierarchy clear?
•  Does mobile actually work as a layout?
•  Did I accidentally redesign unrelated areas?
•  Would this still feel good to use after hundreds of interactions?
•  Does the implementation feel proportional to the feature?
----
Important constraints
•  Do not interpret this skill as "make UI boring."
•  Do not forbid modern design.
•  Do not forbid gradients, glass, animations, cards, icons, or rounded corners when the existing product intentionally uses them.
•  Do not blindly remove existing visual effects.
•  Do not force a minimalist aesthetic.
•  Do not optimize for screenshots or "AI detection."
•  Existing project design language always matters more than this skill's stylistic preferences.
Final principle
Do not design what looks impressive in isolation. Design what feels inevitable inside the product.
