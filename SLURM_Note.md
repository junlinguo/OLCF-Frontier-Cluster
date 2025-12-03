
## DeepAndes + SLURM 

Python script: dinov2.run.submit 

Some parameters can be parsed:

See 
```python
def get_args_parser(
    description: Optional[str] = None,
    parents: Optional[List[argparse.ArgumentParser]] = None,
    add_help: bool = True,
) -> argparse.ArgumentParser:
    parents = parents or []
    slurm_partition = get_slurm_partition()
    parser = argparse.ArgumentParser(
        description=description,
        parents=parents,
        add_help=add_help,
    )
    parser.add_argument(
        "--ngpus",
        "--gpus",
        "--gpus-per-node",
        default=8,  # default is 8
        type=int,
        help="Number of GPUs to request on each node",
    )
    parser.add_argument(
        "--nodes",
        "--nnodes",
        default=1,
        type=int,
        help="Number of nodes to request",
    )
```


```python
    executor_params = get_slurm_executor_parameters(
        nodes=args.nodes,
        num_gpus_per_node=args.ngpus,
        timeout_min=args.timeout,  # max is 60 * 72
        slurm_signal_delay_s=120,
        slurm_partition=args.partition,
        **kwargs,
    )

    # add more parameters (or explicitly add in the submit.py)
    executor_params["gpus_per_node"] = 8
    executor_params["cpus_per_task"] = 1 #16 (max cores in one gpu)
    #executor_params["slurm_qos"] = "debug"
    executor_params["slurm_account"] = "csc662"
    executor_params["slurm_additional_parameters"] = {
        "mail-user": "email_address_here",
        "mail-type": "ALL",
        # "gpu-bind=":"closest",
    }

```
