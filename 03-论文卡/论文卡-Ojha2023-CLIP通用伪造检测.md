---
类型: 论文卡
标题: Towards Universal Fake Image Detectors that Generalize Across Generative Models
作者: Utkarsh Ojha, Yuheng Li, Yong Jae Lee（University of Wisconsin-Madison）
年份: 2023
发表: CVPR 2023
链接: https://openaccess.thecvf.com/content/CVPR2023/papers/Ojha_Towards_Universal_Fake_Image_Detectors_That_Generalize_Across_Generative_Models_CVPR_2023_paper.pdf
代码: https://github.com/WisconsinAIVision/UniversalFakeDetect
状态: 已读（摘要+方法+关键结果）
优先级: 高
创建日期: 2026-10-09
更新日期: 2026-10-09
关联方向: "[[方向卡-Deepfake]]"
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [论文卡, Deepfake, 基线, CLIP, 泛化]
---

# 论文卡 · Ojha 2023（CLIP 通用伪造检测）

## 0. 一句话总结

传统「训练一个分类器判真假」的做法会**非对称地过拟合**：它只学会识别训练所用生成器家族的指纹，把其他一切（包括其他生成器的假图）都归为「真」；作者提出在**未针对真假检测训练过的 CLIP 特征空间**里做最简单的最近邻 / 线性探针分类，在未见扩散模型与自回归模型上大幅超越 SOTA（例如 +25.90% 准确率）。

## 1. 元信息

- 论文链接：CVPR 2023 开放论文页（见 frontmatter）
- 代码 / 数据：https://github.com/WisconsinAIVision/UniversalFakeDetect
- 阅读程度：摘要 + 方法（feature space 选择）+ 主要结果

## 2. 研究问题

- RQ1：在一种生成模型家族（如 GAN）上训练的真假分类器，迁移到未见家族（如 diffusion）时表现如何？
- RQ2：能否用**一个并非为真假检测训练的特征空间**来做真假分类？
- RQ3–RQ6：网络架构与预训练数据的影响、训练数据来源（GAN vs diffusion）的影响、所需最小训练数据量、对后处理（JPEG 压缩、高斯模糊）的鲁棒性。

## 3. 方法

- 核心思路：分类应发生在**一个没有被训练去区分真假**的特征空间里，以避免非对称偏置。
- 关键设计：
  - 用 **CLIP:ViT-L/14**（4 亿图文对训练）的视觉编码器输出作为特征 φ；
  - 两种极简分类器：**最近邻（NN）** 与 **线性探针（LC）**；
  - 训练时冻结骨干（`--fix_backbone`），只训线性层。
- 关键概念：**「sink class」问题**——真类成了「收纳一切不符合已学假模式样本」的垃圾桶。

## 4. 实验设置

| 项目 | 内容 |
| --- | --- |
| 数据集 | 训练：ProGAN（LSUN）+ LDM（LAION）；测试：GAN 家族（StyleGAN/BigGAN/CycleGAN/GauGAN/StarGAN/DeepFake）、扩散（LDM/Guided/Glide）、自回归（DALL-E） |
| 基线 | 端到端训练的深度网络分类器（Wang2020 等） |
| 指标 | AP（平均精度）、Accuracy |
| 训练 / 推理条件 | 冻结 CLIP 骨干，只训线性层；单卡可复现 |

## 5. 主要结果

- 传统分类器迁移到未见家族时**接近随机（约 50–55%）**，且失效方式是「把未见假图判成真」：对 LDM 的假图检测准确率仅 **3.05%**、Guided 仅 **4.67%**，而真图准确率仍很高。
- 作者方法的增益：相对最佳 baseline **+15.07 mAP**、**+25.90% 准确率**；在未见扩散+自回归模型上 **+19.49 mAP**。
- **对常见后处理（JPEG 压缩、高斯模糊）保持鲁棒**，同时保住泛化优势。

## 6. 局限与作者自己承认的问题

- 主要针对**图像**，人脸视频场景需另做适配（后由 DF40 等扩展到人脸）。
- 依赖大规模预训练骨干（CLIP），对算力与权重可用性有依赖。
- 「真实图像」的定义依赖训练集分布，仍是相对判断。

## 7. 与我的方向 / RQ 的关系

- **支持**：为「为什么跨生成器会失效」提供**机制解释**（非对称调优 / sink class / 频域指纹过拟合）——这是 RQ-001 里「障碍（barriers）」那一条的直接来源。
- **可直接借用**：**CLIP + 线性探针**是我的核心 baseline（DF40 也证实 CLIP-large 最强），实现简单、单卡可跑。
- **缺口**：验证了「对 JPEG/模糊有一定鲁棒」，但没有系统做「传播链级后处理 + 未见生成器」的联合评测。

## 8. 可复现性

- 代码是否开源：是。
- 复现难度与算力需求：**低**（冻结骨干 + 线性层），单卡即可。
- 我打算复现吗：**是**，作为 EXP-001 的第二个 baseline（与 Xception 对照）。

## 9. 抽出的证据卡

- [[证据卡-Ojha2023-01]]

## 10. 我的判断（可以是错的，但要写下来）

这篇论文给了我的 RQ 一个**可检验的机制假设**：跨生成器失效的本质是「学到了生成器指纹而非伪造本质」。如果这个假设成立，那么「后处理越强、指纹越被破坏、检测越失效」应当是一条单调曲线——这正是我 EXP 要测的东西。
