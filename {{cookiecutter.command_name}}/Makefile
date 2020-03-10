.PHONY: build ecrpush docker-clean

#################################################################################
# GLOBALS                                                                       #
#################################################################################

PROJECT_DIR := $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))
PROJECT_NAME = supertools

##################################s###############################################
# COMMANDS                                                                      #
#################################################################################

build:
	docker build -t {{cookiecutter.command_name}}_cli:latest .
	
ecrpush:
	docker tag {{cookiecutter.command_name}}_cli:latest {{cookiecutter.ecr_uri}}/{{cookiecutter.command_name}}_cli
	docker push {{cookiecutter.ecr_uri}}/{{cookiecutter.command_name}}_cli

docker-clean:
	docker stop $(docker ps -a -q)
	docker rm -v $(docker ps -a -q)
	docker rmi $(docker images -a -q)
