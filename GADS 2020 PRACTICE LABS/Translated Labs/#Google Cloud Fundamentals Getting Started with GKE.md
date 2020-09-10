#### #Google Cloud Fundamentals: Getting Started with GKE 

#### ##Objectives:

In this lab, you will learn how to perform the following tasks

- Provision a kubernetes cluster using Kubernetes Engine
- Deploy and manage Docker Containers

#### ##Steps:

1. #### Start a Kubernetes Engine Cluster

   - For convenience we are going to create a variable of our assigned zone by quicklabs using the export command in the terminal, this will help us reference it easily later

     ###### 		

     ```
     	export MY_ZONE=us-central1-a
     ```

   - start a Kubernetes Cluster with two running nodes managed by kubernetes engine, name it webfrontend 

     ###### 	     

     ```
     gcloud container clusters create webfronted --zone $MY_ZONE --num-nodes 2
     ```

   - Check for the version of Kubernetes installed after cluster has been created

     ###### 	     

   ```
   	kubectl version
   ```

   - View running nodes in the gcp console, using cloud shell we can list all our instances in the project, these represent the nodes we provisioned

     ###### 	     

   ```
   	gcloud compute instances list
   ```

   

2. #### Run and deploy a container

   - From cloud shell, lets launch a single instance of the nginx container.

     ###### 		

     ```
     kubectl create deploy nginx --image=nginx:1.17.10
     ```

   - View the pod running the nginx container:

     ###### 	    

     ```
     kubectl get pods
     ```

   - Expose the nginx container to the Internet, this makes our application accessible via the internet:

     ###### 	     

     ```
     kubectl expose deployment nginx --port 80 --type LoadBalancer
     ```

   - view the new service:

     ###### 		 

     ```
     kubectl get services
     ```

   - Scale up the number of pods running on your service:

     ###### 	     

     ```
     kubectl scale deployment nginx --replicas 3
     ```

   - Confirm that Kubernetes has updated the number of pods:

     ###### 	     

     ```
     kubectl get pods
     ```

   - Confirm that your external IP address has not changed:

     ######          

     ```
     kubectl get services
     ```

     3. #### Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding. thats all for getting started with kubernetes engine

     

     Lab translation 

     by Colline Louis

     

     

