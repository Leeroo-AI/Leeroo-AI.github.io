# Quick Start Guide

## Introduction

This guide provides detailed instructions for using the Leeroo client to manage workflows. The client simplifies tasks such as initializing workflows, editing configurations, submitting workflows for execution, and checking their status.

### Prerequisites

Before you begin, ensure you have installed the Leeroo client library and configured your environment with your Leeroo user ID and API key.

```bash
pip install leeroo-client
```

## Getting Started

### Initializing the Leeroo Client

Import the necessary libraries and initialize the Leeroo client with your credentials. The client instance will be used to interact with Leeroo's workflow management services.

```python
import os
from leeroo_client import LeerooClient

# Initialize the Leeroo client
client = LeerooClient(user_id="your_user_id", api_key="your_api_key")
```

Replace `"your_user_id"` and `"your_api_key"` with your actual credentials obtained from Leeroo.


### Initializing a Workflow with Seed Data

Initialize a new workflow by providing a task description and a unique name. This step sets up the initial configuration for your workflow.

```python
# Initialize workflow: uploading seed data
workflow_configs = client.initialize_workflow_configs(
    task_description="The AI Customer Care Chat Assistant role at SkyView Travel focuses on enhancing customer experiences through intelligent interaction handling. Trained on extensive travel-related conversational data, this assistant excels in providing personalized travel recommendations, resolving booking queries, and ensuring seamless journey planning. Utilizing advanced natural language processing techniques, it offers empathetic and efficient customer support, aiming to deliver exceptional service with each interaction.",
    workflow_name="SkyView Travel Model"
)
print("Initialized workflow configurations:", workflow_configs)
```

### Editing Workflow Configuration (Optional)

Modify the workflow configuration if necessary. Here, we update a specific parameter (`r`) in the workflow configuration for example.

```python
# Edit workflow configuration
workflow_configs['experiment_config']['0']['training_methods_args']['r'] = 8
workflow_configs['experiment_config']['1']['training_methods_args']['r'] = 16
```


### Submitting a Workflow for Execution

Submit the configured workflow for execution on Leeroo servers. This step initiates the process of running the defined experiments and tasks as per your workflow configuration.

```python
# Submit workflow for execution
running_workflow_status = client.submit_workflow(
    workflow_configs=workflow_configs
)
print("Submitted workflow for execution. Workflow running state:", running_workflow_status)
```


### Retrieving User's Workflows

Fetch all workflows associated with your Leeroo user account. This step provides an overview of all workflows currently managed by your account.

```python
# Retrieve user's workflows
user_workflows = client.all_workflows()
print("User's workflows:", user_workflows)
```


### Checking Status of a Running Workflow

Monitor the current status of a running workflow using its unique running state ID. This step allows you to track the progress and status of your submitted workflows.

```python
# Check status of the running workflow
workflow_running_state_id = running_workflow_status['workflow_running_state_id']
workflow_status = client.get_workflow_status(workflow_running_state_id)
print("Workflow status:", workflow_status)
```


## Conclusion

This guide provides a detailed approach to using the Leeroo client for managing workflows. For advanced usage and detailed API reference, refer to the official Leeroo documentation.
