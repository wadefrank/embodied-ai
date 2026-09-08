# 任务分类

| 任务              | 目标                                  | 代表作                                                                                     |
| --------------- | ----------------------------------- | --------------------------------------------------------------------------------------- |
| **PointNav**    | 已知目标位置，在未知或部分未知环境中安全高效地到达该目标点。      | DD-PPO、Active Neural SLAM、NavDP                                                         |
| **ObjectNav**   | 已知目标物体类别但不知道其位置，通过语义感知与探索找到并到达目标物体。 | SemExp、CogNav、TravExplorer                                                              |
| **VLN**         | 根据自然语言指令理解环境与路线，并完成语言描述的导航任务。       | R2R、HAMT、DualVLN、Embodied-Navigator                                                     |
| **ImageNav**    | 给定目标地点或目标实例的图像，导航到与目标图像对应的位置。       | Memory-Augmented RL for Image-Goal Navigation、Navigating to Objects Specified by Images |
| **Exploration** | 在没有明确终点的情况下，高效探索未知环境并尽可能获取更多环境信息。   | Active Neural SLAM、Neural SLAM / learned exploration 系列                                 |

# Paper

| 实验室                             | 算法/框架              | 主要工作                                                                                                                | 链接                                                                                                                                                                                     |
| ------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Shanghai AI Lab Intern Robotics | NavDP              | 通过扩散策略直接建模视觉—语言条件下的连续导航动作分布，使机器人能够从多模态观测中生成平滑、长时域且具多模态性的导航轨迹。                                                       | [homepage](https://wzcai99.github.io/navigation-diffusion-policy.github.io/)<br>[paper](https://arxiv.org/abs/2505.08712)<br>[github](https://github.com/InternRobotics/NavDP)         |
|                                 | DualVLN            | 通过“VLM 高层全局规划（System 2）+ 低层快速导航策略（System 1）”的双系统架构，将语义推理与连续运动控制解耦，实现更高效、稳健的 VLN 导航。                                 | [paper](https://arxiv.org/abs/2512.08186)<br>[github](https://github.com/InternRobotics/InternNav)                                                                                     |
|                                 | X-NavDP            | 在 NavDP 基础上引入跨机器人形态的在线强化学习后训练，并通过 Group Q-score Reweighted Matching（GQRM）提升扩散导航策略在新行为、困难场景和不同机器人 embodiment 上的泛化能力。 | [paper](https://arxiv.org/abs/2607.28560)                                                                                                                                              |
|                                 | StreamVLN          |                                                                                                                     | [github](https://github.com/InternRobotics/StreamVLN)                                                                                                                                  |
|                                 | LoGoPlanner        |                                                                                                                     | [github](https://github.com/InternRobotics/NavDP/tree/master/baselines/logoplanner)                                                                                                    |
| Alibaba AMAP CV Lab             | ABot-N0            | 通过 Brain-Action 分层 VLA 架构统一多种具身导航任务，实现从高层语义/空间推理到连续 waypoint 轨迹生成的端到端导航。                                            | [homepage](https://amap-cvlab.github.io/ABot-Navigation/ABot-N0/)<br>[paper](https://arxiv.org/abs/2602.11598)<br>[github](https://github.com/amap-cvlab/ABot-Navigation/tree/ABot-N0) |
|                                 | OmniNav            | 提出了一套统一具身导航框架，通过快慢双系统架构结合连续 waypoint 预测与长程规划，在同一模型中同时支持 PointNav、ObjectNav、VLN 和前沿探索，并兼顾实时性与真实机器人部署。                | [github](https://github.com/amap-cvlab/OmniNav/)                                                                                                                                       |
| OpenBMB                         | MiniCPM-RobotTrack | 轻量级端侧具身目标追踪模型，能够根据自然语言指定目标，并直接基于视觉输入驱动机器人持续跟踪静态或动态目标。                                                               | [github](https://github.com/OpenBMB/MiniCPM-Robot)                                                                                                                                     |
| University of Freiburg          | HOV-SG             | 通过构建“楼层—房间—物体”层次化开放词汇 3D 场景图，让机器人能够根据自然语言目标进行语义理解、目标定位和导航。                                                          | [homepage](https://hovsg.github.io/)<br>[paper](https://arxiv.org/abs/2403.17846)<br>[github](https://github.com/hovsg/HOV-SG)                                                         |
| Horizon Robotics                | HoloAgent          | 通过融合 3D 空间记忆、具身技能库和 AgentOS，将自然语言任务分解为可执行技能并支持机器人在真实环境中持续感知、执行、监控与重规划。                                              | [paper](https://arxiv.org/abs/2606.23565)<br>[github](https://github.com/HorizonRobotics/HoloAgent)                                                                                    |
| NJU R&L Group Embodied Lab      | Uni-LaViRA         | 通过“语言动作 → 视觉目标 → 机器人动作”的分层转换框架，利用多模态大模型统一解决 VLN、ObjectNav、EQA 和空中导航等多种具身导航任务。                                       | [homepage](https://xetroubadour.github.io/Uni-LaViRA/)<br>[paper](https://arxiv.org/abs/2605.27582)<br>[github](https://github.com/NJU-R-L-Group-Embodied-Lab/uni-lavira-code)         |

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
| Gibson  |                       |                                                                                                                             |                                                                                                                           |

# Simulator


| 仿真器          |     |     |
| ------------ | --- | --- |
| Matterport3d |     |     |
| Habitat      |     |     |
| Isaac        |     |     |


# 参考资料

## 知乎

[定位范式——具身导航第一性的演进与抉择](https://zhuanlan.zhihu.com/p/2069160310653597629)
