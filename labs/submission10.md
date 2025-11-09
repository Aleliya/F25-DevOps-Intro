# Lab 10

## Task 1

**AWS**
- Service name:
        
    - AWS CodeArtifact
- Supported artifact types: 

    - Maven, Gradle (Maven), npm, yarn, pip, Twine and NuGet
- Key features:

    - Integration with AWS IAM for detailed access control
    - Detailed IAM policies for managing read/write permissions
    - There is no automatic geo-replication, but you can create repositories in different regions and configure cross-region replication
    - It can act as a proxy for public repositories

- Integration capabilities: 

    - Direct integration with AWS CodeBuild, CodePipeline for building and deploying applications
    - Deep integration with AWS Identity and Access Management (IAM) for authentication and authorization
    - It also integrates with AWS CloudWatch (activity monitoring) and AWS KMS (encryption of artifacts on the server)
- Common use cases:

    - Centralized storage of binary artifacts for CI/CD pipelines
    - Caching of public dependencies to speed up builds and increase reliability
    - Dependency management for multidisciplinary projects in one place

---
**GCP**

- Service name:
        
    - Artifact Registry
- Supported artifact types: 

    - Container images (Docker), Maven, npm, Python, universal artifacts (any files)
- Key features:

    - Scanning container images for vulnerabilities using Binary Authorization
    - Support for multi-regional repositories for container images, which ensures high availability and low latency
    - Detailed control via IAM roles
    - The ability to configure rules that prevent image tags from being overwritten
    - Protection against data leakage

- Integration capabilities: 

    - Direct integration with Azure Kubernetes Service for container deployment
    - Using ACR as an image source for CI/CD
    - Azure App Service, Azure Batch for deploying container applications
- Common use cases:

    - Storage and management of container images for AKS and other Azure services
    - Automating container assembly and lifecycle management using ACR Tasks

---
**Microsoft Azure**

- Service name:
        
    - Azure Container Registry (ACR)
- Supported artifact types: 

    - Container images (Docker), Helm charts
- Key features:

    - Scanning images for vulnerabilities
    - Automatic replication of registries between regions
    - Detailed control via Azure RBAC. It also supports anonymous access (pull) via tokens
    - Allows you to automate the assembly, testing, and application of patches to container images in Azure

- Integration capabilities: 

    - Direct and seamless integration with Google Kubernetes Engine, Cloud Run for container deployment
    - Cloud Build is the main CI/CD service that can push/pull artifacts from Artifact Registry
    - Deep integration with Cloud Deployment Manager, IAM for access management and deployment
- Common use cases:

    - Storage and management of container images for GKE and Cloud Run
    - Dependency management for applications running on Google Cloud
    - Creating secure software supply chains with vulnerability testing
    - Hosting OS repositories for virtual machines


---
**Comparison table highlighting similarities and differences**

| Feature | **AWS CodeArtifact** | **Artifact Registry** | **Azure Container Registry** |
| :--- | :--- | :--- | :--- |
| **Primary Focus** | Universal repository for libraries and packages(Maven, npm, Python) | Universal repository with strong focus on containers | Specialized registry for containers and Helm charts |
| **Supported Artifacts** | Wide range of packages(Maven, npm, Python, NuGet) | Containers, packages(Maven, npm, Python), OS packages, universal artifacts | Primarily containers and Helm charts |
| **Geo-Replication** | Manual setup(via repositories in different regions) | Built-in for containers(multi-region) | Built-in only at Premium tier |
| **Vulnerability Scanning** | Built-in for supported packages | Built-in for containers(additional cost) | Built-in for containers(included in all tiers) |
| **Ecosystem Integration** | Excellent integration with AWS CodeBuild/CodePipeline | Excellent integration with GKE, Cloud Run, Cloud Build | Excellent integration with AKS, Azure Pipelines |
| **Unique Features** | "Domains" concept for repository grouping | Support for OS package repositories | ACR Tasks for container automation |
| **Pricing Model** | Storage + operations + traffic | Storage + operations + scanning fee | Subscription tiers(Basic, Standard, Premium) + overage charges |

---
**Which registry service would you choose for a multi-cloud strategy and why?**


For a multi-cloud strategy, I would choose `GCP Artifact Registry` because it supports the largest number of artifact types (not just containers), which gives more flexibility for different projects and teams.



## Task 2

**AWS**

- Service Name:
    - AWS Lambda (The core FaaS offering)
    - AWS Fargate (Serverless containers)

- Key Features and Capabilities
    - Integrates deeply with over 200 AWS services like S3, DynamoDB, API Gateway, and EventBridge
    - Automatically scales from zero to thousands of concurrent executions
    - For sharing code and data across multiple functions
    - For configuring asynchronous invocation results
    - For orchestrating complex workflows involving multiple Lambdas
    - For keeping functions initialized and responsive to avoid cold starts

