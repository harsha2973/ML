pg-1
sudo apt update
sudo apt install openjdk-21-jdk

Maven
sudo apt install maven
mvn --version

Gradle
sudo apt install gradle
gradle --version

pg-2
mvn archetype:generate -DgroupId=com.example -DartifactId=MyMavenApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

tree MyMavenApp
cd MyMavenApp

mvn archetype:generate -DgroupId=com.example -DartifactId=123 DarchetypeArtifactId=Maven-archetype-quickstart -Dinteractivemode=false

pom.xml:
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- Project Coordinates -->
    <groupId>com.example</groupId>
    <artifactId>BGSCET</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <!-- Properties: Customize Java version or plugin versions -->
    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <!-- Dependencies -->
    <dependencies>
        <!-- Example: JUnit dependency for testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <!-- Build: Configuring plugins and build settings -->
    <build>
        <plugins>
            <!-- Example: Maven Compiler Plugin to compile Java code -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>21</source>
                    <target>21</target>
                </configuration>
            </plugin>
            <!-- Example: Maven Surefire Plugin to run tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.1.2</version>
            </plugin>
        </plugins>
    </build>
</project>


mvn compile
mvn test
mvn package
mvn clean


pg-3:
mkdir HelloGradle
cd HelloGradle

gradle init --type java-application

gradle hello

GROOVY DSL
change the contents in build.gradle file:
plugins { 
// Apply the Java plugin for compiling Java code 
id 'java' 
// Apply the application plugin to add support for building an 
application 
id 'application' 
} 
group = 'com.example' 
version = '1.0' 
repositories { 
// Use Maven Central for resolving dependencies. 
mavenCentral() 
} 
dependencies { 
// Define your dependencies. For example, JUnit for testing: 
testImplementation 'junit:junit:4.13.2' 
} 
application { 
// Define the main class for the application. 
mainClass = 'com.example.App'  
} 
Devops lab manual 
// A custom task example: printing a greeting 
task hello { 
doLast { 
println 'Hello, Gradle!' 
}

KOTLYN DSL 
plugins { 
// Apply the Java plugin for compiling Java code 
java 
// Apply the application plugin to add support for building an 
application 
application 
} 
group = "com.example" 
version = "1.0" 
repositories { 
mavenCentral() 
} 

dependencies { 
// Define dependencies using Kotlin DSL syntax 
testImplementation("junit:junit:4.13.2") 
} 
application { 
// Set the main class for the application 
mainClass.set("com.example.App") 
} 
// A custom task example using Kotlin DSL 
tasks.register("hello") { 
doLast { 
println("Hello, Gradle with Kotlin DSL!") 
} 
} 

./gradlew hello
gradle build

gradle run

pg-04
mvn archetype:generate -DgroupId=com.example -DartifactId=HelloMaven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd HelloMaven
mvn package
java -cp target/HelloMaven-1.0-SNAPSHOT.jar com.example.App


B.
mkdir HelloMavenGradle
cd HelloMavenGradle
gradle init --type java-application
mkdir -p src/main/java/com/example
mkdir -p src/test/java/com/example
cp ../HelloMaven/src/main/java/com/example/App.java src/main/java/com/example/
cp ../HelloMaven/src/test/java/com/example/AppTest.java src/test/java/com/example/
nano build.gradle
application {
    mainClass = 'com.example.App'
}
gradle build/run


pg-5
sudo apt update
java -version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins

sudo systemctl start jenkins
sudo systemctl status jenkins

localhost:8080

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Install suggested plugins
enter user and passord
Save and Continue

pg-06
1. http://localhost:8080
Click “New Item”
name:Maven-CI or Gradle-CI
Select “Freestyle project”
Click OK
scm:git:repositoty
*/main
Scroll to “Build” → Add build step → Invoke top-level Maven targets Goals:clean package
 B. For Gradle
 Go to “Build” → Add build step → Invoke Gradle script
Tasks:clean build
6.Click “Save” ->Click “Build Now”
Click “New Item”
name:Maven-CI or Gradle-CI
Select “pipeline”
Click OK
scroll to the “Pipeline”->Pipeline script->choose try sample code ->save->build->build now-> console output




sudo apt install jenkins
sudo update-alternatives --config java
 sudo lsof -i :8080
 sudo systemctl start jenkins
 sudo cat /var/lib/jenkins/secrets/initialAdminPassword
