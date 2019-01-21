Jenkins Details:

http://localhost:8070/

Username/password: root/root


Tomcat details
---------------
http://localhost:8080/


Sonarqube details
---------------
http://localhost:9000/
admin/admin
Token:   Ashish: 62ca0c020ebcdedb4f12304813255072a0143f2c



Springboot Application details
---------------
http://localhost:8090/


JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
M2_HOME=/usr/share/maven


A. Installation needed
===================
1. JDK, 
2. Maven
3. Git
4. github plugin in jenkins

B. Configuration in Jenkins needed
================================
1. Manage Jenkins -> Global Tool Configuration (define jdk, git and maven path)

C. Create a maven project
======================
1. Jenkins home->New Item-> Project name (first-cicd) -> Free style project
2. Add description
3. Add source code location. (github is a public repository so credentials are not needed)
	https://github.com/ashismo/cicd.git
4. Go to the build section. Select "invoke top-level maven target". Enter maven version from Steps B.
5. Save the changes

D. Build the project
====================
Click on the build button next to the project name


E. SCM Poll build
===================
As github is the public account so no need to add password against the github URL. Keep Credential to none.

F. Tomcat configuration
==================
1. Add executon permission to the scripts inside the bin folder
2. Modify tomcat-users.xml file and set password as "tomcat". Modified section looks like this

<role rolename="manager-script"/>
  <role rolename="admin-gui"/>
  <user username="tomcat" password="tomcat" roles="manager-script,admin-gui"/>

G. Deploy application in Staging Environment
===================================
1. Install "copy artifact" and "deploy to container" plugin
2. Create another free style project called -> "Deploy to staging". Then Go to build tab and select dropdown "Copy artifacts from another project". 
		Artifact to copy: **/*.war
3. Post build Actions: Deploy WAR/EAR to a container -> WAR/EAR files: **/*.war
	Select tomcat as container and enter username and password as menioned in tomcat-users.xml
4. Open first-cicd project and add post build action -> Build other project -> deploy-in-staging


AS OF NOW ---- THE UPSTREAM JOB : first-cicd and DOWNSTREAM JOB: deploy to staging

H. Jenkin pipeline for multiple projects dependencies
=======================================
Plugin needed:  Build Pipeline Plugin

+ button will be available next to main tab i.e. "All" tab where all projects get displayed.

I. Jenkins pipeline for staging and production 
==================================
We already created Jenkins pipeline for staging. Now, we shall repeat the same thing in production. The only difference is, the production job will not be triggered automatically. 
So the "Post-build Actions" of the Jenkins-pipeline-Staging should include "deploy-to-production" project. The dropdown value should be "Build other project (Manual step)"


J. Code-based pipeline
===================
Jenkin code-based pipeline is written in Groovy

1. Plugin needed: Pipeline. Check under manage plugin->installed tab:if this is present.
2. Create a project of tye "pipeline project". Say the name of the project is "Code-based Pipeline"
3. Enter the description of the project and go to the pipeline tab. Definition of the pipeline would be "Pipeline scripts from SCM". Enter the respository URL.
4. Add Jenkinsfile in the root path of the project.




