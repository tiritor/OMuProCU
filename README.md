# OMuProCU


## Disclaimer

> The proposed framework uses proprietary software and APIs to initialize hardware, etc. after updating the hardware. Since these are licensed, this was removed, and must be added again or done manually, to get the full functional version used in the papers!

The structure of this framework was presented in the paper [```Improving the Deployment of Multi-Tenant Containerized Network Function Acceleration```](https://ieeexplore.ieee.org/document/9993962).

This repository contains 

- **the implementation of the complete framework** and its evaluation for the proposed paper [```Low Impact Tenant Code Updates on Multi-tenant Programmable Switches```](https://ieeexplore.ieee.org/abstract/document/10327866).
-  **a management plane** which is presented in [```Orchestrating Multi-Tenant Code Updates Across Multiple Programmable Switches```](https://ieeexplore.ieee.org/document/10575368)!
- **a resilent orchestration approach** including a rules updater in the proposed (and *newest*) paper ```Resilient Multi-Tenant Code Updates for Adaptive Network State Changes```

As interface to use the Tofino 1 chip, the proposed [Open-Tofino Code](https://github.com/barefootnetworks/Open-Tofino) is used. 

It consists of the following parts:

- [MD-OMuProCU](https://github.com/tiritor/MD-OMuProCU) (Updated)
- [OMuProCU-core](https://github.com/tiritor/OMuProCU) (Updated)
- [OMuProCU-utils](https://github.com/tiritor/OMuProCU-utils) (Updated)
- [OMuProCU-experiments](https://github.com/tiritor/OMuProCU-experiments) (Updated)
- [TIF-experiments](https://github.com/tiritor/TIF-Experiments)

## Additional information

### TDC Manifests

There are two example TDC manifests available in this repository:

- [TDC.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC.yaml)
- [TDC-2.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC-2.yaml)

Both are implementing two accelerated tenant example CNF for different tenants.

### MD-TDC Manifests

For orchestrating over multiple devices, the manifest is enhanced to support multiple device descriptions which can be seen in [MD-TDC-1.yaml](https://github.com/tiritor/MD-OMuProCU/blob/main/MD-TDC-1.yaml)

## Experiment Setup for Newest Paper

The newest paper ```Resilient Multi-Tenant Code Updates for Adaptive Network State Changes``` contains an evaluation setup which uses a tenant CNF which includes an offloaded ICMP network function (manifest can be found [here](https://github.com/tiritor/MD-OMuProCU/blob/main/MD-TDC-Ping.yaml)). 
The detailed structure is described in the paper. 
How to run the experiment setup is described in the [OMuProCU-experiments](https://github.com/tiritor/OMuProCU-experiments).

