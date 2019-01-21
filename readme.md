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

F. Deploy application in Staging Environment
===================================
1. Install copy artifact and deploy to container plugin




