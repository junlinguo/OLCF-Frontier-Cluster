# OLCF User Notes

This is a Note when going through the OLCF setup/tutorial. Keep updating.

NewUserGuide

- github: https://github.com/olcf/NewUserQuickStart/tree/master/Frontier 
- [zoom recording](https://www.zoomgov.com/rec/component-page?eagerLoadZvaPages=&accessLevel=meeting&action=viewdetailpage&sharelevel=meeting&useWhichPasswd=meeting&requestFrom=pwdCheck&clusterId=gov&componentName=need-password&meetingId=jnkfY3OaITzmdr4Ws9KY6-l_fcvssWagBEQ_D2Dyp1tD6Q6Z39PBrJxIH3vKq1lK.Lt84mgYtFbY_PQVd&originRequestUrl=https%3A%2F%2Fwww.zoomgov.com%2Frec%2Fshare%2F8xRSwRuynSWDSBN8WVqD5IEZbpeJ8QotG02lDgr9hGRIiapIhQKl1IDYGp1xTB8O.L9K55aZaLLDzZh7U%3FstartTime%3D1755794711000) (password:5m44jA%B)



## Contact

QA/Help:

- **emails/QA: <u>help@olcf.ornl.gov</u>**
- **submit [ticket Link](https://www.olcf.ornl.gov/for-users/getting-started/submit-ticket/)**



## System Guide

[Oak ridge national laboratory](https://docs.olcf.ornl.gov/systems/index.html)

>  [Frontier system guide](https://docs.olcf.ornl.gov/systems/frontier_user_guide.html#system-overview)

> [Data Transfer Nodes (DTNs) guide](https://docs.olcf.ornl.gov/systems/dtn_user_guide.html)

There are guides for other systems as well 



##  SSH access (token required)

- userid/username
- projid
- PIN code 

- Passcode: **PIN** then enter **token code**; Wait for it to change and then do the thing above again 

### First Time Access/Activation

```bash
ssh <username>@home.ccs.ornl.gov
```

Then set the PIN code and activate the account. 

### Login to Frontier

login to frontier by executing the following command (replace username with actual username/userid). By default, login to one randomly assigned Login Node

```bash
ssh <username>@frontier.olcf.ornl.gov
```



## Data Transfer Nodes (DTNs)

### Interactive access inside OLCF

Usually inside OLCF. 

DTN access is automatically granted to all enabled OLCF users. For interactive access to DTNs (`ssh`/`scp`/`sftp`), connect to `dtn.ccs.ornl.gov` (for the moderate enclave) or `opendtn.ccs.ornl.gov` (for the open enclave). For example:

```
ssh username@dtn.ccs.ornl.gov
```



Example usage of `scp` image.TIF from kronos dtn to orion member work

```
cd /nl/kronos/olcf/[projid]/users/[userid]
scp image.TIF <userid>@frontier.olcf.ornl.gov:/lustre/orion/[projid]/scratch/[userid]
```



### Access From Globus Online 

DTNs are also accessible via the “OLCF DTN” (for moderate) and “NCCS Open DTN” (for open) Globus endpoints. For more information on using Globus at OLCF see [Globus](https://docs.olcf.ornl.gov/data/index.html#data-transferring-data-globus).

Example of How I transfer data from VU Lab institution to DTN Kronos. 

(1) Open the Globus Personal Connect App folder locally (e.g., globusconnectpersonal-3.2.7)

```bash
cd /path/to/globusconnectpersonal-3.2.7
./globusconnectpersonal
```

Click connect 

(2) Open browser, go to Globus and login (https://www.globus.org/globus-connect-personal)

(3) Select files, Choose local and remote destination path. Hit 'Start' 

![image-20250911113032700](/Users/ezralinn/Library/Application Support/typora-user-images/image-20250911113032700.png)

More Details/Methods from [Data Transfer Nodes (DTNs) guide](https://docs.olcf.ornl.gov/systems/dtn_user_guide.html)



### Summary of  Storage Areas

https://docs.olcf.ornl.gov/data/index.html#summary-of-storage-areas (More Details)

- **Kronos**
  - Kronos system mounted at: [dtn.ccs.ornl.gov](http://dtn.ccs.ornl.gov) 
  - Kronos access via Globus at “OLCF Kronos”

- **Orion (lustre)** (purged)

  `ssh <userid>@frontier.olcf.ornl.gov`

  `cd /lustre/orion/[projid]/scratch/[userid]/`

  - Scratch: user own access 
  - Proj-shared: store and share between other project members 
  - World-shared: store data that anyone can access (across projects) 



**Access through environment variables** (recommended)

On Frontier additional paths to the various project-centric work areas are available via the following symbolic links and/or environment variables:

- Member Work Orion Directory: `/lustre/orion/scratch/[userid]/[projid]` or `$MEMBERWORK/[projid]`
- Project Work Orion Directory: `/lustre/orion/proj-shared/[projid]` or `$PROJWORK/[projid]`
- World Work Orion Directory: `/lustre/orion/world-shared/[projid]` or `$WORLDWORK/[projid]`


Login to Frontier and go to your individual user storage called “scratch”:

Frontier (Orion) :

```
cd /lustre/orion/[projid]/scratch/[userid]
ls
```



You can also do:

```
cd $MEMBERWORK/[projid]
ls
```



Now let’s look at the project level storage, proj-shared:

```
cd /lustre/orion/[projid]/proj-shared/
ls
```



You can also do:

```
cd $PROJWORK/[projid]/
ls
```



And for sharing between projects:

```
cd /lustre/orion/[projid]/world-shared/
ls
```



You can also do:

```
cd $WORLDWORK/[projid]
ls
```





## Python On OLCF Systems

**Check 'Python at OLCF (Tony)' in NewUserQuick Start Readme first** 

need to check that: do not load miniforge twice !!! 

![image-20250911120200888](/Users/ezralinn/Library/Application Support/typora-user-images/image-20250911120200888.png)

[Guide](https://docs.olcf.ornl.gov/software/python/index.html#python-on-olcf-systems)

[PyTorch on Frontier](https://docs.olcf.ornl.gov/software/analytics/pytorch_frontier.html): 
    - Access PyTorch on Frontier
    - Envrionment moved to NVMe (node mem, fastest) 

### Conda 

#### How to use conda in OLCF 

https://docs.olcf.ornl.gov/software/python/conda_basics.html



#### **Best Practices for Custom Conda Environments**

Both Frontier and Andes mount the home and project areas, an environment built for one machine cannot be assumed to work seamlessly on the other, so it is important to have an organization structure for your python environments from the start.

Best Practices:

- **Store in Project Areas:** Place your custom conda environments in your <u>user project areas on NFS</u>. This prevents them from being purged and makes them shareable with your project team.
- **Identify by Machine:** Include the machine name in the environment name or store environments in a directory named for that machine.
- **Keep It Organized:** Save your conda environments in a `.conda` folder to clearly identify them and avoid cluttering your directory listings.
- **Use Source Activate:** ALWAYS use `Source Activate` even when Python prompts you to use `conda activate`. NEVER user `conda activate` on OLCF machines. `conda activate` can put options in your configuration files, which are shared between all the machines, but those options will not work universally on all the machines you use.

```	$ source activate /ccs/proj/<<your_project_id>>/<<your_user_id>>/.conda/frontier/mpi4py_env
$ source activate /ccs/proj/<<your_project_id>>/<<your_user_id>>/.conda/frontier/mpi4py_env
```

#### Load environmental variables  (e.g., first_torch) (before activate conda env) 
```
module load PrgEnv-gnu/8.6.0
module load miniforge3/23.11.0-0 (only load once) 
module load rocm/6.3.1
module load craype-accel-amd-gfx90a

```

#### Jupyter visible to conda 
```
https://docs.olcf.ornl.gov/software/python/jupyter_envs.html
```

## Container (Apptainer) 

A pytorch on container example here: https://github.com/olcf/olcf_containers_examples/tree/main/frontier/sample_apps/pytorch

## Slurm workload manager (schedmd)

Frontier uses SchedMD’s Slurm Workload Manager as the batch scheduling system.

submitting job example (<ins> 56' at the video guide zoom recording </ins>)

Documentation: https://docs.olcf.ornl.gov/systems/frontier_user_guide.html#running-jobs


## Allocate a compute node (interactive) 
```
salloc -A ProjID -t time_assign -p batch -N 1

```
e.g., assign 1 compute node to proj CSC662 (60 mins request), default partition queque is `batch`
```
salloc -A CSC662 -t 60 -N 1
```

## Submit sbatch script 

check the new user guide. 

In the batch script, include `unset SLURM_EXPORT_ENV`

When submit job from a fresh shell: Use --export=NONE
```
sbatch --export=NONE xxx.sbatch
```


## notes (for myself) 

dinov2 paper uses 4 A100-80GB Nodes with 32 GPUs. An example implementation for reference. (https://github.com/facebookresearch/dinov2/blob/main/dinov2/utils/cluster.py#L74) Some settings considered.  
```
- partition 
- request all the memory on each node, use --mem=0
- gpus_per_node: num_gpus_per_node,
- tasks_per_node: num_gpus_per_node,  # one task per GPU
- numbeer of cpus per task: 10 (in paper). experiment with frontier. 

```
check the `srun` commands in [document link](https://docs.olcf.ornl.gov/systems/frontier_user_guide.html#)

**auto generate sbatch script**

https://my.olcf.ornl.gov/script-generator


## other references 

why use a cluster ? [reference](https://epcced.github.io/hpc-intro/aio.html)
Slurm (from training arxiv: [link](https://vimeo.com/828638016?turnstile=0.iVjfNejc-IMwigFqG-tcRjBQtu3zeuqQpIp3qvzaUNAymV53bjHfK7eqxJxySuNHCkaBeEsX0ywLlkc8CFrOXmkIpfyC_gGqWh2ypCZBVmPyUEw-CJdVZXkNY6NQY__S77Vg9YUnQQfQ4uP2NbpuvjZafDkiAiF-6S3DjwUJ3fxVwnJT822JJiN5xCPnxowIHZfWaLlkSReQ37HcLZ1YAnF2c1iQZjMbJWEd5gLjazmvg6Fo-Vp6SYK1erarKyAfnyW193QFP8KPbEoBX9h0Dqgxbvdd0x5h5b2sLLoV1JIg_YCt4tu3Ot1eDI8RxGSuYMT41p-WdGgQ9lFsUbkBaD-ageF81WoZxovvfWRFHTTZ7SdhiY9Fjlkn0CaorqUe8uBVb3S8NWmBygV4BkUoiOdmh_IQ5Vwz2Q1H8RGu8EYs7G65CXJNRx0FSA_Kss24LFVQNfAvkJBDzxxmxbvFe0-M8lHTT8tD-7ddTqlpQ7JnsatWZwxXB7r49Tp0m3KDhEybCDwNFuIX2U4Q8GIOUr8qEcJmoQXgVNvm48NHMNq6hMd4VWxUrDRKPRn8Zhs1G8tAiFC92TyHeIcBVCDSXUu3Rv2z3qiUl8qNsvJJ5BpwefAIiwSHZQJhhz-P2XMcitXQgfCq9SADkH7nWnGYZ__DT3qU0yr4GcAMLoDsLyQ-2Var-ln-noanv_Jt9Q3TBNIoMvhzX86BJAn_AFRjMn1RkMRvc4Q_UJR2dh1WXSmKqXc3vo3_MWFDtIbErX6ZMh9Tlza8VlDwgqgjhTooFZg0U8M1B2BedRCqA78PFL2oONFGJ8WduWSIn9Mr9OEFetUavp-aBnYYDD8eJzTDWG6dS7OaQjx_9mZ2ptgan8aguoHsumksJsAKNH-u3ZEWsU-4lptg_QAPuec_pWLte5lYVTtmczNsEyCY6HxXIjwJWS_BCocL4GeHWVTHekhQ.9GXLSvqOeyawdE7prfgALQ.b0982fb308f65af22399f3192fbeecf0e2c6d66270315487410e0b4955886a12), [slides](https://www.olcf.ornl.gov/wp-content/uploads/2023_05_18_slurm_on_frontier.pdf))


Check the Slurm account (account# is projID)
```
sacctmgr show assoc user=$USER
```




