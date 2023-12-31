# Prerequisite 
You need a Ubuntu Linux to do this.

  An Ubuntu in Virtual Machine is okay.
# Video Tutorial

[YouTube](https://www.youtube.com/watch?v=VVfeuMWjQ5A)

# Instructions

1. Install docker

```
sudo apt install docker.io
# start docker daemon
sudo systemctl start docker
```

2. Install minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start
```

3. Train the model

Install dependencies first

```
sudo apt install python3-pip
pip install tensorflow numpy mnist keras
```

create [train.py](./train.py) file.

train the model
```
python3 train.py
```

4. Create an API service

Install FastAPI dependencies
```
pip install fastapi "uvicorn[standard]" Pillow
```

create [api.py](./api/api.py) file.

5. Build Docker image

First create an account on [Docker Hub](https://hub.docker.com)

And Create a repository called `digitreader`.

Notice that `zigzigcheers` shown below is my Docker Hub account name, be sure to replace it with your account name

```
docker build -t zigzigcheers/digitreader:v1 .
```

test if it works
```
docker run -d -p 8080:8080  zigzigcheers/digitreader:v1 
```

ok, let's push it to Docker Hub
```
docker push zigzigcheers/digitreader:v1
```

6. Deploy to Kubernetes Cluster

```
kubectl create deployment digitreader --image=zigzigcheers/digitreader:v1
kubectl expose deployment digitreader --type=LoadBalancer --port=8080
```

7. Next steps

Using AWS service to make it better

- [Amazon Polly](https://aws.amazon.com/polly/?nc2=type_a) - Text to Speach service
- [Amazon Translate](https://aws.amazon.com/translate/?nc2=type_a) - Translation service
