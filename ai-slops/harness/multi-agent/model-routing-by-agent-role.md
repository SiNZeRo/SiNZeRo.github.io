---
layout: post
title: "Multi-agent Model Routing by Role"
description: "Model allocation and cost/task defaults for Controller, Worker, Reviewer, Explorer, and Advisor roles."
date: 2026-09-12
category: "HARNESS / MULTI-AGENT"
article_parent: /ai-slops/harness/multi-agent/
lang: en
lang_label: EN
translation_url: /ai-slops/harness/multi-agent/model-routing-by-agent-role/zh/
translation_lang: zh-CN
translation_label: 中文
permalink: /ai-slops/harness/multi-agent/model-routing-by-agent-role/
---

These three dimensions make the comparison clearer:

| Role | Default recommendation | Cost-efficient alternative (cost/task) | Quality alternative | Notes |
| --- | --- | --- | --- | --- |
| **Controller** | **Sol-medium** | Luna-max | **Astra-low** | Stable judgment matters by default; escalate hard tasks to Astra. |
| **Worker** | **Luna-max** | Luna-max | **Sol-medium** | For bounded tasks, optimize for lower cost per completed task. |
| **Reviewer (weak)** | **Luna-max** | Luna-max | **Terra-xhigh** | A weak reviewer mainly needs to catch obvious bugs. |
| **Explorer** | **Luna-max** | Luna-max | **Terra-xhigh** | Search and probing consume lots of tokens, so cheap throughput matters. |
| **Advisor** | **Astra-low** | **Sol-medium** | Astra-low | Advisor calls are infrequent, so each judgment can justify more spend. |

## If the default recommendation is redefined around cost/task

| Role | Best-value default | Extreme savings | Quality-first |
| --- | --- | --- | --- |
| Controller | **Sol-medium** | Luna-max | **Astra-low** |
| Worker | **Luna-max** | Luna-max | **Sol-medium** |
| Reviewer (weak) | **Luna-max** | Luna-max | **Terra-xhigh** |
| Explorer | **Luna-max** | Luna-max | **Terra-xhigh / Sol-medium** |
| Advisor | **Sol-medium** | Sol-medium | **Astra-low** |

That slightly changes the earlier conclusion:

- **Sol-medium can also be the default Advisor model.**
  - It is more robust from a `cost/task` perspective.
  - Escalate to Astra-low only for final arbitration, architecture decisions, or difficult multi-option trade-offs.
- **Terra-xhigh**
  - Fits best as a quality-upgrade tier for **Reviewer / Explorer**.
  - It is less attractive as the global default.
- **Luna-max**
  - Is the natural default for Worker / Explorer / weak Reviewer roles.

## Takeaway

> **Sol = default decision layer, Luna = default execution layer, Terra = mid-tier quality upgrade, Astra = high-value arbitration layer.**
