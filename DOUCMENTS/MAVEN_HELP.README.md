
## Create a Stand alone Project from Maven Template

```
$> mvn archetype:generate -DgroupId={project-package} 
   -DartifactId={project-name} 
   -DarchetypeArtifactId=maven-archetype-quickstart 
   -DinteractiveMode=false
```
* FOR EXAMPLE
```
$> mvn archetype:generate -DgroupId=com.adarsh.sample 
   -DartifactId=SampleApplication 
   -DarchetypeArtifactId=maven-archetype-quickstart 
   -DinteractiveMode=false
```

* D:\SampleApplication>tree/f
```
D:
SampleApplication
	│   pom.xml
	│
	└───src
		├───main
		│   └───java
		│       └───com
		│           └───adarsh
		│               └───sample
		│                       App.java
		└───test
			└───java
				└───com
					└───adarsh
						└───sample
								AppTest.java   
   
```   

## Create a Stand alone Project from Maven Template
``` 
$> mvn archetype:generate -DgroupId={project-packaging} 
	-DartifactId={project-name} 
	-DarchetypeArtifactId=maven-archetype-webapp 
	-DinteractiveMode=false	
```
* FOR EXAMPLE
```
$> mvn archetype:generate -DgroupId=MyWebAplication 
	-DartifactId=MyWebAplication 
	-DarchetypeArtifactId=maven-archetype-webapp 
	-DinteractiveMode=false
```	
* D:\MyWebAplication>tree/f
```
D:MyWebAplication
	├─── pom.xml
	│
	└───src
		└───main
			├───resources
			└───webapp
			    ├─── index.jsp
				│
				└───WEB-INF
						├───web.xml	
						
```
* D:\MyWebAplication>mkdir src\main\java\com\adarsh\servlet

* D:\MyWebAplication>tree/f
```
D:MyWebAplication
	├─── pom.xml
	│
	└───src
		└───main
			├───java
			│   └───com
			│       └───adarsh
			│           └───servlet
			├───resources
			└───webapp
				├─── index.jsp
				│
				└───WEB-INF
						├───web.xml					
```	

## Build Project With Maven
 
* $> mvn package


* Standalone application
```
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>SampleApplication</groupId>
	<artifactId>SampleApplication</artifactId>
	<packaging>jar</packaging>
	....
	....
</project>
```


* web application
```
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>MyWebAplication</groupId>
	<artifactId>MyWebAplication</artifactId>
	<packaging>war</packaging>
	....
	....
</project>
```	

### Clean Project With Maven
* $> mvn clean


### Install Your Project Into Maven Local Repository
* $> mvn install


### To create jar file or war file
* $> mvn package


### Run Unit Test With Maven
* $> mvn test


### Generate Documentation Site For Maven Based Project
* $> mvn site


### Deploy Maven Based War File To Tomcat

* Tomcat 7
    * Deploy URL = http://localhost:8080/manager/text
    * $>  mvn tomcat7:deploy

* Tomcat 6
    * Deploy URL = http://localhost:8080/manager/
    * $>  mvn tomcat6:deploy


### 1.1 Tomcat Authentication
* Add an user with roles manager-gui and manager-script.
* %TOMCAT7_PATH%/conf/tomcat-users.xml
```
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<user username="admin" password="password" roles="manager-gui,manager-script" /> 
</tomcat-users>
```

### 1.2 Maven Authentication
    * Add above Tomcat’s user in the Maven setting file, 
    * later Maven will use this user to login Tomcat server.

```
%MAVEN_PATH%/conf/settings.xml
--------------------------------

<?xml version="1.0" encoding="UTF-8"?>
<settings ...>
	<servers>
 
		<server>
			<id>TomcatServer</id>
			<username>admin</username>
			<password>password</password>
		</server>
 
	</servers>
</settings>
```

### 1.3 Tomcat7 Maven Plug-in
    * Declares a Maven Tomcat plug-in.
```
pom.xml

<project ...........>
	
	<plugin>
		<groupId>org.apache.tomcat.maven</groupId>
		<artifactId>tomcat7-maven-plugin</artifactId>
		<version>2.2</version>
		<configuration>
			<url>http://localhost:8080/manager/text</url>
			<server>TomcatServer</server>
			<path>/mkyongWebApp</path>
		</configuration>
	</plugin>
	
</project>	
```

* During deployment, it tells Maven to deploy the 
    * WAR file to Tomcat server via “http://localhost:8080/manager/text” 
      , on path “/myWebAplication“, using “TomcatServer” (in settings.xml) 
    * username and password for authentication.

### 1.4 Deploy to Tomcat
* Commands to manipulate WAR file on Tomcat.
    * $> mvn tomcat7:deploy 
    * $> mvn tomcat7:undeploy 
    * $> mvn tomcat7:redeploy


---

