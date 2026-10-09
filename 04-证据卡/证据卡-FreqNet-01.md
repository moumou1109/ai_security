---
类型: 证据卡
来源: "[[论文卡-Tan2024-FreqNet频域泛化检测]]"
证据类型: 数值
状态: 已核实（来自 AAAI 2024 摘要）
创建日期: 2026-10-09
更新日期: 2026-10-09
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [证据卡, Deepfake, 频域, 泛化]
---

# 证据卡 · FreqNet-01 强制关注高频使跨生成器性能 +9.8% 且参数更少

## 1. 这条证据说什么

既有频域检测方法依赖 GAN 上采样伪影、会过拟合训练数据；FreqNet 通过学习**源无关（source-agnostic）**的频率特征，在 **17 个 GAN** 的跨生成器评测中达到 SOTA，相对当时最佳 **+9.8%**，且**参数量更少**。

## 2. 原文 / 原始记录

> "Extensive experimentation involving 17 GANs demonstrates the effectiveness of our proposed method, showcasing state-of-the-art performance (+9.8%) while requiring fewer parameters."

> "these detectors … tend to overfit to the artifacts present in the training data, leading to suboptimal performance on unseen sources."

## 3. 位置

- 论文：arXiv:2403.07240（AAAI 2024）摘要。

## 4. 证据类型与强度

| 项目 | 内容 |
| --- | --- |
| 类型 | 数值 |
| 可信度 | 高（AAAI 2024 正会；代码开源） |
| 可复现 | 是（https://github.com/chuangchuangtan/FreqNet-DeepfakeDetection） |

## 5. 我能用它做什么

- 支撑：「**频域线索更接近源无关的伪造本质**」这一假设，与 [[证据卡-DeepfakeBench-01]] 互相印证。
- 支撑：频域 baseline 的可获取性（轻量、单卡友好）。
- **引出可检验假设**：频域线索对**压缩敏感** → 预期频域方法在**后处理**下比空域/CLIP 方法更脆弱。这是 RQ-001 中一个待实验验证的交叉假设。
- 写进论文的哪一节：相关工作（方法侧）、实验设计（baseline 分组）。

## 6. 备注

- 评测以 GAN 为主，扩散模型覆盖不足（2024 年的普遍局限）。
- 与 [[证据卡-DeepfakeBench-01]] 的 SPSL 结论一致：频域阵营跨域更强。
