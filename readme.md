https://linuxize.com/post/how-to-install-apache-maven-on-ubuntu-20-04/
https://www.vogella.com/tutorials/ApacheMaven/article.html

https://javakeypoint.wordpress.com/2020/08/18/difference-between-mvn-clean-package-and-mvn-clean-install/

https://bitnami.com/stack/artifactory/cloud/aws

ami-0cd59ecaf368e5ccf (take this ami in ec2 instance)

 Use t2.medium and wait for 5 min to get the application started.
Default credentials can be found at /home/bitnami/bitnami_credentials


apt update && apt install -y openjdk-11-jdk
java -version
apt update && apt install -y maven
mvn --version
wget https://jfrog.bintray.com/artifactory/jfrog-artifactory-oss-6.9.6.zip
unzip -o jfrog-artifactory-oss-6.9.6.zip -d /opt/
cd /opt/artifactory-oss-6.9.6/
./bin/artifactory.sh start


http://ec2-3-238-191-242.compute-1.amazonaws.com:8081/ui/
Or
http://jfrog.awsb49.xyz:8081/ui/

The default logins are:
Username: admin
Password: password

1.	Once JFROG is done, login and go to Application->Artifactory->Artifacts
2.	Select libs-release-local and click on “Set Me Up” and scroll down and click on generate settings. Copy the contexts to /root/.m2/settings.xml.
3.	ONce copied replace ID and Password for both <id>central</id> and <id>snapshots</id>.

set new password to India@123
skip set base URL
skip configure default proxy 
select maven create repositories
next
finish
create repository
libs-release
  set me up
  libs-release-local
  enter password India@123
  update below in pom.xml file
<!-- <distributionManagement>
    <repository>
        <id>central</id>
        <name>libs-release</name>
        <url>http://jfrog.raghu.shop:8081/artifactory/libs-release-local</url>
    </repository>

    <snapshotRepository>
        <id>snapshots</id>
        <name>libs-snapshot</name>
        <url>http://jfrog.raghu.shop:8081/artifactory/libs-snapshot-local</url>
    </snapshotRepository>
 </distributionManagement> -->
  click generate settings
  take as settings.xml in vs code & copy into putty session cd /root/.m2/ folder update id as admin and password as India@123 in settings.xml

mvn clean install deploy

https://github.com/spring-projects/spring-petclinic
https://github.com/mavrick202/spring-petclinic - Use this for Maven Testing

Good videos on Maven: https://www.youtube.com/watch?v=Xatr8AZLOsE

For maven dependencies: https://search.maven.org/
https://springframework.guru/spring-profiles/

To Start a new Java Springboot Project:
https://start.spring.io/


git clone https://github.com/jenkins-docs/simple-java-maven-app.git
mvn validate
mvn compile
mvn test
mvn package
java -jar /root/simple-java-maven-app/target/my-app-1.0-SNAPSHOT.jar
nano /root/simple-java-maven-app/src/main/java/com/mycompany/app/App.java #Add Custom data

nano /root/simple-java-maven-app/src/test/java/com/mycompany/app/AppTest.java #Add Custom data.

mvn clean
mvn clean compile
mvn clean compile test package
mvn clean compile test package verify
mvn clean compile test package verify install
mvn clean compile test package verify install deploy
mvn package -Dmaven.test.skip=true

Copy the contents to a new file in vscode as settings.xml and update ID and Password shown below. 

Create a new file in /root/.m2/settings.xml and copy the above contents to it.

Update <distributionManagement> of the POM file as shown below. Replace URLs of the JFrog Servers.

Perform mvn clean package install deploy and following output must appear



How to increment artifact version

As of now everytime you run mvn clean deploy , it will create and push the package to jfrog with the same version which is 2.7.3. We can increment the version to avoid overwriting the artifacts.

https://medium.com/javarevisited/how-to-increment-versions-for-the-maven-build-java-project-a7596cc501c2

Add following code under the plugins:
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>build-helper-maven-plugin</artifactId>
        <version>3.2.0</version>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>versions-maven-plugin</artifactId>
        <version>2.8.1</version>
      </plugin>

We can set the version by running the command:
mvn versions:set -DnewVersion=1.0.0
mvn install deploy

mvn versions:set -DnewVersion=1.0.1
mvn install deploy

mvn versions:set -DnewVersion=1.0.2
mvn install deploy

sh "mvn versions:set -DnewVersion=Dev-1.0.${BUILD_NUMBER}"
sh "mvn package deploy"

sh "mvn versions:set -DnewVersion=Prod-${BUILD_NUMBER}"
sh "mvn package deploy"
-----------------------------------------------------------------------------------------
  #### azure devops ci cd pipeline #####
Packages Requried for Azure DevOps Agent:
- apt update
- Java 11
- Maven
- unzip jq net-tools
- Terraform
- Packer
- install docker & sudo usermod -a -G docker ubuntu
- AZ CLI
- AWS CLI
- Ansible, create configfile, disable host_key_checking
- trivy #https://github.com/aquasecurity/trivy/releases/tag/v0.41.0
  e.g: wget https://github.com/aquasecurity/trivy/releases/download/v0.57.1/trivy_0.57.1_Linux-64bit.deb

  dpkg -i trivy_0.57.1_Linux-64bit.deb

Run config.sh first and provide PAT token (go LinuxAgentPool agent -> go to user settings above right corner beside account name -> take personal access tokens and create) and then run svc.sh as given below.
sudo ./svc.sh install adminsree  #Adds systemd service
sudo ./svc.sh start


sudo systemd-resolve --flush-caches

1. Application CI/CD Pipeline
   - Sonarqube Scanning
   - Building
   - Publishing artifacts
   - Create COntainer image using the JAR
   - Push to AWS S3, Storage Account, Image to ACR and DockerHUB.
   - Deploy the container image as Azure ACI.
 
