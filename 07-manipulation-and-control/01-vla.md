
# 开源框架

## 面壁智能(OpenBMB)

### MiniCPM-Robot
- github: [https://github.com/OpenBMB/MiniCPM-Robot](https://github.com/OpenBMB/MiniCPM-Robot)
- MiniCPM-Robot 是 MiniCPM 面向真实世界感知、决策与行动的具身智能模型系列。首批模型包括：
	- MiniCPM-RobotManip：🦾 1.5B 通用机器人操作 VLA（仿真与真机）。一套权重覆盖下游任务，代表性评测中超过 π₀.₅ (3B)、 Qwen-VLA (5B+) 等更大模型。流式推理保留原生记忆能力，并且维持了和以前一样的响应速度。
	- MiniCPM-RobotTrack：🎯 首个纯端侧具身目标跟踪方案（0.9B）。覆盖静态、动态与对抗目标，EVT-Bench 开源 SOTA；在 Unitree Go2 EDU 上可达 5+ FPS / 约 180 ms，纯视觉、纯本地自然语言跟踪。