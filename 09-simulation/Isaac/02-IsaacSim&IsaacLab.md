IsaacSim官网：[https://docs.isaacsim.omniverse.nvidia.com/5.0.0/index.html](https://docs.isaacsim.omniverse.nvidia.com/5.0.0/index.html)

IsaacLab官网：[https://developer.nvidia.com/isaac/lab](https://developer.nvidia.com/isaac/lab)

GitHub：[https://github.com/isaac-sim/IsaacLab](https://github.com/isaac-sim/IsaacLab)

IsaacLab主页：[https://isaac-sim.github.io/IsaacLab/main/index.html](https://isaac-sim.github.io/IsaacLab/main/index.html)

# 运行

```shell
# 查看torch版本，并确认cuda是否可用
python -c "import torch; print(torch.__version__); print(torch.version.cuda); print(torch.cuda.is_available())"

# # 输出：
# 2.7.0+cu128
# 12.8
# True
```

```shell
cd ~/IsaacLab

# 查看IsaacLab版本
cat VERSION

# 查看IsaacSim版本
python -c "from importlib.metadata import version; print(version('isaacsim'))"

# 创建一个空场景
./isaaclab.sh -p scripts/tutorials/00_sim/create_empty.py

# 训练robot dog
./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/train.py --task=Isaac-Velocity-Rough-Anymal-C-v0 --num_envs 16

```

# Create new project or task

参考[官方文档](https://isaac-sim.github.io/IsaacLab/main/source/overview/own-project/template.html)

```shell
# generator
./isaaclab.sh --new
# 或者
./isaaclab.sh -n

# ? Task type: External
# ? Project path: /root/fengxian/
# ? Project name: robot_rl
# ? Isaac Lab workflow: Manager-based | single-agent
# ? RL library: rsl_rl

# 把项目装到 Isaac 里面
python -m pip install -e source/robot_rl
```




# Env

[官方提供的环境](https://isaac-sim.github.io/IsaacLab/main/source/overview/environments.html)

有两种：
- 创建Direct  RL Environment，参考[官方文档](https://isaac-sim.github.io/IsaacLab/main/source/tutorials/03_envs/create_direct_rl_env.html)，特点：直接灵活自由度高
	- 优点：非常适合个性化程度高的项目
	- 缺点：维护成本高
- 创建Manager-Based RL Environment，参考[官方文档](https://isaac-sim.github.io/IsaacLab/main/source/tutorials/03_envs/create_manager_rl_env.html)，特点：模块化，把环境按照职责拆开


## Manager-Based RL Environment

### ManagerBasedRLEnvCfg

场景Scene：
- 地面
- 灯光
- 机器人

交互相关：
- Observation
- Action
- Event

强化学习相关：
- reward
- termination

参考配置：[velocity_env_cfg](https://github.com/isaac-sim/IsaacLab/blob/main/source/isaaclab_tasks/isaaclab_tasks/manager_based/locomotion/velocity/velocity_env_cfg.py)