
---

# 📙 `docs/scheduling/node-affinity.md`


# Node Affinity

## What is Node Affinity?

Node Affinity is an **advanced scheduling mechanism**
that allows **expressive rules and preferences**.

Internally:
- `nodeSelector` is converted into nodeAffinity

---

## Types of Node Affinity

1. Required Node Affinity (Hard)
2. Preferred Node Affinity (Soft)

---

## Required Node Affinity

> Pod MUST be scheduled on matching nodes.

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: disktype
          operator: In
          values:
          - ssd
```
##Characteristics
1. Pod stays Pending if no node matches
2. Running Pods are not evicted

##Preferred Node Affinity
Scheduler tries preferred nodes first.

```yaml
affinity:
  nodeAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 100
      preference:
        matchExpressions:
        - key: zone
          operator: In
          values:
          - zone-a
```
