# Datasets

| 数据集     | 作者                    | 主要贡献                                                                                                                        | 链接                                                                                                                        |
| ------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| R2R     | Peter Anderson et al. | 首次提出 “视觉 - 语言导航” 任务，奠定领域研究基础；提出 Matterport3D Simulator 开源工具与 R2R 数据集，成为领域基准。                                                | [homepage](https://bringmeaspoon.org/)<br>[paper](https://arxiv.org/abs/1711.07280)<br>                                   |
| R4R     |                       | 受数据生成流程所限，所有 R2R 参考路径在构建时均为 “直达目标的最短 路径”。为解决路径结构多样性不足的问题，谷歌团队提出 Room-for-Room（R4R） 数据集。                                     | [paper](https://arxiv.org/abs/1905.12255)<br>[github](https://github.com/google-research/google-research/tree/master/r4r) |
| RxR     | Alexander Ku et al.   | 规模是R2R的 10 倍；支持多语言（英语、印地语和泰卢固语）；包含的路径更长且多样性更 高；此外，该数据集还具备细粒度视觉接地（fine-grained visual groundings）功能（可将每个单词与环境中的像素 / 表面建立关联）。 | [paper](https://arxiv.org/abs/2010.07954)<br>[github](https://github.com/google-research-datasets/RxR)                    |
| VLN-CE  | Jacob Krantz et al.   | 将 VLN 任务从离散动作空间扩展至连续动作空间，引入物理碰撞与运动 约束，更贴近真实机器人导航场景。基于 Matterport3D 与 Habitat 平台构建，强调感知、避障与路径规划的综 合能力评估。                     | [homepage](https://jacobkrantz.github.io/vlnce/)<br>[paper](https://arxiv.org/abs/2004.02857)                             |
| CVDN    |                       | 模拟真实家庭对话场景，定义 “基于对话历史的导航任务”， 推动 VLN 与对 话系统的融合。                                                                              | [paper](https://arxiv.org/abs/1907.04957)<br>[github](https://github.com/mmurray/cvdn/)                                   |
| HANNA   |                       | 创新引入 “多模态助手（ANNA）”，为智能体提供语言与视觉辅助，结合 回溯好奇心激励模仿学习，提升目标导航效率。                                                                   | [paper](https://arxiv.org/abs/1909.01871)                                                                                 |
| SOON    |                       | 提出 “基于图的探索（GBE）” 方法，将导航过程建模为动态语义图构建， 结合模仿学习与强化学习优化策略，适用于复杂场景下的目标导航。                                                         | [paper](https://arxiv.org/abs/2103.17138)                                                                                 |
| REVERIE |                       | REVERIE 将视觉导航与物体定位结合，要求智能体在复杂室内场景中根据远程 描述找到特定目标物品。数据基于 Matterport3D，包含丰富的自然语言指令与目标物 体标注，任务难度高，需要结合全局导航规划与局部视觉识别。            | [paper](https://arxiv.org/abs/1904.10151)<br>[github](https://github.com/YuankaiQi/REVERIE)                               |

# Paper

## 算法

| 论文               | 主要贡献                                                                                           | 链接                                                                                                                                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| VLN-R1           | 基于大型视觉语言模型（如 Qwen2-VL）构建框架，结合监督微调 （SFT）与带时间衰减奖励（TDR）的 GRPO 强化微调（RFT），实现端到端的第一 视角视频流到连续导航动作的转化。 | [homepage](https://vlnr1.github.io/)<br>[paper](https://arxiv.org/abs/2506.17221)<br>[github](https://github.com/Qi-Zhangyang/GPT4Scene-and-VLN-R1)<br>[公开课](https://www.shenlanxueyuan.com/open/course/291) |
| RCM              | 提出了创新性的强化跨模态匹配（RCM）和自监督模仿学习（SIL）方 法，显著提升了导航代理在真实 3D 环境中的指令跟随能力与泛化性。                            | [paper](https://arxiv.org/abs/1811.10092)                                                                                                                                                                    |
| Speaker-Follower | 提出双模型架构， “说话者（Speaker）” 模型从视觉轨迹生成指令以扩充 数据， “跟随者（Follower）” 模型验证指令并生成轨迹，形成数据增强闭环。               | [homepage](https://ronghanghu.com/speaker_follower/)<br>[paper](https://arxiv.org/abs/1806.02724)<br>[github](https://github.com/ronghanghu/speaker_follower)                                                |

## 综述

| 论文                                                                                          | 主要贡献                                             | 会议/期刊 | 年份   | 链接                                                                                                                         |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------ | ----- | ---- | -------------------------------------------------------------------------------------------------------------------------- |
| Vision-and-Language Navigation Today and Tomorrow: A Survey in the Era of Foundation Models | 聚焦基础模型对 VLN 研究范式的重构，分析当前技术突破与未来研究方向，具备较强的前瞻性。    | TMLR  | 2024 | [paper](https://arxiv.org/abs/2407.07035)<br>[github](https://github.com/zhangyuejoslin/VLN-Survey-with-Foundation-Models) |
| Vision-and-Language Navigation: A Survey of Tasks, Methods, and Future Directions           | 全面梳理 VLN 领域的核心任务、数据集、评估指标、技术方法及待解决挑战，是领域入门的权威参考。 |       | 2022 | [paper](https://arxiv.org/abs/2203.12667)                                                                                  |

# Metrics

| 评价指标    | 全称                                                       | 主要衡量                                 | 公式                                                        |
| ------- | -------------------------------------------------------- | ------------------------------------ | --------------------------------------------------------- |
| NE      | Navigation Error                                         | 最终位置距目标多远                            | $NE=d(p_{final},g)$                                       |
| SR      | Success Rate                                             | 是否成功到达目标                             | $SR = \frac{\text{succ episode}}{\text{total episode }}$  |
| SPL     | Success weighted by Path Length                          | 成功 + 路径效率                            | $SPL = \frac{1}{N} \sum_i S_i \frac{L_i} {\max(P_i,L_i)}$ |
| OSR     | Oracle Success Rate                                      | 过程中是否曾到达目标附近（只要轨迹中某一时刻曾经进入目标附近，就算成功） | $\min_t d(p_t,g) < d_{th}$<br>$OSR \ge SR$                |
| TL / PL | Trajectory / Path Length                                 | 实际走了多远                               | $TL=\sum_{t=1}^{T-1} d(p_t,p_{t+1})$<br>                  |
| CLS     | Coverage Weighted by Length Score                        | 智能体的轨迹与参考路径的贴合程度                     |                                                           |
| nDTW    | Normalized Dynamic Time Warping                          | 会惩罚与真实轨迹的偏差                          |                                                           |
| sDTW    | Normalized Dynamic Time Warping Weighted by Success Rate | 会惩罚与真实轨迹的偏差，同时也会考量成功率                |                                                           |








# Introduction

Q: 什么是具身智能（Embodied AI）？
A: 具生智能是指研究能够感知、推理和行动以与物理世界交互的智能体，通过身体与环境的交互来学习和理解。

Q: 什么是视觉与语言导航（VLN）？
A: VLN是具生AI的一个子领域，目标是训练智能体根据自然语言，融合视觉和语言信息以进行决策，在3D环境中导航。
- 输入：视觉感知和自然语言指令
- 输出：线速度+角速度

Q: 目前VLN的关键挑战

- 感知模糊性：视觉信息可能不完整或模糊。
- 语言模糊性：自然语言指令可能不精确、有歧义或包含隐含信息。
- 泛化能力：在未见过的环境中导航的能力。
- 长程规划：规划跨越多个房间或复杂路径的行动序列。
- 指令遵循：准确理解和执行指令的每个部分。
- 记忆与推理：记住已探索的区域和指令进度。




核心组件：
- 视觉编码器
- 语言编码器
- 跨模态融合
- 导航策略

学习范式
- 模仿学习
- 强化学习
- 混合学习

早期方法

Seq2Seq VLN模型
- 将语言指令和视觉序列映射到行动序列
- Encoder-Decoder结构
	- Encoder：编码语言指令
	- Decoder：根据编码后的指令和视觉观测生成行动
- Language Encoder：通常使用LSTM或者GRU编码指令
- Vision Encode：提取当前视角的特征，使用CNN，Resnet
- Decoder：另一个LSTM或者GRU生成行动

注意力机制
- 语言注意力
- 跨模态注意力


