# Microservices Introduction
## Concept
- A typical microservices architecture breaks a large monolithic application into smaller independent units that communicate with each other through APIs where each unit/service handles a specific business requirement e.g. authentication, payments, catalog, orders etc.
# Core Components
- **API Gateway:** Acts as a single entry point to all backend microservices. Responsible for handling routing, authentication, rate limiting, caching and protocol translation.
- **Service Registry/Discovery:** Keeps track of active service instances and enables dynamic service discovery. Tools: Consul, Eureka, etc.
- **DNS:** It maps service names to IPs for internal and external access. It is often integrated with service discovery for microservices.
- **Load Balancer:** It distributes incoming traffic across multiple instances of a microservice to ensure high availability and scalability. It can be hardware based, software based or cloud managed. (e.g. Nginx, AWS ELB).
- **Database per Service:** Each service has its own database to maintain loose coupling. It can be SQL (PostgreSQL, MySQL) or NoSQL (MongoDB, DynamoDB, Cassandra) depending on specific requirements.
- **SQL Databases:** Used when structured data storage is required. It supports transactions and complex queries. It is best for relational data and consistency needs.
- **NoSQL Databases:** Provides flexible schema, horizontal scalability and high throughput. Suitable for unstructured data, caching and fast lookups.
- **Synchronous Communication:** Request - Response Communication between services, usually over HTTP/REST or gRPC. Easier to implement but can increase latency.
- **Asynchronous Communication:** Event-driven communication via message brokers. Decouples services and improves scalability and resilience.
- **Message Broker:** They handle async communication, message queues, pub/sub, and event streaming. E.g. Kafka, RabbitMQ, or AWS SQS
- **Swagger/OpenAPI:** Used for API documentation and contract generation. Helps teams understand endpoints, request/response models, and test APIs easily.
- **Event Sync/Event Bus:** Services publish events to an event bus (Kafka, NATS). Other services subscribe to events for **reactive workflows**. Supports eventual consistency.
- **Externalized Config and Logs:** Centralized configuration (e.g. Spring Cloud Config, Consul) and externalized logs (ELK stack, CloudWatch) for easier management and troubleshooting.
- **Monitoring/Tracing:** Observability tools to track service health, performance and errors. Examples: Prometheus, Grafana, Jaeger, Zipkin.
- **Reporting/Analytics:** Aggregates data from multiple services for business intelligence and reporting. Often build on ELK, Redshift, Snowflake, or custom analytics pipelines.
# Domain Name System (DNS)
- It translates human readable domain names into IP addresses.
- Client sends a request to myapp.com
- DNS resolver queries: Root Server -> TLD Server (.com) -> Authoritative Server
- Returns IP address.
- Browser connects to that IP.
- In Cloud Context: Services like AWS Route 53, Azure DNS, or Cloudflare manage DNS zones with load balancing, failover and latency based routing.
# Load Balancers
- It evenly distributes incoming requests among multiple backend servers to ensure high availability, fault tolerance, and scalability. 
- Types of load balancers:
	- L4 (Transport)
		- Operates on TCP/UDP
		- Example: AWS NLB, HAProxy
		- Use case: Fast, for network level routing
	- L7 (Application)
		- Operates on HTTP/HTTPS
		- Example: AWS ALB, Nginx, Traefik
		- Use case: Smarter, inspects URLs, headers and cookies.
- Features: 
	- Health Checks
	- Sticky sessions
	- SSL termination
	- Auto-scaling integration
# Synchronous vs Asynchronous Communication
- In **synchronous communication**, the caller sends a request and waits for a response before moving forward. This approach is common in real-time operations such as user login, where an immediate reply is needed. It usually relies on protocols like **HTTP/HTTPS**. However, it can lead to tight coupling between services and may suffer from latency issues.
- In **asynchronous communication**, the caller sends a message and continues without waiting for a response. This is often used for background or decoupled tasks such as sending notifications or processing billing. It uses protocols like **AMQP**, **MQTT**, or **Kafka**. The downside is that it can be harder to debug and typically involves eventual consistency rather than immediate feedback.
- **Visual Representation:**
	- **Synchronous:** Client → Service A → _waits_ → Response
	- **Asynchronous:** Client → Service A → _sends to Queue_ → Service B processes later
