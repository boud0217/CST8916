# Assignment 2: Cloud Service Providers Comparison Report
## Executive Summary 
Real‑time data processing has become essential for industries ranging from finance to IoT and e‑commerce. Cloud Service Providers (CSPs) — AWS, Azure, and GCP — each deliver distinct services for WebSockets, GraphQL, data streaming, and stream analytics. This report compares their offerings, focusing on cost, performance, ease of integration, and ecosystem maturity.  
AWS provides strong real‑time capabilities through Kinesis for streaming and AppSync for GraphQL. Kinesis offers serverless ingestion, analytics, and delivery pipelines, while AppSync simplifies GraphQL APIs with built‑in subscriptions. AWS excels in high‑throughput scenarios, integrates seamlessly with its broader ecosystem (Lambda, DynamoDB, SageMaker), and is widely adopted in regulated industries. The trade‑offs include vendor lock‑in and rising costs at scale.  
Azure emphasizes enterprise integration with Event Hubs for ingestion and Stream Analytics for SQL‑based real‑time queries. GraphQL is supported via App Service, Functions, or open‑source frameworks. Azure’s strength lies in IoT and analytics, with direct connections to Power BI and IoT Hub. Its limitations are reduced flexibility compared to custom frameworks and reliance on SQL‑style processing.  
GCP focuses on advanced analytics pipelines with Pub/Sub for messaging, Dataflow for stream/batch processing, and Datastream for change data capture. GraphQL is supported via Cloud Run or GKE using Apollo/Hasura. GCP’s ecosystem is powerful for data‑intensive workloads, but requires more expertise and can be costly for continuous pipelines.
We find out that : 
- AWS is best for financial and mission‑critical workloads requiring scale, compliance, and ML integration.
- Azure is most suitable for IoT and smart city projects, thanks to Event Hubs, Stream Analytics, and Power BI.
- GCP excels in data‑intensive analytics pipelines, leveraging Pub/Sub and Dataflow for complex transformations.

## Introduction
In today’s digital landscape, real‑time data processing has become a cornerstone for modern applications. From financial institutions monitoring transactions to smart cities managing IoT devices, the ability to capture, analyze, and act on data streams instantly is critical. Cloud Service Providers (CSPs) such as AWS, Azure, and GCP offer a range of solutions for WebSockets, GraphQL, data streaming, and stream analytics, each with distinct strengths and trade‑offs. This report explores these services, compares their capabilities, and evaluates their suitability for different real‑world scenarios by considering cost, performance, ease of integration, and ecosystem maturity.


### Service Comparison
#### RESTful API Services
##### **AWS**
AWS's primary RESTful API service is "**Amazon API Gateway**". It is designed to simplify API creation and management while ensuring scalability and security. Amazon API Gateway is a fully managed service that lets developers create, publish, maintain, monitor, and secure RESTful APIs at any scale. It acts as a front door for applications to access data, business logic, or functionality from backend services such as AWS Lambda, EC2, or DynamoDB.  
As advantages, it works natively with Lambda, DynamoDB, S3, IAM, CloudWatch and other AWS services. This allows deep integration in AWS ecosystem. It also supports many protocols like WebSockets and GraphQL subscriptions via AppSync. This flexibility allows developers to choose the right protocol for each scenario. It integrates CloudWatch for request metrics, latency, and error tracking that is useful for real-time troubleshooting and performance optimization. API Gateway auto-scales to handle millions of requests per second, critical for apps with unpredictable traffic.  
However, API Gateway have inconvenients. It introduces extra hops compared to direct backend calls. For ultra-low-latency apps (e.g., financial trading), this can be a bottleneck. For high-throughput real-time apps (millions of events per minute), costs can escalate quickly compared to self-hosted gateways. Mapping templates, throttling policies, and caching rules can be complex to set up for real-time pipelines. Developers often face a steep learning curve when tuning for performance.  
AWS API Gateway is powerful for remote data and real-time applications because it combines REST, WebSockets, and GraphQL with streaming backends like Kinesis. The trade-off is latency, cost, and complexity, you gain scalability and security, but you must carefully architect to avoid inefficiencies.  


