# Learning Target Environment Model (TarEnvModel)

## Overview

The **Target Environment Model (TarEnvModel, `*.tarEnv`)** describes the physical setup for a deployment, including devices, their configurations, and connections. This model is essential for defining the environment where the software will run.


When you create a new deployment project by following [Create an empty project](../README.md#create-an-empty-deployment-project), a template of `*.tarEnv` file is automatically included.

---

## Example: Target Environment Model Template

### Default Template: `deploy_my_first_application_env.tarEnv`
When you create a project named as "deploy_my_first_application", the `deploy_my_first_application_env.tarEnv` file has the following content:

```yaml
TargetDeployEnviroment:
  name: deploy_my_first_application_env # name of this target environment"
  includeDevice:
    computationDevice:
      - name: "TODO: name of this device"
        refDeviceType: PC # note: it references to a computation device type from the device catalog, you can change it if you create your owns
        configDeviceProperty:
          - name: "os_name"
            from: "PC.operting_system.os_name"
            value: ubuntu # note: only support ubuntu so far
          - name: "os_version"
            from: "PC.operting_system.os_version"
            value: focal # ubuntu version
          - name: "processor_architecture"
            from: "PC.processor.processor_architecture"
            value: x86

```

Key Elements
- TargetEnvironment:
  - `name`: Unique identifier for the environment (e.g "deploy_my_first_application_env").
  - `includeDevices`:
    Each device defined here is reference to a Device Type defined in `*.dev` model files. This allows you to reuse device definitions (properties and connections) across different target environments. In the .tarEnv file, you can then override or assign specific values for each property declared in the referenced `.dev` file.

    It must include a computation device.

    - `computationDevice`:
        Refers to any PC or server used to run the software. The reference model is defined in a "*.dev". Each device can have configured properties such as OS name or processor architecture.
        It references to "[pc.dev](https://github.com/ipa-rwu/DeploymentDeviceCatalog/blob/main/de.fraunhofer.ipa.deployment.catalog.devices/pc.dev)" by default.
    - `device` (optional):
        Represent hardware (robots, grippers, cameras) with assigned types and optional properties like device_type or serial_number.

  - `configConnection`(optional):
    Specify how devices interact over various interfaces (Ethernet, USB). Only devices with matching communication types can be connected. Property values, such as IP addresses or device volumes, are then assigned here.

The example with optional items as follows:

```yaml
TargetDeployEnviroment:
  name: deploy_my_first_application_env # name of this target environment"
  includeDevice:
    computationDevice:
      - name: my_laptop
        refDeviceType: PC # note: it references to a computation device type from the device catalog, you can change it if you create your owns
        configDeviceProperty:
          - name: "os_name"
            from: "PC.operting_system.os_name"
            value: ubuntu # note: only support ubuntu so far
          - name: "os_version"
            from: "PC.operting_system.os_version"
            value: focal # ubuntu version
          - name: "processor_architecture"
            from: "PC.processor.processor_architecture"
            value: x86
    device:
      - name: my_robot
        refDeviceType:UR5E
        configDeviceProperty:
          - name: type
            from: "UR5E.device_info.type"
            value: ur5e
  configConnection:
    - name: connect_ur5e_pc
      connectDevice:
        - refDevice: my_robot
          refConnection: "UR5E.ethernet"
          configuration:
            - name: ip_address
              refConnectionProperty: "UR5E.ethernet.ip_address"
              value: "192.168.0.1"
        - refDevice: my_laptop
          refConnection: "PC.ethernet"
          configuration:
            - name: ip_address
              refConnectionProperty: "PC.ethernet.ip_address"
              value: "192.168.0.2"

```
