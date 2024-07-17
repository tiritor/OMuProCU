# OMuProCU Core

This repository contains the core framework of the paper [`Low Impact Tenant Code Updates on Multi-tenant Programmable Switches`](https://ieeexplore.ieee.org/abstract/document/10327866) where the first version was presented.
Meanwhile, extended versions of the core framework are added used in the paper [`Orchestrating Multi-Tenant Code Updates Across Multiple Programmable Switches`](https://ieeexplore.ieee.org/document/10575368) and `Resilient Multi-Tenant Code Updates for Adaptive Network State Changes`.

As interface to use the Tofino 1 chip, the proposed [Open-Tofino Code](https://github.com/barefootnetworks/Open-Tofino) is used. 

## Disclaimer

> The framework proposed in the used proprietary software and APIs to initialize hardware, etc. after updating the hardware. Since these are licensed, this was removed, and must be added again or done manually, to get the full functional version used in the paper!


## Requirements

- Python 3.8
- Pip 3.21.1
- Kubernetes Distribution (e.g. K3s)
- Accelerator Hardware (Tofino 1 chip or BMv2)

## Installation

As first step, we recommend to create virtual environment:

```
python3 -m venv .venv
source .venv.bin
```

Then, you need to install the python packages needed in this repository:

```
pip3 install -r requirements.txt
```

Also, you need to build and install [**OMuProCU-utils**](https://github.com/tiritor/OMuProCU-utils) pip packages. 

```
cd ../OMuProCU_utils
pip3 install -r requirements.txt
python3 setup.py sdist
pip3 install ../OMuProCU_utils
```

## Usage

**ATTENTION: The programmable switch must be started and ready for reconfiguration! This is not part of OMuProCU!**

The [orchstrator.py](orchestrator.py) contains the mangement process which starts also all other components in the right order. 
So running ```python3 orchestrator.py``` will start the orchestrator with default parameters.

### Available Options

| Parameter         | Options      |  Description |
|-----------|------------|-------------|
| --no_cleanup | ---      |    Disable the cleanup procedure if orchestrator is shutdown  |
| --experiment-protocol      | ["TCP", "UDP" ]  | Which protocol is used for the timemeasurement differentiation in the experiment (only for data collection) [Default: TCP]  |
| --dev-init-mode      | ["0", "1" ]  | Which dev-init-mode should be set to supported accelerators [Default: 0 (fast-reconfig)]  |

## Structure

The OMuProCU core consists of different microservices:

- [Management](#management)
- [Reconfiguration Scheduler](#reconfiguration-scheduler)
- [NOS Updater](#nos-updater-structure-nos-updater)
- [In-Network Updater](#in-network-updater)
- [TIF Updater](#tif-updater)

Also, there are some modules which are used from the [OMuProCU-utils](https://github.com/tiritor/OMuProCU-utils) package like:

- Validator
- Persistor
- Tenant Communication Controller
- Protobuf Message Descriptions and its GRPC interfaces

### Management

The core of the OMuProCU is the Management Process which is covered in the [orchestrator.py](orchestrator.py). 
It contains the submission process for TDCs and health check pipeline control.

### Reconfiguration Scheduler

The reconfiguration scheduler executes the deployment pipeline proposed in the paper.
The implementation is covered in [reconfig_scheduler.py](reconfig_schedule,r.py)

### NOS Updater

This component manages the Container deployment of the accelerated CNF.
Its implementation is covered in [nos_updater.py](updater/nos_updater.py).
The API implementation is done only for the Kubernetes API.

### In-Network Updater

General abstraction for OTF code placement and accelerator code generation from TIF template and its compilation.
Its implementation is covered in [in_network_updater.py](updater/in_network_updater.py).

### TIF Updater

Abstraction component for applying the generated TIF and pulling the applied TIF to supported accelerated hardware or chips. 
In this implementation, BMv2 and Tofino 1 chip apply is available.
Its implementation can be found in [tif_updater.py](updater/tif_updater.py)

#### Tofino 1

As described before, the [Open-Tofino](https://github.com/barefootnetworks/Open-Tofino) API is used for the configuration of the Tofino 1 chip.
Due to license of some used APIs (e.g., proprietary SAL for Hardware initialization), these code parts are removed.

#### BMv2

If you want to use BMv2, this must be built with GRPC support.

### Rules Updater

As new component of the paper `Resilient Multi-Tenant Code Updates for Adaptive Network State Changes`, a rules updater is introduced which can add/update/delete rules for provider tables as well as tenant tables.

The communication is done via GRPC. The [MOC Shell](https://github.com/tiritor/MD-OMuProCU) in the [MD-OMuProCU](https://github.com/tiritor/MD-OMuProCU) repository can be used to use it. 


## Configuration 

### [tenant_security_config.json](conf/tenant_security_config.json)

In this file, the configuration for tenants is saved which consist of:

- Tenant ID as key (number)
- Name of the tenant
- VNIs which the tenant can use for its accelerated CNFs. 
- Names of deployed TDCs 
- Names of the main ingresses defined in the submitted TDCs **(ATTENTION: This will be automatically configured!)**

### [grpc_settings.py](conf/grpc_settings.py)

This contains the configuration of addresses and ports for GRPC server of the OMuProCU components.

### [in_updater_settings.py](conf/in_updater_settings.py)

The configuration [In-Network Updater](#in-network-updater) component can be done here. 
Mainly, new accelerators can be added or existing ones changed.
If a new accelerator is added, the name (more precisely the key in the dict) must be added to the [extern_blacklist.json](#extern_blacklistjson)!

### [time_measurement_settings.py](conf/time_measurement_settings.py)

Here is possible to configure the time measurement used for evaluating and experimenting in the paper.

### [extern_blacklist.json](conf/extern_blacklist.json)

If any extern should not be used by a tenant, this can be added into the list of the associated accelerator. 