##### **Azure**
Azure provides many services for REST API : **Azure App Service**, **Azure Functions** and **Azure API Management**.  
**Azure API Management** is an enterprise-grade API gateway and lifecycle management platform. it provides a central gateway for REST APIs with features like versioning, policies, analytics, and a developer portal. While it manges full lifecycle, strong security (AAD integration), hybrid/multi-cloud support and analytics, it's also high cost, complex, latency overhead, less focus on real-time protocols (WebSockets/GraphQL).  
**Azure App Service** is a PaaS (Platform as a Service) offering hosting web applications and APIs without managing infrastructure. Developers can deploy RESTful APIs directly as API Apps or Web Apps and it supports multiple programming languages. it's easy to deploy and scale, to integrate with Azure DevOps and CI/CD pipelines, supports custom domains, SSL, and authentication and ideal for hosting traditional REST APIs with minimal ops overhead. But, it has less features than Azure API Management, scaling costs can rise for high-throughput real-time workloads and requires manual implementation of advanced features like rate limiting, caching.  
**Azure Functions** is a serverless compute service that runs event-driven code, often used to expose lightweight RESTful APIs. Functions can be triggered by HTTP requests, making them natural REST endpoints. They integrate with other Azure services. It has pay-per-execution pricing model, allows rapid development with minimal infrastructure management and is perfect for microservices and event-driven architectures. However, it encounters cold start latency (when not used for longtime), has limited execution time and cannot be used for complex APIs and debugging and monitoring can be trickier compared to full App Service.  
| Service | Best For | Advantages | Inconvenients | 
| ------- | -------- | ---------- | ------------- | 
| API Management | Enterprise API lifecycle management | Security, versioning, analytics, developer portal | Expensive, complex, latency overhead |
| App Service | Hosting traditional REST APIs | Easy deployment, scaling, CI/CD integration | Less governance, scaling costs, manual advanced features |
| Functions | Lightweight REST endpoints | Pay-per-execution, rapid development, event-driven | Cold start latency, limited execution time, complex APIs |

##### **Google Cloud**
GCP provides many services for REST API: **Cloud Endpoints**, **API Gateway**, **Cloud Functions**, and **Cloud Run**.  
**Cloud Endpoints** is a lightweight API management service that lets you expose RESTful APIs using OpenAPI or gRPC definitions. It provides authentication, monitoring, and quota enforcement. While it is simple, cost-effective, and integrates with IAM and Firebase Auth, it has limited advanced features, no developer portal, and is less suited for large-scale enterprise governance.  
**API Gateway** is a fully managed gateway service designed for serverless backends (Cloud Functions, Cloud Run, App Engine). It provides routing, authentication, monitoring, and scaling for REST APIs. It offers managed scaling, OpenAPI support, and integration with Cloud Logging/Monitoring. However, it is newer, has fewer enterprise features compared to AWS API Gateway or Azure APIM, and lacks a built-in developer portal.  
**Cloud Functions** is a serverless compute service that runs event-driven code, often used to expose lightweight RESTful APIs. Functions can be triggered by HTTP requests, making them natural REST endpoints. They integrate with other GCP services like Pub/Sub and Firestore. They are cost-efficient with pay-per-execution pricing, auto-scaling, and rapid development. But they suffer from cold start latency, limited execution time, and are better suited for lightweight APIs than complex enterprise APIs.  
**Cloud Run** is a fully managed container service that allows developers to deploy any containerized application and expose it via HTTPS as a REST API. It is flexible (supports any language/runtime), scales to zero when idle, and integrates easily with GCP services. However, it has cold starts when idle, requires containerization knowledge, and involves more operational overhead compared to Functions.  
| Service | Best For | Advantages | Inconvenients |
|-------- |--------- |----------- |-------------- |
| Cloud Endpoints | Lightweight API management | Simple, cost-effective, IAM integration | Limited features, no portal, manual lifecycle mgmt |
| API Gateway | Serverless REST APIs | Managed scaling, OpenAPI support, monitoring | Newer, fewer enterprise features, no portal |
| Cloud Functions | Lightweight REST endpoints | Pay-per-execution, auto-scaling, rapid dev | Cold start latency, limited execution time |
| Cloud Run | Containerized REST APIs | Flexible runtime, scales to zero, cost savings | Cold starts, containerization required, more ops |


