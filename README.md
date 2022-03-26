# Dynamic Risk Assessment System

## Description
Machine Learning Model Scoring and Monitoring. The problem is to create, deploy, and monitor a risk assessment ML model that will estimate the attrition risk of each of the company's clients. Also setting up processes to re-train, re-deploy, monitor and report on the ML model.

## Prerequisites
- Python 3 required
- Linux environment / Windows subsytem for Linux - WSL

## Dependencies
This project dependencies is available in the ```requirements.txt``` file.

## Installation
Use the package manager [pip](https://pip.pypa.io/en/stable/) to install the dependencies from the ```requirements.txt```. Its recommended to install it in a separate virtual environment.

```
pip install -r requirements.txt
```

## Steps Overview
1. **Data ingestion:** Automatically check if new data that can be used for model training. Compile all training data to a training dataset and save it to folder. 
2. **Training, scoring, and deploying:** Write scripts that train an ML model that predicts attrition risk, and score the model. Saves the model and the scoring metrics.
3. **Diagnostics:** Determine and save summary statistics related to a dataset. Time the performance of some functions. Check for dependency changes and package updates.
4. **Reporting:** Automatically generate plots and PDF document that report on model metrics and diagnostics. Provide an API endpoint that can return model predictions and metrics.
5. **Process Automation:** Create a script and cron job that automatically run all previous steps at regular intervals.

<img src="images/process_flow_chart.jpg" width=550 height=300>

### The following are the Python files that are in the starter files:

training.py, a Python script meant to train an ML model
scoring.py, a Python script meant to score an ML model
deployment.py, a Python script meant to deploy a trained ML model
ingestion.py, a Python script meant to ingest new data
diagnostics.py, a Python script meant to measure model and data diagnostics
reporting.py, a Python script meant to generate reports about model metrics
app.py, a Python script meant to contain API endpoints
wsgi.py, a Python script to help with API deployment
apicalls.py, a Python script meant to call your API endpoints
fullprocess.py, a script meant to determine whether a model needs to be re-deployed, and to call all other Python scripts when needed

## Usage

### 1- Edit config.json file to use practice data

```bash
"input_folder_path": "practicedata",
"output_folder_path": "ingesteddata", 
"test_data_path": "testdata", 
"output_model_path": "practicemodels", 
"prod_deployment_path": "production_deployment"
```

### 2- Run data ingestion
```python
cd src
python ingestion.py
```
Artifacts output:
```
data/ingesteddata/finaldata.csv
data/ingesteddata/ingestedfiles.txt
```

### 3- Model training
```python
python training.py
```
Artifacts output:
```
models/practicemodels/trainedmodel.pkl
```

###  4- Model scoring 
```python
python scoring.py
```
Artifacts output: 
```
models/practicemodels/latestscore.txt
``` 

### 5- Model deployment
```python
python deployment.py
```
Artifacts output:
```
models/prod_deployment_path/ingestedfiles.txt
models/prod_deployment_path/trainedmodel.pkl
models/prod_deployment_path/latestscore.txt
``` 

### 6- Run diagnostics
```python
python diagnostics.py
```

### 7- Run reporting
```python
python reporting.py
```
Artifacts output:
```
models/practicemodels/confusionmatrix.png
models/practicemodels/summary_report.pdf
```

### 8- Run Flask App
```python
python app.py
```

### 9- Run API endpoints
```python
python apicalls.py
```
Artifacts output:
```
models/practicemodels/apireturns.txt
```

### 11- Edit config.json file to use production data

```bash
"input_folder_path": "sourcedata",
"output_folder_path": "ingesteddata", 
"test_data_path": "testdata", 
"output_model_path": "models", 
"prod_deployment_path": "production_deployment"
```

### 10- Full process automation
```python
python fullprocess.py
```
### 11- Cron job

Start cron service
```bash
sudo service cron start
```

Edit crontab file
```bash
sudo crontab -e
```
   - Select **option 3** to edit file using vim text editor
   - Press **i** to insert a cron job
   - Write the cron job in ```cronjob.txt``` which runs ```fullprocces.py``` every 10 mins
   - Save after editing, press **esc key**, then type **:wq** and press enter
  
View crontab file
```bash
sudo crontab -l
```

## License
Distributed under the [MIT](https://choosealicense.com/licenses/mit/) License. See ```LICENSE``` for more information.
