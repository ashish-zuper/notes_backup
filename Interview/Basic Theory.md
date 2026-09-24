# Full-Stack JavaScript Developer Interview (4–5 Years)

**Style: Conversational Deep-Dive + Answers**

This sheet contains **primary questions**, **follow-up questions**, and **expected strong answers**. Follow-ups are triggered depending on how deeply the candidate answers.

---

## 1. JavaScript Fundamentals & Event Loop

**Q1:** Can you explain how the JavaScript event loop works?

**Expected Answer:** JavaScript is single-threaded. The call stack executes synchronous code first. Asynchronous tasks (like setTimeout, fetch, promises) go to Web APIs, then their callbacks move to the callback or microtask queue, which the event loop checks and pushes back to the call stack when it's empty.

**Follow-up Q:** What's the difference between microtask and macrotask queues?

**Answer:** Microtasks (Promises, queueMicrotask) run **before** macrotasks (setTimeout, setInterval). After every execution cycle, the event loop clears the microtask queue first.

**Follow-up Q:** Why is `Promise.then()` executed before `setTimeout(fn, 0)`?

**Answer:** Because Promise callbacks are microtasks, and microtasks have higher priority.

---

## 2. Scopes, Closures & Hoisting

**Q1:** What is a closure? Give an example.

**Expected Answer:** A closure is formed when an inner function captures variables from its lexical scope even after the outer function has executed.

**Example:**

```
function counter() {
  let count = 0;
  return function() { count++; return count; }
}
```

**Follow-up Q:** Why are closures useful?

**Answer:** They help in data privacy, state management, and function factories.

**Follow-up Q:** What issue do closures cause inside loops?

**Answer:** If using `var`, the loop variable is shared across iterations. Using `let` binds it per iteration.

---

## 3. Async Programming & Promises

**Q1:** Explain async/await.

**Expected Answer:** `async/await` is syntactic sugar over Promises that makes asynchronous code look sequential.

**Follow-up Q:** What happens if you forget `await`?

**Answer:** It returns a Promise instead of the resolved value.

**Follow-up Q:** How to handle errors in async/await?

**Answer:** Use try/catch or `.catch()`.

---

## 4. Node.js Runtime

**Q1:** Why is Node.js good for I/O heavy apps?

**Expected Answer:** It uses a non-blocking event loop which allows high concurrency for network/database calls.

**Follow-up Q:** When is Node.js _not_ a good choice?

**Answer:** CPU-heavy tasks (image/video processing) because they block the event loop.

**Follow-up Q:** How to fix CPU blocking?

**Answer:** Use Worker Threads or move heavy tasks to microservices.

---

## 5. Express.js & Backend Architecture

**Q1:** How do middleware functions work in Express?

**Expected Answer:** Middleware are functions that run before route handlers, receiving `req`, `res`, and `next()`.

**Follow-up Q:** How do you handle errors globally?

**Answer:** Create an error-handling middleware `(err, req, res, next)`.

**Follow-up Q:** Difference between `app.use()` and `app.get()`?

**Answer:** `use()` binds middleware to all methods; `get()` binds a route for GET only.

---

## 6. Frontend Framework (Angular)

**Q1:** What are Angular components and how do they communicate?**

**Expected Answer:** Components are the primary building blocks of Angular applications. Each component has a TypeScript class, an HTML template, and optional CSS. Components communicate using:

- `@Input()` to receive data from parents
    
- `@Output()` with `EventEmitter` to send events to parents
    

**Follow-up Q:** If data needs to be shared across unrelated components, what would you use?  
**Expected:** A shared service with Angular's Dependency Injection.

**Follow-up Q:** What is the role of Dependency Injection in Angular?  
**Expected:** DI allows services to be provided and consumed across the app without manually managing instances.

---

**Q2:** Explain the purpose of Angular Modules.

**Expected Answer:** NgModules group related components, directives, pipes, and services. They help in organizing applications and enabling lazy loading.

**Follow-up Q:** What are Standalone Components?  
**Expected:** Components that don't need to be declared inside an NgModule (introduced to simplify module complexity).

---

**Q3:** How do Angular forms work? Template-driven vs Reactive forms.

**Expected Answer:**

- Template-driven: Form logic resides in the template, easier for simple forms.
    
- Reactive: Form state managed in TS, better for complex validation and dynamic behavior.
    

**Follow-up Q:** Why would you choose Reactive forms in enterprise apps?  
**Expected:** Stronger control, testability, dynamic validation, and observable-based state.

---

**Q4:** What is RxJS and why is it important in Angular?

**Expected Answer:** RxJS enables reactive programming with Observables. Angular HTTP and many core APIs rely on Observables.

**Follow-up Q:** Difference between `Observable` and `Promise`?  
**Expected:** Observables are lazy and can emit multiple values; Promises are eager and emit a single value.

---

