Install Pytorch Env Notes
# Install/Reproduce dinov2 ssl / deepAndes env

## load environment module 
```
module load PrgEnv-gnu/8.6.0
module load miniforge3/23.11.0-0 (only load once) 
module load rocm/6.3.1
module load craype-accel-amd-gfx90a
```

## create conda env (could be other virtual env too)
```
conda create -p /lustre/orion/<<your_project_id>>/proj-shared/<<your_user_id>>/.conda/frontier/dino_env python=3.12 -c conda-forge

source activate /lustre/orion/<<your_project_id>>/proj-shared/<<your_user_id>>/.conda/frontier/dino_env
```

## install pytorch (ROCM) 
```
pip install torch==2.7.0 torchvision==0.22.0 torchaudio==2.7.0 --index-url https://download.pytorch.org/whl/rocm6.3
```
