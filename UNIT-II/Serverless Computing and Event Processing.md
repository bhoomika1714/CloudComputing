

### **1. A software development company is modernizing its legacy system by migrating to a cloud environment. They are exploring scaling and serverless computing. What challenges might they face in scaling a server within a cloud environment?**

From the slide **"Scaling A Server In A Cloud Environment"**:

**Challenges they might face:**

* **Vertical Scaling Limitations:**

  * While increasing CPU, RAM, or storage (scale-up) can help, it **eventually hits hardware and cost limitations**.
  * Suitable only for applications that require more resources per server but not always cost-effective.

* **Horizontal Scaling Complexity:**

  * Adding more servers (scale-out) introduces **complexities like load balancing**, data synchronization, and **consistency across distributed systems**.
  * Requires proper orchestration to ensure traffic is evenly distributed and services stay fault-tolerant.

* **Load Balancer Dependency:**

  * Correctly configuring and managing **load balancers** is crucial to effective scaling.
  * Any misconfiguration may cause **uneven traffic distribution**, service unavailability, or degraded performance.

* **Resource Management & Monitoring:**

  * Dynamic workloads require **real-time monitoring and scaling**, which, if not handled properly, can lead to over-provisioning or under-provisioning.

---

### **2. Describe the concept of stateless servers and their relationship with containerization.**

From the slide **"Stateless Servers and Containers"**:

* **Stateless Servers:**

  * A **stateless server** does **not store client-related data internally**.
  * It treats each client request as **independent**, ensuring better scalability and fault tolerance.
  * Unlike stateful servers, which maintain session or user data, stateless servers avoid such persistence.

* **Relation to Containerization:**

  * Stateless servers are ideal for **containerized deployments**.
  * Containers can be **quickly started, stopped, and replicated** without the need to maintain session continuity.
  * **Serverless systems deploy code in stateless containers**, making it easier to **scale out and orchestrate** across distributed systems.
  * **Orchestration systems**, like those in Kubernetes, efficiently handle these containers, allowing smooth deployment and management.

---

### **3. Explain the architecture of a serverless infrastructure, including its key components and how it differs from traditional server-based architectures.**

From the slide **"The Architecture of a Serverless Infrastructure"**:

#### **Key Components of Serverless Architecture:**

1. **Function-as-a-Service (FaaS):**

   * Executes code in response to **specific events** (e.g., HTTP requests, file uploads).

2. **Event Sources:**

   * Trigger the execution of functions (e.g., changes in database, object storage).

3. **Backend Services:**

   * Includes databases, storage, and authentication systems which functions can access.

4. **Orchestration Services:**

   * Coordinate workflows and manage the execution of multiple functions in sequence or parallel.

5. **Dispatcher & Event Queue (as used in Kubernetes-like architecture):**

   * Events are placed into a **queue** and a **dispatcher** assigns worker nodes (containers) to process them.

#### **Differences from Traditional Architectures:**

* **Traditional:**

  * Requires manual **server provisioning, maintenance, and scaling**.
  * Developers must manage uptime, patches, and resource allocation.

* **Serverless:**

  * **Abstracts infrastructure management**—developers only focus on writing code.
  * **Auto-scales** on demand with **pay-per-use** billing.
  * Highly **event-driven and stateless**, enabling faster deployments and updates.

---

### **4. Provide an example of how a media streaming company could leverage serverless processing for video encoding/transcoding. Discuss advantages and disadvantages.**

From the slide **"An Example of Serverless Processing"** (Netflix case):

#### **Example: Netflix using AWS Lambda**

* When a new video is uploaded:

  * Stored in **Amazon S3**, which **triggers an event**.
  * The event **invokes a serverless function** to split the video into 5-minute segments.
  * Each segment is placed back in S3, which **triggers additional serverless functions** to transcode those segments.
  * **Transcoding proceeds in parallel**, increasing efficiency and speed.

#### **Advantages of Serverless in this Use Case:**

* **Cost Efficiency:** Only pay for compute time during encoding/transcoding tasks.
* **Parallel Processing:** Breaks videos into segments and transcodes them simultaneously, reducing total processing time.
* **No Server Management:** Developers don’t need to maintain encoding infrastructure.
* **Automatic Scaling:** Can handle spikes in uploads or user demand without manual intervention.

#### **Disadvantages:**

* **Cold Start Latency:** The first invocation of a function may introduce a delay.
* **Execution Time Limits:** Serverless functions may not support long-running tasks, requiring careful segmentation.
* **Vendor Lock-In:** Tied to services like AWS Lambda and S3, making migration complex.
* **Debugging Complexity:** Distributed event-driven flows are **harder to trace and debug** compared to monolithic applications.
* **Resource Restrictions:** Limits on memory, CPU, or disk may restrict encoding capabilities for very large or high-quality files.

