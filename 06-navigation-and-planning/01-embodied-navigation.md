# Paper

| 实验室                             | 算法/框架              | 主要工作                                                                                                                | 链接                                                                                                                                                                                     |
| ------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Shanghai AI Lab Intern Robotics | NavDP              | 通过扩散策略直接建模视觉—语言条件下的连续导航动作分布，使机器人能够从多模态观测中生成平滑、长时域且具多模态性的导航轨迹。                                                       | [paper](https://arxiv.org/abs/2505.08712)                                                                                                                                              |
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

| 数据集           |
| ------------- |
| R2R           |
| RxR           |
| VLN-CE        |
| InternData-N1 |




# 参考资料

## 知乎

[定位范式——具身导航第一性的演进与抉择](https://zhuanlan.zhihu.com/p/2069160310653597629)
