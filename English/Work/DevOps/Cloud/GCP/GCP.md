# Google Cloud Platform (GCP) Basics for DevOps

This guide covers the essential concepts and services of Google Cloud Platform (GCP) relevant to DevOps practices, focusing on infrastructure management, automation, and CI/CD workflows.

## 1. Core GCP Concepts

- **Projects**: The fundamental organizational unit in GCP. All resources (VMs, storage, etc.) belong to a project. Each project has a unique ID and is isolated for billing and permissions.
- **Regions and Zones**: GCP resources are hosted in regions (geographic areas) and zones (isolated locations within a region). Choose regions/zones based on latency, availability, and compliance.
- **Identity and Access Management (IAM)**: Controls who (users, groups, service accounts) can access what (resources, APIs). Use roles (predefined or custom) to grant granular permissions.
- **Billing**: Centralized per project. Set budgets and alerts to monitor costs. Use labels for cost allocation and tracking.

## 2. Key GCP Services for DevOps

### Compute

- **Compute Engine**: Virtual machines (VMs) for running workloads. Supports custom machine types, preemptible VMs (cost-effective, short-lived), and autoscaling.
- **Google Kubernetes Engine (GKE)**: Managed Kubernetes for containerized applications. Automates cluster management, scaling, and upgrades. Ideal for microservices.
- **[[Cloud Run]]**: Serverless platform for running containerized applications. Scales automatically based on HTTP requests. Simplifies deployment for stateless workloads.

### Storage

- **Cloud Storage**: Object storage for unstructured data. Offers different storage classes (Standard, Nearline, Coldline, Archive) for cost optimization.
- **Persistent Disk**: Block storage for Compute Engine VMs or GKE. Supports snapshots for backups and replication for high availability.

### Networking

- **Virtual Private Cloud (VPC)**: Isolated network for resources. Configure subnets, firewall rules, and routes for secure communication.
- **Cloud Load Balancing**: Distributes traffic across instances or regions. Supports HTTP(S), TCP, and SSL load balancing for high availability.
- **Cloud Armor**: Security policies to protect applications from DDoS attacks and web vulnerabilities.

### CI/CD and Automation

- **Cloud Build**: Managed service for building, testing, and deploying code. Integrates with GitHub, Bitbucket, and other repositories. Supports custom workflows via YAML.
- **Artifact Registry**: Stores and manages container images, Maven, and npm packages. Replaces Container Registry with added features like regional repositories.
- **Cloud Deploy**: Managed service for deploying to GKE and other environments. Supports canary and blue-green deployments.

### Monitoring and Logging

- **Cloud Monitoring**: Tracks performance metrics (CPU, memory, latency) for GCP resources. Create dashboards and alerts for proactive issue detection.
- **Cloud Logging**: Centralized logging for applications and infrastructure. Integrates with BigQuery for advanced log analysis.
- **Cloud Trace**: Distributed tracing for debugging application latency in production.

## 3. DevOps Practices in GCP

### Infrastructure as Code (IaC)

- Use **Terraform** or **Google Cloud Deployment Manager** to define and provision infrastructure. Store configurations in version control (e.g., Git).
- Example: Create a Compute Engine instance with Terraform:

```hcl
resource "google_compute_instance" "default" {
  name         = "devops-vm"
  machine_type = "e2-standard-2"
  zone         = "us-central1-a"
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }
  network_interface {
    network = "default"
    access_config {}
  }
}
```

### CI/CD Pipelines

- Set up pipelines with **Cloud Build** for automated builds, tests, and deployments.
- Example Cloud Build configuration (`cloudbuild.yaml`):

```yaml
steps:
  - name: 'gcr.io/cloud-builders/docker'
    args: ['build', '-t', 'gcr.io/$PROJECT_ID/my-app', '.']
  - name: 'gcr.io/cloud-builders/docker'
    args: ['push', 'gcr.io/$PROJECT_ID/my-app']
  - name: 'gcr.io/cloud-builders/gcloud'
    args: ['run', 'deploy', 'my-app', '--image', 'gcr.io/$PROJECT_ID/my-app', '--region', 'us-central1']
```

### Containerization

- Use **Docker** to package applications and deploy to GKE or Cloud Run.
- Push images to **Artifact Registry** for secure storage.
- Example: Deploy to Cloud Run:

```bash
gcloud run deploy my-service \
  --image gcr.io/my-project/my-app:latest \
  --region us-central1 \
  --platform managed \
  --allow-unauthenticated
```

### Monitoring and Incident Response

- Configure **Cloud Monitoring** dashboards to visualize key metrics (e.g., CPU usage, request latency).
- Set up alerts to notify teams via Slack, PagerDuty, or email when thresholds are breached.
- Use **Cloud Logging** to query logs during incidents. Example query: `resource.type="gce_instance" severity=ERROR`.

## 4. Best Practices

- **Least Privilege**: Assign IAM roles with minimal permissions. Use service accounts for automation.
- **High Availability**: Deploy across multiple zones or regions. Use managed services like GKE or Cloud Run for automatic scaling.
- **Cost Optimization**: Use preemptible VMs, committed use discounts, and appropriate storage classes. Monitor costs with billing reports.
- **Security**: Enable VPC Service Controls, use Cloud Armor for web protection, and encrypt data at rest and in transit.
- **Version Control**: Store IaC, CI/CD configs, and application code in Git for traceability and collaboration.

## 5. Getting Started

1. **Set Up GCP Account**: Create a project in the GCP Console. Enable billing and APIs for required services.
2. **Install Tools**:
    - **gcloud CLI**: For managing GCP resources from the terminal.
    - **Terraform**: For IaC.
    - **Docker**: For containerization.
3. **Learn with Qwiklabs**: Hands-on labs for GCP services (e.g., GKE, Cloud Build).
4. **Explore Documentation**: GCP’s official docs provide tutorials and reference guides.

## 6. Common Commands

- Initialize gcloud CLI:

```bash
gcloud init
```

- Create a GKE cluster:

```bash
gcloud container clusters create my-cluster --zone us-central1-a
```

- Deploy a Compute Engine instance:

```bash
gcloud compute instances create my-vm --machine-type=e2-standard-2 --zone=us-central1-a
```

- List Cloud Storage buckets:

```bash
gsutil ls
```

This guide provides a foundation for leveraging GCP in DevOps workflows. Explore specific services and tools based on your project’s needs.

---
**Tags**: #DevOps #GCP #CI/CD #Kubernetes #IaC