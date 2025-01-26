# Learning PlanRos Model (PlanModel)

## Overview

The **PlanRos Model (PlanModel, `*.planros`)** bridges the software system (defined in a RosSystem Model) with the physical environment (defined in a TarEnvModel). It specifies the software-to-hardware assignments, execution parameters, and additional configurations required for deployment.

When you create a new deployment project by following [Create an empty project](../README.md#create-an-empty-deployment-project), a template `*.planros` file is automatically included. This file serves as a skeleton for defining deployment plans and must be updated with the specifics of your system, target environment, and software components.

---

## Example: PlanRos Template

### Default Template: `deploy_my_first_application.planros`

When you create a project named as "deploy_my_first_application", the `deploy_my_first_application.planros` file has the following content:

```yaml
DeploymentPlanWithRos:
  name: deploy_my_first_application
  targetRossystem: "TODO: reference to a rossystem"
  deployTo: "TODO: reference to a target environment"
  assignment:
    - name: "TODO: name for this assignment, will use it as docker image name"
      executedBy: "TODO: reference to a computation device in this target environment"
      version: "TODO: version in string"
      middleware: "TODO: ROS version"
      softwareComponents:
        - "TODO: reference to a rossystem or component on this rossystem":
      runtimeType:
        type: container
        registry: "TODO: registry for releasing docker image"

```

Key Elements of the Template:

- DeploymentPlanWithRos: The root of the PlanModel, encapsulating the deployment plan details.
- name: A unique identifier for the deployment plan (e.g., deploy_my_first_application).
- targetRossystem: A reference to the RosSystem model that describes the software system for deployment.
- deployTo: A reference to the Target Environment model (*.tarEnv) where the software will be deployed.
- assignment: Contains details about how the software is deployed:
    - name: A name for the deployment assignment, often used as the Docker image name.
    - executedBy: reference to a computation device in the target environment responsible for running the software.
    - version: The version of the software being deployed.
    - middleware: The ROS version (e.g., humble).
    - softwareComponents: References the software components or subsystems from the "targetRossystem".
    - runtimeType: Defines the runtime environment:
        type: Specifies the runtime environment such as container (docker container)
    - registry: The registry URL for releasing the Docker image.

## Updating the PlanRos Model
To customize the PlanRos model:

1. Set the targetRossystem:
    Replace the placeholder with the name of your *.rossystem file.

    ![alt text](images/planros_set_targetrossys.gif)

2. Set the deployTo:
    Update this field with the name of your *.tarEnv file.

    ![alt text](images/planros_set_targetenv.gif)

3. Customize Assignments:
    Define the name, executedBy, version, middleware, and softwareComponents for each deployment assignment.
    ![alt text](images/planros_set_assignment.gif)

If there are issues in the model (e.g., unresolved references, missing values), an error symbol ![](images/error.png) will appear in front of the line with the issue.
For example, if all software components from the *.rossystem are not assigned to an assignment. The tooling will display a tooltip explaining which components are missing.
![alt text](images/planros_set_assignment_error.gif)
