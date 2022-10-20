# Atlas Installation  ![image info](./pictures/Atlas_small.png) 
Resources for installing OHDSI ATLAS using Docker containers.

## Preparation
### Configure the Database
Follow these [instructions](https://github.com/OHDSI/WebAPI/wiki/PostgreSQL-Installation-Guide) for preparing the PostgreSQL database.

### Build WebAPI app
In either a Linux or a [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) terminal:
* Install [Java 8](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html)
* Install [Apache Maven](https://maven.apache.org/download.cgi)
* Set the environment variable MAVEN_OPTS to prevent _out of memory_ errors with

		MAVEN_OPTS="-Xmx 1024"		
* Install [Git](https://gitforwindows.org/)
* Install Git Large File Systems (Git-LFS) with

		sudo apt update
		sudo apt install git-lfs

* Create a new directory `~/git/OHDSI` and `cd` to it.
* Download the latest version of WebAPI with

		git clone https://github.com/OHDSI/WebAPI.git
		git checkout refs/tags/v2.11.1
	
* Customize the WebAPI `settings.xml` file with the details of the PostgreSQL database as specified [here](https://github.com/OHDSI/WebAPI/wiki/WebAPI-Installation-Guide#configure-the-maven-profile).
* From the directory created by the `git clone` operation, (like `~/git/ohdsi/WebAPI`), build the [.war](https://www.geeksforgeeks.org/servlet-war-file/#:~:text=What%20is%20WAR%20File%3F,A%20file%20entitled%20web.) file with

		mvn clean package -DskipUnitTests -DskipITtests -s WebAPIConfig/settings.xml -P webapi-postgresql
		
* Upload the `~/git/OHDSI/WebAPI/target/WebAPI.war` file to the DBMI `AtlasInstallation` [repo](https://github.com/DBMI/AtlasInstallation).
 
## Installing for each user

### Linux

### Windows

#### Install in Docker container
* Install [Docker](https://docs.docker.com/get-started/).
* Install [Git](https://gitforwindows.org/).
* In a convenient subdirectory (perhaps `C:\Git\OHDSI`) clone the `AtlasInstallation` repo:

		git clone https://github.com/DBMI/AtlasInstallation.git
	
* In the `C:\Git\OHDSI\AtlasInstallation` directory, build the Docker container with

		docker build . -t atlas-installation

* Run the Docker image with

		docker run -d -p 8080:8080 atlas-installation		
* View the Atlas start page at