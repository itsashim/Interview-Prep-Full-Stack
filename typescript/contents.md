You are an expert TypeScript instructor and senior software engineer with 15+ years of experience. I am an intermediate web developer who already knows JavaScript, HTML, CSS, and basic web development concepts. I need you to create an EXHAUSTIVE, COMPLETE, and DETAILED TypeScript tutorial that covers EVERY concept from top to bottom.

## INSTRUCTIONS:
- Do NOT skip any concept, no matter how small.
- Provide **real-world code examples** for EVERY concept.
- Explain the **"WHY"** behind each concept (why it exists, when to use it).
- Include **common mistakes and pitfalls** for each topic.
- Add **best practices and industry standards**.
- Compare with JavaScript equivalents where applicable.
- Use progressive difficulty (build on previous concepts).
- Include **mini-exercises** at the end of each section.
- Mark topics as [BEGINNER], [INTERMEDIATE], or [ADVANCED].

## COMPLETE CURRICULUM TO COVER (Do NOT skip ANY of these):

### MODULE 1: FOUNDATIONS & SETUP
1. What is TypeScript and why use it over JavaScript
2. TypeScript vs JavaScript — detailed comparison
3. How TypeScript works (compilation, transpilation, tsc)
4. Installing TypeScript (npm, globally, locally)
5. tsconfig.json — EVERY compiler option explained (target, module, strict, outDir, rootDir, include, exclude, lib, declaration, sourceMap, esModuleInterop, resolveJsonModule, skipLibCheck, forceConsistentCasingInFileNames, noEmit, isolatedModules, moduleResolution, baseUrl, paths, etc.)
6. Setting up TypeScript with different environments (Node.js, React, Next.js, Vite, Webpack)
7. TypeScript Playground usage
8. .ts vs .tsx vs .d.ts file extensions

### MODULE 2: TYPE SYSTEM BASICS
9. Type Annotations (explicit typing)
10. Type Inference (implicit typing)
11. Primitive Types: string, number, boolean, null, undefined, symbol, bigint
12. The `any` type (and why to avoid it)
13. The `unknown` type (safe alternative to any)
14. The `never` type (exhaustive checks, functions that never return)
15. The `void` type
16. The `object` type vs `Object` vs `{}`
17. Type Assertions (as keyword, angle bracket syntax)
18. Non-null assertion operator (!)
19. Optional chaining (?.) with TypeScript
20. Nullish coalescing (??) with TypeScript

### MODULE 3: ARRAYS, TUPLES & SPECIAL TYPES
21. Array types (Type[] vs Array<Type>)
22. ReadonlyArray<T>
23. Tuple types
24. Named tuples
25. Optional tuple elements
26. Rest elements in tuples
27. Readonly tuples
28. Enum types (numeric, string, const enums, heterogeneous)
29. Enum reverse mapping
30. Enum vs Union types — when to use which
31. Literal types (string literals, number literals, boolean literals)
32. Template literal types

### MODULE 4: UNIONS, INTERSECTIONS & TYPE NARROWING
33. Union types (|)
34. Intersection types (&)
35. Discriminated unions (tagged unions)
36. Type narrowing techniques:
    - typeof guards
    - instanceof guards
    - in operator
    - Equality narrowing
    - Truthiness narrowing
    - Assignment narrowing
37. Custom type guards (type predicates with `is`)
38. Assertion functions (asserts keyword)
39. Exhaustive checking with never

### MODULE 5: INTERFACES & TYPE ALIASES
40. Interface declaration
41. Type alias declaration
42. Interface vs Type — complete comparison and when to use each
43. Optional properties (?)
44. Readonly properties
45. Index signatures ([key: string]: type)
46. Extending interfaces (single & multiple inheritance)
47. Intersection types for extending type aliases
48. Interface merging (declaration merging)
49. Implementing interfaces in classes
50. Hybrid types (callable + object)
51. Recursive types / self-referencing types
52. Excess property checks

### MODULE 6: FUNCTIONS IN TYPESCRIPT
53. Function parameter types
54. Function return types
55. Optional parameters
56. Default parameters
57. Rest parameters
58. Function overloads
59. Call signatures
60. Construct signatures
61. `this` parameter type
62. `void` vs `undefined` return types
63. Function type expressions
64. Generic functions (intro)
65. Typing callbacks
66. Typing higher-order functions
67. Typing async functions and Promises

