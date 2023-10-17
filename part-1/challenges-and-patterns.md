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
6. Retries: Retry a failed request.
7. Retry budgets: Apply constraints to retries: that is, limit the number of retries in a given period (for example, only retry 50% of the calls in a 10-second window).
8. Deadlines: Give requests context about how long a response may still be useful; if outside the deadline, disregard processing the request.

## Understanding what’s happening in real time

As we make changes to our services, do we understand what impact (positive or negative) they will have? Do we know how things are running before we make changes?

Observing the system with metrics, logs, and traces is a crucial part of running a services architecture to ensure that the system is not on the verge of collapse.

# Solving these challenges with application libraries

Large internet companies like google and netflix pioneered the cloud infrastructure as we know it today.
they built application libraries to solve the challenges of running services in a cloud native environments like:
- Hystrix: Circuit breaking and bulkheading
- Ribbon: Client-side load balancing
- Eureka: Service registration and discovery
- Zuul: Dynamic edge proxy

## Drawbacks to application-specific libraries

Although we’ve mitigated a concern about large-scale services architectures when we decentralize and distribute the implementation of application resiliency into the
applications themselves, we’ve introduced some new challenges.

- The first challenge is around the expected assumptions of any application:
    If we wish to introduce a new service into our architecture, it will be constrained to implementation decisions made by other people and other teams.

- The second issue is restrictions around introducing a new language or framework to implement a service.

- Finally, maintaining a handful of libraries across a bunch of programming languages and frameworks requires a lot of discipline and is very hard to get right.

Although the decentralization of application networking is better for cloud architectures, the operational burden and constraints this approach puts on a system in
exchange will be difficult for most organizations to swallow. 

# Pushing these concerns to the infrastructure

These basic application-networking concerns are not specific to any particular application, language, or framework. Retries, timeouts, client-side load balancing, circuit
breaking, and so on are also not differentiating application features.
They are critical concerns to have as part of your service, but investing massive time and resources into language-specific implementations for each language you intend to use (including the other drawbacks from the previous section) is a waste of time.
What we really want is a technology-agnostic way to implement these concerns and relieve applications from having to do so themselves.

## The application-aware service proxy

Using a proxy is a way to move these horizontal concerns into the infrastructure.
A proxy is an intermediate infrastructure component that can handle connections and redirect them to appropriate backends.
We use proxies all the time (whether we know it or not) to handle network traffic, enforce security, and load balance work to backend servers.
For example, **HAProxy** is a simple but powerful reverse proxy for distributing connections across many backend servers. 