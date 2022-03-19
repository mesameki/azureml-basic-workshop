# AzureML and Data Science Overview Workshop

The purpose of this workshop is for you to work through a basic end-to-end flow for a data scientist starting to work with AzureML to train a model, test it with an endpoint, then experiment to improve the outcomes. Work through the scenario with the Studio, CLI v2, and the SDK where appropriate. Use our docs and samples to figure out syntax. The scenario has been tested and you’ll see that the product is pretty good overall. Things are not consistent and some experiences aren’t good. With the exception of some internal private preview features, this is what our customers see.

This is hands-on and not a demo or tour of the product. The knowledge required of python, Linux, AzureML and Azure is minimal. There are some hints below to point you in the right direction. Search the Web, read docs and samples, and reach out to team members for help if you get stuck.


## 0. Getting Started

You need access to an Azure subscription. If it’s a shared subscription, the owner should provide you with a resource group and assign you as owner so you can wear an IT hat and create a workspace and required resources. 

This repo [repo link] has the python scripts and data files you need to get started. 

Hint: You need compute quota for AzureML in the region for the workspace for the VM family you want to use. 6 cores of any D series should be fine to create a compute instance, cluster, and realtime endpoint. 


## 1. Train and test Locally
First step is to train a model locally to make sure it works. You can do this with a Compute Instance, a DSVM, or your local machine. Linux is easier to setup than Windows. You can work from Visual Studio Code, a terminal window, or notebook. 

The script uses MLFlow logging and will log to an AzureML workspace without having to submit a run. Take a look at the experiment in Studio.

Once you’ve trained a model locally, try the score.py script to test it locally. 

Hints: For local training, the train.py script is setup to use the training data csv file in the same directory. It writes the model file to a new folder, deleting an existing folder with the same name if found. You may need to configure your Python environment with the packages needed for the training script. If not using a Compute Instance you will need to set the workspace to log to.


## 2. Train in Cloud
Now that you’ve confirmed the training code works, train the model in the cloud using an AzureML job. Use the train.py and flightdelayweather_ds_clean.csv from the repo (but imagine that you’re training on petabytes of data). Try this from both the Studio and the v2 CLI.

Hints: Your training run needs an environment with the package dependencies and the CSV file in a dataset as input to train with. There is more than one way to handle this. Remember that the local training run you did assumed a local data file instead of passing this in as a parameter as --data. 


## 3. Create Managed Real-Time Endpoint
After training a model, create a real-time managed endpoint and test us using the sample JSON file in the repo. Try this with the Studio and the v2 CLI. 

TODO: Need sample JSON to test with

You could also write a script or app to use the endpoint. 

## 4. Create Managed Batch Endpoint
Next create a batch endpoint. There is a scoring CSV in the repo. If you do this in the Studio, you will see that a pipeline was created. Look at the results and how many flights are predicted to be on-time vs delayed. 

Hint: Use the predict_data.csv for the batch scoring job.


## 5. Experiment
Now we get into the science part to experiment on how we could improve the model. Edit the train.py file and change [param] to True.

Train the model again and compare metrics with the first model. What do you see?

Test the new model by creating a new batch endpoint or scoring locally. Are the results different? What metrics do you think are important to measure quality of this prediction? Try optimizing for a different metric than auc.


## 6. Explore the Data
The data imbalance hyperparameter in LightGBM helps in the case where the training data has more on-time flights and so biased the outcome in the model. This is something a data scientist needs to be aware of.

Try different ways to explore the data. Open it in Excel, important it as a tabular dataset, or use Python tools. Think about how we can help with this.


## 7. Reflect and Discuss
This was a simple exercise, but used the breadth of AzureML for ML Pros working with python scripts using Studio, CLI, VS Code or other tools. You had to create a basic workspace (no VNET today), create and use computes, train models, look at metrics, create and test endpoints, and experiment with the training code and data.
Was it easy to get started and figure out what to do? Did you need to look at documentation or samples? We’re things consistent across the Studio, v2 CLI and SDK? Did you have to troubleshoot any error messages? Was the Studio experience intuitive? What are you going to personally improve from what you experienced in this workshop?


## 8. Bonus: Improve the Model
Now think about this as a Kaggle competition. Have some fun and try out different ways to improve the model quality. You could look at AutoML, Flaml, or other approaches. Share your best model with the team. 


## 9. Bonus: Create a component
Create a component from the train.py file and use it in a pipeline to re-train a model that is then used for batch scoring. Try this using the CLI and Studio.
