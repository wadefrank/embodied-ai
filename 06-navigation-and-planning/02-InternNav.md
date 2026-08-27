
# 环境配置
## 安装

参考：[安装文档](https://internrobotics.github.io/user_guide/internnav/quick_start/installation.html)

```shell
# Clone the InternNav repository
git clone https://github.com/InternRobotics/InternNav.git --recursive
cd InternNav

# create a new isolated environment for model server
conda create -n internnav python=3.10 libxcb=1.14
conda activate internnav

pip install pyyaml typeguard

# install PyTorch (CUDA 11.8)
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --index-url https://download.pytorch.org/whl/cu118

# 如果上面的方式下载速度很慢，可以先先用 wget 把 wheel 下载下来，再让 pip 本地安装。
mkdir -p /home/gm_wadefrankslam/fengxian/wheel
cd /home/gm_wadefrankslam/fengxian/wheel

# torch 2.5.1 + CUDA 11.8
wget -c https://download.pytorch.org/whl/cu118/torch-2.5.1%2Bcu118-cp310-cp310-linux_x86_64.whl

# torchvision 0.20.1 + CUDA 11.8
wget -c https://download.pytorch.org/whl/cu118/torchvision-0.20.1%2Bcu118-cp310-cp310-linux_x86_64.whl

# torchaudio 2.5.1 + CUDA 11.8
wget -c https://download.pytorch.org/whl/cu118/torchaudio-2.5.1%2Bcu118-cp310-cp310-linux_x86_64.whl

# cuBLAS
wget -c https://download.pytorch.org/whl/cu118/nvidia_cublas_cu11-11.11.3.6-py3-none-manylinux1_x86_64.whl

pip install \
  ./nvidia_cublas_cu11-11.11.3.6-py3-none-manylinux1_x86_64.whl \
  ./torch-2.5.1+cu118-cp310-cp310-linux_x86_64.whl \
  ./torchvision-0.20.1+cu118-cp310-cp310-linux_x86_64.whl \
  ./torchaudio-2.5.1+cu118-cp310-cp310-linux_x86_64.whl



# 下载 NVIDIA 官方的 CUDA 11.8 本地 APT 仓库安装包
cd /home/gm_wadefrankslam/fengxian/wheel
wget -c https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-11-8-local/cuda-D95DBBE2-keyring.gpg \
  /usr/share/keyrings/
sudo apt-get update \
  -o Dir::Etc::sourcelist="/etc/apt/sources.list.d/cuda-ubuntu2204-11-8-local.list" \
  -o Dir::Etc::sourceparts="-" \
  -o APT::Get::List-Cleanup="0"
sudo apt install -y cuda-toolkit-11-8
  
# install InternNav with model dependencies
pip install setuptools_scm
pip install psutil==5.9.8
pip install -e .[model] --no-build-isolation
```

问题
```shell

ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.  
vcs-versioning 2.3.1 requires packaging>=26.2, but you have packaging 24.2 which is incompatible.

# 解决
pip uninstall -y setuptools-scm vcs-versioning
pip check

```

## 下载权重

参考：[下载权重链接](https://internrobotics.github.io/user_guide/internnav/quick_start/installation.html#download-checkpoints)

下载 [InternVLA-N1 pretrained Checkpoints](https://huggingface.co/InternRobotics/InternVLA-N1-DualVLN)

```shell
conda activate internnav
cd /home/gm_wadefrankslam/fengxian/project/InternNav
pip install -U huggingface_hub
export HF_ENDPOINT=https://hf-mirror.com
hf download InternRobotics/InternVLA-N1-DualVLN \
    --local-dir checkpoints/InternVLA-N1-DualVLN
```

下载 [DepthAnything v2 Checkpoints](https://huggingface.co/depth-anything/Depth-Anything-V2-Metric-Hypersim-Small/resolve/main/depth_anything_v2_metric_hypersim_vits.pth)

