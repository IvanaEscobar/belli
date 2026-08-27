[![DOI](https://zenodo.org/badge/710899553.svg)](https://doi.org/10.5281/zenodo.21298576)

# Bump to MITgcm 69m...

# belli: Underwater acoustics for MITgcm

`belli` is a physics package in [MITgcm](https://mitgcm.readthedocs.io/en/latest/getting_started/getting_started.html), allowing for simulations to investigate underwater acoustics. This code, based on Modern Fortran, is a ray-trace simulation of sound propagation. Lightweight cost function routines are based on [`pkg/obsfit`](https://github.com/MITgcm/MITgcm/tree/master/pkg/obsfit) written by Ariane Verdy Ph.D. 

The package interacts with the MITgcm kernel during initialisation, time-stepping, and in post-processing.

Development is up to date with [MITgcm `checkpoint69f`](https://github.com/MITgcm/MITgcm/commit/214bfe91bf8caee3cf215213baad672483c85b49)

Download just checkpoint69f of MITgcm using a shallow fetch of the repository:
```
git clone --filter=blob:none --no-checkout https://github.com/MITgcm/MITgcm.git
cd MITgcm
git fetch --depth 1 origin 214bfe91bf8caee3cf215213baad672483c85b49
git checkout 214bfe91bf8caee3cf215213baad672483c85b49
```

## How-to use
MITgcm code modifications are saved in [belli/mitgcm_code](mitgcm_code):
- adds `useBELLI` to `PARAMS.h`
- inserts `pkg/BELLI` in `forward_step.F`
- allows for `SVEL` and `SLD` as GCM diagnostics using `pkg/diagnostics` with optional `pkg/mnc`
- opens `pkg/BELLI` for inclusion in **TAF** TL and AD models, can be used with and without `pkg/ecco`

`belli` is dependent on the following packages:
- `cal` for storing times of sound transmissions
- `cost` for aggregation of acoustic cost function contributions

## Tips

### Create belli domain
For input, you will be asked to generate range points along a 2D plane between 
a source and receiver. The number of range points can vary from 2 to N, and is saved in `b_ranges`. The position of a receiver _must_ be contained within the ranges specified, see image below for context. At ray fan initialisation, the tracing step size is 10% the maximum ocean depth defined in your `.bty` file.

![belli domain](doc/z_readme/ihop_domain_setting.png)

## TO-DO
- [ ] DOC: create minimal documentation to help user get started with MITgcm+belli
- [ ] PYTHON: add input file generation
- [ ] FORTRAN: add working verification problem
- [ ] PYTHON: add synthetic observation data file generation
- [ ] PYTHON: create introductory analysis document

## Citing
```
@software{belli,
    author={Ivana Escobar},
    title = {{belli}: Underwater Acoustics for MITgcm},
    version = {0.8},
    year = {2026},
    url = {https://github.com/IvanaEscobar/belli/tree/v0.8}
    doi = {10.5281/zenodo.21298577}
}
```
