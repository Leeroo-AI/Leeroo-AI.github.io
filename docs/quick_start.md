# Quick Start

## Introduction

This guide provides detailed instructions for using the Leeroo client to manage workflows. The client simplifies tasks such as initializing workflows, editing configurations, submitting workflows for execution, and checking their status.

### Prerequisites

Before you begin, ensure you have installed the Leeroo client library and configured your environment with your Leeroo user ID and API key.

```bash
pip install leeroo-client
```

or install from source by:

```bash
git clone https://github.com/Leeroo-AI/leeroo-client
cd leeroo-client 
pip install -e .
```

## Getting Started

### Initializing the Leeroo Client

Import the necessary libraries and initialize the Leeroo client with your credentials. The client instance will be used to interact with Leeroo's workflow management services.

```python
import os
from leeroo_client.client import LeerooClient

# Initialize the Leeroo client
client = LeerooClient(user_id="your_user_id", api_key="your_api_key")
```

Replace `"your_user_id"` and `"your_api_key"` with your actual credentials obtained from Leeroo.


### Initializing a Workflow with Seed Data

Initialize a new workflow by providing a evaluation criteria, a unique name, and path of your seed data. This step sets up the initial configuration for your workflow.

```python
# Initialize workflow: uploading seed data
workflow_configs = client.initialize_workflow_configs(
    evaluation_criteria="""
    - Assess clarity of the response by determining if the response is well-structured and easy to understand.
    - Evaluate accuracy by verifying the correctness of the mathematical content and solutions.
    - Check completeness by ensuring that the response addresses all parts of the question thoroughly.
    - Finally, judge pedagogical effectiveness by considering if the explanation is insightful and promotes understanding, 
    utilizing examples and step-by-step reasoning where appropriate.
    
    Each response should be rated on these aspects to ensure a comprehensive evaluation.""",
    workflow_name="math_tutor_test",
    seed_data_path='math_tutor_data.json",
    budget=2,
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
