
# MAVEN MULTI PROFILE POM.XML EXAMPLE 

---

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
		 					 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>MavenTest</groupId>
    <artifactId>Profile</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

	<profiles>
			<profile>
			    <id>profile0</id>
			    <activation>
			        <activeByDefault>true</activeByDefault>
			    </activation>
			     <properties>
        				...........
    			</properties>
 				<dependencies>
		                ...........
		         </dependencies>
			    <build>
		         	<resources>
						<resource>
							<directory>src/main/resources</directory>
							<filtering>true</filtering>
						</resource>
					</resources>
            		<plugins>
            		 ........
            		  <!-- display active profile in compile phase -->
			            <plugin>
			                <groupId>org.apache.maven.plugins</groupId>
			                <artifactId>maven-help-plugin</artifactId>
			                <version>3.1.0</version>
			                <executions>
			                    <execution>
			                        <id>show-profiles</id>
			                        <phase>compile</phase>
			                        <goals>
			                            <goal>active-profiles</goal>
			                        </goals>
			                    </execution>
			                </executions>
			            </plugin>
            		 </plugins>
            	</build>
			</profile>

	        <profile>
		         <id>profile1</id>
		         <properties>
        				...........
    			</properties>
		         <dependencies>
		                ...........
		         </dependencies>
		         <build>
		         	<resources>
						<resource>
							<directory>src/main/resources</directory>
							<filtering>true</filtering>
						</resource>
					</resources>
            		<plugins>
            		 ........
            		  <!-- display active profile in compile phase -->
			            <plugin>
			                <groupId>org.apache.maven.plugins</groupId>
			                <artifactId>maven-help-plugin</artifactId>
			                <version>3.1.0</version>
			                <executions>
			                    <execution>
			                        <id>show-profiles</id>
			                        <phase>compile</phase>
			                        <goals>
			                            <goal>active-profiles</goal>
			                        </goals>
			                    </execution>
			                </executions>
			            </plugin>
            		 </plugins>
            	  </build>
			</profile>
			<profile>
		         <id>profile2</id>
		         <properties>
        				...........
    			</properties>
		         <dependencies>
		                ...........
		         </dependencies>
		         <build>
		         	<resources>
						<resource>
							<directory>src/main/resources</directory>
							<filtering>true</filtering>
						</resource>
					</resources>
            		<plugins>
            		 ........
            		  <!-- display active profile in compile phase -->
			            <plugin>
			                <groupId>org.apache.maven.plugins</groupId>
			                <artifactId>maven-help-plugin</artifactId>
			                <version>3.1.0</version>
			                <executions>
			                    <execution>
			                        <id>show-profiles</id>
			                        <phase>compile</phase>
			                        <goals>
			                            <goal>active-profiles</goal>
			                        </goals>
			                    </execution>
			                </executions>
			            </plugin>
            		 </plugins>
            	</build>
			</profile>
	<profiles>

</project>

```

### To Build 
* `$ mvn clean package 															     // profile0`
* `$ mvn -P profile1 clean package     or     $ mvn package package -D env=profile1  // profile1`
* `$ mvn -P profile2 clean package     or     $ mvn package package -D env=profile2  // profile2`
