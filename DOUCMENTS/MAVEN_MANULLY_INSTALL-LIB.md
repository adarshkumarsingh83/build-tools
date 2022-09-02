* c:/>mvn install:install-file -Dfile=[path-to-file with jar file name] -DgroupId=[group-id] \
    -DartifactId=[artifact-id] -Dversion=[version] -Dpackaging=[packaging]

```	
<dependency>
 <groupId>[group-id]</groupId>
 <artifactId>[artifact-id]</artifactId>
 <version>[version]</version>
</dependency>
```

* Exmaple
```
c:/>mvn install:install-file -Dfile=C:\ojdbc6.jar -Dpackaging=jar\ -DgroupId=com.oracle -DartifactId=ojdbc6 -Dversion=11.2.0.3
 
<dependency>
 <groupId>com.oracle</groupId>
 <artifactId>ojdbc6</artifactId>
 <version>11.2.0.3</version>
</dependency>
```