# SQL vs NoSQL Databases
- **SQL databases** (relational) organize data in tables with rows and columns and rely on a **fixed schema**. They typically scale **vertically** by adding more CPU or memory to a single server. Common examples include **MySQL** and **PostgreSQL**. These databases are ideal for structured data and transactional systems where data integrity is crucial. Queries are written using **SQL**.
- **NoSQL databases** (non-relational) store data in more flexible formats such as **key-value pairs**, **documents**, **graphs**, or **wide-column stores**. They support a **dynamic schema** and scale **horizontally** by adding more nodes to the system. Examples include **MongoDB**, **DynamoDB**, and **Cassandra**. NoSQL is often used for systems that require high scalability and flexibility, using **custom query languages** (often JSON-like).
- In modern architectures, especially microservices, teams often combine both approaches—a concept known as **polyglot persistence**—using SQL for structured data and NoSQL for more flexible or large-scale components.
# API Gateway
- Its role is to sit between the client and the backend services.
- Its responsibilities include:
	- Routing: Direct request to proper microservice.
	- Authentication/Authorization: Validate tokens (OAuth2, JWT)
	- Rate Limiting & Throttling: Protect from overload.
	- Request Transformation: Modify headers, URLs, or payloads.
	- Caching: Improve response speed.
	- Monitoring/Logging: Centralized request tracing.
- Popular gateways include AWS API gateway, Kong, Nginx, Istio (in service mesh), Apigee (Google Cloud)
# Externalizing Logs
- Each microservice runs in containers/pods - their local logs vanish when the container restarts. So logs are centralized in an external system.
- **Common Logging Setup**
	- **Fluentd / Fluent Bit / Logstash** – These tools are responsible for **collecting and aggregating logs** from different sources.
	- **Elasticsearch / Loki** – Used to **store and index logs** so they can be efficiently searched and analyzed.
	- **Kibana / Grafana** – Provide **visual dashboards** and allow users to **search, filter, and monitor logs** in real time.
	- **Cloud-native options** – Include services like **Dynatrace**, **CloudWatch (AWS)**, and **Stackdriver (GCP)**, which offer integrated logging and monitoring solutions within their respective cloud ecosystems.
- Benefits include unified view of system behavior, easier debugging and auditing, and log based alerting via (Prometheus + Alertmanager)
# 12-Factor Apps
- It is a design philosophy for building scalable, cloud ready microservices.
- Principles: 
	1. **Codebase** – Maintain a single codebase tracked in version control, but deploy it to multiple environments.
	2. **Dependencies** – Clearly specify all dependencies using a package or dependency manager (like pip or npm).
	3. **Config** – Store configuration details in environment variables, not in the source code.
	4. **Backing Services** – Treat databases, queues, and caches as external resources that can be swapped without code changes.
	5. **Build, Release, Run** – Keep these stages distinct: build the code, combine it with config to create a release, and then run it.
	6. **Processes** – Run the application as **stateless processes**, with no dependency on local storage or memory between requests.
	7. **Port Binding** – Expose the app’s services through a specific port rather than relying on an external web server.
	8. **Concurrency** – Scale the application by running multiple process instances.
	9. **Disposability** – Ensure fast startup and graceful shutdown to improve resilience and scaling.
	10. **Dev/Prod Parity** – Keep development, staging, and production environments as similar as possible.
	11. **Logs** – Treat logs as continuous event streams, not as files to be managed manually.
	12. **Admin Processes** – Run administrative or maintenance tasks (like database migrations) as **one-time processes**, separate from the main app.
- These principles ensure portability, scalability, and resilience - ideal for microservices, containers and Kubernetes.