### MODULE 7: OBJECT TYPES & ADVANCED PATTERNS
68. Object type annotations
69. Nested object types
70. Optional properties in objects
71. Readonly modifier (deep readonly patterns)
72. Record<Keys, Type>
73. Mapped types basics
74. Utility types for objects:
    - Partial<T>
    - Required<T>
    - Pick<T, Keys>
    - Omit<T, Keys>
    - Readonly<T>
    - Record<K, V>
75. Property modifiers

### MODULE 8: CLASSES IN TYPESCRIPT
76. Class declarations with types
77. Constructor typing
78. Access modifiers: public, private, protected
79. Parameter properties (shorthand constructor)
80. Readonly class properties
81. Getters and setters
82. Static members
83. Abstract classes and abstract methods
84. Class inheritance with types
85. Implementing multiple interfaces
86. Class expressions
87. `this` types in classes
88. Generic classes
89. Class decorators (with experimentalDecorators and TC39 decorators)
90. Method decorators
91. Property decorators
92. Parameter decorators
93. Accessor decorators
94. Decorator factories
95. Decorator composition
96. `override` keyword
97. Member visibility and ECMAScript private fields (#)
98. Static blocks in classes
99. `satisfies` operator with classes

### MODULE 9: GENERICS (COMPLETE DEEP DIVE)
100. What are generics and why use them
101. Generic functions
102. Generic interfaces
103. Generic classes
104. Generic type aliases
105. Multiple type parameters
106. Generic constraints (extends keyword)
107. Using type parameters in generic constraints
108. Generic parameter defaults
109. Generic conditional expressions
110. The `keyof` constraint pattern
111. Generic utility patterns
112. Generic factories
113. Bounded polymorphism
114. F-bounded polymorphism
115. Higher-kinded types patterns

### MODULE 10: ADVANCED TYPE SYSTEM
116. Conditional types (T extends U ? X : Y)
117. Distributive conditional types
118. Inferring within conditional types (infer keyword)
119. Mapped types (in-depth)
120. Key remapping in mapped types (as clause)
121. Template literal types (advanced patterns)
122. Intrinsic string manipulation types (Uppercase, Lowercase, Capitalize, Uncapitalize)
123. Indexed access types (T[K])
124. keyof type operator
125. typeof type operator
126. Recursive conditional types
127. Variadic tuple types
128. Named and anonymous mapped types
129. Homomorphic mapped types

### MODULE 11: UTILITY TYPES (COMPLETE LIST)
130. Partial<T>
131. Required<T>
132. Readonly<T>
133. Record<K, V>
134. Pick<T, K>
135. Omit<T, K>
136. Exclude<T, U>
137. Extract<T, U>
138. NonNullable<T>
139. Parameters<T>
140. ConstructorParameters<T>
141. ReturnType<T>
142. InstanceType<T>
143. ThisParameterType<T>
144. OmitThisParameter<T>
145. ThisType<T>
146. Awaited<T>
147. NoInfer<T>
148. Intrinsic string types
149. Building custom utility types
150. Combining utility types for complex patterns

### MODULE 12: MODULES & NAMESPACES
151. ES Modules in TypeScript (import/export)
152. Default exports vs named exports
153. Type-only imports and exports (import type / export type)
154. Dynamic imports
155. Module resolution strategies (node, classic, bundler)
156. Path aliases and baseUrl
157. Namespaces (internal modules)
158. Namespace merging
159. Ambient modules
160. Module augmentation
161. Global augmentation
162. Declaration files (.d.ts)
163. Triple-slash directives
164. @types packages and DefinitelyTyped

### MODULE 13: TYPE DECLARATIONS & THIRD-PARTY TYPES
165. Writing declaration files (.d.ts)
166. declare keyword (declare const, declare function, declare class, declare module, declare global, declare namespace)
167. Ambient declarations
168. Using @types/ packages
169. Creating custom type definitions for untyped libraries
170. Module declaration for non-JS assets (CSS, images, JSON)
171. Global type declarations
172. Declaration merging patterns (interface, namespace, class, enum)
173. Augmenting existing modules
174. Augmenting global scope

### MODULE 14: ERROR HANDLING IN TYPESCRIPT
175. Typing try-catch blocks (unknown vs any in catch)
176. Custom error classes
177. Result/Either pattern in TypeScript
178. Type-safe error handling strategies
179. Discriminated union error handling
180. Assertion functions for validation

### MODULE 15: TYPESCRIPT WITH DOM & BROWSER APIs
181. DOM type hierarchy (HTMLElement, HTMLInputElement, etc.)
182. Event types (MouseEvent, KeyboardEvent, ChangeEvent, etc.)
183. Typing event handlers
184. Typing querySelector and getElementById
185. Working with forms in TypeScript
186. Typing Web APIs (fetch, localStorage, sessionStorage)
187. Typing window and document
188. Typing timers (setTimeout, setInterval)

### MODULE 16: TYPESCRIPT WITH REACT (COMPLETE)
189. Setting up React with TypeScript
190. Typing functional components (React.FC vs explicit typing)
191. Typing props (interface vs type)
192. Typing children prop
193. Typing state with useState
194. Typing useEffect
195. Typing useRef
196. Typing useReducer
197. Typing useContext
198. Typing useMemo and useCallback
199. Typing custom hooks
200. Typing event handlers in React
201. Typing forms in React
202. Typing Higher-Order Components (HOCs)
203. Typing Render Props
204. Typing React.forwardRef
205. Typing React.lazy and Suspense
206. Generic React components
207. Typing component libraries
208. Typing styled-components / CSS modules
209. React TypeScript best practices and patterns

### MODULE 17: TYPESCRIPT WITH NODE.js & APIs
210. Setting up Node.js with TypeScript (ts-node, tsx)
211. Typing Express.js (Request, Response, NextFunction, middleware)
212. Typing REST API responses
213. Typing environment variables (process.env)
214. Typing configuration files
215. Typing database models (with Prisma/TypeORM patterns)
216. Typing middleware patterns
217. Typing WebSocket events

### MODULE 18: ADVANCED PATTERNS & DESIGN PATTERNS
218. Builder pattern in TypeScript
219. Factory pattern in TypeScript
220. Singleton pattern in TypeScript
221. Observer pattern in TypeScript
222. Strategy pattern in TypeScript
223. Repository pattern in TypeScript
224. Dependency injection pattern
225. Mixin pattern
226. Brand types / Opaque types / Nominal typing
227. Type-safe event emitters
228. Type-safe builders
229. Phantom types
230. Type-level programming
231. Pattern matching with TypeScript
232. The `satisfies` operator (complete guide)
233. The `const` assertion (`as const`)
234. Using `as const` for readonly arrays and objects
235. Type-safe exhaustive switch statements
236. Discriminated unions for state machines

### MODULE 19: TYPESCRIPT CONFIGURATION & TOOLING
237. tsconfig.json — complete deep dive
238. Project references (composite projects)
239. TypeScript with ESLint (@typescript-eslint)
240. TypeScript with Prettier
241. TypeScript with Jest (ts-jest, @types/jest)
242. TypeScript with Vitest
243. TypeScript strict mode options breakdown:
    - strict
    - strictNullChecks
    - strictFunctionTypes
    - strictBindCallApply
    - strictPropertyInitialization
    - noImplicitAny
    - noImplicitThis
    - alwaysStrict
244. Additional compiler checks:
    - noUnusedLocals
    - noUnusedParameters
    - noImplicitReturns
    - noFallthroughCasesInSwitch
    - noUncheckedIndexedAccess
    - exactOptionalPropertyTypes
245. Watch mode and incremental compilation
246. TypeScript with monorepos

### MODULE 20: PERFORMANCE, MIGRATION & BEST PRACTICES
247. Migrating JavaScript project to TypeScript (step-by-step)
248. Using allowJs and checkJs
249. JSDoc type annotations for gradual migration
250. TypeScript performance tips (avoiding complex types, type instantiation limits)
251. TypeScript anti-patterns to avoid
252. TypeScript coding conventions and style guide
253. Type safety levels (from loose to strict)
254. When NOT to use TypeScript features
255. Debugging TypeScript
256. TypeScript compiler API basics
257. Staying up to date with TypeScript releases

## FORMAT REQUIREMENTS:
- Start each module with a brief overview
- Use code blocks with proper syntax highlighting
- Add comments in code explaining what's happening
- Include "💡 Pro Tip" callouts for expert advice
- Include "⚠️ Common Mistake" callouts for pitfalls  
- Include "🔑 Key Takeaway" at the end of each section
- After every module, provide 3-5 practice exercises
- Use tables for comparisons where helpful
- At the very end, provide a "TypeScript Cheat Sheet" summarizing key syntax

## DELIVERY:
Since this is extensive, break it into parts. Start with Modules 1-3 first. At the end of each response, ask me if I'm ready for the next set of modules. Continue until ALL 20 modules are fully covered.

Begin now with Modules 1-3. Be thorough. Do not summarize or shorten. Give me COMPLETE content.