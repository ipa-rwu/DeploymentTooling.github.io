# Learning Target Environment Model (TarEnvModel)

## Overview

The **Target Environment Model (TarEnvModel, `*.tarEnv`)** describes the physical setup for a deployment, including devices, their configurations, and connections. This model is essential for defining the environment where the software will run.

When you create a new deployment project by following the steps in [Create an empty project](../README.md#create-an-empty-deployment-project), a template `*.tarEnv` file is automatically included.

---

## Example: Target Environment Model Template

### Default Template: `deploy_my_first_application_env.tarEnv`

When you create a project named `deploy_my_first_application`, the `deploy_my_first_application_env.tarEnv` file will have the following content:

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
            value: jammy # ubuntu version
          - name: "processor_architecture"
            from: "PC.processor.processor_architecture"
            value: x86
```

---

### Key Elements of the Template

- **TargetEnvironment**:
  - **name**: A unique identifier for the environment (e.g., `deploy_my_first_application_env`).
  - **includeDevices**:
    Each device listed here references a `DeviceType` defined in `*.dev` files. This approach enables reusing device definitions (properties and connections) across different target environments. Specific values can be overridden or assigned in the `.tarEnv` file.

    - **computationDevice**:
      - Refers to any PC or server used to run the software.
      - Defaults to referencing [pc.dev](https://github.com/ipa-rwu/DeploymentDeviceCatalog/blob/main/de.fraunhofer.ipa.deployment.catalog.devices/pc.dev).
      - Device properties like OS name and processor architecture can be configured here.

    - **device (optional)**:
      - Represents hardware devices like robots, grippers, or cameras.
      - Allows specifying properties such as `device_type` or `serial_number`.

  - **configConnection (optional)**:
    - Specifies how devices interact over various interfaces (e.g., Ethernet, USB).
    - Property values such as IP addresses or device volumes can be assigned here.

---

## Advanced Example

Here’s a more complete example with optional elements included:

```yaml
TargetDeployEnviroment:
  name: deploy_my_first_application_env # Name of this target environment
  includeDevice:
    computationDevice:
      - name: my_laptop
        refDeviceType: PC # Reference to a computation device type from the device catalog
        configDeviceProperty:
          - name: "os_name"
            from: "PC.operating_system.os_name"
            value: ubuntu # Only supports Ubuntu so far
          - name: "os_version"
            from: "PC.operating_system.os_version"
            value: focal # Ubuntu version
          - name: "processor_architecture"
            from: "PC.processor.processor_architecture"
            value: x86
    device:
      - name: my_robot
        refDeviceType: UR5E
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

---

## Tips for Editing

### Using the Device Catalog

1. Import the device catalog to access predefined device models:
   [How to Import the Device Catalog](../Environment_setup.md#import-the-device-catalog).
2. Reference predefined devices or customize them in the `.tarEnv` file.

### Resolving Device References

- Use `Ctrl + Click` on a referenced device (e.g., `PC`) to navigate to its definition in the device catalog.
- This is especially helpful for verifying or customizing properties.
