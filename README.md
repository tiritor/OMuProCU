# OMuProCU


## Disclaimer

> The proposed framework uses proprietary software and APIs to initialize hardware, etc. after updating the hardware. Since these are licensed, this was removed, and must be added again or done manually, to get the full functional version used in the paper!

This repository contains the implementation about the complete framework and its evaluation for the proposed paper [```Low Impact Tenant Code Updates on Multi-tenant Programmable Switches```](https://ieeexplore.ieee.org/abstract/document/10327866).

Now, the updated version contains also **a management plane** which is presented in ```Orchestrating Multi-Tenant Code Updates Across Multiple Programmable Switches```!

As interface to use the Tofino 1 chip, the proposed [Open-Tofino Code](https://github.com/barefootnetworks/Open-Tofino) is used. 

It consists of the following parts:

- *[MD-OMuProCU](https://github.com/tiritor/MD-OMuProCU)* (New)
- [OMuProCU-core](https://github.com/tiritor/OMuProCU) (Updated)
- [OMuProCU-utils](https://github.com/tiritor/OMuProCU-utils) (Updated)
- [OMuProCU-experiments](https://github.com/tiritor/OMuProCU-experiments)
- [TIF-experiments](https://github.com/tiritor/TIF-Experiments)

## Additional information

### TDC Manifests

There are two example TDC manifests available in this repository:

- [TDC.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC.yaml)
- [TDC-2.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC-2.yaml)

Both are implementing two accelerated tenant example CNF for different tenants.

### MD-TDC Manifests

For orchestrating over multiple devices, the manifest is enhanced to support multiple device descriptions which can be seen in [MD-TDC.yaml](https://github.com/tiritor/MD-OMuProCU/blob/main/MD-TDC-1.yaml)
