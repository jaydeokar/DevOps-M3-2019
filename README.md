# DevOps-Milestone3:Deploymemt,Infrastructure and Special Minetsone


**Team Members**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

**Contributions**
1. Production deployment: Bhavya Dwivedi
2. Feature flags: Jay Deokar
3. Infrastructure Upgrades (microservices+cluster): Gautam Worah
4. Something special: Suraj Kumar P

**Implementation:**


**Deployment Components**
Following is the architecture that we have created :
We have one configuration server imlemented on Vagrant, Jenkins server running on an EC2 instance, Itrust Production server, Checkbox Production server deployed on an EC2 server . Also, for Infrastucture upgrade we have one Kubernetes cluster running on an EC2 instance with 2 slaves and one master.

**[DIAGRAM]**

**Deployment:** Deploy iTrust and checkbox.io to a production environment. Create a git hook on your jenkins server that will trigger a deployment when doing a git push to "production". The deployment needs to occur on actual remote machine (e.g. AWS, droplet, VCL), and not a local VM. The deployment should provision and configure the production environment using scripts+ansible.


**Implementation:** 

1. Update the variables in 'variables.yml' file with Email password and your access tokens.
2. Run the playbook 'playbook.yml' from configuration server: this create and set up a rmote insatnce for Jenkins server with both ITrust and  Checkbox applications.
3. Once , the runnning of playbook has completed, login to Jenkins server
4. cd CheckBoxCode/
5. Create a new file , add, commit and push to the repository. This would trigger a build on Jenkins server , post which the deployment at Production Checkbox Server would take place if the Build passes successfully)
6. cd iTrustv-4/
7. Repeat step 6


**Feature Flags:** Create a configuration server for managing feature flags (using redis) that can be used to turn off/on features on iTrust in production. Pick one feature to demo in screencast.

**Implementation:

1. Open your browser and open the URL <IP of Itrust production server>:8080/iTrust2. This would open the Itrust web-page
2. Click on 'admin' 
3. Click on 'Manage Drugs' on the menu bar
4. This feature has been used for demo purpose. 
 
 We have configured redis-cli for feature flag implementation. 
 You can turn on/off the feature by logging into the ITrust production server and then following these steps:
    redis-cli
    "set admin/drugs 'True'" or  "set admin/drugs 'False'"
 Refresh the 'Manage Drugs' page , you would see the feature turning on and off. 
 
 







