####  Websockets
##### **AWS**
AWS provides WebSocket services mainly through Amazon API Gateway (WebSocket APIs).  
Amazon API Gateway (WebSocket APIs) is a fully managed service that enables bi-directional communication between clients and servers using the WebSocket protocol. It allows developers to build real-time applications such as chat systems, live dashboards, multiplayer games, and notifications. API Gateway manages the connection lifecycle (connect, disconnect, message routing), integrates with backend services like AWS Lambda and DynamoDB, and scales automatically to handle large numbers of concurrent connections. While it provides managed WebSocket connections, deep AWS integration, and scalability, it can be costly at scale, adds latency overhead compared to direct socket servers, and requires careful design for state management and message routing.  

##### **Azure**
Azure WebSocket main services are Azure Web PubSub and Azure App Service (WebSockets support).  
Azure Web PubSub is a fully managed service for real-time messaging using WebSockets and publish-subscribe patterns. It enables developers to build applications like live dashboards, chat apps, multiplayer games, and collaborative tools. It manages client connections, scaling, authentication, and message broadcasting. While it provides managed WebSocket connections, integration with Azure services, and scalability, it can be costly at scale, requires learning the PubSub model, and adds complexity when integrating with custom backends.  
Azure App Service (WebSockets support) allows developers to enable WebSocket connections directly in their hosted web applications or APIs. It is useful for scenarios where applications need persistent connections without a separate messaging service. While it is simple to enable, integrates with existing App Service deployments, and supports multiple programming languages, it lacks advanced features like connection management, message routing, and scaling optimizations compared to Azure Web PubSub.  

| Service | Best For | Advantages | Inconvenients |
|---------|----------|------------|---------------|
| Azure Web PubSub | Real-time messaging & Pub/Sub | Managed connections, scalable, Azure integration | Costly at scale, PubSub learning curve, backend complexity |
| App Service (WebSockets)| Persistent connections in web apps | Easy to enable, integrates with App Service, multi-language | Limited features, no advanced routing, less optimized scaling |

##### **GCP**
GCP WebSocket services are Cloud Run, App Engine, and Google Kubernetes Engine (GKE), since Google Cloud does not offer a dedicated managed WebSocket service like AWS API Gateway or Azure Web PubSub.  
Cloud Run is a fully managed container service that can host applications supporting WebSockets. Developers can deploy any containerized app (Node.js, Python, Go, etc.) with WebSocket libraries (e.g., Socket.IO) and expose it via HTTPS. It scales automatically and integrates with GCP services. While it is flexible, supports any runtime, and scales to zero when idle, it suffers from cold starts, requires containerization knowledge, and persistent WebSocket connections may complicate scaling.  
App Engine (Flexible/Standard) supports WebSockets in applications deployed on its platform. It allows developers to build real-time apps without managing infrastructure. While it is easy to deploy, integrates with GCP services, and supports multiple languages, it has limitations in scaling persistent connections, less flexibility compared to Cloud Run, and higher costs for long-lived connections.  
Google Kubernetes Engine (GKE) allows developers to run containerized workloads with full control, including WebSocket servers. It is ideal for large-scale real-time applications where developers need fine-grained control over scaling and networking. While it provides maximum flexibility, scalability, and control, it requires more operational overhead, cluster management, and expertise compared to serverless options.  

| Service | Best For | Advantages | Inconvenients |
|---------|----------|------------|---------------|
| Cloud Run | Containerized WebSocket apps | Flexible runtime, auto-scaling, integrates with GCP  | Cold starts, containerization required, scaling persistent connections |
| App Engine     | WebSockets in hosted web apps     | Easy deployment, multi-language support, GCP integration | Limited scaling for persistent connections, less flexible, higher costs |
| GKE  | Large-scale WebSocket workloads   | Maximum flexibility, scalability, full control       | Operational overhead, cluster management complexity, requires expertise |

