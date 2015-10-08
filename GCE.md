This gist shows how to setup the InvoicePlane application with kubernetes.

# Reqs
* Google cloud engine account
* This repo :-)

# TODO
Use replication controlers

# Inspired by
https://github.com/kubernetes/kubernetes/tree/master/examples/mysql-wordpress-pd


# Setup
Steps to create kubernetes pods from the InvoicePlane docker images

## Create cluster

## Load configuration
* gcloud
* kubectl

## Create disks
gcloud compute disks create --size=1GB mysql-disk
gcloud compute disks delete mysql-disk
gcloud compute disks create --size=1GB invoiceplane-disk


# Setup the application

## Create mysql pod & service
kubectl create -f mysql.yaml
kubectl create -f mysql-service.yaml

## Create wordpress pod & service
kubectl create -f invoiceplane.yaml
kubectl create -f invoiceplane-service.yaml

### Show active pods
kubectl get pods

### Show active services
kubectl get services

## Get external IP
gcloud compute forwarding-rules list
or
kubectl get services/invoiceplane-app

## Openup firewall so we can use invoice plane
gcloud compute firewall-rules create http --allow tcp:80

## Ip adres frontend
http://[result_from_above]

### More details on pods
kubectl describe pod mysql
kubectl describe pod invoiceplane-app


# Tear down
## Remove Pods and Services
kubectl delete -f invoiceplane.yaml
kubectl delete -f invoiceplane-service.yaml
kubectl delete -f mysql.yaml
kubectl delete -f mysql-service.yaml

* Remove cluster
