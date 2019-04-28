# DevOps-Milestone3:Deploymemt,Infrastructure and Special Miletsone


**Team Members**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

**Contributions**
1. Production deployment: Bhavya Dwivedi
2. Feature flags: Jay Deokar
3. Infrastructure Upgrades (microservices+cluster): Gautam Worah
4. Something special: Suraj Kumar K P

**Implementation:**


**Deployment Components**
Following is the architecture that we have created :
We have one configuration server imlemented on Vagrant, Jenkins server running on an EC2 instance, Itrust Production server, Checkbox Production server deployed on an EC2 server . Also, for Infrastucture upgrade we have one Kubernetes cluster running on an EC2 instance with 2 slaves and one master.

**[DIAGRAM]**

**Deployment:** Deploy iTrust and checkbox.io to a production environment. Create a git hook on your jenkins server that will trigger a deployment when doing a git push to "production". The deployment needs to occur on actual remote machine (e.g. AWS, droplet, VCL), and not a local VM. The deployment should provision and configure the production environment using scripts+ansible.


**Implementation:** 

1. Update the variables in 'variables.yml' file with email password, aws pem file and your access tokens.
2. Run the playbook 'playbook.yml' from configuration server. This would create and set up a remote instance for Jenkins server with both ITrust and  Checkbox applications.
3. Once the runnning of playbook has completed, login to Jenkins server
4. cd CheckBoxCode/
5. Create a new file , add, commit and push to the repository. This would trigger a build on Jenkins server , post which the deployment at Production Checkbox Server would take place if the build passes successfully)
6. cd iTrustv-4/
7. Create a new file , add, commit and push to the repository. This would trigger a build on Jenkins server , post which the deployment at Production Itrust Server would take place if the build passes successfully)



**Feature Flags:** Create a configuration server for managing feature flags (using redis) that can be used to turn off/on features on iTrust in production. Pick one feature to demo in screencast.

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

**Infrastructure Components ** 
**Infrastructure Upgrade Make improvements to the infrastructure of checkbox.io.**
Extract a new microservice for rendering markdown => html in checkbox.io. Deploy several instances of microservice (at least  3). Demonstrate service availabilty after turning off nodes. You may use a cluster such as nomad, kubernetes, or implement your own strategy. 

**Implementation:**
As shown above in the architecture diagram, we have created a Kubernetes cluster with 3 microservice instances each running 'markdown' service of Checkbox. The service availability would be ensured by the Kubernetes cluster. 
You can use the following commands to check the pods: 
kubectl get pods
**[SCREENSHOT]**

As you can see from the screenshot above, once one of the pod have been deleted using 'kubectl delete pod <pod name>' , the cluster would ensure service availability by terminating the specified pod and creating another one on its place seamlessly. 
 
 









































