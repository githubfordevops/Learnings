# Understanding the Reconciler in a Kubernetes Operator (Go)

## Overview
In a Kubernetes operator built using Kubebuilder, the **Reconciler** is the core component responsible for driving the actual state of the cluster towards the desired state defined by a Custom Resource (CR).

Each reconciliation cycle operates on **one specific resource instance**.

---

## Reconciler function signature

```go
func (r *MyReconciler) Reconcile(
    ctx context.Context,
    req ctrl.Request,
) (ctrl.Result, error)
