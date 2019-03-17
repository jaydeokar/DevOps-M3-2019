# DevOps-Milestone2 : Test And Analysis Milestone


**Team Members**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

A jenkins server has been provisoned and configured through an ansible playbook. Along with Jenkins, iTrust, checkbox.io has also been installed and configured on the same server.

The following playbooks perform the mentioned functionalities.

 1) jenkins.yml:
 
    Installs and configures jenkins, jenkins job builder to build iTrust and checkbox.io.
    
 2) sqlinstall.yml:
 
    Installs and configures mysql server for iTrust
    
 3) javainstall.yml:
 
    Installs Oracle Java 8
    
 4) mavenins.yml:
 
    Installs maven 
    
 5) itrust.yml:
 
    Clones iTrust from git repo, establishes the application and Database connection, runs maven tests for iTrust
    
 6) main.yml:
 
    Parent playbook which runs the installation and configuration playbooks
    
 7) fuzzer.yml:
 
    Clones TestPrioritizationAnalysis from the repository and then calls the fuzzAndCommit.yml n times(100) using a sequence. It also       runs the test prioritization analysis post the fuzzing and build and outputs the result in a file
    
 8) fuzzAndCommit.yml:
 
    Fuzzes the code, does a commit on the fuzzer branch and then pushes the code on remote repository. It waits till the execution of       the build is completed (failed/success) after which the repository is again brough back to the previous commit.
 
The following repositories have been used:

  1) [Test Prioritization Analysis](https://github.com/jaydeokar/TestPrioritizationAnalysis.git) 
     Has the functionality of carrying out test case analysis and priorititization by analyizing surefire-reports
  
  2) [Commit Fuzzing](https://github.com/gautamworah96/CommitFuzzing)
     Has the functionality of randomly commiting a change in the code based on some predefined operations.
  
  3) For esprima part
 
Tasks done:

Using jenkins-job-builder and ansible, a jenkins pipeline has been built for two applications:

    checkboxbuild
    iTrust Build 

### For ITrust Build:

We have configured Jenkins Job in such a way that it builds the project when a push is made to the git remote repository. We have included two static analysis tools FindBugs and Checkstyle and Jacoco plugin which calculates the statement coverage

We run **mvn -f pom-data.xml process-test-classes** which builds the database and creates a sample data.

Post this we run **mvn clean test verify checkstyle:checkstyle findbugs:findbugs** which runs the unit tests, launches the server, runs the integration tests, and then runs the static analysis checks.

We have also defined the thresholds in the jenkins job builder which fails the build based on the number of High Prirority warnings from Checkstyle, FindBugs or Code Coverage values from Jacoco report


                      
                      
checkboxbuild Job --> **npm test** starts the NodeJS server, tests the GET API at localhost:3002/api/study/listing , shuts down the server using pm2.                    

**To run the playbook ------**

Run the following command from an ansible server

```ansible-playbook -i inventory main.yml```

where inventory contains the details of the web server host to be configured.

**Learning Outcome ------**
    
**iTrust build:**

Avoid bind exeception by killing the process with port conflict /ERROR:Address already in use
Setting up Jenkins jobs using job builder and ansible.
Cleaning up Jenkins workspaces before and after a jenkins build
Integration of iTrust with mysql server

**Checkbox.io build:**

Setting up the Jenkins server with automated login, credentials etc
Setting up the checkbox.io app to start, stop automatically as part of a test using pm2
Modifying environment variables so that they are available immediately
    
 Screencast link for DevOps Milestone 1:
 [Milestone-1 Screencast](https://drive.google.com/file/d/1YAakDM-N1AfKEkKyH2UHsnNfi29OXASh/view?usp=sharing)
    
    
    
    
    
    
    
    


