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
    main.yml        --> Parent playbook which runs the installation and configuration playbooks
Tasks done:

Using jenkins-job-builder and ansible, a jenkins pipeline has been built for two applications:

    checkboxbuild
    iTrust Build 

iTrust Build Job  --> **mvn -f pom-data.xml process-test-classes** builds the database and creates sample data and 
                      **mvn clean test verify checkstyle:checkstyle** runs the unit tests, launches the server, runs the integration tests
checkboxbuild Job -->                     

**To run the playbook**

Run the following command from an ansible server
        ansible-playbook -i inventory main.yml
where inventory contains the details of the web server host to be configured.

Learning Outcome

    Avoid bind exeception by killing the process with port conflict /ERROR:Address already in use
    Setting up Jenkins jobs using job builder and ansible.
    Cleaning up Jenkins workspaces before and after a jenkins build
    Integration of iTrust with mysql server
    


