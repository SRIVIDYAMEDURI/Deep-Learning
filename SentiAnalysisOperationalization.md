## 1. Objectives

The aim of this lab is to publish the sentiment analysis model (hd5) and code as web services locally using a DSVM running on Azure.

## 2. Setup

Launch a Data Science Virtual Machine (Ubuntu) from portal.azure.com as shown below. Follow the steps to create the virtual machine on selection and ssh into the machine.

![DataScienceVirtualMachine](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/DataScienceVirtualMachine.png)

Pip is a better alternative to Easy Install for installing Python packages. To install pip on ubuntu run the bellow command:
```
sudo apt-get install python-pip
```
Only users with sudo access will be able to run docker commands. Optionally, add non-sudo access to the Docker socket by adding your user to the docker group.

```
sudo usermod -a - G docker $(whoami)
```

If you encounter “locale.Error: unsupported locale setting” error, perform the below export:

```
export LC_ALL=C
```

Install azure-cli and azure-cli-ml using pip:

```
pip install azure-cli
pip install azure-cli-ml
```

In addition, change python default version and run the below commands. Local mode deployments run in docker containers on your local computer, whether that is your personal machine or a VM running on Azure. You can use local mode for development and testing. 

```
alias python=python3
source ~/.bash_aliases
az ml env setup
source ~/.amlenvrc
cat < ~/.amlenvrc >> ~/.bashrc
```
Upload the below files to the vm (you could use scp to perform the upload):
conda_dependencies.yml
sentModel.h5
myschema.json
senti_schema.py

## 3. Image Creation

Edit the conda_dependencies.yml to contain only the following content:
name: project_environment

```
dependencies:
  - pip:
    # This is the operationalization API for Azure Machine Learning. Details:
    # https://github.com/Azure/Machine-Learning-Operationalization
    - azure-ml-api-sdk
    - keras
    - scikit-learn
    - pandas
    - tensorflow
    - h5py
```

Note that we have removed ipykernel as we will not be needing it. The following command creates an image which can be used in any environment.

```
az ml image create -n ads1 -v -c conda_dependencies.yml -m sentModel.h5 -s myschema.json -f senti_schema.py -r python
```

![PuttyImage](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/PuttyImage.png)

You will find the image id displayed when you create the image. Use the image id in the next command to specify the image to use. 

```
az ml image usage -i 9bebf880-dc0d-4b2c-9e00-f19f8e09102a
```
In some cases, you may have more than one image and to list them, you can run az ml image list.

Ensure local is used as the deployment environment:

```
az ml env local
```

In local mode, the CLI creates locally running web services for development and testing.

Change to root:

```
sudo su
```

## 4. Realtime Service

Create a realtime service by running the below command using the image-id. In the below command, we create a realtime service called sentiservice.

```
az ml service create realtime -n sentiservice –-image-id 9bebf880-dc0d-4b2c-9e00-f19f8e09102a
```
An example of a successful run of az ml service create looks as follows. In addition, you can also  docker ps to view the container.

![DockerPs](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/DockerPs.png)

Run the service (sentiservice) created using az ml service run. Note the review text created and passed to call the web service.

```
az ml service run realtime -i sentiservice -d "{\"input_df\": [{\"reviewText\": \"The movie was great. I liked it\"}]}"
```

![Sentiservice](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/Images/Sentiservice.png)

The model built was on a very small dataset. Hence, you will find the sentiment scores are not very robust. In comparison, the IMDB Movie reviews sentiment classification problem (https://keras.io/datasets/#datasets ) from keras consists of a dataset of 25,000 movies reviews from IMDB, labeled by sentiment (positive/negative). The intention of this lab was to show you how to perform sentiment analysis using Deep Learning with AMLWorkbench.

## Exercise

To improve the sentiment scores, can you use a large set of reviews and rebuild the model? You can test the service using the newly trained model.




