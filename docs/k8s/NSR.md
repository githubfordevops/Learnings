# NSR in Kubernetes Contexts

This document explains two possible interpretations of **NSR** in Kubernetes-related architectures:
1. **NSR in Network Service Mesh**
2. **Container Registry usage in Kubernetes** (if NSR was a misinterpretation)

---

## NSR within a Kubernetes Network Service Mesh

In the **Network Service Mesh (NSM)** architecture, the **NSR** (also referred to as **MSR – Mesh Service Registry**) acts as the **central service discovery mechanism**.

### Service Discovery

- The Kubernetes API server’s **etcd** is commonly leveraged as the backing store for the registry.
- It stores information about:
  - Available network services
  - Network Service Endpoints (NSEs)
  - Associated metadata

---

### Registration Process

- **NSMgr (Network Service Manager)** runs as a control-plane component on each node.
- Its responsibilities include:
  - Discovering local Network Service Endpoints (NSEs)
  - Registering these NSEs with the NSR via the Kubernetes API server

This ensures that all available services and endpoints are visible at the mesh level.

---

### Service Consumption

- A **Network Service Client (NSC)**, typically a Pod with specific annotations, requests a network service.
- The workflow is as follows:
  1. The local NSMgr receives the service request
  2. It queries the NSR (via the API server) for a suitable NSE
  3. A **virtual wire** (connection) is established between:
     - The requesting client
     - The selected Network Service Endpoint

This enables dynamic, policy-driven service connectivity across the mesh.

---

## General Container Registry Usage in Kubernetes

If **“NSR”** is a typo or misinterpretation and instead refers to the general concept of a **container image registry** in Kubernetes, the process is different and focuses on **image distribution and authentication**.

---

### Image Pulling

- The **kubelet** component on each node is responsible for pulling container images.
- It uses the configured container runtime, such as:
  - Docker
  - containerd
  - CRI-O
- Images are pulled from a specified container registry.

---

### Authentication (Image Pull Secrets)

For **private container registries** (for example: Docker Hub, AWS ECR, Azure Container Registry, Google Artifact Registry):

- A Kubernetes `Secret` of type `kubernetes.io/dockerconfigjson` must be created.
- This secret stores:
  - Registry endpoint
  - Authentication credentials

---

### Linking Secrets to Pods

- The image pull secret is referenced in the Pod specification.
- This allows the kubelet to authenticate with the registry and pull the required image.

Example usage scenarios include:
- Private enterprise registries
- Cloud-provider-managed registries
- Secured internal image repositories

---

## Summary

- In **Network Service Mesh**, NSR refers to a **service registry** used for discovering and connecting network services.
- In standard Kubernetes usage, registries are used for **container image storage and distribution**.
- These two concepts are unrelated but can be confused due to similar terminology.

Understanding the context in which **NSR** is used is critical to interpreting its role correctly.
