
---

# 🚫 `docs/scheduling/taints.md`

```md
# Taints

## Why Taints Exist

Before taints:
> Pods freely scheduled onto nodes

Problems:
- Infra nodes polluted
- Control-plane overloaded
- Special hardware misused

---

## What is a Taint?

A **taint** is applied to a **node** to repel Pods.

```text
key=value:effect
```

## Taint Effects

### NoSchedule
- Blocks new Pods
- Existing Pods stay running

### PreferNoSchedule
- Scheduler avoids the node if possible
- Not guaranteed (best-effort)

### NoExecute
- Evicts existing Pods
- Blocks new Pods

> ⚠️ **NoExecute is the most dangerous taint effect** and should be used with extreme caution.
