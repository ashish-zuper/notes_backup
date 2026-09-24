---

# Angular Frontend Deep Dive Interview Sheet (SDE-3)

---

## 1. Angular Architecture & Design

### Q1.

**How do you structure a large Angular application that will be maintained by 10+ engineers for years?**

**Expected Answer**

* Feature-based modules (not layer-based)
* CoreModule (singletons), SharedModule (dumb components, pipes)
* Clear domain boundaries
* Lazy loading for major features
* Strict typing & lint rules

**Red Flags**

* “One big AppModule”
* Shared services everywhere

---

### Q2.

**Standalone components vs NgModules – when would you use each?**

**Expected Answer**

* Standalone for:

  * New apps
  * Micro-frontends
  * Libraries
* NgModules still useful for:

  * Legacy apps
  * Grouping providers
* Tree-shakability improves with standalone

---

## 2. Change Detection & Performance

### Q3.

**Explain Angular’s change detection mechanism.**

**Expected Answer**

* Based on **Zone.js**
* Triggers on:

  * Async events
  * Promises
  * DOM events
* Runs top-down on component tree

**Bonus**

* Ivy optimizations
* Signals (Angular 16+)

---

### Q4.

**When and why would you use `ChangeDetectionStrategy.OnPush`?**

**Expected Answer**

* Runs CD only when:

  * @Input reference changes
  * Observable emits
  * Event inside component
* Reduces unnecessary re-rendering
* Requires immutability

**Common Pitfall**

* Mutating objects instead of replacing them

---

### Q5.

**How would you optimize an Angular page rendering 10k+ rows (AG Grid / tables)?**

**Expected Answer**

* Virtual scrolling
* Pagination
* `trackBy`
* OnPush strategy
* Web Workers for heavy computation

---

## 3. RxJS & State Management

### Q6.

**Explain cold vs hot observables with real Angular examples.**

**Expected Answer**

* Cold:

  * HTTP calls
  * New execution per subscription
* Hot:

  * Subjects
  * WebSocket streams
* Use `shareReplay()` carefully

---

### Q7.

**How do you prevent memory leaks in Angular applications?**

**Expected Answer**

* `takeUntil(destroy$)`
* `async` pipe
* Avoid manual subscriptions
* `ngOnDestroy`

**Red Flags**

* “Angular handles it automatically”

---

### Q8.

**How would you chain dependent API calls cleanly?**

**Expected Answer**

* `switchMap` for dependent calls
* `forkJoin` for parallel calls
* `concatMap` when order matters
* Avoid nested subscriptions

---

## 4. Forms & Validation

### Q9.

**Reactive Forms vs Template-Driven Forms – when and why?**

**Expected Answer**

* Reactive:

  * Complex validation
  * Dynamic forms
  * Testability
* Template-Driven:

  * Simple forms
  * Rapid prototyping

---

### Q10.

**How do you build dynamic multi-step forms with validation?**

**Expected Answer**

* FormArray + nested FormGroups
* Step-wise validation
* Custom validators
* Persist draft state

---

## 5. Routing & Security

### Q11.

**How do Angular route guards work?**

**Expected Answer**

* `CanActivate`, `CanLoad`, `Resolve`
* Prevent route access or preload data
* Used for auth, permissions, feature flags

---

### Q12.

**How do you secure an Angular application?**

**Expected Answer**

* JWT stored in memory / HttpOnly cookie
* HttpInterceptors
* XSS protection via sanitization
* Role-based UI guards (not security alone)

---

## 6. Testing & Quality

### Q13.

**How do you test Angular components effectively?**

**Expected Answer**

* TestBed
* Shallow testing
* Mock services
* Avoid real HTTP calls

---

### Q14.

**Unit tests vs E2E tests – what’s the right balance?**

**Expected Answer**

* Heavy unit test coverage
* Minimal E2E for critical flows
* Avoid flaky tests

---

## 7. Build, Deployment & Performance

### Q15.

**How does Angular build optimization work?**

**Expected Answer**

* AOT compilation
* Tree shaking
* Differential loading
* Lazy loading chunks

---

### Q16.

**How would you reduce bundle size by 50%?**

**Expected Answer**

* Lazy load features
* Remove unused libraries
* Analyze bundles
* Avoid moment.js
* Prefer ES modules

---

## 8. Advanced & Bar-Raiser Questions

### Q17.

**Explain Signals and how they compare to RxJS.**

**Expected Answer**

* Push-based reactivity
* Fine-grained change detection
* Complements RxJS, doesn’t replace it

---

### Q18.

**How would you design a frontend architecture for real-time dashboards?**

**Expected Answer**

* WebSockets
* State store
* Throttling & debouncing
* Push-based UI updates

---

### Q19.

**Describe a major Angular performance issue you fixed in production.**

**Evaluates**

* Debugging depth
* Measurement-driven fixes
* Ownership mindset

---

## 🧠 What This Sheet Evaluates

| Area         | Signal                    |
| ------------ | ------------------------- |
| Architecture | Long-term maintainability |
| Performance  | Change detection mastery  |
| RxJS         | Async reasoning           |
| Scalability  | Enterprise readiness      |
| Seniority    | Trade-off awareness       |

---

## ⭐ Optional Hands-On Task (SDE-3)

> Build a **resource allocation dashboard**:

* Lazy-loaded modules
* OnPush components
* RxJS-driven state
* Server-side pagination

---

If you want, I can:

* Add **coding exercises**
* Create **expected scoring rubrics**
* Convert this into a **panel interview sheet**
* Tailor it specifically for **Angular + enterprise HR systems**

Just tell me 👍
