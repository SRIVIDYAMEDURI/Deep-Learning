# Deploying a scoring service to the Azure Container Serice (AKS)

This hands-on lab guides you through deploying a Machine Learning scoring file to a remote environment using [Azure Machine Learning Services](https://docs.microsoft.com/en-us/azure/machine-learning/preview/overview-what-is-azure-ml) with the Azure Machine Learning Workbench. 

In this workshop, you will:
- Understand how to create a model file
- Generate a scoring script and schema file
- Prepare your scoring environment
- Deploy your model
- Run and update the real-time web service

***NOTE:*** There are several pre-requisites for this course, including an understanding and implementation of: 
  *  Programming using an Agile methodology
  *  Machine Learning and Data Science
  *  Intermediate to Advancced Python programming
  *  Familiarity with Docker containers and Kubernetes

There is a comprehensive Learning Path you can use to prepare for this course [located here](https://github.com/Azure/learnAnalytics-CreatingSolutionswiththeTeamDataScienceProcess-/blob/master/Instructions/Learning%20Path%20-%20Creating%20Solutions%20with%20the%20Team%20Data%20Science%20Process.md).

## Building the Scoring for remote Deployment

(Note - [Our primary example is here](https://docs.microsoft.com/en-us/azure/machine-learning/preview/tutorial-classifying-iris-part-3) and [Another example is here](https://blogs.technet.microsoft.com/machinelearning/2017/09/25/deploying-machine-learning-models-using-azure-machine-learning/) )

The general configuration for working with the  Azure Container Service has this architecture:

![AKS](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/15159959-b5cd-4fe9-aeba-441139943ecd.png)

We will review these articles in class: 
  1.  [A quick overview of the Azure Container Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough)
  2.  [Understanding Service Principals](https://docs.microsoft.com/en-us/azure/aks/kubernetes-service-principal)
  3.  [Scoring Setup and Configuration](https://docs.microsoft.com/en-us/azure/machine-learning/preview/deployment-setup-configuration)
  4.  [Scaling Clusters](https://docs.microsoft.com/en-us/azure/machine-learning/preview/how-to-scale-clusters)


### Lab 1: Generate Naive Bayes and Decision Tree Model files

In this lab you'll create an churn prediction experiment, examine its configuration, and run the experiment locally to generate model files.
- Open the Azure Machine Learning Services Workbench tool locally or on your Data Science Virtual Machine. 
- Add the below code snippet to the end of CATelcoCustomerChurnModeling.py:
````
# serialize the dt on disk in the 'outputs' folder
print ("Export the dt model to outputs/model.pkl")
f = open('./outputs/dt.pkl', 'wb')
pickle.dump(dt, f)
f.close()
````
- Launch CLI and run ```az ml experiment submit -c local CATelcoCustomerChurnModeling.py```
- Check if dt.pkl and model.pkl is in the output folder as shown below.

![CATelcoCustomer](images/CATelcoCustomer_gWithoutDprep)

- Download the model files and put in root folder.
- If you have not already generated Schema, generate the schema by running ```python churn_schema_gen.py```

### Lab 2: Deploy Service to Production

- To deploy your web service to a production environment, first set up the environment using the following command:

```az ml env setup --cluster -n [your environment name] -l [Azure region e.g. eastus2] [-g [resource group]]```

This sets up an ACS cluster with Kubernetes as the orchestrator. The cluster environment setup command creates the following resources in your subscription: 
1. A resource group (if not provided, or if the name provided does not exist)
2. A storage account
3. An Azure Container Registry (ACR)
4. A Kubernetes deployment on an Azure Container Service (ACS) cluster
5. An Application insights account

The resource group, storage account, and ACR are created quickly. The ACS deployment can take up to 20 minutes.

**Check Status:**
To check the status of an ongoing cluster provisioning, use the following command:

```az ml env show -n [environment name] -g [resource group]```

Ensure that “Provisioning State” is set to "Succeeded" before proceeding.
