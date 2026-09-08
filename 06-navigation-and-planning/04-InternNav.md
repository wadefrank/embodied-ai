
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
pip install numpy-quaternion
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

## 验证

为了验证 InternNav 的安装，先启动模型服务器

```shell
python scripts/eval/start_server.py --port 8087
```

正常会显示：

```shell
PROJECT_ROOT_PATH:/home/gm_wadefrankslam/fengxian/project/InternNav
Warning: (No module named 'habitat'), Habitat Evaluation is not loaded in this runtime. Ignore this if not using Habitat.
Starting Agent Server...
Warning: No config file provided, using port 8087
WARNING:  Current configuration will not reload as not all conditions are met, please refer to documentation.
INFO:     Started server process [45204]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8087 (Press CTRL+C to quit)
```

### 验证模型是否加载成功

安装依赖项

```shell
pip install huggingface-hub==0.30.2
python -m pip install setuptools==75.8.0

```

运行

```shell
python - <<'PY'
import torch
from transformers import AutoProcessor
from internnav.model.basemodel.internvla_n1.internvla_n1 import InternVLAN1ForCausalLM

model_path = "checkpoints/InternVLA-N1-DualVLN"

print("1. Loading processor...")
processor = AutoProcessor.from_pretrained(
    model_path,
    trust_remote_code=True,
)
print("Processor OK:", type(processor))

print("\n2. Loading InternVLA-N1 with CPU offload...")

model = InternVLAN1ForCausalLM.from_pretrained(
    model_path,
    torch_dtype=torch.bfloat16,
    attn_implementation="flash_attention_2",
    device_map="auto",
    max_memory={
        0: "14GiB",      # 给 16GB GPU 留一些余量
        "cpu": "48GiB",  # 如果机器内存更大，可以改成 64GiB
    },
    low_cpu_mem_usage=True,
    offload_folder="./offload_internvla",
    offload_state_dict=True,
)

model.eval()

print("\n3. Model loaded successfully!")
print("Model type:", type(model))

params = sum(p.numel() for p in model.parameters())
print(f"Parameters: {params / 1e9:.2f} B")

print("\nDevice map:")
print(model.hf_device_map)

print("\nCUDA memory:")
print(
    f"Allocated: {torch.cuda.memory_allocated(0) / 1024**3:.2f} GiB"
)
print(
    f"Reserved:  {torch.cuda.memory_reserved(0) / 1024**3:.2f} GiB"
)

print("\nInternVLA-N1 loading test PASSED.")
PY
```

### 验证推理

使用inference_only_demo.ipynb进行验证。

```shell
# 安装Jupyter Lab
pip install jupyterlab


# 启动
jupyter lab \
  --ip=0.0.0.0 \
  --port=8888 \
  --no-browser \
  --allow-root
  
# 打开出现的网址：http://127.0.0.1:8888/lab

```

# 参考资料

## 知乎

[从仿真到真机：导航模型部署全流程｜冠军队伍经验分享](https://zhuanlan.zhihu.com/p/1969046543286907790)

