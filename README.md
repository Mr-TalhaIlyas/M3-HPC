# M3-HPC
### STRUDLE
[S T R U D L E](https://beta.desktop.cvl.org.au/login)
[VS Code](https://docs.massive.org.au/M3/connecting/strudel2/connecting-to-vscode.html)

### Activate your Conda Env
[Link](https://docs.massive.org.au/M3/software/pythonandconda/python-anaconda.html)
```
module load git/2.25.2 # if you get git version warning
module load anaconda/2020.07-Python3.8-gcc8 
export PROJECT=hl62
export CONDA_ENVS=/scratch/$PROJECT/$USER/conda_envs
source activate $CONDA_ENVS/<your env name you created>


### MiniConda
source /scratch/hl62/tilyas/miniconda/bin/activate 

```

### Sample Job Script

```
#!/bin/bash
#SBATCH --job-name=mrcnn
#SBATCH --account=hl62
#SBATCH --time=96:00:00
#SBATCH --ntasks=24
#SBATCH --mem-per-cpu=4096
#SBATCH --cpus-per-task=1
#SBATCH --partition=m3u020 
#SBATCH --gres=gpu:1
module load anaconda/2020.07-Python3.8-gcc8 
export PROJECT=hl62
export CONDA_ENVS=/scratch/$PROJECT/$USER/conda_envs
source activate $CONDA_ENVS/pyt
python my_train.py
```

#### Sample Test Script

```python
#%%
import importlib.util
import sys

# Function to check for library installation and version
def check_installation(lib_name):
    lib_spec = importlib.util.find_spec(lib_name)
    if lib_spec is not None:
        lib = importlib.import_module(lib_name)
        print(f"{lib_name} is installed. Version: {lib.__version__}")
    else:
        print(f"{lib_name} is NOT installed.")

# Function to check for GPU support and details in PyTorch
def check_torch_cuda():
    torch = importlib.import_module('torch')
    if torch.cuda.is_available():
        print("PyTorch can use CUDA.")
        print(f"CUDA Version: {torch.version.cuda}")
        for i in range(torch.cuda.device_count()):
            print(f"Device {i}: {torch.cuda.get_device_name(i)}")
            print(f"Memory Allocated: {torch.cuda.memory_allocated(i) / 1e9} GB")
            print(f"Memory Cached: {torch.cuda.memory_reserved(i) / 1e9} GB")
    else:
        print("PyTorch cannot use CUDA.")

# Check for matplotlib, cv2 (opencv-python), numpy and torch
check_installation("matplotlib")
check_installation("cv2")
check_installation("numpy")
check_installation("torch")

# Additional check for PyTorch CUDA capabilities
check_torch_cuda()
```


## CMD

```
# infor
user_info
# see resources
show_cluster
# cancel a job
scancel <job id>
```
