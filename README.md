# DevOps-Milestone1

**Team Members:**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

A jenkins server has been provisoned and configured through an ansible playbook. Along with Jenkins, iTrust, checkbox.io has also been installed and configured on the same server.

The following playbooks perform the mentioned functionalities.

    jenkins.yml     --> Installs and configures jenkins, jenkins job builder to build iTrust and checkbox.io.
    sqlinstall.yml  --> Installs and configures mysql server for iTrust
    javainstall.yml --> Installs Oracle Java 8
    mavenins.yml    --> Installs maven 
    itrust.yml      --> Clones iTrust from git repo, establishes the application and Database connection, runs maven tests for iTrust
    vars.yml 		    --> Paramter file for setting environmental variables


Tasks done:

Using a combination of jenkins-job-builder and ansible, jenkins build job for two applications:
A nodejs web application checkbox.io.
An "enterprise" Java system iTrust



Run the jenkins.yml file
Jenkins username: jenkins
Pwd: userPasswordDemo
