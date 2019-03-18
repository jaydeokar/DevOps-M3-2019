# DevOps-Milestone2 : Test And Analysis Milestone


**Team Members**

Bhavya Dwivedi (bdwived), Gautam Worah (gworah), Jay Deokar (jsdeokar), Suraj Kumar K P (skrish26)

**Contributions**
Automated test generation on Checkbox: Gautam Worah, Bhavya Dwivedi
Jenkins setup and Jacoco coverage: Gautam Worah ,Jay Deokar
iTrust Commit Fuzzer & Test prioritization: Jay Deokar,Bhavya Dwivedi
Report generation: Bhavya Dwivedi,Jay Deokar,Gautam Worah

**Coverage/Jenkins Support**
We have used Jacoco for coverage support 

**Automated Commit Generation - Commit Fuzzer**
We have created 2 files fuzzer.yml and fuzzAndCommit.yml. Their descriptions are below in the next section. 
**Some of our fuzzing operations:**
1. swap "<" with ">"
2. swap "==" with "!=" 
3. swap 0 with 1 
4. swap "++" with "--" 
5. swap "true" with "false"

**Test prioritization analysis**


**Analysis**
**iTrust:**
For iTrust, we have used FindBugs plugin for jenkins and we have extended the build job as reqquired to fail the Build if thresholds are violated. The changes for this have been done in pom.xml and /ansible-srv/jobs/iTrust.yml
Also, we have set the minimum testing criteria for 50% statement coverage as threshold and configured the build to fail on violating this threshold.

**CheckBox:**
For checkbox, we have main.js in the COmplexity repository which is being cloned for doing the complexity analysis of checkbox's code and would fail if the threshold for these custom metrics are violated. 
1. Max condition
2. Long Method
3. Freestyle: We did an analsis of if '==' or '!=' is being used to compare strings in the code. 


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
  
  3) [For esprima part](https://github.com/JARVIS1093/complexity)
 
Tasks done:

Using jenkins-job-builder and ansible, a jenkins pipeline has been built for two applications:

    checkboxbuild
    iTrust Build 
    
### Report:



### For ITrust Build:

We have configured Jenkins Job in such a way that it builds the project when a push is made to the git remote repository. We have included two static analysis tools FindBugs and Checkstyle and Jacoco plugin which calculates the statement coverage

We run **mvn -f pom-data.xml process-test-classes** which builds the database and creates a sample data.

Post this we run **mvn clean test verify checkstyle:checkstyle findbugs:findbugs** which runs the unit tests, launches the server, runs the integration tests, and then runs the static analysis checks.

We have also defined the thresholds in the jenkins job builder which fails the build based on the number of High Prirority warnings from Checkstyle, FindBugs or Code Coverage values from Jacoco report


                      
                      
checkboxbuild Job --> **npm test** starts the NodeJS server, tests the GET API at localhost:3002/api/study/listing , shuts down the server using pm2.                    

**To run the playbook ------**

Run the following command from an ansible server

```ansible-playbook -i inventory playbook.yml```

where inventory contains the details of the web server host to be configured.

