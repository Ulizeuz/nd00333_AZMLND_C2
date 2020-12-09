# OVERVIEW

Basically, Machine Learning Operations is applying DevOps principles like deploying a model, consuming endpoints and automating a pipeline. We show a end to end Operationalizing Machine Learning:

- Auto ML model
- Deploy the best Model
- Enable Loggin
- Consume model endpoints
- Create and publish pipeline

We don't include Autentication step because was done for us in the enviroment. We start running a an Automated ML experiment to deploy the best model.

Next, we enable Application Insight to review information about the service when consuming model.

Finally, we'll create and publish a pipeline. At the end of this file, you can find a screencast with step-by-step process

# ARCHITECTURAL DIAGRAM

![Architectural Diagram](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img01%20Process.png)

# HOW TO IMPROVE THE PROJECT IN THE FUTURE

There are some lines of investigation to follow in the future:

- Use ParalellRunStep to create a Pipeline step to process large amount of data asynchronously and in parallel
- Test a local container downloading a Docker image that contains the model and  other files needed to host it as a web service
- Export the model to support ONNX ( Open Neural Network Exchange) to optimize the inference on production data


# PROCESS

## Autentication

As mention before, autentication step was done for us. In this step we should Install az and login, install Azure Machine Learning extension and create a Service Principal

## Auto ML model

Once security was enabled and authentication is completed we create an Automated ML run. We use in this example the Bankmarketing dataset:

![dataset](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img01_dataset.png)

Then, we create a new Automated ML experiment and run it using Clasification and ensuring Explain Best Model is checked. After some minutes (about 30) the experiment is completed:

![experiment completed](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img03_experiment.png)

And we can get the best model. For this, was VotingEnsemble with 0.9162 of accuracy:

![Best Model](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img04_model.png)

## Deploy the best Model

As we see above, we can find the best model when the experiment finish. 

We use this model to deploy to interact with the HTTP API service. In this step we deploy the model enabling Authentication and using Azure Container Instance (ACI)

## Enable loggin

The next step, after the best model was deployed, is enabling Aplication Insights and retrieve logs. For this, we use the logs.py script with this code: service.update(enable_app_insights=True):

![Logs](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img05_logs.png)

And we can find in Detail tab that Application Insights is enabled:

![Logs](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img06_insights.png)

## Consume model endpoint

### Swagger

First, we consume the model using Swagger. Swagger is a useful tool to display the contents of the API. Next images show Swagger running on localhost and the HTTP API methods and responses for the model:

![Swagger server](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img07_swagger1.png)

![Swagger server](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img08_swagger2.png)

![Swagger server](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img09_swagger3.png)

### Endpoint script

We use the endpoint script to interact with the trained model. To use it, we need update the scoring_uri and the key to match with our service:

![Swagger server](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img10_endpoint.png)

### Benchmark

To load-test our model we run again endpoint.py script and a data.json apears in our directory. Then, we run the benchmark file to retrieve performace results:

![benchmark](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img11_benchmark.png)

## Create and publish a pipeline

Finally, we use Jupyter notebook to create and publish a pipeline. We can verify in Azure the correct process to create

### Pipeline created

- The pipeline created:

![pipeline](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img12_pipeline.png)

- The pipeline endpoint:

![pipeline](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img13_pipeline_endpoint.png)

- Bankmarketing dataset

![dataset](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img14_marketing_ds.png)

### Pipeline published

Finally we publish the pipeline. We use runDetails to monitoring the progress:


![publish](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img16_publishing.png)

![publish](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img17_rundetails.png)



In the published pipeline overview we can see the status (ACTIVE) and a REST endpoint

![publish](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img15_published.png)

And we can see the scheduled run

![Scheduled](https://github.com/Ulizeuz/nd00333_AZMLND_C2/blob/master/Screenshots/img18_completed%20run.png)



# VIDEO