*  Sample Maven pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
		                     http://maven.apache.org/xsd/maven-4.0.0.xsd">
							 
    <modelVersion>4.0.0</modelVersion>

    <groupId>pm</groupId>
    <artifactId>pm</artifactId>
    <version>1.0-SNAPSHOT</version>

    <packaging>jar/war/ear</packaging>
    <name>pm</name>
    <url>http://maven.apache.org</url>

    <repositories>

        <repository>
            <id>maven2-repository.java.net</id>
            <name>Java.net Repository for Maven</name>
            <url>http://download.java.net/maven/2/</url>
        </repository>

        <repository>
            <id>JBoss repository</id>
            <url>http://repository.jboss.org/nexus/content/groups/public/</url>
        </repository>

    </repositories>

    <properties>
        <project.name>pm</project.name>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>1.7</java.version>
        <junit.version>4.8.1</junit.version>
    </properties>

    <dependencies>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>${junit.version}</version>
        </dependency>

    </dependencies>

    <build>
        <finalName>${project.name}</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                    <encoding>${project.build.sourceEncoding}</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>	
</project>

```
* ===============================EXECUTABLE JAR EXAMPLE ==================================

* D:\MySampleExecutableJar>tree/f
```
D:MySampleExecutableJar
		├─── pom.xml
		│
		└───src
			├───main
			│   ├───java
			│   │   └───com
			│   │       └───adarsh
			│   │           └───sample
			│   │                  ├─── ApplicationMain.java
			│   │
			│   └───resources
			│           ├───log4j.xml
			│
			└───test
				└───java

```
* ------------ApplicationMain.java----------------------------------
```
package com.adarsh.sample;

import org.apache.log4j.Logger;
public class ApplicationMain {

    private static final Logger logger = Logger.getLogger(ApplicationMain.class);
    public static void main(String[] args) {
      logger.info("\nApplication Main method started ");
        System.out.println("Welcome to Java Executable Jar Example");
      logger.info("\nApplication Main method ended ");
    }
}
```
* ------------------------------log4j.xml--------------------------------
```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern"
                value="%d [%t] %-5p %c %x %m%n"/>
        </layout>
    </appender>

    <appender name="FILE" class="org.apache.log4j.DailyRollingFileAppender">
        <param name="DatePattern" value="'.'yyyy-MM-dd"/>
        <param name="File" value="./logs/application.log"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern"
                value="%d [%t] %-5p %c %x %m%n"/>
        </layout>
    </appender>

    <logger name="com.adarsh.sample">
        <level value="INFO"/>
    </logger>

    <root>
        <level value="ERROR"/>
        <appender-ref ref="FILE"/>
        <appender-ref ref="CONSOLE"/>
    </root>

</log4j:configuration>
```
* -----------------------------pom.xml------------------------------------
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
		                     http://maven.apache.org/xsd/maven-4.0.0.xsd">

        <modelVersion>4.0.0</modelVersion>
        <groupId>MySampleExecutableJar</groupId>
        <artifactId>MySampleExecutableJar</artifactId>
        <version>1.0-SNAPSHOT</version>

        <packaging>jar</packaging>
        <name>MySampleExecutableJar</name>
        <url>http://maven.apache.org</url>

        <repositories>
            <repository>
                <id>maven2-repository.java.net</id>
                <name>Java.net Repository for Maven</name>
                <url>http://download.java.net/maven/2/</url>
            </repository>
            <repository>
                <id>JBoss repository</id>
                <url>http://repository.jboss.org/nexus/content/groups/public/</url>
            </repository>
        </repositories>

        <properties>
            <project.name>MySampleExecutableJar</project.name>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <java.version>1.7</java.version>
            <junit.version>4.11</junit.version>
            <log4j.version>1.2.17</log4j.version>
        </properties>

        <dependencies>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>${junit.version}</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>${log4j.version}</version>
            </dependency>
        </dependencies>

        <build>
            <finalName>${project.name}</finalName>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>2.3.1</version>
                    <configuration>
                        <source>${java.version}</source>
                        <target>${java.version}</target>
                        <encoding>${project.build.sourceEncoding}</encoding>
                    </configuration>
                </plugin>

                <!-- Make this jar executable -->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-jar-plugin</artifactId>
                    <configuration>
                        <!--<excludes>
                            <exclude>**/log4j.properties</exclude>
                        </excludes>-->
                        <archive>
                            <manifest>
                                <addClasspath>true</addClasspath>
                                <mainClass> com.adarsh.sample.ApplicationMain</mainClass>
                                <classpathPrefix>dependency-jars/</classpathPrefix>
                            </manifest>
                        </archive>
                    </configuration>
                </plugin>

                <!-- Copy project dependency -->
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-dependency-plugin</artifactId>
                    <version>2.5.1</version>
                    <executions>
                        <execution>
                            <id>copy-dependencies</id>
                            <phase>package</phase>
                            <goals>
                                <goal>copy-dependencies</goal>
                            </goals>
                            <configuration>
                                <!-- exclude junit, we need runtime dependency only -->
                                <includeScope>runtime</includeScope>
                                <outputDirectory>${project.build.directory}/dependency-jars/</outputDirectory>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>
    </project>
 ```   

