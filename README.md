# Machine-Learning-Pipeline-using-Kubeflow

## INTRODUCTION

This project investigates the deployment of machine learning models on Kubernetes and Localhost Server leveraging Kubeflow, 
an open-source program that serves as an operational toolset for the complete ML stack. Our objective is to construct pipelines 
for complete machine learning models using Kubeflow while considering a variety of aspects, including the tool’s capabilities, 
setup, deployment models and performance. This project mainly focuses on new users (with no knowledge or very less knowledge of Kubeflow)
of Kubernetes and the Google Cloud Platform enabling them to set up machine learning models and create ML pipelines with the aid of our project.


## OVERVIEW:
What is Kubeflow? An open-source project that combines the most widely used data science tools. The main idea is to accelerate the development of machine learning applications starting with the prototype stage. Google created the open source Kubeflow platform to contain the machine learning model development life cycle. The machine learning life cycle is made up of several operations, including data exploration, feature engineering, feature transformation, model experimentation, training, assessment, tuning, serving, and versioning. The set of tools that make up Kubeflow addresses each of these aspects. A Kubernetes cluster's built-in capabilities, such as container orchestration and auto-scaling, are used by Kubeflow because it is created to run on top of Kubernetes.
Although Kubernetes is a widely used technology for container orchestration, it may be difficult and time-consuming for data scientists or machine learning engineers to configure and coordinate each stage of the machine learning life cycle in a Kubernetes cluster. Therefore, Kubeflow acts as the platform that offers the tools to build, create, automate, and deploy each stage of the machine learning life cycle in a Kubernetes cluster rather than needing data scientists or machine learning engineers to do it manually.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/199405667-3f7062b0-bbf9-44ab-9429-6f20484d43cb.png">

Figure 1: Kubeflow
    
## RELATED WORK:
There are some similar systems for MLOps and pipelining that are currently present in the market. Following is a few of those:
Argo: Argo serves as the foundation for several Kubeflow components, however Argo is designed to orchestrate any process, whereas Kubeflow is focused on machine learning-specific tasks like model deployment and hyperparameter tuning. While Argo mandates the use of YAML for task declaration, Kubeflow permits the use of a Python interface. Argo may be used to manage a DAG of generic tasks executing on Kubernetes pods, while Kubeflow can be used if you prefer a tool with a stronger focus on machine learning. Both Kubeflow and Argo require Kubernetes as their prerequisite.
MLFlow: Kubeflow and MLFlow are both smaller, more focused task orchestration systems than more comprehensive systems like Airflow. With Kubernetes integration, Kubeflow can be used to keep track of machine learning experiments and deliver your solutions in a more specialized way. If you prefer a simpler method of tracking experiments and want to deploy to managed platforms, you may utilize MLFlow. While Kubeflow is heavily reliant on Kubernetes, MLFlow is a Python utility that enables experiment tracking in your existing machine learning programs. MLFlow already offers the ability to deploy scikit-learn models to Azure ML or Amazon Sagemaker, but Kubeflow enables you to construct a full DAG where each step is a Kubernetes pod.
Airflow: While Kubeflow is geared at machine learning operations, Airflow provides a framework for general task orchestration. Python jobs may be defined using either tool. While Kubeflow may be utilized if one already uses Kubernetes and requires more out-of-the-box patterns for machine learning solutions, Airflow can be used if a large ecosystem that can handle several jobs is required.
Luigi: Luigi concentrates on model deployment and CI/CD in contrast to the core Kubeflow functionalities. While Kubeflow provides prebuilt patterns for delivering Jupyter notebooks and optimizing hyper-parameters, Luigi is a Python-based toolkit developed for orchestrating general processes. If you use Kubernetes and want to orchestrate standard machine learning activities, you can use Kubeflow. If you need to orchestrate a variety of different processes, from data purification to model deployment, you can use Luigi.

BUSINESS POINT OF VIEW:
Kubeflow is essentially MLOps in the Cloud and sits at the nexus of Machine Learning, DevOps, and Data Engineering. Kubeflow addresses several MLOps problems such as lack of iterative deployment, inadequate infrastructure and methods, the necessity of automated CI/CD pipelines, and handling the proliferation of data and processing capacity.
According to SlashData's most recent State of Cloud Native Development Report for CNCF [10], 5.6 million developers used Kubernetes in 2021, which has shown amazing growth over the past few years. In 2017, there were 3.9 million Kubernetes engineers in the globe and in 2021, this category comprises 31% of all backend developers, an increase of 4% from 2020 to 2021.
  
