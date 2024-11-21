https://linuxize.com/post/how-to-install-apache-maven-on-ubuntu-20-04/
https://www.vogella.com/tutorials/ApacheMaven/article.html

https://javakeypoint.wordpress.com/2020/08/18/difference-between-mvn-clean-package-and-mvn-clean-install/

apt update && apt install -y openjdk-11-jdk
java -version
apt update && apt install -y maven
mvn --version

 
 
 

https://github.com/spring-projects/spring-petclinic
https://github.com/mavrick202/spring-petclinic - Use this for Maven Testing

Good videos on Maven: https://www.youtube.com/watch?v=Xatr8AZLOsE

For maven dependencies: https://search.maven.org/
https://springframework.guru/spring-profiles/

To Start a new Java Springboot Project:
https://start.spring.io/



 

Use below step:
cd /opt
wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz 
tar xzvf apache-maven-3.8.4-bin.tar.gz 
mv apache-maven-3.8.4-bin.tar.gz  maven
echo 'export M2_HOME=/opt/maven' >> ~/.bashrc
echo 'export PATH=${M2_HOME}/bin:${PATH}' >> ~/.bashrc
source ~/.bashrc
mvn  –version

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

 


