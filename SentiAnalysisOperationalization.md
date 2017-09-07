## 1. Objectives

The aim of this lab is to publish the sentiment analysis model (hd5) and code as web services locally using a DSVM running on Azure.

## 2. Setup

Launch a Data Science Virtual Machine (Ubuntu) from portal.azure.com as shown below. Follow the steps to create the virtual machine on selection and ssh into the machine.

![DataScienceVirtualMachine]()

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
