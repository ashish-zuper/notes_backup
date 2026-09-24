## System Design & Architecture in JavaScript Ecosystems

### **Question**

> You are designing a **multi-tenant SaaS platform** using Node.js where:
> 
> - Each tenant has isolated data
>     
> - The system must handle **webhooks, background jobs, and real-time updates**
>     
> - Traffic can spike unpredictably
>     
> 
> **Design the high-level architecture**, covering:
> 
> - API layer design (REST vs GraphQL)
>     
> - Background job processing
>     
> - Message queues / event-driven patterns
>     
> - Database access patterns and isolation
>     
> - Error handling and retries
>     
> 
> Then deep-dive into:
> 
> - How you would ensure **idempotency** for webhook processing
>     
> - How you would prevent **one tenant from degrading system performance**
>     
> - Trade-offs between **horizontal scaling vs vertical scaling** in Node.js
>