####  GraphQL
##### **AWS**
The primary GraphQL offering on AWS is AppSync, a managed service for building APIs.  
AWS AppSync is a fully managed service that allows developers to build GraphQL APIs with real-time data capabilities. It integrates with data sources such as DynamoDB, Lambda, RDS, and Elasticsearch, and supports subscriptions for live updates using WebSockets. AppSync automatically handles connection management, scaling, and filtering of events, making it easier to build collaborative applications, dashboards, and mobile apps. While it simplifies GraphQL adoption, provides strong integration with AWS services, and supports offline synchronization for mobile clients, it also introduces vendor lock-in, has a learning curve for teams new to GraphQL, and costs can rise with many concurrent subscriptions or complex queries.  

##### **Azure**
Azure does not offer a dedicated managed GraphQL service like AWS AppSync. Instead, developers typically implement GraphQL APIs using Azure App Service, Azure Functions, or by deploying open-source GraphQL servers (such as Apollo Server or Hasura) on Azure infrastructure.  
Azure App Service (GraphQL via API Apps) can host GraphQL servers built with frameworks like Apollo or Hot Chocolate. It provides a PaaS environment where developers deploy their GraphQL APIs without managing infrastructure. This makes it easy to integrate with CI/CD pipelines, scale applications, and connect to Azure databases. While it simplifies deployment and supports multiple languages, it lacks native GraphQL features, requires manual setup for subscriptions, and scaling costs can increase for real-time workloads.  
Azure Functions (GraphQL endpoints) allow developers to expose GraphQL APIs in a serverless model. Functions can be triggered by HTTP requests and run GraphQL resolvers, integrating with Cosmos DB or other Azure services. This approach is cost-efficient, scales automatically, and is well-suited for microservices. However, cold start latency can affect performance, execution time is limited, and complex GraphQL schemas may be harder to manage in a serverless environment.  
Open-source GraphQL frameworks on Azure (Apollo, Hasura, Hot Chocolate) are often deployed on App Service, AKS (Azure Kubernetes Service), or VMs. They provide full GraphQL capabilities, including subscriptions for real-time data. The advantage is flexibility and community support, but the downside is that developers must handle scaling, monitoring, and lifecycle management themselves.  
| Service                        | Best For                          | Advantages                                               | Inconvenients                                                |
|--------------------------------|-----------------------------------|----------------------------------------------------------|--------------------------------------------------------------|
| App Service (GraphQL servers)  | Hosting GraphQL APIs on PaaS       | Easy deployment, CI/CD integration, multi-language       | No native GraphQL support, manual setup, scaling costs       |
| Functions (GraphQL endpoints)  | Serverless GraphQL microservices   | Cost-efficient, auto-scaling, integrates with Azure DBs  | Cold starts, limited execution time, complex schema handling |
| OSS frameworks (Apollo/Hasura) | Full GraphQL features on Azure infra| Flexibility, subscriptions, community support            | Requires ops management, monitoring, scaling overhead        |

##### **GCP**
On Google Cloud, GraphQL isn’t offered as a native managed service. Instead, developers typically rely on Cloud Run, Cloud Functions, or Google Kubernetes Engine (GKE) to host GraphQL frameworks such as Apollo Server, Hasura, or other open‑source solutions.  
Cloud Run makes it possible to deploy containerized GraphQL servers and expose them securely over HTTPS. It supports any language or runtime, integrates smoothly with GCP services, and scales automatically depending on demand. The flexibility and cost savings from scaling down to zero are clear advantages. The downsides are cold starts when services are idle, the need to manage container images, and additional effort required to handle persistent subscriptions.  
Cloud Functions can serve GraphQL endpoints through HTTP triggers. This approach works well for lightweight APIs or microservices that connect to Firestore, Pub/Sub, or other GCP services. It’s inexpensive, scales transparently, and accelerates development. The limitations include cold start delays, capped execution time, and difficulty managing complex GraphQL schemas in a serverless environment.  
GKE allows teams to run full GraphQL platforms like Hasura or Apollo inside Kubernetes clusters. This option is best suited for large‑scale deployments where fine‑grained control over networking, scaling, and subscriptions is required. The benefits are maximum flexibility and enterprise‑grade scalability. The trade‑offs are heavier operational responsibilities, cluster maintenance, and the need for Kubernetes expertise.
| Service        | Best For                          | Advantages                                               | Inconvenients                                                |
|----------------|-----------------------------------|----------------------------------------------------------|--------------------------------------------------------------|
| Cloud Run      | Containerized GraphQL servers     | Flexible runtime, auto-scaling, integrates with GCP      | Cold starts, containerization complexity, subscription handling |
| Cloud Functions| Lightweight GraphQL microservices | Low cost, auto-scaling, quick to build                   | Cold starts, limited execution time, schema complexity        |
| GKE (Hasura/Apollo)| Large-scale GraphQL workloads | Full control, enterprise scalability, supports subscriptions| Operational overhead, cluster management, requires expertise |

