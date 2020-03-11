.PHONY: build push deploy ns cwagent fluentd destroy restart kubedash ui clean  

#################################################################################
# GLOBALS                                                                       #
#################################################################################

##################################s###############################################
# COMMANDS                                                                      #
#################################################################################

build:
	docker build -t {{cookiecutter.local_airflow_image_name}}:latest -f config/docker/Dockerfile .
	
push:
	aws ecr get-login --no-include-email --region us-west-1 --no-verify-ssl | echo $($0)
	docker tag {{cookiecutter.local_airflow_image_name}}:latest {{cookiecutter.airflow_image_repository}}
	docker push {{cookiecutter.airflow_image_repository}}

ns:
	kubectl create namespace airflow;
	
deploy:
	kubectl apply -f config/kube/git-credentials.secret.yaml --namespace airflow
	kubectl apply -f config/kube/airflow-role-binding.yaml --namespace airflow
	helm install -f config/helm/charts/airflow-{{ cookiecutter.airflow_executor.lower() }}.yaml --namespace airflow airflow stable/airflow
	
cwagent:
	kubectl apply -f https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/cloudwatch-namespace.yaml
	kubectl apply -f https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/cwagent/cwagent-serviceaccount.yaml
	kubectl apply -f config/kube/cwagent-configmap.yaml
	kubectl apply -f https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/cwagent/cwagent-daemonset.yaml
	
fluentd:
	kubectl apply -f https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/cloudwatch-namespace.yaml
	kubectl create configmap cluster-info --from-literal=cluster.name=test-2 --from-literal=logs.region=us-west-2 -n amazon-cloudwatch
	kubectl apply -f https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/fluentd/fluentd.yaml
	
destroy:
	kubectl delete namespace airflow
	
restart:
	make destroy
	make ns
	make deploy

kubedash:
	kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep eks-admin | awk '{print $1}')
	kubectl proxy

ui:
	kubectl -n airflow port-forward $(pod) 8080:8080

clean:
	docker stop $(docker ps -a -q)
	docker rm -v $(docker ps -a -q)
	docker rmi $(docker images -a -q)