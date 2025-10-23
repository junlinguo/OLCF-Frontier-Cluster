Create a conda env and install pytorch on frontier hpc (Notes) 

> Install/Reproduce dinov2 ssl / deepAndes env

## load environment module 
```
module load PrgEnv-gnu/8.6.0
module load miniforge3/23.11.0-0 
module load rocm/6.3.1
module load craype-accel-amd-gfx90a
```
for every session, only load miniforge3 once

## create conda env (could be other virtual env too)
```
conda create -p /lustre/orion/<<your_project_id>>/proj-shared/<<your_user_id>>/.conda/frontier/dino_env python=3.12 -c conda-forge

source activate /lustre/orion/<<your_project_id>>/proj-shared/<<your_user_id>>/.conda/frontier/dino_env

# deactivate
source deactivate /lustre/orion/<<your_project_id>>/proj-shared/<<your_user_id>>/.conda/frontier/dino_env
```

## install pytorch (ROCM) 
```
pip install torch==2.7.0 torchvision==0.22.0 torchaudio==2.7.0 --index-url https://download.pytorch.org/whl/rocm6.3
```
test installation 
```
import torch
print(torch.cuda.is_available())
print(torch.__version__)
```

## Jupyter visible to conda

https://docs.olcf.ornl.gov/software/python/jupyter_envs.html
```
pip install ipykernel
ipython kernel install --user --name=jupyter_env_frontier
```

## install dinov2 paper / deepandes paper related packages 
[dinov2_install_readme](https://github.com/geopacha/DeepAndes/blob/main/dinov2_ssl_8bands/README(from%20dinov2%20original%20repo).md)

[deepandes install readme](https://github.com/geopacha/DeepAndes/tree/main/dinov2_ssl_8bands/README.md)
