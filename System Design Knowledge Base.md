# System Design Knowledge Base

## Table of Contents
1. [Client-Server Architecture](#1-client-server-architecture)
2. [IP Addressing](#2-ip-addressing)
3. [Domain Name System (DNS)](#3-domain-name-system-dns)
4. [Forward Proxy](#4-forward-proxy)
5. [Reverse Proxy](#5-reverse-proxy)
6. [Latency](#6-latency)
7. [HTTP vs HTTPS](#7-http-vs-https)
8. [APIs (Application Programming Interfaces)](#8-apis-application-programming-interfaces)
9. [REST vs GraphQL](#9-rest-vs-graphql)
10. [Database Systems](#10-database-systems)
11. [SQL vs NoSQL Databases](#11-sql-vs-nosql-databases)
12. [Vertical vs Horizontal Scaling](#12-vertical-vs-horizontal-scaling)
13. [Load Balancing](#13-load-balancing)
14. [Database Indexing](#14-database-indexing)
15. [Data Replication](#15-data-replication)
16. [Sharding (Horizontal Partitioning)](#16-sharding-horizontal-partitioning)
17. [Vertical Partitioning](#17-vertical-partitioning)
18. [Caching Strategies and Patterns](#18-caching-strategies-and-patterns)
19. [CAP Theorem](#19-cap-theorem)
20. [Blob/Object Storage](#20-blobobject-storage)
21. [Content Delivery Networks (CDN)](#21-content-delivery-networks-cdn)
22. [WebSockets](#22-websockets)
23. [Webhooks](#23-webhooks)
24. [Microservices vs Monolithic Architecture](#24-microservices-vs-monolithic-architecture)
25. [Message Queues / Event Streaming](#25-message-queues--event-streaming)
26. [Rate Limiting Strategies](#26-rate-limiting-strategies)
27. [API Gateway](#27-api-gateway)
28. [Idempotency in Distributed Systems](#28-idempotency-in-distributed-systems)
29. [Denormalization](#29-denormalization)

## 1. Client-Server Architecture
### Definition
A distributed interaction model in which clients initiate requests and servers process requests and return responses over a network.
### Core Design Elements
- Separation of presentation, business logic, and data access concerns.
- Stateless or stateful communication model selection.
- Protocol choice, typically HTTP/HTTPS, gRPC, or TCP.
### Trade-Offs
- Centralized servers simplify governance but can become bottlenecks.
- Stateless servers improve scalability but require external state stores.
### Example and Real-World Usage
Web applications where browser clients call backend APIs hosted behind load balancers in cloud environments.

## 2. IP Addressing
### Definition
A logical addressing scheme that uniquely identifies network interfaces for routing traffic across local and wide-area networks.
### Core Design Elements
- IPv4 uses 32-bit addresses; IPv6 uses 128-bit addresses.
- Public versus private ranges determine internet routability.
- Subnetting defines network boundaries and broadcast domains.
### Trade-Offs
- IPv4 has broad compatibility but limited address space.
- IPv6 provides scale and modern networking features but can increase operational complexity during transition.
### Example and Real-World Usage
Kubernetes clusters use private CIDR blocks for pod networking while exposing services through public IPs or ingress endpoints.

## 3. Domain Name System (DNS)
### Definition
A hierarchical, distributed naming system that translates human-readable domain names into IP addresses and service records.
### Core Design Elements
- Recursive resolvers, authoritative name servers, and root/TLD hierarchy.
- Record types such as A, AAAA, CNAME, MX, TXT, and SRV.
- TTL values control cache freshness and propagation behavior.
### Trade-Offs
- Lower TTL improves agility for failover but increases query load.
- Higher TTL reduces resolver traffic but slows traffic redirection.
### Example and Real-World Usage
Global services use geo-DNS and health-based routing to direct users to healthy regional endpoints.

## 4. Forward Proxy
### Definition
An intermediary server that sits between clients and external servers, forwarding outbound requests on behalf of clients.
### Core Design Elements
- Policy enforcement for egress traffic.
- Request filtering, authentication, and auditing.
- Optional content caching for repeated external requests.
### Trade-Offs
- Improves security and governance but adds a network hop.
- Central control simplifies compliance but introduces a potential single point of failure.
### Example and Real-World Usage
Enterprise environments route employee internet access through forward proxies for DLP and threat inspection.

## 5. Reverse Proxy
### Definition
An intermediary server that receives inbound client traffic and forwards it to backend services.
### Core Design Elements
- TLS termination, request routing, and connection pooling.
- Header normalization, WAF integration, and compression.
- Load distribution across backend instances.
### Trade-Offs
- Improves performance and security posture but adds operational complexity.
- Centralized ingress control can become critical infrastructure risk if not highly available.
### Example and Real-World Usage
Nginx or Envoy fronts microservices, terminating TLS and routing requests by path or host.

## 6. Latency
### Definition
The elapsed time between request initiation and response completion, measured at network and application layers.
### Core Design Elements
- Network latency, server processing time, and queue wait time.
- Percentile metrics such as p50, p95, and p99.
- Tail-latency management through timeouts, retries, and load shedding.
### Trade-Offs
- Aggressive retries may improve success rate but can amplify load and worsen tail latency.
- Strong consistency often increases latency relative to eventually consistent designs.
### Example and Real-World Usage
Payment systems optimize p99 latency to reduce transaction abandonment under peak demand.

## 7. HTTP vs HTTPS
### Definition
HTTP is an application protocol for data exchange; HTTPS is HTTP secured with TLS for confidentiality, integrity, and authentication.
### Core Design Elements
- TLS handshake, certificate validation, and session encryption.
- HSTS, modern cipher suites, and certificate rotation.
- HTTP/2 or HTTP/3 transport enhancements over TLS.
### Trade-Offs
- HTTPS introduces cryptographic overhead but is mandatory for modern security and compliance.
- Operational requirements increase due to certificate lifecycle management.
### Example and Real-World Usage
Production APIs enforce HTTPS-only access and reject plaintext HTTP except for controlled redirects.

## 8. APIs (Application Programming Interfaces)
### Definition
Contract-driven interfaces that expose system capabilities and data to internal and external consumers.
### Core Design Elements
- Resource modeling, versioning strategy, and error contracts.
- Authentication and authorization controls.
- Backward compatibility and deprecation governance.
### Trade-Offs
- Rich APIs accelerate integrations but increase maintenance burden.
- Strict versioning improves reliability but can slow product evolution.
### Example and Real-World Usage
B2B platforms publish authenticated APIs with rate limits and SLA-backed availability guarantees.

## 9. REST vs GraphQL
### Definition
REST exposes resource-oriented endpoints; GraphQL exposes a typed query language for client-specified data retrieval.
### Core Design Elements
- REST: endpoint granularity, HTTP semantics, and cacheability.
- GraphQL: schema design, resolvers, and query complexity controls.
### Trade-Offs
- REST is operationally simple and cache-friendly but can over-fetch or under-fetch.
- GraphQL improves client flexibility but requires strong governance for query cost and backend fan-out.
### Example and Real-World Usage
Mobile applications often use GraphQL for tailored payloads, while public APIs frequently use REST for broad interoperability.

## 10. Database Systems
### Definition
Persistent data platforms that provide storage, retrieval, consistency guarantees, and concurrency control.
### Core Design Elements
- Data model, transaction semantics, indexing, and durability.
- Backup, recovery, and high-availability architecture.
- Capacity planning for compute, storage, and IOPS.
### Trade-Offs
- Strong transactional guarantees can reduce throughput.
- Specialized databases optimize specific workloads but increase platform heterogeneity.
### Example and Real-World Usage
E-commerce systems combine transactional stores for orders with analytical stores for reporting.

## 11. SQL vs NoSQL Databases
### Definition
SQL databases use relational schemas and ACID transactions; NoSQL databases prioritize flexible models and horizontal scale patterns.
### Core Design Elements
- SQL: normalized schemas, joins, declarative queries.
- NoSQL: key-value, document, wide-column, and graph models.
### Trade-Offs
- SQL excels in relational integrity and complex querying.
- NoSQL improves scale and agility for certain access patterns but may shift consistency and query complexity to application code.
### Example and Real-World Usage
A platform can use PostgreSQL for billing and a document store for user-generated content metadata.

## 12. Vertical vs Horizontal Scaling
### Definition
Vertical scaling increases resources on a single node; horizontal scaling adds more nodes to distribute load.
### Core Design Elements
- Vertical: CPU, memory, and storage upgrades.
- Horizontal: stateless service design, partitioning, and distributed coordination.
### Trade-Offs
- Vertical scaling is simple but constrained by hardware ceilings.
- Horizontal scaling offers elastic growth but introduces distributed-system complexity.
### Example and Real-World Usage
Stateless API tiers scale horizontally behind load balancers during seasonal traffic spikes.

## 13. Load Balancing
### Definition
A traffic distribution mechanism that routes client requests across multiple service instances for resilience and throughput.
### Core Design Elements
- Algorithms such as round-robin, least-connections, and weighted routing.
- Health checks and automatic instance removal.
- Layer 4 versus Layer 7 balancing decisions.
### Trade-Offs
- Layer 7 provides advanced routing but adds processing overhead.
- Aggressive health checks improve failure detection but can generate excess control traffic.
### Example and Real-World Usage
Cloud load balancers distribute API traffic across availability zones for high availability.

## 14. Database Indexing
### Definition
Auxiliary data structures that accelerate query performance by reducing full-table scans.
### Core Design Elements
- B-tree, hash, and specialized index types.
- Composite index column ordering based on access predicates.
- Selectivity and cardinality considerations.
### Trade-Offs
- Indexes improve read performance but increase write amplification and storage cost.
- Over-indexing can degrade insert/update throughput.
### Example and Real-World Usage
Order systems index customer_id and created_at to support recent-order retrieval and operational dashboards.

## 15. Data Replication
### Definition
The process of maintaining multiple copies of data across nodes or regions for availability, durability, and locality.
### Core Design Elements
- Synchronous versus asynchronous replication.
- Leader-follower or multi-leader topologies.
- Replication lag monitoring and failover orchestration.
### Trade-Offs
- Synchronous replication strengthens consistency but increases write latency.
- Asynchronous replication reduces latency but risks stale reads and data loss windows.
### Example and Real-World Usage
Managed relational services replicate across zones to survive infrastructure failures with minimal downtime.

## 16. Sharding (Horizontal Partitioning)
### Definition
A scaling strategy that splits large datasets across independent partitions based on a shard key.
### Core Design Elements
- Shard key selection aligned to query distribution.
- Routing layer for shard discovery and request dispatch.
- Rebalancing and hotspot mitigation strategies.
### Trade-Offs
- Improves write/read parallelism but complicates cross-shard queries and transactions.
- Poor shard-key selection causes uneven load and operational instability.
### Example and Real-World Usage
Multi-tenant SaaS platforms shard tenant data by tenant_id to isolate workload growth.

## 17. Vertical Partitioning
### Definition
A schema strategy that splits table columns into separate tables based on access frequency or sensitivity.
### Core Design Elements
- Separation of hot and cold columns.
- Access-path optimization for narrow queries.
- Independent security controls for sensitive attributes.
### Trade-Offs
- Reduces I/O for common queries but introduces join complexity.
- Can improve cache efficiency while increasing schema management overhead.
### Example and Real-World Usage
User profile systems separate frequently accessed identity fields from large optional preference blobs.

## 18. Caching Strategies and Patterns
### Definition
Techniques for storing frequently accessed data in low-latency layers to reduce backend load and response times.
### Core Design Elements
- Cache-aside, read-through, write-through, and write-back patterns.
- Eviction policies such as LRU, LFU, and TTL-based expiration.
- Coherency controls and cache invalidation design.
### Trade-Offs
- Caching improves latency and throughput but risks stale data and consistency anomalies.
- Higher cache hit rates reduce cost but require disciplined key design and invalidation logic.
### Example and Real-World Usage
Catalog services cache product summaries in Redis with event-driven invalidation on product updates.

## 19. CAP Theorem
### Definition
A distributed-system principle stating that during a network partition, a system can guarantee either consistency or availability, but not both simultaneously.
### Core Design Elements
- Consistency: every read receives the latest write.
- Availability: every request receives a non-error response.
- Partition tolerance: system continues operation despite network segmentation.
### Trade-Offs
- CP systems prioritize correctness under partition at the expense of potential request rejection.
- AP systems prioritize responsiveness under partition with eventual consistency reconciliation.
### Example and Real-World Usage
Financial ledgers favor CP behavior, while social feed systems often tolerate AP behavior for user responsiveness.

## 20. Blob/Object Storage
### Definition
A scalable storage model for unstructured data objects addressed by keys within buckets or containers.
### Core Design Elements
- Object immutability patterns and metadata tagging.
- Lifecycle policies for archival and deletion.
- Multi-part upload and pre-signed access controls.
### Trade-Offs
- Highly durable and cost-efficient for large objects but not suited for low-latency random updates.
- Strong scalability with eventual consistency considerations in some operations.
### Example and Real-World Usage
Media platforms store images and videos in object storage and serve them through CDN layers.

## 21. Content Delivery Networks (CDN)
### Definition
A geographically distributed edge network that caches and serves content closer to end users.
### Core Design Elements
- Edge caching, origin shielding, and cache key normalization.
- Purge/invalidation mechanisms.
- TLS at edge and regional routing optimization.
### Trade-Offs
- Significantly reduces latency and origin load but can serve stale content if invalidation is misconfigured.
- Improves resilience yet requires disciplined cache control policies.
### Example and Real-World Usage
Global web applications use CDNs for static assets, software downloads, and edge security filtering.

## 22. WebSockets
### Definition
A full-duplex, persistent communication protocol over a single TCP connection for real-time bidirectional messaging.
### Core Design Elements
- Connection lifecycle management and heartbeat mechanisms.
- Stateful session mapping and fan-out architecture.
- Backpressure and message ordering strategy.
### Trade-Offs
- Enables low-latency real-time interaction but increases infrastructure statefulness and connection management complexity.
- Persistent connections can raise resource utilization under large concurrent populations.
### Example and Real-World Usage
Trading dashboards and collaborative editors rely on WebSockets for sub-second update propagation.

## 23. Webhooks
### Definition
Event-driven HTTP callbacks where a producer pushes notifications to subscribed consumer endpoints.
### Core Design Elements
- Delivery signing and endpoint authentication.
- Retry policies with exponential backoff and dead-letter handling.
- Idempotent event processing at consumers.
### Trade-Offs
- Reduces polling overhead but introduces delivery uncertainty and consumer endpoint dependency.
- Scales well for event fan-out when contracts are versioned and monitored.
### Example and Real-World Usage
Payment providers emit webhook events for authorization, capture, and settlement lifecycle changes.

## 24. Microservices vs Monolithic Architecture
### Definition
Monolithic architecture packages functionality in a single deployable unit; microservices decompose functionality into independently deployable services.
### Core Design Elements
- Monolith: shared codebase and centralized deployment.
- Microservices: bounded contexts, service contracts, and decentralized data ownership.
### Trade-Offs
- Monoliths simplify early development and operational overhead.
- Microservices improve team autonomy and scalability but add distributed-system concerns such as observability, network reliability, and data consistency.
### Example and Real-World Usage
Organizations often begin with a modular monolith and evolve to microservices where domain or scale boundaries justify decomposition.

## 25. Message Queues / Event Streaming
### Definition
Asynchronous communication mechanisms that decouple producers and consumers for reliable workload distribution or ordered event propagation.
### Core Design Elements
- Queues support competing consumers and at-least-once delivery patterns.
- Streams preserve ordered logs with consumer offsets and replay.
- Dead-letter queues and retention configuration.
### Trade-Offs
- Improves resilience and elasticity but introduces eventual consistency and operational tuning requirements.
- High throughput can increase complexity in partitioning and consumer lag management.
### Example and Real-World Usage
Order pipelines use queues for fulfillment jobs and event streams for audit and analytics pipelines.

## 26. Rate Limiting Strategies
### Definition
Controls that constrain request rates to protect service capacity, fairness, and abuse resistance.
### Core Design Elements
- Algorithms: token bucket, leaky bucket, fixed window, and sliding window.
- Scope dimensions: user, API key, IP, tenant, or endpoint.
- Response semantics, including 429 handling and retry hints.
### Trade-Offs
- Strict limits protect infrastructure but can degrade user experience.
- Generous limits improve usability but increase risk during abuse or traffic spikes.
### Example and Real-World Usage
Public APIs enforce per-key and per-minute quotas with burst allowances and adaptive throttling during incidents.

## 27. API Gateway
### Definition
A centralized ingress layer that brokers external API traffic to internal services while enforcing cross-cutting policies.
### Core Design Elements
- Authentication, authorization, and request transformation.
- Rate limiting, routing, and protocol translation.
- Observability integration for tracing, metrics, and logging.
### Trade-Offs
- Simplifies client integration and policy consistency but can become a performance and availability critical point.
- Feature concentration improves governance while increasing gateway complexity.
### Example and Real-World Usage
Enterprise platforms expose a unified API endpoint through gateways that route traffic to domain-specific services.

## 28. Idempotency in Distributed Systems
### Definition
A property where repeated execution of the same operation with the same intent produces the same effective outcome.
### Core Design Elements
- Idempotency keys and deduplication stores.
- Deterministic request fingerprinting and replay handling.
- Safe retry semantics for network and timeout failures.
### Trade-Offs
- Enhances reliability for retried operations but requires storage and lifecycle management for keys.
- Incorrect key design can cause false deduplication or duplicate side effects.
### Example and Real-World Usage
Payment APIs use idempotency keys to prevent duplicate charges during client retries.

## 29. Denormalization
### Definition
A data modeling technique that intentionally introduces redundancy to optimize read performance and simplify access patterns.
### Core Design Elements
- Precomputed aggregates and duplicated reference fields.
- Event-driven synchronization and reconciliation jobs.
- Versioning and consistency controls across duplicated data.
### Trade-Offs
- Faster reads and simpler queries at the cost of increased write complexity and storage overhead.
- Requires robust integrity monitoring to prevent divergence.
### Example and Real-World Usage
Analytics and feed-generation systems denormalize data into read-optimized views for low-latency consumption.

## Conclusion
These concepts form the architectural foundation for designing secure, scalable, and resilient distributed systems. Effective system design requires balancing trade-offs among performance, consistency, operability, cost, and developer velocity in the context of explicit business and reliability objectives.
