# 简介

官网：[https://mujoco.org/](https://mujoco.org/)

GitHub：[https://github.com/google-deepmind/mujoco](https://github.com/google-deepmind/mujoco)

基于mujoco的开源框架：

[mujoco_playground](https://github.com/google-deepmind/mujoco_playground)

[loco-mujoco](https://github.com/robfiras/loco-mujoco)

# 安装

## 从源码编译安装

参考文档：[https://mujoco.readthedocs.io/en/latest/programming/#building-from-source](https://mujoco.readthedocs.io/en/latest/programming/#building-from-source)

推荐环境：
- Ubuntu 22.04 LTS
- Python 3.10
- MuJoCo 3.2.7
- ROS 2 Humble
- CUDA 12.x

编译：

```shell
# 兼容性最好
git clone -b 3.2.7 https://github.com/google-deepmind/mujoco.git
cd mujoco/
mkdir build
cd build && cmake ..
cmake --build . -j20

cmake -DCMAKE_INSTALL_PREFIX=/opt/mujoco .
sudo cmake --install .

# 测试
cd bin/
./simulate ../model/humanoid.xml 

```

## Python安装

```
pip install mujoco==3.2.7
```