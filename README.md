# Scalable Airflow Setup Template
##### This repo's goal is to get you going fast and scalable with your Airflow on Kubernetes Setup.  

# Features

:baby: **Easy Setup**: Using cookiecutter to fill in the blanks.

:fire: **Disposable Infrastructure**: Using helm and some premade commands, we can destroy and re-deploy the entire infrastructure easily.

:rocket: **Cost-Efficient**: We use kubernetes as the tasks' engine. Airflow scheduler will run each task on a new pod and delete it upon completion. Allowing us to scale according to workload using the minimal amount of resources.

:nut_and_bolt: **Decoupled Executor**: Another great advantage of using Kubernetes as the task runner is - decoupling orchestration from execution. You can read more about it in [We're All Using Airflow Wrong and How to Fix It](https://medium.com/bluecore-engineering/were-all-using-airflow-wrong-and-how-to-fix-it-a56f14cb0753).

:runner: **Dynamically Updated Workflows**: We use Git-Sync containers. Those will allow us to update the workflows using git alone. No need to redeploy Airflow on each workflow change.  


## Installation

```console
$ cookiecutter https://github.com/talperetz/scalable-airflow-template

```

### Cookicutter Options Explained
* airflow_executor: You can use Kubernetes for execution with both Celery and Kubernetes as executors. To learn more checkout [Scale Your Data Pipelines with Airflow and Kubernetes](https://medium.com/@talperetz24)
* local_airflow_image_name: image name. required if you want to build your own Airflow image.
* airflow_image_repository: ECR repository link. required if you want to build your own Airflow image.
* git_repo_to_sync_dags: link to the scalable_airflow repository with your new workflows on github.
* git_username_in_base_64: 
You can convert strings to base64 via shell with:
```console
$ echo -n "github_username" | base64
```
* git_password_in_base_64: 
You can convert strings to base64 via shell with:
```console
$ echo -n "github_password" | base64
```
* fernet_key: 
You can fill fernet_key option with the response from this command: 
```console
$ python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
```


## Usage

### Prerequisites
```console
$ brew install kubectl
```
```console
$ brew install helm
```
* make sure your [kubectl context is configured to your EKS cluster](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html).

for custom Airflow image you'll also need: <br>
[Kubernetes cluster set with autoscaler](https://docs.aws.amazon.com/eks/latest/userguide/cluster-autoscaler.html)<br>
[ECR Repository for the docker image](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)<br>

It is also recommended to [set up Kubernetes Dashboard](https://aws.amazon.com/premiumsupport/knowledge-center/eks-cluster-kubernetes-dashboard/)

### Default Airflow Image
```console
$ make deploy
```
At this point you should see the stack deployed to kubernetes.<br>
To see Airflow's UI:

```console
$ make ui pod=[webserver-pod-name]
```
### Custom Airflow Image
After changing the config/docker/Dockerfile and scripts/entrypoint.sh<br> 
Build your custom airflow image<br>
```console
$ make build
```
Push to ECR
```console
$ make push
```
Deploy to Kubernetes
```console
$ make deploy
```    
To see Airflow's UI:

```console
$ make ui pod=[webserver-pod-name]
```
---

## Fine Tuning The Setup

This template uses:


**Airflow Helm Chart**: <a href="https://github.com/helm/charts/tree/master/stable/airflow" target="_blank">Airflow stable helm chart</a>

**Docker Image**: <a href="https://github.com/puckel/docker-airflow" target="_blank">https://github.com/puckel/docker-airflow</a>

for more details and fine tuning of the setup please refer to the links above.
 
---