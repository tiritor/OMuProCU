# OMuProCU

## Disclaimer

> The proposed framework uses proprietary software and APIs to initialize hardware, etc. after updating the hardware. Since these are licensed, this was removed, and must be added again or done manually, to get the full functional version used in the paper!

## Structure

This repository contains the implementation from the complete framework and its evaluation for the proposed paper ```Low Impact Tenant Code Updates on Multi-tenant Programmable Switches```.

As interface to use the Tofino 1 chip, the proposed [Open-Tofino Code](https://github.com/barefootnetworks/Open-Tofino) is used. 

It consists of the following parts:

- [OMuProCU-core](https://github.com/tiritor/OMuProCU)
- [OMuProCU-utils](https://github.com/tiritor/OMuProCU-utils)
- [OMuProCU-experiments](https://github.com/tiritor/OMuProCU-experiments)
- [TIF-experiments](https://github.com/tiritor/TIF-Experiments)

## Additional information

### TDC Manifests

There are two example TDC manifests available in this repository:

- [TDC.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC.yaml)
- [TDC-2.yaml](https://github.com/tiritor/OMuProCU-experiments/blob/main/experiment-files/TDC-2.yaml)

Both are implementing two accelerated tenant example CNF for different tenants.