- Supported Runtimes and Languages
    - Native Runtimes: Node.js, Python, Ruby, Java, Go, .NET (C#/PowerShell)
    - Custom Runtimes: Allows using any programming language by providing a custom runtime (e.g., Rust, PHP, Elixir)

---
**GCP**
- Service Name:
    - Google Cloud Functions (The core FaaS offering)
    - Google Cloud Run (Serverless containers)
    - App Engine (Serverless application platform)

- Key Features and Capabilities
    - Triggers from Google Cloud services (Pub/Sub, Storage, Firestore) and HTTP via Cloud Endpoints
    - Automatically scales based on incoming request volume
    - Newer generation offering improved performance, longer request timeouts, and deeper integration with Cloud Run and Eventarc
    - Provides a consistent way to route events from Google Cloud, SaaS, and on-premises systems

- Supported Runtimes and Languages
    - Native Runtimes: Node.js, Python, Go, Java, .NET, Ruby, PHP
    - Custom Runtimes: Supported through container images on Cloud Run, allowing any language, library, or binary

---
**Azure**
- Service Name:
    - Azure Functions (The core FaaS offering)
    - Azure Container Instances (ACI) (Serverless containers)
    - Azure Logic Apps (Serverless workflow orchestration)

- Key Features and Capabilities
    - Triggers from Azure services (Blob Storage, Cosmos DB, Service Bus) and HTTP
    - Built-in autoscaling based on triggers
    - An extension for building stateful, orchestrated workflows in a serverless environment
    - Consumption Plan (pure serverless), Premium Plan (enhanced performance, VNet integration), and Dedicated (App Service) Plan

- Supported Runtimes and Languages
    - Native Runtimes: C#, Java, JavaScript/Node.js, Python, PowerShell
    - Custom Runtimes: Supported via Custom Handlers, allowing any language that supports HTTP primitives


---
**Pricing Comparison**

| Provider | Pricing Model |
| :--- | :--- |
| **AWS** |  Pay per request + Compute duration. Free tier includes 1M requests and 400,000 GB-s per month. |
| **GCP** | Pay per request + Compute duration, Memory, and CPU. Free tier includes 2M requests, 400,000 GB-s, and 200,000 GHz-s. |
| **Azure** | Pay per request + Compute duration. Free tier includes 1M requests and 400,000 GB-s per month. |

---
**Performance Characteristics**

- Cold Starts: All providers experience "cold starts". This is most noticeable with VMs requiring just-in-time compilation.
    - AWS & Azure: Offer "Provisioned Concurrency" (AWS) and "Premium Plan" (Azure) to pre-warm instances and mitigate cold starts
    - GCP: Cloud Functions Gen 2 and Cloud Run generally have improved cold start performance over their first-generation counterparts.
- Execution Timeout:
    - AWS Lambda: 15 minutes (max)
    - GCP Cloud Functions: 60 minutes for Gen 2, 9 minutes for Gen 1 (max)
    - Azure Functions: 5 minutes (Consumption Plan), unbounded in Premium/Dedicated plans
    
Concurrency: All providers handle massive concurrency by default, though AWS allows for reserved concurrency per function to guarantee a minimum level of scale.

---
**Comparison Table**

| Feature | AWS Lambda | GCP Cloud Functions | Azure Functions |
| :--- | :--- | :--- | :--- 
| **Max Timeout** | 15 min | 60 min (Gen 2) | 5 min (Consumption) / Unlimited (Premium) |
| **Stateful Workflows** | Step Functions | Workflows | Durable Functions |
| **VPC Access** | Yes (slower cold starts) | Yes (Serverless VPC Access) | Yes (Premium Plan) |
| **Cold Start Mitigation** | Provisioned Concurrency | Improved in Gen 2 | Premium Plan |
| **Container Support** | Lambda Container Image | Cloud Run | Custom Handlers, Container-based Functions |
| **Key Integration Ecosystem** | Huge, native with 200+ AWS services | Strong with Google services, Firebase | Deep integration with Microsoft ecosystem |
| **Typical Use Case** | Event-driven microservices, API backends, data processing | Event processing, lightweight APIs, mobile backends (Firebase) | Enterprise integrations, event-driven apps, complex orchestration |

---
**Which serverless platform would you choose for a REST API backend and why?**

For the REST API, I would choose `AWS Lambda`. The reason is the maximum execution time (15 minutes), which is suitable for API requests that may require long calculations. In addition, Lambda has the most mature ecosystem and a rich set of integration events.

---
**What are the main advantages and disadvantages of serverless computing?**

Advantages:
- There is no need to manage servers
- Automatic scaling
- Payment is only for actual use (it may be cheaper for non-permanent loads)

Disadvantages:
- "Cold start" (delay on the first call)
- Time limits for the function execution
- The risk of "Vendor Lock-in" when the code is tailored to the services of the same cloud