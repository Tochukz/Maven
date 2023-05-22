# Maven By Example
__By SonarType__   
[sonatype.com](https://www.sonatype.com/)  
Maven is a build tool, a project management tool, an abstract container for running build tasks.

## Chapter 1: Introducing Apache Maven
Maven is a project management tool which encompasses a _project object model_, a set of standards, a project lifecycle, a dependency management system, and logic for executing plugin goals at defined phases in a lifecycle.

__Universal Reuse through Maven Plugins__  
The Maven Surefire plugin is the plugin that is responsible for running unit tests.  
Maven has plugins for everything from compiling Java code, to generating reports, to deploying to an application server. Maven has abstracted common build tasks into plugins which are maintained centrally and shared universally.  

__Comparing Maven with Ant__   
When you use _Ant_, you supply Ant with specific instructions for compiling and packaging your output. This is done in a _build.xml_ file.   
You have to tell Ant exactly where your source is, where you want the resulting bytecode to be stored, and how to package this all into a JAR file.  
In _Maven_, to create a JAR file from some Java source, all you need to do is create a simple _pom.xml_, place your source code in _${basedir}/src/main/java_ and then run `mvn install` from the command line.  
Running `mvn install` from the command line will process resources, compile source, execute unit tests, create a JAR, and install the JAR in a local repository for reuse in other projects. Without modification, you can run `mvn site` and then find an _index.html_ file in _target/site_ that contains links to JavaDoc and a few reports about your source code.  

## Chapter 2: Installing Maven  
Your only prerequisite is an installed Java Development Kit (JDK).   
Verify your Java Installation
```
$ java --version
```

__Installing Mavin on MacOS__  
__Method 1:__ Using Home Brew
```
$ brew install maven
$ mvn --version
```
__Method 2:__ Manual download
1. Download Maven for MacOS [Mavin Apache download](https://maven.apache.org/download.cgi). Download the _Binary tar.gz archive_ file.
2. After downloading, extract it using the below command.
```
$ tar -xvf apache-maven-3.9.2-bin.tar.gz
```
3. Set Maven Environment Variables - _M2_HOME_ and _Path_.   
Open `~/.zprofile` or `~/.bash_profile` depending on your OS shell.  
Append the following to the end of the file
```
export M2_HOME="/Users/tochukz/apache-maven-3.9.2"
PATH="${M2_HOME}/bin:${PATH}"
export PATH
```
I moved the extracted folder _apache-maven-3.9.2_ to my home directory, hence the _M2_HOME_ path  is `/Users/tochukz/apache-maven-3.9.2`.  
4. Close the terminal and reopen it. Then test `mvn`
```
$ mvn --version
```
The output should show maven home location, the JDK it’s using and also the Mac OS version details.  

Learn more [Maven on MacOS](https://www.digitalocean.com/community/tutorials/install-maven-mac-os)  

__Install Mavin on Windows using choco__  
If you dont already have _chocolatey_ installed, [setup and install chocolatey](https://docs.chocolatey.org/en-us/choco/setup).  

```
$ choco install mavin
$ mvn --version
```  
You may need to restart the terminal before running `mvn --version`.  

__Install Mavin on Linux__  
```
$ apt install mavin
$ mvn --version
```  

## Chapter 3: A Simple Maven Project
This chapter’s example project may be downloaded with the book’s example code at:
[books.sonatype.com/mvnex-book/mvnex-examples.zip](http://books.sonatype.com/mvnex-book/mvnex-examples.zip).    
Inside the unzip folder, the directory named _ch-simple_ contains the source code for this chapter.  

__Create a simple project__  
```
$ mvn archetype:generate -DgroupId=xyz.tochukwu.hellomav \
-DartifactId=hellomav \
-Dpackage=xyz.tochukwu.hellomav \
-Dversion=1.0-SNAPSHOT
```
A number of archetypes are available in Maven for anything from a simple application to a complex web application, and the archetype:generate offers a list of archetypes to choose from.

__Build and run__   
To build the project
```
$ cd hellomav
$ mvn install
```
To run the compiled program
```
$ java -cp target/hellomav-1.0-SNAPSHOT.jar xyz.tochukwu.hellomav.App
```  

__Effective POM__  
To see this _effective_ POM, run the following command in the project’s base directory.
```
$ mvn help:effective-pom
```
The effective POM, is a combination of settings from this project’s pom. xml, all parent POMs, a super-POM defined within Maven, user-defined settings, and active profiles.  

#### Core Concepts
