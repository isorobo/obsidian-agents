---
type: meta
title: Mermaid Diagram Library
status: permanent
created: 2026-07-10
topic:
- topic/meta
tags:
- diagrams
---

# Mermaid Diagram Library

Reusable diagram sources. Copy a block into any note inside a ```mermaid fence.

## The Agent Loop

```mermaid
flowchart TD
    A[Goal] --> B[Perceive context]
    B --> C[Reason / plan next step]
    C --> D{Tool needed?}
    D -- yes --> E[Call tool]
    E --> F[Observe result]
    F --> C
    D -- no --> G[Produce answer]
    G --> H{Goal met?}
    H -- no --> C
    H -- yes --> I[Stop]
```

Used by [[the-agent-loop]].

## ReAct

```mermaid
flowchart LR
    T[Task] --> Th[Thought]
    Th --> Ac[Action]
    Ac --> Ob[Observation]
    Ob --> Th
    Ob --> Fin{Done?}
    Fin -- yes --> Ans[Answer]
    Fin -- no --> Th
```

Used by [[react]].

## Plan-and-Execute

```mermaid
flowchart TD
    G[Goal] --> P[Planner: build step list]
    P --> S1[Step 1]
    S1 --> S2[Step 2]
    S2 --> Sn[Step n]
    Sn --> R{Plan complete?}
    R -- no --> RP[Replan]
    RP --> S1
    R -- yes --> Done[Result]
```

Used by [[plan-and-execute]].

## Supervisor-Worker

```mermaid
flowchart TD
    U[User goal] --> Sup[Supervisor]
    Sup --> W1[Worker: research]
    Sup --> W2[Worker: code]
    Sup --> W3[Worker: verify]
    W1 --> Sup
    W2 --> Sup
    W3 --> Sup
    Sup --> Out[Synthesised result]
```

Used by [[supervisor-worker-multi-agent]].

## Deployment Pipeline

```mermaid
flowchart LR
    Dev[Develop] --> Test[Test + eval]
    Test --> CI[CI/CD]
    CI --> Cont[Containerise]
    Cont --> Deploy[Deploy: cloud / local / edge]
    Deploy --> Obs[Observe: logs + traces]
    Obs --> Eval[Evaluate in production]
    Eval --> Dev
```

## See also

- [[MOC - Architectures]]
- [[MOC - Deployment]]
