#### #Google Cloud Fundamentals: Getting Started with Deployment Manager and Cloud Monitoring

#### ##Objectives:

In this lab, you will learn how to perform the following tasks

- Create a Deployment Manager deployment.
- Update a Deployment Manager deployment.
- View the load on a VM instance using Cloud Monitoring.

#### ##Steps:

1. #### Confirm that needed APIs are enabled

   - list all available APIs and services with command

     ###### 		

     ```
     	gcloud services list --available
     ```

   - Enable Cloud Monitoring API

     ###### 	     
     
     ```
     gcloud services enable cloudmonitoring.googleapis.com
     ```

2. #### Create a Deployment Manager deployment

   - place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE

     ###### 		

     ```
     export MY_ZONE=us-central1-a
     ```

   - download an editable Deployment Manager template:

     ###### 	    

     ```
     gsutil cp gs://cloud-training/gcpfcoreinfra/mydeploy.yaml mydeploy.yaml
     ```

   - use the sed command to replace the `PROJECT_ID` placeholder string with your Google Cloud Platform project ID

     ###### 	     

     ```
     sed -i -e "s/PROJECT_ID/$DEVSHELL_PROJECT_ID/" mydeploy.yaml
     ```

   - use the sed command to replace the `ZONE` placeholder string with your Google Cloud Platform zone

     ###### 		 

     ```
     sed -i -e "s/ZONE/$MY_ZONE/" mydeploy.yaml
     ```

   - View the `mydeploy.yaml` file, with your modifications

     ###### 	     

     ```
     cat mydeploy.yaml
     ```

   - Build a deployment from the template

     ###### 	     

     ```
     gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml
     ```

   - Confirm that the deployment was successful by listing VMs available

     ######          

     ```
     gcloud compute instances list
     ```

     3. ####  Update a Deployment Manager deployment

        - ​	 In Cloud Shell prompt. Launch the `nano` text editor to edit the **mydeploy.yaml** file:

     ```g
     nano mydeploy.yaml
     ```

     ###### 				

     - Find the line that sets the value of the startup script, `value: "apt-get update"`, and edit it to this:

       ```
       ###### 	value: "apt-get update; apt-get install nginx-light -y"
       
       ###### 	ctrl+o
       
       ###### 	ctrl+x
       ```

       ###### 	

       ######            

     - In Cloud Shell prompt. Update your deployment to install the new startup script by running the following command:

       ```
       gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml
       ```
       
       ###### 			

     

     in GCP console, on navigate to Compute Engine, Select VM instances and locate"my-vm", click into its detail and locate custom metadata section, confirm that the startup script has been updated to the value you declared in the deployment manager template.

     

     SSH into my-vm instance and stress load it, with the following command.

     ```
     dd if=/dev/urandom | gzip -9 >> /dev/null &
     ```

        

     ### 4. Create a Monitoring workspace

     You will now setup a Monitoring workspace that's tied to your Qwiklabs GCP Project. The following steps create a new account that has a free trial of Monitoring.

     1. In the Google Cloud Platform Console, click on **Navigation menu** > **Monitoring**.
     2. Wait for your workspace to be provisioned.

     When the Monitoring dashboard opens, your workspace is ready.

     Configure cloud monitroing trial and install both monitoring and logging agents on the vm created.

     SSH into vm and run folling commands to install monitoring agent.

     in the termial

     1.add the agents package repository:

     ```
     curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
     sudo bash add-monitoring-agent-repo.sh
     sudo apt-get update
     ```

     Install the agent, in this case install the major version that allows backward compatibility

     ```
     sudo apt-get install -y 'stackdriver-agent=
     major-version.*'
     ```

     Start the agent service

     ```
     sudo service stackdriver-agent start
     ```

     verify that the agent is running

     ```
     sudo service stackdriver-agent status
     ```

     

     

     

     