* go inside the location where pom.xml is present
    * d:\MySampleExecutableJar\>	mvn clean
    * d:\MySampleExecutableJar\>	mvn compile
    * d:\MySampleExecutableJar\>	mvn install
    * d:\MySampleExecutableJar\>	mvn package
    * d:\MySampleExecutableJar\>	tree/f
    * D:\MySampleExecutableJar>tree/f

```
D:MySampleExecutableJar 
		├───pom.xml
		├───src
		│   ├───main
		│   │   ├───java
		│   │   │   └───com
		│   │   │       └───adarsh
		│   │   │           └───sample
		│   │   │                 ├───ApplicationMain.java
		│   │   └───resources
		│   │           ├───log4j.xml
		│   └───test
		│       └───java
		└───target
			├─── MySampleExecutableJar.jar
			├───classes
			│   │   log4j.xml
			│   └───com
			│       └───adarsh
			│           └───sample
			│                   ├───ApplicationMain.class
			├───dependency-jars
			│      ├───log4j-1.2.17.jar
			├───generated-sources
			│   └───annotations
			└───maven-archiver
					├───pom.properties
```

* D:\MySampleExecutableJar>java -jar target\MySampleExecutableJar.jar 
```
2014-12-11 17:58:51,834 [main] INFO  com.adarsh.sample.ApplicationMain
Application Main method started
Welcome to Java Executable Jar Example
2014-12-11 17:58:51,836 [main] INFO  com.adarsh.sample.ApplicationMain
Application Main method ended
```

### MAVEN WEB APPLICATION 
```
d:/>mvn archetype:generate -DgroupId=MyWebAplication 
	-DartifactId=MyWebAplication 
	-DarchetypeArtifactId=maven-archetype-webapp 
	-DinteractiveMode=false
	
d:/>cd MyWebAplication
D:\MyWebAplication>mkdir src\main\java\com\adarsh\servlet	
```

* pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
		                     http://maven.apache.org/xsd/maven-4.0.0.xsd">
							 
    <modelVersion>4.0.0</modelVersion>

    <groupId>MyWebAplication</groupId>
    <artifactId>MyWebAplication</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>MyWebAplication</name>
    <url>http://maven.apache.org</url>   

    <repositories>
        <repository>
            <id>maven2-repository.java.net</id>
            <name>Java.net Repository for Maven</name>
            <url>http://download.java.net/maven/2/</url>
        </repository>
        <repository>
            <id>JBoss repository</id>
            <url>http://repository.jboss.org/nexus/content/groups/public/</url>
        </repository>
    </repositories>

    <properties>
        <project.name>MyWebAplication</project.name>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>1.7</java.version>
        <junit.version>4.8.1</junit.version>
    </properties>

    <dependencies>
	    <dependency>
	       <groupId>javax.servlet</groupId>
	       <artifactId>servlet-api</artifactId>
	       <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>${junit.version}</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>${project.name}</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                    <encoding>${project.build.sourceEncoding}</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>	
</project>
```


* HelloWorldServlet.java
```
package com.adarsh.servlet;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloWorldServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)  
            throws ServletException, IOException {
        resp.getOutputStream().write("Hello World From Maven".getBytes());
    }
}
```

* web.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
                    http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">
  <servlet>
    <display-name>HelloWorldServlet</display-name>
    <servlet-name>HelloWorldServlet</servlet-name>
    <servlet-class>com.adarsh.servlet.HelloWorldServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>HelloWorldServlet</servlet-name>
    <url-pattern>/myServlet</url-pattern>
  </servlet-mapping>
</web-app>
```

* D:\MyWebAplication>tree/f
```
D:MyWebAplication
	│   pom.xml
	└───src
		└───main
			├───java
			│   └───com
			│       └───adarsh
			│           └───servlet
			│                   HelloWorldServlet.java
			├───resources
			└───webapp
				│   index.jsp
				└───WEB-INF
						web.xml
```

* D:\MyWebAplication>mvn clean 
* D:\MyWebAplication>mvn compile 
* D:\MyWebAplication>mvn install
* D:\MyWebAplication>mvn package


* D:\MyWebAplication>tree/f
```
D:MyWebAplication
│   pom.xml
├───src
│   └───main
│       ├───java
│       │   └───com
│       │       └───adarsh
│       │           └───servlet
│       │                   HelloWorldServlet.java
│       ├───resources
│       └───webapp
│           │   index.jsp
│           └───WEB-INF
│                   web.xml
└───target
    │   MyWebAplication.war
    ├───classes
    │   └───com
    │       └───adarsh
    │           └───servlet
    │                   HelloWorldServlet.class
    ├───generated-sources
    │   └───annotations
    ├───maven-archiver
    │       pom.properties
    │
    └───MyWebAplication
        │   index.jsp
        │
        ├───META-INF
        └───WEB-INF
            │   web.xml          
            ├───classes
            │   └───com
            │       └───adarsh
            │           └───servlet
            │                   HelloWorldServlet.class
            └───lib
                    junit-4.8.1.jar
                    servlet-api-2.5.jar
```