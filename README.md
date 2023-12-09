Jenkins
It is an open-source automation server. Jenkins helps automate parts of the software development process, particularly in building, testing, and deploying code.
Jenkins allows users to define and customize these stages based on their specific requirements. The pipeline is typically described in a Jenkins file, which is a text file written in a domain-specific language (DSL) that defines the steps and conditions of the pipeline.
Jenkins supports a wide range of plugins, which extend its functionality and allow integration with various tools and services. This extensibility makes Jenkins a popular choice for continuous integration and continuous delivery (CI/CD) pipelines in software development.
Stages in CI/CD
Continuous Download
Continuous Build
Continuous Deployment
Continuous Testing
Continuous Delivery
Developing a Jenkin-freestyle project :Hello World!
STEP-1
Launch three instances (dev-server, qa-server ,prod-server)—jenkins-key—security(Jenkins-sec-all-traffic)with all traffic
STEP-2
Connect the SSH connection of dev-server
“sudo apt update -y”
“sudo apt install openjdk-11-jdk -y”
sudo apt install maven git -y”
Now search for Jenkins prerequities—WAR file—latest Jenkins WAR—generic java package—copy link
"wget paste(above link)"
Ls
java -jar Jenkins.war
Copy the public_ip of dev-server and paste it in browser with the end “:8080”
Paste the password in Jenkins –continue—install.
STEP-3
Installing TOMCAT in qa-server & prod-server
Connect SSH connection of qa-server
“sudo apt update -y”
“sudo apt install tomcat9 -y”
“sudo apt install tomcat9-admin -y”
Copy public-ip of qa-server and paste it in browser with the end “:8080”(It works!)
“cd /etc/tomcat9”
“sudo nano tomcat-users.xml”
<user username="training" password="sherin" roles="manager-script,manager-status,manager-gui"/> (Ctrl O+Ctrl X)
“sudo systemctl restart tomcat9”
“sudo systemctl status tomcat9”
Copy public-ip of qa-server and paste it in browser with the end “:8080/manager”(give username and password -- signin)
STEP-4
Connect SSH connection of prod-server
“sudo apt update -y”
“sudo apt install tomcat9 -y”
“sudo apt install tomcat9-admin -y”
Copy public-ip of qa-server and paste it in browser with the end “:8080”(It works!)
“cd /etc/tomcat9”
“sudo nano tomcat-users.xml”
<user username="testing" password="sherin" roles="manager-script,manager-status,manager-gui"/> (Ctrl O+Ctrl X)
“sudo systemctl restart tomcat9”
“sudo systemctl status tomcat9
STEP-4
Jenkins is ready
Username-admin
Password-admin
Stage 1: Continuous Download START CI-CD
•	Job—development—freestyle project—OK
•	Click on source code management—select GIT—https://github.com/samiuddin-imaad/maven
•	Apply & save
•	Run the job
•	Check the console output
•	Connect to the dev server
•	Go to the location where code is downloaded
•	sudo su –
•	cd path of the folder
•	ls
Stage 2: Continuous Build
•	In this it will convert the java files into .war files
•	Development—configure
•	Goto build step
•	Add build step
•	Invoke top-level maven targets
•	Put goal name as package 
•	Apply & Save
•	Run the job
•	Check the console output
•	Copy the path of war file and check 
•	Go to the location where code is downloaded
•	sudo su –
•	cd path of the folder
•	ls
Stage 3: Continuous Deployment 
•	Here we need to deploy the war file into qa-server
•	Goto dashboard
•	Manage Jenkins—plugins—available Jenkins—deploy to container—select & install
•	Now development project—configure
•	Post build actions
•	Add post build action
•	Deploy war/ear to container
•	War/ear file (**/*.war)
•	Context path (qaenv)
•	Container (tomcat9)
•	Credentials (add-Jenkins-username(training)-password(sherin))
•	Select credential as training
•	give the private ip of the QA server.
•	http://private_ip:8080
•	Apply & Save
•	Run the job
•	To access
•	Public_ip of qa server with “:8080/qaenv”(Hello World!)
Stage 4: Continuous Testing
•	Create new job
•	Testing—freestyle project—OK
•	Source code management—GIT-- https://github.com/samiuddin-imaad/test-repo
•	Apply & Save
•	Run the job
•	Check the path in console output
•	Configure the testing job
•	Build action
•	Add build step
•	Execute shell
•	Command : “Test is passed”
•	Goto development job 
•	Configure
•	Post build actions
•	Add post build actions
•	Build other project
•	Project to build
•	Select testing project
•	Save
•	Copying artifacts from development job to testing job
•	The artifacts (war) created by the development job should be passed to the testing job so that the testing job can deploy that into tomcat in the prod environment.
•	Dashboard—manage Jenkins-plugins—available plugin—“copy artifacts”—select—install
Stage 5: Continuous Delivery
•	Development—configure
•	Post build actions
•	Add post build actions
•	“archive the artifacts”
•	**/*.war
•	Apply &  save
•	Testing project—configure
•	Build actions
•	Add build actions
•	“copy artifacts from another project”
•	Enter development project name
•	Post build actions
•	Add post build actions
•	deploy war/ear to a container
•	**/*.war  (war/ear )
•	Context path (proden)
•	container 
•	tomcat 9
•	Credentials
•	private ip:8080 of the prod server
•	Apply and save
•	Run the job
•	Copy the public_ip of prod-server in browser with “:8080/prodenv”(Hello World)
•	Successfully you have got the output.












 













