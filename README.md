# CloudComputing

Alright, Bhoomika — let’s turn all this into a clean, step-wise, professional-looking lab documentation. I’ll keep it crisp, structured, and aesthetic so you can easily insert screenshots wherever you want (Docker, Prometheus, Grafana dashboards, Minikube, YAML files, etc.).
I’ll also give it that traditional-meets-modern vibe you like — steady, poetic, organized, but still Gen-Z-fresh.

---

# **Lab Evaluation Documentation**

*(You can paste this directly into your report and insert images where indicated.)*

---

# **📘 Lab Evaluation 2: Virtualization and Containerization Techniques**

## **1. Objective**

To understand the fundamentals of virtualization and containerization, and to practically work with Docker for creating, managing, and running containerized applications.

---

## **2. Tasks Performed**

### **2.1 Installed Docker**

* Installed Docker Engine and Docker CLI on the local system.
* Verified installation using:

  ```bash
  docker --version
  docker run hello-world
  ```

📷 *Insert Docker installation screenshot here.*

---

### **2.2 Created Docker Images and Containers**

* Wrote Dockerfiles for sample applications.
* Built custom Docker images using:

  ```bash
  docker build -t sample-app .
  ```
* Created and ran containers:

  ```bash
  docker run -d --name sample-container sample-app
  ```

📷 *Insert Dockerfile screenshot here.*

---

### **2.3 Managed Container Lifecycle**

Used Docker CLI to:

* Start containers

  ```bash
  docker start container-name
  ```
* Stop containers

  ```bash
  docker stop container-name
  ```
* Restart containers

  ```bash
  docker restart container-name
  ```

📷 *Insert container lifecycle screenshot.*

---

### **2.4 Explored Container Isolation & Resource Sharing**

* Checked namespaces and cgroups usage in Docker.
* Examined resource limits:

  ```bash
  docker run -d --memory="256m" --cpus="1" sample-app
  ```

---

## **3. Tools / Technologies Used**

* Docker Engine
* Docker CLI
* Docker Hub

---

## **4. Outcome**

* Clear understanding of *virtualization vs containerization*.
* Successfully built and deployed Docker containers.
* Understood the advantages of containers such as:

  * lightweight nature
  * fast deployment
  * portability
  * isolation

---

---

# **📗 Lab Evaluation 3: Kubernetes Orchestration and Automation**

## **1. Objective**

To explore Kubernetes fundamentals, understand container orchestration, and deploy scalable multi-container applications.

---

## **2. Tasks Performed**

### **2.1 Set Up Kubernetes Using Minikube**

* Installed Minikube and kubectl.
* Started local cluster:

  ```bash
  minikube start
  ```

📷 *Insert Minikube dashboard screenshot.*

---

### **2.2 Deployed Multi-Container Applications**

* Wrote Kubernetes manifests in YAML for:

  * Pods
  * Services
  * Deployments
* Applied configurations using:

  ```bash
  kubectl apply -f deployment.yaml
  ```

📷 *Insert YAML manifest screenshot.*

---

### **2.3 Explored Key Kubernetes Components**

* **Pods** → smallest deployable units
* **Services** → stable networking
* **Deployments** → manage replicas & updates
* **ReplicaSets** → maintain pod count

---

### **2.4 Implemented Scaling & Rolling Updates**

* Scaled deployment:

  ```bash
  kubectl scale deployment my-app --replicas=3
  ```
* Performed rolling update:

  ```bash
  kubectl set image deployment/my-app app=new-image:latest
  ```

📷 *Insert kubectl output screenshot.*

---

## **3. Tools / Technologies Used**

* Minikube
* Kubernetes
* kubectl CLI
* Sample microservices app

---

## **4. Outcome**

* Understood Kubernetes architecture and orchestration flow.
* Successfully deployed and scaled containerized apps.
* Learned automation using rolling updates and self-healing mechanisms.

---

---

# **📙 Lab Evaluation 4: Microservices Application – Hospital Management System Monitoring**

## **1. Overview**

A microservices-based **Hospital Management System (HMS)** was created with the following services:

* **patient-service**
* **doctor-service**
* **billing-service**
* **frontend**

All services run inside a shared Docker network:
`monitoring-net`

Monitoring stack used:

* **Prometheus** → for scraping and collecting metrics
* **Grafana** → for visualizing service performance

📷 *Insert architecture diagram here.*

---

## **2. Architecture Flow**

1. Each microservice exposes metrics at `/actuator/prometheus` or custom endpoints.
2. Prometheus scrapes metrics periodically.
3. Grafana connects to Prometheus as a data source.
4. Visual dashboards show health, performance, and traffic.

---

## **3. Step-by-Step Implementation**

### **3.1 Created Microservices**

* Implemented separate REST microservices for patient, doctor, billing, and frontend.
* Containerized each service using Docker.



---

### **3.2 Created Dedicated Monitoring Docker Network**

```bash
docker network create monitoring-net
```

---

### **3.3 Connected All Services to the Monitoring Network**

Example:

```bash
docker run -d --network monitoring-net --name patient-service patient-image
```

---

### **3.4 Configured Prometheus**

* Created `prometheus.yml` file with job configurations:

  ```yaml
  scrape_configs:
    - job_name: 'patient-service'
      static_configs:
        - targets: ['patient-service:8080']
    - job_name: 'doctor-service'
      static_configs:
        - targets: ['doctor-service:8081']
    - job_name: 'billing-service'
      static_configs:
        - targets: ['billing-service:8082']
  ```


---

### **3.5 Started Prometheus in Docker**

```bash
docker run -d -p 9090:9090 \
  --network monitoring-net \
  -v ./prometheus.yml:/etc/prometheus/prometheus.yml \
  --name prometheus prom/prometheus
```

📷 *Insert Prometheus UI screenshot.*

---

### **3.6 Installed Grafana**

```bash
docker run -d -p 3000:3000 \
  --network monitoring-net \
  --name grafana grafana/grafana
```

* Added Prometheus as data source
* Created custom dashboards



---

## **4. Outcome**

* Successfully implemented a **fully monitored microservice architecture**.
* Learned:

  * Service health checking
  * Metrics scraping
  * Dashboard visualization
  * Real-time monitoring techniques
* Gained practical experience in Docker networks, Prometheus configs, and Grafana dashboards.

---

