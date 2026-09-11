
homepage: [https://aihabitat.org/](https://aihabitat.org/)
github: [https://github.com/facebookresearch/habitat-sim](https://github.com/facebookresearch/habitat-sim)


# 环境配置

```shell
### 1.新建conda环境
conda create -n internnav_habitat python=3.9 -y
conda activate internnav_habitat

### 2.安装 Habitat-Sim
# 2.1 conda安装
conda install habitat-sim==0.2.4 withbullet headless -c conda-forge -c aihabitat

### 3.安装Habitat-Lab
# 3.1 拉取github代码
git clone --branch v0.2.4 https://github.com/facebookresearch/habitat-lab.git

# 3.2 安装依赖项
cd habitat-lab
pip install -e habitat-lab
pip install -e habitat-baselines

# 4.检查 Habitat 能不能正常工作
# 正常情况下输出：
# habitat import: OK
# habitat_sim import: OK
# habitat_sim version: 0.2.4
python - <<'PY'
import habitat
import habitat_sim

print("habitat import: OK")
print("habitat_sim import: OK")
print("habitat_sim version:", getattr(habitat_sim, "__version__", "unknown"))
PY

# 5.pip check
# generate-parameter-library-py 0.5.0 requires jinja2, which is not installed.
# generate-parameter-library-py 0.5.0 requires typeguard, which is not installed.
pip install jinja2 typeguard

# 6.检查Habitat的版本和配置加载

cd /home/gm_wadefrankslam/fengxian/project/habitat-lab

python - <<'PY'
import habitat

config = habitat.get_config(
    config_path="benchmark/nav/pointnav/pointnav_habitat_test.yaml"
)

print("PointNav config loaded successfully")
print("task type:", config.habitat.task.type)
print("dataset type:", config.habitat.dataset.type)
PY

# 正常情况下输出：
# PointNav config loaded successfully
# task type: Nav-v0
# dataset type: PointNav-v1

```

# 测试

下载最小测试场景和 PointNav 数据

```shell
cd /home/gm_wadefrankslam/fengxian/project/habitat-lab

python -m habitat_sim.utils.datasets_download \
    --uids habitat_test_scenes \
    --data-path data/

python -m habitat_sim.utils.datasets_download \
    --uids habitat_test_pointnav_dataset \
    --data-path data/

python - <<'PY'
import habitat

config = habitat.get_config(
    config_path="benchmark/nav/pointnav/pointnav_habitat_test.yaml"
)

env = habitat.Env(config=config)
obs = env.reset()

print("=== SUCCESS ===")
print("obs:", obs.keys())
print("episode:", env.current_episode.episode_id)
print("scene:", env.current_episode.scene_id)
print("start:", env.current_episode.start_position)
print("goal:", env.current_episode.goals[0].position)
print("pointgoal:", obs["pointgoal_with_gps_compass"])

env.close()
PY

```


运行ShortestPathFollower + 可视化

```shell
cd /home/gm_wadefrankslam/fengxian/project/habitat-lab

python - <<'PY'
import os
import habitat

from habitat.config.default_structured_configs import (
    TopDownMapMeasurementConfig,
    FogOfWarConfig,
    CollisionsMeasurementConfig,
)

from habitat.tasks.nav.shortest_path_follower import ShortestPathFollower

from habitat.utils.visualizations.utils import (
    observations_to_image,
    images_to_video,
    overlay_frame,
)

# 减少 Habitat-Sim 日志
os.environ["MAGNUM_LOG"] = "quiet"
os.environ["HABITAT_SIM_LOG"] = "quiet"

config = habitat.get_config(
    config_path="benchmark/nav/pointnav/pointnav_habitat_test.yaml"
)

# 添加 TopDownMap 和碰撞信息
with habitat.config.read_write(config):
    config.habitat.task.measurements.update(
        {
            "top_down_map": TopDownMapMeasurementConfig(
                map_padding=3,
                map_resolution=1024,
                draw_source=True,
                draw_border=True,
                draw_shortest_path=True,
                draw_view_points=True,
                draw_goal_positions=True,
                draw_goal_aabbs=True,
                fog_of_war=FogOfWarConfig(
                    draw=True,
                    visibility_dist=5.0,
                    fov=90,
                ),
            ),
            "collisions": CollisionsMeasurementConfig(),
        }
    )

env = habitat.Env(config=config)

obs = env.reset()

goal = env.current_episode.goals[0].position

follower = ShortestPathFollower(
    sim=env.sim,
    goal_radius=0.2,
    return_one_hot=False,
)

frames = []

# 初始帧
info = env.get_metrics()

frame = observations_to_image(obs, info)

# overlay_frame 不需要 top_down_map 本身
text_info = dict(info)
text_info.pop("top_down_map", None)

frame = overlay_frame(frame, text_info)
frames.append(frame)

step = 0

while not env.episode_over and step < 500:

    action = follower.get_next_action(goal)

    if action is None:
        break

    obs = env.step(action)

    info = env.get_metrics()

    frame = observations_to_image(obs, info)

    text_info = dict(info)
    text_info.pop("top_down_map", None)

    frame = overlay_frame(frame, text_info)

    frames.append(frame)

    step += 1

print("steps:", step)
print("metrics:", env.get_metrics())

output_dir = "./output"
os.makedirs(output_dir, exist_ok=True)

images_to_video(
    frames,
    output_dir,
    "pointnav_oracle",
    fps=6,
    quality=9,
)

print("video saved to:")
print(os.path.abspath("./output/pointnav_oracle.mp4"))

env.close()
PY

```