#### Data Streaming Services
##### **AWS**
AWS offers two main services for data streaming: Amazon Kinesis and Amazon MSK (Managed Streaming for Apache Kafka).  
Amazon Kinesis is a serverless platform designed to capture and process streaming data in real time. It includes Data Streams for ingestion, Firehose for delivery into storage or analytics tools, and Data Analytics for querying streams with SQL. Kinesis is easy to set up, scales automatically, and integrates tightly with AWS services like Lambda and S3. However, it locks you into AWS, offers less flexibility than Kafka, and costs can rise quickly with heavy throughput.  
Amazon MSK provides a fully managed Apache Kafka environment. It allows teams to run Kafka clusters without worrying about infrastructure, while keeping full compatibility with existing Kafka tools and libraries. MSK is ideal for organizations already invested in Kafka and needing complex pipelines. On the downside, it requires Kafka expertise, scaling is more manual compared to Kinesis, and operational overhead is higher for small teams.  

##### **Azure**
Azure provides several options for streaming data: Azure Event Hubs and Azure Stream Analytics.  
Azure Event Hubs is a big data streaming platform and event ingestion service. It can collect millions of events per second from applications, IoT devices, or services, and make them available for real‑time processing. Event Hubs is highly scalable, integrates with Azure services, and supports multiple consumers. However, it is tightly bound to Azure, requires careful partition management, and costs can increase with very high throughput.  
Azure Stream Analytics is a real‑time analytics engine that processes data from Event Hubs, IoT Hub, or Blob Storage. It allows developers to run SQL‑like queries on streaming data and push results to dashboards, databases, or alerts. Stream Analytics is easy to use, serverless, and integrates well with Power BI. On the downside, it is limited to SQL‑style processing, less flexible than custom frameworks, and not ideal for very complex transformations.

##### **GCP**
GCP provides several services for streaming data: Pub/Sub, Dataflow, and Datastream.  
Pub/Sub is Google Cloud’s messaging and event distribution service. It enables applications to send and receive messages in real time, supporting millions of events per second. Pub/Sub is fully managed, scales automatically, and integrates with other GCP services. Its drawbacks include vendor lock‑in, limited fine‑grained control compared to Kafka, and potential costs at very high throughput.  
Dataflow is a serverless stream and batch processing service based on Apache Beam. It allows developers to build pipelines that transform and analyze data in motion. Dataflow is powerful for real‑time analytics, supports complex transformations, and integrates with BigQuery and AI services. On the downside, it has a steep learning curve, requires pipeline design expertise, and can be expensive for continuous workloads.  
Datastream is a change data capture (CDC) and replication service. It streams data from sources like relational databases into GCP targets such as BigQuery or Cloud SQL. Datastream simplifies database replication and analytics integration. However, it is focused on CDC use cases, less flexible than general streaming platforms, and may not fit all real‑time scenarios.

