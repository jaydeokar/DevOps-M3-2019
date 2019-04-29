# DevOps - Milestone 3: Deployment, Infrastructure and Special Component


**Team Members**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

**Contributions**
1. Production deployment: Bhavya Dwivedi
2. Feature flags: Jay Deokar
3. Infrastructure Upgrades (microservices+cluster): Gautam Worah
4. Something special: Suraj Kumar K P

**Deployment Components**
Following is the architecture that we have created :
We have one configuration server imlemented on Vagrant, Jenkins server running on an EC2 instance, Itrust Production server, Checkbox Production server deployed on an EC2 server. Also, for Infrastructure upgrade we have one Kubernetes cluster running on an EC2 instance with 2 slaves and one master.

![image](https://github.ncsu.edu/bdwived/Devops-Milestone3/blob/master/second.jpg)


**Deployment:** Deploy iTrust and checkbox.io to a production environment. Create a git hook on your jenkins server that will trigger a deployment when doing a git push to "production". The deployment needs to occur on actual remote machine (e.g. AWS, droplet, VCL), and not a local VM. The deployment should provision and configure the production environment using scripts + ansible.


**Implementation:** 

1. Update the variables in 'variables.yml' file with email password, aws pem file and your access tokens.
2. Run the playbook with sudo 'playbook.yml' from configuration server. This would create and set up a remote instance for Jenkins server with both ITrust and Checkbox applications installed and configured.
3. Once the playbook runs successfully, login to the Jenkins server.
4. cd CheckBoxCode/
5. Create a new file, add, commit and push to the repository. This would trigger a build on Jenkins server, post which the deployment at Production Checkbox Server would take place if the build passes successfully.
6. cd iTrustv-4/
7. Create a new file, add, commit and push to the repository. This would trigger a build on Jenkins server, post which the deployment at Production Itrust Server would take place if the build passes successfully.



**Feature Flags:** Create a configuration server for managing feature flags (using redis) that can be used to turn off/on features on iTrust application in production. Pick one feature to demo in screencast.

**Implementation:**

1. Open your browser and open the URL <IP of Itrust production server>:8080/iTrust2. This would open the Itrust web-page
2. Click on 'admin' user 
3. Click on 'Manage Drugs' on the menu bar
4. This feature has been used for demo purpose. 
 
 We have configured redis-cli for feature flag implementation. 
 You can turn on/off the feature by logging into the ITrust production server and then following these steps:
    redis-cli
    "set admin/drugs 'True'" or  "set admin/drugs 'False'"
 Refresh the 'Manage Drugs' page , you would see the feature turning on and off. 

**Infrastructure Components** 

**Infrastructure Upgrade Make improvements to the infrastructure of checkbox.io.**
Extract a new microservice for rendering markdown => html in checkbox.io. Deploy several instances of microservice (at least  3). Demonstrate service availabilty after turning off nodes. You may use a cluster such as nomad, kubernetes, or implement your own strategy. 

**Implementation:**
As shown above in the architecture diagram, we have created a Kubernetes cluster with 3 microservice instances (pods) each running 'markdown' service of Checkbox. The service availability would be ensured by the Kubernetes cluster. 
You can use the following commands to check the pods: 
kubectl get pods
![image](https://github.ncsu.edu/bdwived/Devops-Milestone3/blob/master/third.png)

As you can see from the screenshot above, if we delete one of the pods using 'kubectl delete pod <pod name>', the cluster would ensure service availability by terminating the specified pod and creating another one on its place seamlessly. 
 
 **Special Component**
 
 **Monitoring/Analysis**
 
 Why Monitoring?
 
 Monitoring helps you observe response times, availability, resource consumption levels, performance, as well as predict potential   issues. When you deploy and manage numerous of instances in cloud, you want them to be monitored regularly and manage their monitoring  through automation. Monitoring also helps to identity which servers are the most/least used with which we can Scale In/Out.
 
 **Tools Used:**  Grafana ( Visualization ) and AWS CloudWatch ( Monitoring )
 
 **Grafana**
 
Grafana is a Visualization and a monitoring tool used to plot various metrics on virtual machines running remotely on a data centre or Cloud. For this special milestone, we have used the opensource free version of Grafana to plot dashboards, visualize metrics that are being received from CloudWatch. The reason for using Cloudwatch is, it can monitor all the instances in any VPCs and Grafana is used to plot a unified dashboard of metrics from every application server and configuration server deployed and running. The Grafana application is installed and configured on the port 3000. The dashboard can be viewed at http://<public-ip of grafana server>:3000.

**AWS CloudWatch**

CloudWatch is a monitoring and management PaaS offered by AWS.  Here, we have used the free tier of AWS CloudWatch to monitor the servers that are being deployed on AWS. Every metric is polled with a configurable interval of 15s.

**Metrics Monitored:**

1)	**Average CPU Utilization:** CPU utilization is the proportion of the total available processor cycles that are consumed by each process.  It signifies how under/over utilised the server is by running/idle/waiting processes.  

2) **NetworkOut:** Average network egress traffic on a server. It is measured in MB/s. It signifies the network load on the server and gives us an understanding on how much traffic is flowing  out of the server. 

3) **StatusCheckedFailed_Instance:**   As defined by AWS, the value is 0 if the instance is passing the status checks and 1 if the status checks fails. During a status check, the health of the server is continuously polled by sending an ARP request. This metric indicates whether the server is online or offline.

![image](https://github.ncsu.edu/bdwived/Devops-Milestone3/blob/master/first.png)


 
 









































