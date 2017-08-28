# Churn Prediction using AMLWorkbench
# Operationalization
# Objectives
The aim of this lab is to publish churn models and code as web services so that they can be consumed to produce business results.
# Setup
Local mode deployments run in docker containers on your local computer, whether that is your personal machine or a VM running on Azure. You can use local mode for development and testing.
To prepare the operationalization environment, in the CLI window type the following to set up the environment for local operationalization:

az ml env setup

Follow the instructions to provision an Azure Container Registry (ACR) instance and a storage account in which to store the Docker image we are about to create. When finished, a file named .amlenvrc.cmd is created in your home directory (usually C:\Users<username>) which contains then names and credentials of the ACR and storage account.

To set the environment variables required for operationalization, simply execute the .amlenvrc.cmd file from the command line.

c:\Users\<username>\.amlenvrc.cmd

To verify that you have properly configured your operationalization environment for local web service deployment, enter the following command:

az ml env local
# Scoring and Schema Files
Open churn_schema_gen.py to investigate the code. Churn_schema_gen.py is responsible for generating the scoring and schema files necessary to operationalize Churn Prediction. Prepare the web service definition by authoring init() and run() functions.
The init() function loads the model (model.pkl) as shown below:
```def init():
    from sklearn.externals import joblib

    # load the model file
    global model
    model = joblib.load('model.pkl')
```
