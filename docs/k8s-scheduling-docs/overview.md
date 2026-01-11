# Scheduling Overview

Kubernetes scheduling answers **two independent questions**:

## 1. Where does the Pod WANT to run?
- nodeSelector
- Node Affinity

## 2. Is the Pod ALLOWED to run on the node?
- Taints
- Tolerations

> A Pod is scheduled **only if both conditions succeed**.

---

## Node Labels (Foundation)

All scheduling rules depend on **node labels**.

```bash
kubectl label node node-1 disktype=ssd
kubectl label node node-2 gpu=true
