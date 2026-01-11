
---

# 📘 `docs/scheduling/nodeselector.md`

# nodeSelector

## What is nodeSelector?

`nodeSelector` is a **built-in PodSpec field** that enforces a **hard scheduling rule**
based on **exact node label matches**.

> “Schedule this Pod ONLY on nodes with these labels.”

---

## Where It Is Used

Defined inside **PodSpec**, therefore works for:
- Pod
- Deployment
- StatefulSet
- DaemonSet
- Job
- CronJob

---

## Syntax

```yaml
spec:
  nodeSelector:
    disktype: ssd
```
