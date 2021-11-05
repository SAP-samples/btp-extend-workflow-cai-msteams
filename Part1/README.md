# Setting up for Workflow Management on SAP Business Technology Platform

In this part you'll set up and configure the basic aspects of the SAP Workflow Management.  

From a service perspective, you'll be using a number of services from the start:

* **Workflow Service**: Build, run, and manage simple and complex workflows spanning across various organizations and applications.
* **Workflow Management**: Configure the process flows, decisions and visibility scenarios in a low-code, no-code approach to improve process experience.
* **SAP Business Application Studio**: Develop, debug, test, and deploy SAP business applications.
* **Authorization & Trust Management**: to manage application authorizations and trust to identity providers

## Step 1 - Set up your trial account for SAP Workflow Management

To accelerate the setup process, BTP offers **Boosters** concept which will help you to automate the onboarding process and save several manual efforts for configuring and activating required services.

In a Booster Catalog you can find booster **"Set up account for Workflow Management"** which helps you to set up a development environment where you can work with SAP Workflow Management service in your SAP BTP account.

This guided set of automated steps will configure entitlements of workflow management services, subscribe to the workflow management application, create a service instance for: workflow management, workflow, create needed destinations, and assign all needed roles to your user. In the background, the booster will also automatically enable Cloud Foundry and create default space, if not done already.

As the booster completes, your subaccount will be ready to start building using SAP Workflow Management. You'll have appropriate authorizations set up and assigned to your user, an SAP Business Application Studio (IDE) setup and configured to work with Workflow artifacts, and an instance of the main Workflow service set up explicitly.
   
### 1.1.  Go to your SAP BTP trial account and go to *Boosters* section. Find the *"Set up account for Workflow Management"* booster and open it.

![Boosters](./images/boosterstart.png)

### 1.2. Get overview which Services and Subscriptions are part of this booster and *start* the booster

![Booster Overview](./images/boosteroverview.png)

### 1.3. Booster will start executing following tasks:
   * Assigning Service Quotas
   * Subscribing to SaaS Applications
   * Creating Service Instances
   * Creating Destination
   * Assigning Role Collections
   
   After finishing all the tasks you will see a success message.

![Booster Execution](./images/boosterexecution.png)

### 1.4. After successful execution you can navigate to *Instances and Subscriptions* of your subaccount and find
   * **SAP Business Application Studio** and **Workflow Management** subscribed in **Subscriptions** Tab
   * **Destination** and **Workflow** Service instances created in **Instances** Tab
   * **Cloud Foundry Runtime** environment created in **Environments** Tab

   ![Booster Results](./images/boosterfinish.png)

### 1.5. After booster execution you can also find all the required roles assigned to your user, so no manual assignment is necessary.
   
   ![Workflow Roles](./images/workflowroles.png)

### 1.6. In upcoming parts we will use workflow APIs and for that we need to add the required authorization scopes to the services instance. Using the *"Instances and Subscriptions"* menu item on the left, update the *wm_workflow* service instance by using the "Update" button and following the dialog flow, paying attention at each of the steps:

![Update WF Service instance](./images/wf_update_service_instance.png)

- Step "Basic info": make sure that you don't change the name
- Step "Parameters": specify the following authorization scopes in the text area:

    ```
        {
        "authorities": [
            "TASK_COMPLETE",
            "WORKFLOW_DEFINITION_DEPLOY",
            "TASK_GET_CONTEXT",
            "TASK_UPDATE",
            "TASK_GET_FORM_MODEL",
            "TASK_GET_FORM",
            "TASK_GET",
            "TASK_GET_ATTRIBUTES",
            "PROCESS_TEMPLATE_DEPLOY",
            "PROCESS_VARIANT_DEPLOY",
            "TASK_GET_ATTACHMENTS",
            "WORKFLOW_INSTANCE_START"
            ]
    }
    ```

![Update WF Service instance](./images/wf_update_scopes.png)

> The authorities you specified in the "Parameters" step will be needed in a later part, when you come to call the Workflow API.


## Step 2 - Configure SAP Business Application Studio for development

### 2.1. Open SAP BTP cockpit and navigated to *Instances and Subscriptions* inside your trial subaccount. Find **"SAP Business Application Studio"** within Application Subscriptions and launch it either from launch icon or "..." --> "Go to Application"
   
![Start Business Application Studio](./images/bas_launch.png)
   
### 2.2. Create a new development Space 
   
![Create Dev Space](./images/bas_create_space.png)
    
### 2.3. Select Following Extensions to enable them in the development space:
    * Java Tools - For developing and running Java Apps
    * MTA Tools - For build/deploy/... Multitarget Applications
    * Workflow Management - For creating Workflow Applications
   
   ![Create Dev Space](./images/bas_new_space.png)

### 2.4. After creation you can find newly defined and preconfigured development space with all required tools. In the next part we will use this space for building and deploying the workflow application. 
   
   ![BAS WF Dev Space](./images/bas_wf_space.png)

## Summary

Good work!
You successfully finished the setup and configuration of all necessary services and tools which is required for the later steps.
