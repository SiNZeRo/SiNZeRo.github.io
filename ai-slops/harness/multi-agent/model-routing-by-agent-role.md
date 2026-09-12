---
layout: post
title: "Multi-agent Model Routing by Role"
description: "Controller, Worker, Reviewer, Explorer, Advisor 的模型分工与 cost/task 默认选择。"
date: 2026-09-12
category: "HARNESS / MULTI-AGENT"
article_parent: /ai-slops/harness/multi-agent/
---

可以，改成这三个维度更清楚：

| Role | 默认推荐 | 性价比备选（cost/task） | 优质备选 | 备注 |
| --- | --- | --- | --- | --- |
| **Controller** | **Sol-medium** | Luna-max | **Astra-low** | 默认需要稳定判断；难任务升 Astra |
| **Worker** | **Luna-max** | Luna-max | **Sol-medium** | bounded task 优先压低单任务成本 |
| **Reviewer (weak)** | **Luna-max** | Luna-max | **Terra-xhigh** | weak reviewer 主要抓明显 bug |
| **Explorer** | **Luna-max** | Luna-max | **Terra-xhigh** | 搜索/试探很吃 token，便宜最重要 |
| **Advisor** | **Astra-low** | **Sol-medium** | Astra-low | advisor 调用少，单次判断价值高 |

## 如果把「默认推荐」也按 cost/task 逻辑重新定义

| Role | 最佳性价比默认 | 极致省钱 | 追求质量 |
| --- | --- | --- | --- |
| Controller | **Sol-medium** | Luna-max | **Astra-low** |
| Worker | **Luna-max** | Luna-max | **Sol-medium** |
| Reviewer (weak) | **Luna-max** | Luna-max | **Terra-xhigh** |
| Explorer | **Luna-max** | Luna-max | **Terra-xhigh / Sol-medium** |
| Advisor | **Sol-medium** | Sol-medium | **Astra-low** |

这里我其实会稍微修正前面的结论：

- **Advisor 默认也可以用 Sol-medium**
  - 从 `cost/task` 看更稳。
  - 只有真正需要「最终裁决 / 架构判断 / 多方案取舍」时再上 Astra-low。
- **Terra-xhigh**
  - 最适合放在 **Reviewer / Explorer 的质量升级档**。
  - 不太适合当全局默认。
- **Luna-max**
  - 在 Worker / Explorer / weak Reviewer 上几乎是天然默认。

## Takeaway

> **Sol = 默认决策层，Luna = 默认执行层，Terra = 中档质量升级，Astra = 高价值裁决层。**
