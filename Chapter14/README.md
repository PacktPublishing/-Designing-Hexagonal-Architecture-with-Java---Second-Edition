# Chapter 14 - Setting up Dockerfile and Kubernetes Objects for Cloud Deployment
Following are the instructions to test the code samples.

Make sure you have Docker running before executing the following commands.

You need to run these commands from within the chapter 14 directory:

**To generate a Docker image with Uber Jar**
```
$ mvn clean package
$ docker build . -t topology-inventory
```
**To generate a Docker image with native executable**
```
$ mvn clean package -Pnative -Dquarkus.native.container-build=true -Dnative-image.xmx=6g
$ docker build . -t topology-inventory-native -f Dockerfile-native
```
**To start the container with Uber Jar**
```
docker run -p 5555:8080 topology-inventory
```
**To start the container with native executable**
```
docker run -p 5555:8080 topology-inventory-native
```
**To access the Dockerized application**
```
http://localhost:5555/q/swagger-ui/
```

**Testing Minikube from Windows**
```
minikube ssh "ip addr show eth0 | grep \"inet\b\" | awk '{print$2}' | cut -d/ -f1"
// 192.168.49.2
Open http://192.168.49.2:30080/q/health/ready in the browser
```