**Q5:** Explain State Management and when to use NgRx.

**Expected Answer:** NgRx is useful when the application has complex shared state, multiple data sources, or frequent UI state synchronization.

**Follow-up Q:** What pattern does NgRx implement?  
**Expected:** Redux pattern → Store (state) + Actions + Reducers + Effects.

---

## 7. REST APIs & HTTP

**Q1:** What is idempotency?

**Expected Answer:** An idempotent API returns the same result no matter how many times it is invoked (e.g., PUT, GET).

**Follow-up Q:** Why is POST not idempotent?

**Answer:** It creates new resources each time.

**Follow-up Q:** How to make PATCH safe?

**Answer:** Add versioning or etags to avoid conflicting updates.

---

## 8. Angular Fundamentals

**Q1:** What triggers a re-render in Angular?

**Expected Answer:** State changes, props changes, or context updates.

**Follow-up Q:** Why use `useCallback` or `useMemo`?

**Answer:** To prevent unnecessary re-renders or re-computations.

**Follow-up Q:** Why avoid storing derived data in state?

**Answer:** It creates inconsistency; recompute instead.

---

## 9. State Management

**Q1:** When should you use Redux over Context?

**Expected Answer:** When state is large, shared across many components, or needs predictable reducers.

**Follow-up Q:** Why is Redux considered predictable?

**Answer:** State updates are pure functions with no side effects.

**Follow-up Q:** What causes “prop drilling” and how to fix?

**Answer:** Passing props deeply — fix using Context or state management library.

---

## 10. System Design Basics

**Q1:** How would you design a rate-limited API?

**Expected Answer:** Use a token bucket / sliding window algorithm; store counters in Redis.

**Follow-up Q:** Why Redis?

**Answer:** Fast in-memory store with atomic ops, suitable for distributed environments.

**Follow-up Q:** How to scale horizontally?

**Answer:** Use load balancing + shared data layer (Redis / DB clustering).

---

**End of Interview Sheet.**

---

## 11. Backend Deep-Dive (Node.js / Architecture / APIs)

**Q1:** How do you structure a backend Node.js application for scalability?

**Expected Strong Answer:** Use separation of concerns: controllers (handle http), services (business logic), repositories/DAO (database), and models/DTOs. Use dependency injection where possible (NestJS style). Avoid putting logic in route handlers.

**Follow-up Q:** How do you handle shared logic across modules?  
**Expected Answer:** Create reusable service layers or shared utility modules. Do not duplicate logic across controllers.

**Q2:** How do you manage environment-based configuration?  
**Expected Answer:** Using `.env` files + a config module or library (like `dotenv`, `config`, or NestJS ConfigModule). Never hardcode credentials.

**Follow-up Q:** How do you secure secrets in production?  
**Expected Answer:** Use secrets manager (AWS SM, Vault, GCP Secret Manager), not environment files.

**Q3:** How do you optimize API performance in Node?  
**Expected Strong Answer:** Implement caching (Redis), use async operations, avoid blocking the event loop, database indexing, pagination, batching, and connection pooling.

**Follow-up Q:** How do you detect event-loop blocking?  
**Expected Answer:** Using monitoring tools like clinic.js, New Relic, or Node's `--trace-event`.

**Q4:** How do you handle errors across the application?  
**Expected Strong Answer:** Use centralized error middleware, return consistent error responses, log with context, differentiate between operational errors and programming errors.

**Follow-up Q:** How do you retry failed external operations safely?  
**Expected Answer:** Use exponential backoff + circuit breaker pattern.

**Q5:** How do you design APIs for large-scale systems?  
**Expected Answer:** Use REST conventions or GraphQL where suitable, version APIs, implement pagination, rate limiting, authentication/authorization, and idempotency for write operations.

**Follow-up Q:** When would you choose GraphQL over REST?  
**Expected Answer:** When clients need flexibility in selecting fields, or when over/under-fetching is an issue.


## 12. System Design Round (Medium-High Depth)

**Design Question:** Design a **multi-tenant SaaS application** where multiple companies use the same application but should not see each other's data.

**Strong Expected Answer:**

- Use a **single codebase**, shared infrastructure.
    
- **Tenant isolation strategies:**
    
    1. **Shared DB, tenant_id column** (simple, but weaker isolation)
        
    2. **Shared DB, separate schemas** (better isolation + cost efficient)
        
    3. **Separate DB per tenant** (highest isolation, more ops overhead)
        
- Tenant should be identified via **JWT claims**, subdomain routing, or API key mapping.
    
- Use **middleware** to enforce tenant scoping before hitting business logic.
    

**Follow-up Q:** How do you prevent one tenant's queries from accessing another tenant's data?

**Expected Answer:** Always add tenant filters at **repository/ORM** layer — never rely on UI or caller. Consider query builder wrappers.

**Red Flag:** "We depend on frontend to send tenant_id" (security flaw).