---
类型: 证据卡
来源: "[[论文卡-Yan2023-DeepfakeBench标准化基准]]"
证据类型: 数值
状态: 已核实（来自论文评测结果）
创建日期: 2026-10-09
更新日期: 2026-10-09
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [证据卡, Deepfake, 频域, 跨域]
---

# 证据卡 · DeepfakeBench-01 频域方法 SPSL 跨域 AUC 最高（78.75%）

## 1. 这条证据说什么

在统一协议下，UCF（空间域）取得最高**域内**平均 AUC 95.27%；而 **SPSL（频域）取得最高跨域平均 AUC 78.75%**。同时，域内 AUC 可达 99%+，跨到未见伪造方法或不同数据集时急剧下降。说明：**频域线索在跨域场景更可迁移**。

## 2. 原文 / 原始记录

> "UCF achieved the highest average within-domain AUC of 95.27%. … SPSL, a frequency-based detector, demonstrated superior robustness in cross-domain evaluations, reaching an average AUC of 78.75% on unseen datasets."

> "While many models achieve near-perfect AUC scores (99%+) on within-domain data, their performance drops sharply when tested on unseen manipulation methods or different datasets."

## 3. 位置

- 论文：arXiv:2307.01426（NeurIPS 2023 D&B），Experimental Results and Insights 章节。

## 4. 证据类型与强度

| 项目 | 内容 |
| --- | --- |
| 类型 | 数值 |
| 可信度 | 高（NeurIPS 2023；标准化协议下的可比结果，代码开源） |
| 可复现 | 是（https://github.com/SCLBD/DeepfakeBench，提供预训练权重） |

## 5. 我能用它做什么

- 支撑：RQ-001 中「**频域方法跨生成器更鲁棒**」这一 baseline 选择与假设。
- 支撑：**in-domain vs cross-domain 指标必须分开报告**（呼应课件 P25 的 clean/attack 分离）。
- 支撑：**CLIP 与频域方法在后处理下的对比假设**（频域线索易被压缩破坏）。
- 写进论文的哪一节：相关工作、实验设计（baseline 分组：naive / spatial / frequency）。

## 6. 备注

- 该工作亦发现「简单检测器 + 统一训练协议常不输复杂方法」→ 提示我做评测时要控制训练协议一致，否则比较不公平。
- 高斯模糊增强提升压缩鲁棒性但损害高质量数据表现（增强的权衡）→ 与后处理实验相关。
