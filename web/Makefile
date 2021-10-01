
#version = latest
#account = $(shell aws sts get-caller-identity --query "Account" --output text)
#repo = webapp

build:
	@docker build -t webapp.192614706870.dkr.ecr.us-east-1.amazonaws.com/webapp:latest .

push: login
	@docker push 192614706870.dkr.ecr.us-east-1.amazonaws.com/webapp:latest

login:
	@aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 192614706870.dkr.ecr.us-east-1.amazonaws.com
version = latest
account = $(shell aws sts get-caller-identity --query "Account" --output text)
repo = webapp

build:
	@docker build -t $(account).dkr.ecr.us-east-1.amazonaws.com/$(repo):$(version) .

push: login
	@docker push $(account).dkr.ecr.us-east-1.amazonaws.com/$(repo):$(version)

login:
	@aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $(account).dkr.ecr.us-east-1.amazonaws.com

deploy:
	@kubectl apply -f kubernetes/deployment.yaml
	@kubectl apply -f kubernetes/svc.yaml
