---
类型: 关键词卡
中文术语: Deepfake 检测
英文术语: Deepfake Detection / Face Forgery Detection
别名: 深伪检测、人脸伪造检测、AI 换脸检测
上位概念: AIGC 内容安全 / 生成内容检测
状态: 使用中
创建日期: 2026-10-09
更新日期: 2026-10-09
关联方向: "[[方向卡-Deepfake]]"
关联RQ: ["[[RQ-001-Deepfake检测器跨生成器泛化与后处理可靠性]]"]
标签: [关键词卡, Deepfake]
---

# 关键词卡 · Deepfake 检测

## 1. 定义

- 通俗版：判断一张人脸图片或一段人脸视频「是真实拍摄的，还是 AI 生成 / 篡改的」。
- 学术版：给定媒体样本 $x$，学习判别函数 $f(x) \in \{\text{real}, \text{fake}\}$（或输出伪造概率与伪造区域掩码）。

## 2. 为什么要建这张卡

这是本方向的核心任务词。检索论文、找数据集、找基线代码，都以它为主入口；后续所有的 RQ 都建立在「检测器在什么条件下会失效」这个问题上。

## 3. 常用检索式（Google Scholar / arXiv / Semantic Scholar）

- `"deepfake detection"`
- `"face forgery detection" OR "face manipulation detection"`
- `deepfake detection generalization unseen generator`
- `deepfake detection robustness compression post-processing`
- `deepfake detection benchmark evaluation`
- `audio deepfake detection`（想要音频方向时）

## 4. 相关关键词（待建卡）

- [[关键词卡-跨生成器泛化]]（已有）
- 对抗样本（概念卡，待建）
- 后处理鲁棒性 / 传播链退化 → [[概念卡-后处理鲁棒性]]（已建）
- 水印与溯源（待建）
- 数据集偏置 / shortcut learning → [[概念卡-捷径学习]]（已建）

## 5. 相关论文（阶段 2 文献调研后补全）

| 论文 | 年份 | 类型 | 卡片 |
| --- | --- | --- | --- |
| DF40 | 2024 | 基准 | [[论文卡-Yan2024-DF40下一代深伪检测基准]] |
| Croitoru 综述 | 2024 | 综述 | [[论文卡-Croitoru2024-生成式AI时代深伪检测综述]] |
| DeepfakeBench | 2023 | 基准+框架 | [[论文卡-Yan2023-DeepfakeBench标准化基准]] |
| Deepfake-Eval-2024 | 2025 | 基准 | [[论文卡-Chandra2025-DeepfakeEval2024真实场景基准]] |
| Ojha 2023 (CLIP) | 2023 | 方法 | [[论文卡-Ojha2023-CLIP通用伪造检测]] |
| ProFake | 2024 | 方法 | [[论文卡-Xu2024-ProFake质量退化鲁棒检测]] |
| FreqNet | 2024 | 方法 | [[论文卡-Tan2024-FreqNet频域泛化检测]] |
| Real World DFD | 2025 | 评测 | [[论文卡-2025-真实世界深伪检测评估]] |

## 6. 备注 / 易混点

- 「检测器准确率高」≠「安全」：课件 P4 明确把 Deepfake 检测的红色风险标为**未知生成器**，也就是跨生成器泛化问题。
- 「检测」与「定位」是两件事：检测给标签，定位给区域（后者通常用于取证场景）。
- 评测时要区分 clean 条件与 attack 条件（课件 P25：Clean Accuracy 与 Attack Success Rate 必须分开看）。
