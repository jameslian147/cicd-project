# Overview ![Python application test with Github Actions](https://github.com/jameslian147/cicd-project/workflows/Python%20application%20test%20with%20Github%20Actions/badge.svg)
This is a python project that demostrates the necessary steps in setting up CI CD in Azure and Github actions

## Project Plan
Trello board
https://trello.com/b/j66JLQ23

Management Spreadsheet
https://docs.google.com/spreadsheets/d/1g__ADvqWh5nC4_anMRsUzwtnP_uprrVialXOOlmvjC0/edit?usp=sharing

## Instructions

### Quick view of architecture
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/architecture.png?raw=true "Architecture")

# Overview ![Python application test with Github Actions](https://github.com/jameslian147/cicd-project/workflows/Python%20application%20test%20with%20Github%20Actions/badge.svg)
This is a python project that demostrates the necessary steps in setting up CI CD in Azure and Github actions

## Project Plan
Trello board
https://trello.com/b/j66JLQ23

Management Spreadsheet
https://docs.google.com/spreadsheets/d/1g__ADvqWh5nC4_anMRsUzwtnP_uprrVialXOOlmvjC0/edit?usp=sharing

## Instructions

### Quick view of architecture
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/architecture.png?raw=true "Architecture")

### In brief
This is the desired setup we want to do at the end of this project. When there are changes to the git repo, eg. file modification, Gitactions will auto run the Makefile all thru the file .github/workflows/pythonapp.yml.

Azure Pipelines works quite similar with Gitactions except we will be doing deployment to app services after a successful build.

### Prerequisites
1. Account in Azure Devops
2. Account in Github
3. Account in Azure Portal
4. Python3 with brew
5. virtual environments https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/
6. a fork of https://github.com/jameslian147/cicd-project



### Build Steps in local desktop
1. cd into directory
2. make setup for environment
```
make setup
```
3. go in to virual environment
```
source ~/.udacity-devops/bin/activate
```
4. make project
```
make all
```
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/build-all.png?raw=true "Build all")
5. load test
```
make loadtest
```
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/loadtest1.png?raw=true "load test")
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/loadtest2.png?raw=true "load test")


### GitAction Steps
1. Go to the repo page and click Actions

2. Click on Create new workflow >> set up a workflow yourself

3. Copy the contents of ex-github.yml and paste it on the edit box
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/github-flow.png?raw=true "Cloud Shell")

4. Click `Start Commit` >> create new file

5. Go back to `Actions` and you will see a new gitflow
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/github-flow-actions.png?raw=true "Cloud Shell")

6. Now your project will detect any changes on `master` branch and start build

### Azure Pipeline Steps
1. Go to Azure Portal

2. Click on Cloud Shell

![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/cloud-shell.png?raw=true "Cloud Shell")

3. Clone this project at the cloud shell

![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/git-status.png?raw=true "Git Status")


4. Authorize App Service. Navigate to the folder inside and run the following command

```bash
az webapp up -n <your-appservice>
```
Change <your-appservice> to a name for your app service that's unique across Azure. Typically, you use a personal or company name along with an app identifier, such as <your-name>-flaskpipelines. The app URL becomes <your-appservice>.azurewebsites.net.

![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/az-app-services.png?raw=true "App Services")

5. Go to Azure Pipelines
https://dev.azure.com

8. Create a new project
and go to Settings >> Pipelines >> Service Connections
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/new-project.png?raw=true "New Project")

9. Select Azure Resource Manager >> Service Principal (automatic)

10. Select your Azure Subscription and Resource Group and a new Service Name
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/new-service-connection.png?raw=true "Service Connection")

11. Go to pipelines >> Create Pipeline
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/create-pipeline.png?raw=true "Create Pipeline")

12. Select your repository
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/select-repo.png?raw=true "Select Repo")

13. Python to Linux Web App on Azure
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/selet-step-azure.png?raw=true "Select Step")

14. Review and save the pipeline yml
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/save-pipeline.png?raw=true "Save Pipeline")

15. App Deployment will be shown with pipeline
![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/deployment-success.png?raw=true "Save Pipeline")

16. As your app is up. Go to your repo in Azure Cloud Shell and copy your app name. eg. flask-ml-ap.azurewebsites.net
Edit it and replace it in make_predict_azure_app.sh

```
 -H "Content-Type: application/json" \
     -X POST https://<yourappname>.net:$PORT/predict 
     #your application name <yourappname>goes here
```

The output should look similar to this:

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

17. to check the logs of your app
use this command
```bash
az webapp log tail -n <appname> --resource-group <resourcegroup>
```
* Example Output of streamed log

![alt text](https://github.com/jameslian147/cicd-project/blob/master/images/output.png?raw=true "Save Pipeline")


## Enhancements
To organise shell scripts into one folder
To provide visual ui for showing prediction


## Demo 

Link to demo
https://youtu.be/2jvoZ5oRJcs



