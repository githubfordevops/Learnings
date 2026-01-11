
---

# 🎟️ `docs/scheduling/tolerations.md`

# Tolerations

## What is a Toleration?

A toleration allows a Pod to **bypass node taints**.

> Tolerations do NOT attract Pods  
> They only allow scheduling

---

## Toleration Syntax

```yaml
tolerations:
- key: "dedicated"
  operator: "Equal"
  value: "infra"
  effect: "NoSchedule"
```

## Operators

### Equal
- Exact match

### Exists
- Any value accepted

---

## tolerationSeconds (NoExecute only)

```yaml
tolerationSeconds: 300
