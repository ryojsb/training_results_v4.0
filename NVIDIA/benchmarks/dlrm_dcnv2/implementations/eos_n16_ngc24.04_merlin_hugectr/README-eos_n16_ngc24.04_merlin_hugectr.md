## Steps to launch training

### eos_n16_ngc24.04_merlin_hugectr

Launch configuration and system-specific hyperparameters for the
eos_n16_ngc24.04_merlin_hugectr submission are in the
`benchmarks/dlrm_dcnv2/implementations/merlin_hugectr/config_DGXH100_16x8x1056.sh` script.

Steps required to launch training for eos_n16_ngc24.04_merlin_hugectr.  The sbatch
script assumes a cluster running Slurm with the Pyxis containerization plugin.

1. Build the docker container and push to a docker registry

```
docker build --pull -t <docker/registry:benchmark-tag> .
docker push <docker/registry:benchmark-tag>
```

2. Launch the training
```
source config_DGXH100_16x8x1056.sh
CONT=<docker/registry:benchmark-tag> DATADIR=<path/to/data/dir> LOGDIR=<path/to/output/dir> sbatch -N ${DGXNNODES} -t ${WALLTIME} run.sub
```