<img width="203" alt="image" src="https://user-images.githubusercontent.com/11815663/211220019-b4a924ec-41d6-4212-9048-4f99c9d6f94a.png">
<img width="197" alt="image" src="https://user-images.githubusercontent.com/11815663/211220032-dce534b9-e838-4ec0-b0a9-1bdf151b2023.png">

Figure 2: Popularity of Kubernetes
                                              
Kubernetes has proven that it can satisfy the demands of the enterprise by being embraced by big businesses and by the exponential expansion of containers. Without realizing it, developers are utilizing Kubernetes in some or other way. Many of the most well-known services may use Kubernetes to a greater or lesser extent than developers are aware of. Even though Kubernetes has drawn more attention since 2020, many backend engineers are still unaware of its potential benefits. 21% of them claim to have heard of Kubernetes but have no clue what it does, while 11% say they have never ever heard of it.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220299-7cb5f07e-0355-4f2e-a9c5-86f8dd8388b1.png">

Figure 3: Kubernetes usage and with respect to its awareness among backend developers

  
## DEV/STAGING/PROD ENVIRONMENT:

LOCALHOST SERVER (INSTALLATION):

The environment to create and run Kubeflow pipelines UI on Localhost Server is as follows:
- Install Docker Desktop (Windows): https://docs.docker.com/desktop/install/windows install/
- Install kind:
o curl.exe-Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.16.0/kind-
windows-amd64
- Creating clusters: cmd: kind create cluster

<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220285-f8aa6e71-1f3e-4eab-acf5-74ac83e5d7c3.png">

- Execute the following commands to deploy the Kubeflow Pipelines:
o kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-
scoped-resources?ref=1.8.5"
o kubectl wait --for condition=established --timeout=60s
crd/applications.app.k8s.io o kubectl apply -k
"github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-
pns?ref=1.8.5"
- By port-forwarding, confirm that the Kubeflow Pipelines UI is reachable:
o kubectl port-forward -n kubeflow svc/ml-pipeline-ui 50112:80
- Go to the Kubeflow Pipelines UI by going to http://localhost:50112/

GOOGLE CLOUD KUBERNETES (INSTALLATION):

The environment to create and run Kubeflow pipelines UI on Google Cloud Platform is as follows:
- Google Cloud Platform setup.
- Google cloud SDK to run Google Cloud CLI. (Documentation on:
https://cloud.google.com/sdk/docs/install)
- A repository is created containing the following files:
o Docker File: Used for building image locally and exporting to GCP. This image is run on cloud to create containers.
o Requirement.txt: Contains python libraries needed for code execution. o Cloudbuild.yaml: Yaml configuration file specifying steps for build order.
   o curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.16.0/kind- windows-amd64
o Move-Item .\kind-windows-amd64.exe c:\kind\kind.exe
   
   - By running the following command on google cloud CLI, an image is built according to the yaml configuration file. This image is then exported our GCP project where a container of this image is run.
o gcloud builds submit --config configbuild.yaml . --timeout=10000
- The container created can be verified on GCP U.
- Create a Kubernetes cluster on GCP.
- Kubeflow pipelines can now be created in the pipeline section of AI Platform. Now you
can click on it, to open the Kubeflow UI.

## CODE ARTIFACTS:

LOCALHOST SERVER KUBERFLOW UI:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220133-e9c9aae4-a79f-4dc3-bbe0-bf5ca03a6dca.png">

GOOGLE CLOUD KUBERNETES KUBERFLOW UI:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220143-f5a28846-51b3-4f08-8c2d-a87639a9e2cb.png">

-	Creating a new pipeline taking .yaml file:
<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220166-5c9fe6b4-c761-4f36-a723-d565f3ca9c24.png">

-	Testing the pipeline!
<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220183-c4e5536a-7bf3-4732-b75b-81fbf7709787.png">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220184-fc361734-dbcb-4545-a971-319b9a072c4c.png">

-	Test Run (Finding the Accuracy)
<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220203-02c66c3a-1c49-48fa-95b7-51775f8dc54d.png">
<img width="500" alt="image" src="https://user-images.githubusercontent.com/11815663/211220206-3c413efc-db91-46f1-85f1-1dec92a86c5b.png">



