---
类型: 证据卡
来源: "[[论文卡-Xu2024-ProFake质量退化鲁棒检测]]" 与 "[[论文卡-Chandra2025-DeepfakeEval2024真实场景基准]]"
证据类型: 数值
状态: 已核实（来自论文摘要）
创建日期: 2026-10-09
更新日期: 2026-10-09
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [证据卡, Deepfake, 后处理, 鲁棒性]
---

# 证据卡 · Robustness2026-01 压缩与模糊使平均准确率从 94.7% 降到 67.8%

## 1. 这条证据说什么

在 FF++ 与 Celeb-DF v2 上系统评测 5 个换脸检测器（XceptionNet、MesoNet、FSD-GAN、FakeTracer、Hybrid+Landmark）在四类退化下的表现：**平均准确率从干净条件 94.7% 降至退化条件 67.8%（总体退化率 −26.9%）**；JPEG 压缩与运动模糊造成最大下降（最多 35%），尤其打击轻量 CNN 检测器。

## 2. 原文 / 原始记录

> "Average accuracy declined from 94.7% on clean data to 67.8% on distorted data, corresponding to an overall degradation rate of −26.9%. JPEG compression and motion blur caused the most significant performance drops, with reductions of up to 35%, particularly for lightweight CNN-based detectors."

退化条件（可用于我的后处理分档设计）：

- JPEG 压缩：质量 20–90
- 高斯噪声：σ = 0.01–0.05
- 运动模糊：核大小 3–15
- 视频编码伪影：码率 50–500 kbps

## 3. 位置

- 论文：*Evaluating the real-world robustness of face-swap detection models under compression and noise*，Frontiers in AI，2026，Abstract 与 Results。DOI: 10.3389/frai.2026.1835651

## 4. 证据类型与强度

| 项目 | 内容 |
| --- | --- |
| 类型 | 数值 |
| 可信度 | 中–高（期刊论文，数字明确；但与 ProFake/DFEval 的具体协议不同，跨论文绝对值不可直接比较） |
| 可复现 | 部分（数据集公开；实验脚本需自查） |

## 5. 我能用它做什么

- 支撑：RQ-001 的后处理分支——**后处理是独立于「跨生成器」的第二个强失效来源**，且影响幅度可量化（−26.9% 平均，最坏 −35%）。
- 支撑：**退化操作清单与强度区间**（JPEG 20–90、噪声 σ、模糊核、码率）可作为我后处理分档的**直接依据**。
- 写进论文的哪一节：实验设计（后处理变量定义）、预期结果。

## 6. 备注

- 与 [[论文卡-2025-真实世界深伪检测评估]] 的「后处理影响很小」结论**看似矛盾**——原因是后者样本已退化（饱和效应），前者从干净样本出发。**我的实验设计必须明确站在「从干净样本施加退化」这一侧**，并在论文中解释这一方法学分歧。
- FSD-GAN、FakeTracer 类「隐指纹/痕迹嵌入」方法退化更小（≤ −15%），提示**线索类型**决定后处理脆弱度 → 可检验假设。