#### Stream Analytics
##### **AWS**
AWS provides stream analytics mainly through Amazon Kinesis Data Analytics.  
Amazon Kinesis Data Analytics is a fully managed service that lets you analyze streaming data in real time using SQL or Apache Flink. It can process data from Kinesis Data Streams or Firehose and deliver insights directly to dashboards, alerts, or storage. The service is serverless, scales automatically, and integrates with other AWS tools. However, it is limited to SQL/Flink paradigms, requires expertise for complex pipelines, and costs can grow with continuous workloads.  
##### **Azure**
Azure provides stream analytics mainly through Azure Stream Analytics.  
Azure Stream Analytics is a fully managed real‑time analytics engine. It can process data from sources like Event Hubs, IoT Hub, or Blob Storage and push results to Power BI, SQL Database, or other outputs. The service is serverless, easy to configure, and scales automatically. It’s well suited for dashboards, alerts, and IoT scenarios. On the other hand, it is limited to SQL‑like query language, less flexible than custom frameworks, and complex transformations can be harder to implement.  

##### **GCP**
GCP provides stream analytics mainly through Cloud Dataflow.  
Cloud Dataflow is a fully managed service for stream and batch data processing, built on Apache Beam. It allows developers to design pipelines that transform, enrich, and analyze data in motion. Dataflow integrates tightly with BigQuery, Pub/Sub, and AI services, making it powerful for real‑time analytics. Its strengths are scalability, flexibility, and support for complex transformations. The downsides are a steep learning curve, pipeline design complexity, and potentially high costs for continuous workloads.  


## Use Case Analysis
### Use Case 1: Real-time Fraud Detection in Online Banking
A financial institution needs to process millions of transactions per second, detect anomalies instantly, and trigger alerts to prevent fraud.  
 - Requirements : High throughput ingestion of event, real-time analytics with low latency,and tight integration with existing cloud databases and machine learning models.
We recommend AWS using Amazon Kinesis with Kinesis Data Analytics.
 - Justification : 
    - Performance: Kinesis can handle millions of events per second with sub-second latency.
    - Integration: Seamless with AWS ML services (SageMaker), DynamoDB, and Lambda for automated responses.
    - Cost: Pay-as-you-go model with auto-scaling; efficient for variable workloads.
    - Ecosystem: Strong financial services adoption, mature tooling, and compliance certifications.

### Use Case 2: Smart City IoT Monitoring (Traffic & Sensors)
A city wants to collect sensor data from traffic lights, cameras, and IoT devices to optimize traffic flow and provide real-time dashboards.
 - Requirements : Event ingestion from thousands of IoT devices, real-time analytics and visualization, Easy integration with BI tools for city planners.
We recommend Azure using Event Hubs + Stream Analytics + Power BI.
 - Justification: 
    - Performance: Event Hubs supports massive IoT event ingestion with high reliability.
    - Integration: Stream Analytics connects directly to Power BI for real-time dashboards.
    - Cost: Serverless model reduces infrastructure overhead; predictable pricing for IoT workloads.
    - Ecosystem: Azure has strong IoT solutions (IoT Hub, Digital Twins) and enterprise adoption in public sector projects.


## Conclusion
Real‑time applications demand platforms that balance scalability, integration, and cost efficiency. AWS excels in high‑throughput financial use cases with strong compliance and machine learning integration, while Azure stands out in IoT and smart city projects thanks to its seamless Power BI and IoT ecosystem. GCP, with Pub/Sub and Dataflow, offers powerful analytics pipelines and flexibility for organizations prioritizing advanced data processing. Ultimately, the choice of CSP depends on the specific context: AWS for mission‑critical financial workloads, Azure for IoT‑driven environments, and GCP for data‑intensive analytics. By aligning technical requirements with provider strengths, organizations can unlock the full potential of real‑time applications.


## References
- Martinez, V. (2024, November 8). Modern web application architecture on AWS: Patterns, hosting, and apis with GraphQL, WebSockets, and rest. DEV Community. https://dev.to/vamartinez/modern-web-application-architecture-on-aws-patterns-hosting-and-apis-with-graphql-websockets-and-rest-2jii 

- Choose between REST apis and HTTP apis - amazon API gateway. (n.d.). https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html 

- No Author. (2025a, August 19). AWS API gateway choices: Pros and cons of rest, GraphQL, and HTTP API - business compass LLC. Business Compass LLC - Cloud migration? Let’s talk. https://knowledge.businesscompassllc.com/aws-api-gateway-choices-pros-and-cons-of-rest-graphql-and-http-api/ 