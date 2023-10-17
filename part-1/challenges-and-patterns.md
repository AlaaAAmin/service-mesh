# Chanllenges of going faster

## The following things must be addressed when moving to a services-oriented architecture:

1. Keeping faults from jumping isolation boundaries
2. Building applications/services capable of responding to changes in their environment
3. Building systems capable of running in partially failed conditions
4. Understanding what’s happening to the overall system as it constantly changes and evolves
5. Inability to control the runtime behaviors of the system
6. Implementing strong security as the attack surface grows
7. Lowering the risk of making changes to the system
8. Enforcing policies about who or what can use system components, and when

## Service interactions resilience

Some patterns have evolved to help make applications more resilient to unplanned, unexpected failures:

1. Client-side load balancing: Give the client the list of possible endpoints, and let it decide which one to call.
2. Service discovery: A mechanism for finding the periodically updated list of healthy endpoints for a particular logical service.
3. Circuit breaking: Shed load for a period of time to a service that appears to be misbehaving.
4. Bulkheading: Limit client resource usage with explicit thresholds (connections, threads, sessions, and so on) when making calls to a service.
5. Timeouts: Enforce time limitations on requests, sockets, liveness, and so on when making calls to a service.
6. Retries—Retry a failed request.
7. Retry budgets: Apply constraints to retries: that is, limit the number of retries in a given period (for example, only retry 50% of the calls in a 10-second window).
8. Deadlines—Give requests context about how long a response may still be useful; if outside the deadline, disregard processing the request.