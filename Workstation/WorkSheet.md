
| Type   | Task Name                                     | Task Content                                                                                             | Task Deadline | State      |
|--------|-----------------------------------------------|----------------------------------------------------------------------------------------------------------|---------------|------------|
| Study  | Learn about creating a Kubernetes client      | - Gather and study information need to know about building a Kubernetes client Pod, Go lang, gRPC, Kubernetes API client library, event model                | 01-10         | In Progress |
| #1 Demo| Create Kubernetes pod using Go lang           | - Make pod with Go lang - Which info should be loaded in the pod?                                         | 01-17         | Waiting    |
|        | Define Pod specifications (image, resources, etc.)| - Container Image - Resources CPU and Memory constraints - Environment Variables - Volumes - Ports - Lifecycle(Implement Pod lifecycle event handling) - Labels | 01-17 | Waiting    |
| #1 Demo| Create service code to handle pod             | - Service to handle pod                                                                                  | 01-17         | Waiting    |
|        | Specify communication protocol & methods     | - Communication Protocol(HTTP, gRPC, etc.) - Define Service Endpoint - Request Methods(GET, POST, PUT, DELETE, etc.) - Data Format(JSON) - Authentication and Authorization(JWT, roles) - Error Handling & fault tolerance - Data Validation | 01-17 | Waiting    |
| #1 Demo| Create client                                | - In the client, it gathers pod info, service and endpoint info in real-time - based Config - Host Process | 01-17         | Waiting    |
|        | Specify data format for gathering real-time info| - Data Encoding/Decoding - Versioning - Security Considerations - Compatibility with Kubernetes Events    | 01-17         | Waiting    |
| #1 Test| Test client                                  | - Test (Mocking) - Is this really making pod and handling it? - Actions work properly?                    | 01-17         | Waiting    |
| Study  | Learn how to service #1 Demo client           | - How to service Go client on Kubernetes? - How to make a client service on a container?                 | 01-24         | Waiting    |
| #2 Demo| Create client container and service on Kubernetes| - Make the previous client a container and upload to Kubernetes                                         | 01-31         | Waiting    |
|        | Explore containerization options (Docker, containerd, etc.)                                            |                                              | 01-31         | Waiting    |
| #2 Demo| Make service to run on Kubernetes             | - Make additional service code to maintain in Kubernetes                                                 | 01-31         | Waiting    |
|        | Implement service discovery and dynamic service location                                              | - Service Discovery Mechanism - Service Name Conventions - Health Checking - Load Balancing - Fallback Mechanism - Logging and Monitoring | 01-31 | Waiting    |
| #2 Test| Test container & client                      | - Unit Tests for Container - Integration Tests for Container and Client - Mocking Kubernetes API Responses - Mocking External Dependencies - Edge Cases and Boundary Tests - Logging and Monitoring(Assertions) - Test Report and Analysis | 01-31 | Waiting    |
| Study  | Learn how to control pod in a specific location| - How to schedule in Kubernetes elements. Schedule elements like Pod, ReplicaSet, Kublet                   | 02-07         | Waiting    |
| #3 Demo| Create Custom Client using gRPC              | - Develop custom client interaction to cluster using client-go & gRPC                                     | 02-14         | Waiting    |
|        | Define gRPC service and message definitions  | - Service Definition - Message Definition - RPC Method Signatures - Error Handling - Streaming RPCs - Security Considerations | 02-14 | Waiting    |
| #1 Optimize | Project Finalization and Optimization       | - Optimizing Kubernetes client - Documentation the project and testing                                  | 02-21         | Waiting    |

### Learn about creating a Kubernetes client

> Gather and study information need to know about building a Kubernetes client Pod, Go lang, gRPC, Kubernetes API client library, event model

