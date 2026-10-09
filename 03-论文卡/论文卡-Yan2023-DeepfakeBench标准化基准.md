---
类型: 论文卡
标题: DeepfakeBench - A Comprehensive Benchmark of Deepfake Detection
作者: Zhiyuan Yan, Yong Zhang, Xinhang Yuan, Siwei Lyu, Baoyuan Wu（腾讯 AI Lab + CUHK-Shenzhen + SUNY Buffalo）
年份: 2023
发表: NeurIPS 2023 (Datasets and Benchmarks Track)
链接: https://arxiv.org/abs/2307.01426
代码: https://github.com/SCLBD/DeepfakeBench
状态: 已读（摘要+框架+关键结果）
优先级: 高
创建日期: 2026-10-09
更新日期: 2026-10-09
关联方向: "[[方向卡-Deepfake]]"
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [论文卡, Deepfake, 基准, 工具链]
---

# 论文卡 · DeepfakeBench（Yan 2023）

## 0. 一句话总结

深伪检测领域缺乏**标准化、统一、全面**的基准，导致性能比较不公平、结论可能误导；本文给出第一个综合性基准 **DeepfakeBench**：统一数据管理 + 集成 15 个 SOTA 检测方法的可扩展代码框架 + 标准化指标与协议（9 个数据集），并由此揭示「**简单检测器 + 统一训练协议**常常不输复杂方法」以及「**域内接近完美、跨域急剧下降**」两点关键结论。

## 1. 元信息

- 论文链接：https://arxiv.org/abs/2307.01426
- 代码 / 数据：https://github.com/SCLBD/DeepfakeBench（后续已扩展到 36 个检测器）
- 阅读程度：摘要 + 框架说明 + 关键结果

## 2. 研究问题

为什么深伪检测论文之间的性能**不可比**？根源是：① 数据预处理流程不统一（人脸裁剪、对齐、帧采样、压缩处理各不相同）；② 实验设置差异大；③ 评测策略与指标缺标准化。论文要建立一个「苹果对苹果」的比较平台。

## 3. 方法

- 核心思路：不是新方法，而是**标准化基础设施**。
- 关键模块：
  1. **数据处理模块**：统一人脸检测（DLIB）/ 对齐 / 裁剪，JSON 管理，支持 LMDB 加速 I/O；
  2. **训练模块**：实现 15 个 SOTA 检测方法，分三类——Naive（Xception/EfficientNet）、Spatial（Face X-ray/CORE）、Frequency（F3Net/SPSL）；
  3. **评测与分析模块**：标准指标 AUC/AP/ACC/EER + Grad-CAM、t-SNE 等诊断工具。

## 4. 实验设置

| 项目 | 内容 |
| --- | --- |
| 数据集 | 9 个主流数据集：FaceForensics++、Celeb-DF(v1/v2)、DFDC、DFDC-P、UADFV 等 |
| 基线 | 15 个 SOTA 检测器（后扩展到 36 个，含 Xception、EfficientNet-B4、SBI、SLADD、LSDA、I3D、FTCN、TALL、VideoMAE 等） |
| 指标 | Frame-level / Video-level AUC、ACC、EER、PR/AP |
| 训练 / 推理条件 | 统一切分 JSON，支持单卡与多卡 DDP；提供全部预训练权重 |

## 5. 主要结果

- **「简单」检测器很强**：用相同数据增强与预训练策略后，Xception、EfficientNet-B4 常常追平甚至超过更复杂的 SOTA 方法 → 架构创新的实际收益可能不如训练协议重要。
- **骨干选择是性能主因**：Xception / EfficientNet 因 depthwise separable 卷积，持续优于 ResNet。
- **域内/跨域落差**：许多模型域内 AUC 接近满分（99%+），但换到未见伪造方法或不同数据集时急剧下降。
- **标杆数字**：UCF（Spatial）域内平均 AUC 最高 95.27%；**SPSL（频域）跨域平均 AUC 最高 78.75%**。
- **数据增强是权衡**：高斯模糊提升压缩鲁棒性，但会损害高质量数据上的表现（模糊掉细粒度伪造线索）。

## 6. 局限与作者自己承认的问题

- 当时的基准以**帧级/图像级**为主，视频时序动态覆盖不足（作者列为后续工作）。
- 伪造类型覆盖面随时间会显得不够（后来 DF40 正是补这一块）。
- 数据集需自行下载预处理版本，初次配置有门槛。

## 7. 与我的方向 / RQ 的关系

- **支持**：为「域内高、跨域低」提供第二组独立证据；并明确「**频域方法 SPSL 跨域最强**」这一可复现的 baseline 线索。
- **可直接借用**：**作为我实验的工程底座**——统一预处理、统一指标、现成 baseline 权重，能在单卡上迅速跑出 EXP-001 的 in-domain 参考指标。
- **缺口**：基准本身不含「真实传播链后处理」维度 → 我的实验可在其之上叠加后处理模块。

## 8. 可复现性

- 代码是否开源：是（代码、评测、分析全开源；支持 Docker/Conda）。
- 复现难度与算力需求：**低–中**，提供预训练权重，单条命令即可评测；是入门首选。
- 我打算复现吗：**是**，EXP-001 直接基于此框架。

## 9. 抽出的证据卡

- [[证据卡-DeepfakeBench-01]]

## 10. 我的判断（可以是错的，但要写下来）

DeepfakeBench 是「工程地基」型的贡献：它不解决泛化，但让泛化研究变得**可比、可复现**。我的 EXP-001 用它跑基线，能避免「自己搭预处理导致数字不可比」的坑。它和 DF40 是互补的：前者管「统一」，后者管「多样」。
