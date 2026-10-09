---
类型: 证据卡
来源: "[[论文卡-2025-真实世界深伪检测评估]]"
证据类型: 结论
状态: 已核实（来自论文）
创建日期: 2026-10-09
更新日期: 2026-10-09
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [证据卡, Deepfake, 商业工具, 方法学]
---

# 证据卡 · RealWorld2025-01 商业工具宣称 98–99%、实测多款低于 65%

## 1. 这条证据说什么

商业深伪检测工具常宣称 98–99% 准确率，但独立评测中**被测的四款工具准确率低于 65%**；同时，在对已来自社交媒体的样本追加后处理时，性能变化比多在 **[0.9, 1.1]**，作者解释为**样本已含压缩/模糊（饱和效应）**，而非检测器真的鲁棒。

## 2. 原文 / 原始记录

> "…several companies claim more than 98 or 99% accuracy, whereas four of the tools we test are below 65% accuracy."

> "For both image and video sets, we find that most performance change ratios (with post-processing versus without) fall within the range of [0.9, 1.1], indicating that post-processing has minimal impact… This stability may be attributed to the fact that political deepfake samples in the PDID are sourced from social media, where they have already undergone various post-processing operations."

后处理操作清单：JPEG Compression (JC)、Gaussian Blur (GB)、HSV Shift、Brightness/Contrast (BC)、Rotation (RT)。

## 3. 位置

- 论文：arXiv:2510.16556，Table 4 与 §2.2 后处理鲁棒性评估、Figure 5。

## 4. 证据类型与强度

| 项目 | 内容 |
| --- | --- |
| 类型 | 结论 + 数值 |
| 可信度 | 中–高（预印本；商业黑盒评测有时效性与覆盖度限制，作者已声明） |
| 可复现 | 部分（商业 API 不可复现；方法学可借鉴） |

## 5. 我能用它做什么

- 支撑：宣称的检测性能不可信（工业界与学术界都有此问题）。
- 支撑：**后处理操作标准清单**（JC/GB/HSV/BC/RT）作为我的后处理库。
- **方法学警示（最重要）**：后处理实验必须**从干净样本出发**施加退化阶梯，否则会因饱和效应低估影响 → 直接写入我的实验设计约束。
- 写进论文的哪一节：实验设计（变量定义与方法学辩护）、引言。

## 6. 备注

- 商业工具会版本更新、评测结果有时效性。
- 数据集聚焦政治深伪（PDID），领域偏窄，不能外推所有场景。
