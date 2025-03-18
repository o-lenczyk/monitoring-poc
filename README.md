# Feasibility Check (POC Estimation) - Cloud Agnostic Version

## 1. Compute

- **Virtual Machines:** Host the Kubernetes or Docker environment.
- **Instance Type:**
  - 2x VMs with 2 vCPUs, 8 GB RAM for Kubernetes/Docker control and worker nodes.
  - Sufficient for hosting Sock Shop and monitoring tools.
  - **Estimated Cost:** Varies by cloud provider; approximately $90-$100/month per instance (on-demand pricing).

## 2. Kubernetes/Docker Orchestration

- **Managed Kubernetes Service (if using Kubernetes):**
  - GKE (Google Cloud), AKS (Azure), OpenShift, or self-managed Kubernetes.
  - Control Plane: Managed service costs range from ~$70-$80/month.
  - Worker Nodes: As above (2x VM instances with 2 vCPUs, 8 GB RAM).
  
- **Alternative:** Docker Compose
  - No additional orchestration costs, as it runs directly on VM instances.

## 3. Storage

- **Object Storage:** Store logs and traces.
  - Options: Google Cloud Storage, Azure Blob Storage, MinIO (self-hosted).
  - 50 GB estimated usage.
  - **Estimated Cost:** ~$2/month.

- **Persistent Block Storage:** Persistent storage for Prometheus TSDB and Kubernetes volumes.
  - Options: Google Persistent Disk, Azure Managed Disks, OpenEBS.
  - ~50 GB General Purpose SSD per instance.
  - **Estimated Cost:** ~$5/month per volume.

## 4. Networking

- **Virtual Network:** Secure networking for Sock Shop and monitoring tools.
  - Included with VM instance costs.
  
- **Load Balancer:** Distribute traffic to Sock Shop services.
  - Options: Google Cloud Load Balancer, Azure Load Balancer, Traefik/NGINX (self-hosted).
  - **Estimated Cost:** ~$20-$30/month.

## 5. Monitoring Tools

- **Grafana, Prometheus, Loki, Fluent Bit:**
  - Deployed in the same Docker/Kubernetes environment.
  - No additional compute resources required beyond the existing setup.

- **Cloud Monitoring (if applicable):**
  - Options: Google Cloud Operations Suite, Azure Monitor, self-hosted Prometheus.
  - **Estimated Cost:** ~$10/month.

## 6. Miscellaneous

- **OpenTelemetry Collector:** Process and forward telemetry data.
  - Hosted on existing infrastructure; no additional cost.

| Resource                  | Estimated Cost (USD) |
|---------------------------|---------------------|
| Virtual Machines (2x 2 vCPU, 8GB RAM) | ~$180-$200 |
| Managed Kubernetes Control Plane (optional) | ~$70-$80 |
| Object Storage (50 GB for logs/traces) | ~$2 |
| Block Storage (50 GB per instance) | ~$10 |
| Load Balancer | ~$20-$30 |
| Cloud Monitoring | ~$10 |
| **Total with Managed Kubernetes** | **~$300-$330** |
| **Total with Docker Compose** | **~$220-$250** |

This estimation provides a vendor-neutral overview of the potential costs for running the Sock Shop microservices architecture across different cloud providers or on-premises setups.