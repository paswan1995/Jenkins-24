# Build

# Maven is Build tool 
 
* __Make__: 

 * This is a first generation build tool which has automated building of c and c++ projects.
 * The build steps are configured in a file which is called as Makefile
 * To work with maven we need the pom.xml (Project object model)  ---For writing this pom.xml writing this there is schema this written by Developer we dont need to write this .

* __Apache Ant__:
 
  * This is a build tool majorly used in Java Projects for building packages
  * The build steps are configure in a file called as build.xml

* __Apache Maven__:

  * Maven is a build tool used for java and java based languages (Groovy and Scala).
  * Maven belives in convention over configuration
  * Maven helps in
    * Building 
    * Testing
    * Packaging 
    * managing dependencies.

  * Maven has a standard directory layout 
  * Maven has archetypes using which we can generate folder structures with sample code.
  * To Write this pom.xml need to define projectlike

# Setup Maven

 * Maven relies on java, so java should be installed
 
 ```
 sudo apt update
 sudo apt install openjdk-17-jdk -y
 ```

 # Project Object Model 

  * [Refer](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)
  
* Lets use untar approach to install maven (3.9.8)
* reference article
[Refer](https://www.digitalocean.com/community/tutorials/install-maven-linux-ubuntu)
 
 * Simple pom.xml
 * Any java base project we can use maven. in this project we need to do change we want:
````
 * Simple Pom.xml
<project>
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>io.lerningthoughts.app</groupId> # Name of organisation or group
  <artifactId>hello-maven</artifactId> # Artifact id means what the project about.
  <version>1.0.0-SNAPSHOT</version>            # SNAPESHOT  means this project is under develop | RELEASE means this project is complited.
</project>
````
# This Above content in the pom.xml file .
# so we  using java programing language so the second file should be in src\main\java\io\learningthoughts\devops\main.java.




### Distributed Build: 
   
   * A distributed build is a process where the tasks involved in building software—such as compiling code, running tests, or packaging artifacts—are divided and executed across multiple machines or nodes in a network. This approach is designed to speed up the build process, especially for large codebases or complex projects, by leveraging parallel processing and optimizing resource utilization

##  To Add Other nodes to Jenkins master node othernode need openjdk-17-java install

##  To Configur Other node With Jenkins node add other node '`private ip` all three nodes are on same network os use private ip' 
  * For This We use `ssh -i jenkins.pem ubuntu@<private_Ip_of_othernode>` and for this we need this [.pem] which install on local system need this on jenkins system node.
  * So add this [.pem] file go in jenkins master Dashboard and to changes 
          * Location ware to add --->  `Dashboard>Manage jenkins>Credentials>System>Global credentials(unrestricted)`


  [After_This_We_get_the_key_file_which_we_save_in_the_local_node_Till_this_We_just_added_pemfile_key]


## Now Add the Nodes bases on that .pem file key

  * Location Ware to add --> `DashBoard > Manage jenkins > Nodes > New node`



## After Add .pem File on the jenkins master node and also after adding the node to it Now Perform some build on the nods

# This Following Task for `spc node`

  * using the lable we need to build the project in node

  * Creat a Freestyle project 1st >>> it take you in Configuration >>> General 
    `Restrict where this project can be run ?` In this session mention the label.\

# This Following Task for `Nop node` 

  * Same Create One new Project for Nop node  With dotenet  create a new log view name of freestyle nop-freestyle >> Configuration

  * In Configuration build the code  From git 

# To create Artifact of build This get install in nop node 


  * To Create a Artifact fo the build go in Build Step > Execute shell 
      In that shell run this command `mkdir published `
                                     `ndotnet publish -c Release src/Presentation/Nop.Web.csproj -o ./published/` Try to move your output here.

    * Now Mention this published folder in Archive the  rtifacts in post-build Action.
          `published/*`  -> it means add any thing

  * It's Artifacts create hole folder we need to zip those folder
  Install zip if its not install 

  * It create a Artifacts of nop-freestyle in  published folder So zip those file inside published folder. from terminal using command `zip -r Nop.Web.Zip published/`

  * Create a new to delete the workspace and also include this commad in the Execute shell `zip -r Nop.web.zip published folder/` ans archive Nop.web.zip


# Maven Lifecycle 
  
   ```
     validate
     compile 
     test 
     package 
     install 
     deploy  
     
   ```

# Information about maven 

 * Maven will create a folder called as target and add all artifacts into it.
 * clean step removes the target folder
 * When we install maven in the home directory (C:\Users<username>\ or /home/created).
 * This .m2 folder will have all the dependencies downloaded over here and is also referred as local repository.
 
 * In maven we deal with 3 repositories
    * local
    * remote
    * central 

![](images/1.jpg)

# Building Sample Project

  * we have installed jdk 17
  * Lets build [Refer](https://www.geeksforgeeks.org/installation-guide/how-to-install-openjdk-in-linux/)
  
```
git clone https://github.com/jenkins-docs/simple-java-maven-app.git
cd simple-java-maven-app
mvn validate 
mvn compile 
mvn test 
mvn package 
```

# Lets build spring pet clinic

```
 history
    1  sudo apt update

    2  sudo apt install openjdk-17-jdk -y
      right click on link and copy link and then  `wget https://dlcdn.apache.org/maven/maven-3/3.9.11/binaries/apache-maven-3.9.11-bin.tar.gz`

    4  sudo tar -xvzf apache-maven-3.9.11-bin.tar.gz -C /opt/
    5  cd /opt
    6  sudo ln -s apache-maven-3.9.11 apache-maven
    7  sudo nano /etc/profile.d/maven.sh
      ```
      export M2_HOME=/opt/apache-maven
      export MAVEN_HOME=/opt/apache-maven
      export PATH=${M2_HOME}/bin:${PATH}

      ```
    8  ls
    9  sudo chmod +x /etc/profile.d/maven.sh
   10  source /etc/profile.d/maven.sh
   11  mvn -version
   12  cd
   13  mvn -version
   14  ls
   15  history
```
![](images/5.jpg) 

``` 
do this in terminal
-------------------

git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
mvn clean package 
```
![](images/2.jpg)

![](images/3.jpg)

![](images/4.jpg)


| Command             | Lifecycle Phase  | What It Does                                                           | Output/Effect                                       |
|---------------------|------------------|-----------------------------------------------------------------------|-----------------------------------------------------|
| `mvn validate`      | validate         | Checks project structure and config (like `pom.xml`)                  | Detects config errors early                         |
| `mvn compile`       | compile          | Compiles source code in `src/main/java`                               | `.class` files in `target/classes`                  |
| `mvn test-compile`  | test-compile     | Compiles test code in `src/test/java`                                 | Test `.class` files in `target/test-classes`        |
| `mvn test`          | test             | Runs unit tests after compiling test code                             | Test result reports                                 |
| `mvn package`       | package          | Packages compiled code as JAR or WAR file                             | JAR/WAR in `target/`                                |
| `mvn verify`        | verify           | Runs additional checks (integration tests, etc.)                      | Optional checks completed                           |
| `mvn install`       | install          | Installs artifact to your local Maven repository (`~/.m2/repository`) | Can be used as a dependency locally                 |
| `mvn deploy`        | deploy           | Uploads artifact to a remote Maven repository                         | Used for releases/distribution                      |
| `mvn clean`         | clean            | Removes the `target` directory and build artifacts                    | Cleans up all generated files                       |
                     |

![Preview](images/7.jpg)
![Preview](images/8.png)
![](images/6.jpg)


# Multi-project model: 

* Try building game-of-life : [Refer](https://github.com/wakaleo/game-of-life.git)

* __References:__ 
 * Libraries: Library is a reusable code. Libraries are of two types
   * static library:
   * dynamic library:
 
 * Dependency: Dependency at a source code level, means relying on libraries to acheive some funtionility. 

* Modern build tools
   * build code 
   * dependency management
   * artifact versioning and storage support

