## PulsePoint Jersey 1.X

This is a temporary fork of Jersey 1.X (1.19-5) used strictly to get rid of shaded/repackaged ASM dependencies.
After Exchange migration to Jersey 2 this fork can be deprecated.

Because this is a temporary project, releases are done by hand:

### Building

`mvn -Paspectjrt-jdk8 -DskipTests -am -pl jersey-server,jersey-servlet clean package`

### Deploying

* Edit `~/.m2/settings.xml` to add a server called `thirdparty-releases`
* Deploy jetty-server
    ```
    mvn -Paspectjrt-jdk8 deploy:deploy-file -Durl=https://nexus.pulsepoint.com/repository/thirdparty-releases/ \
                           -DrepositoryId=thirdparty-releases \
                           -Dfile=jersey-server/target/jersey-server-1.20-SNAPSHOT.jar \
                           -DgroupId=com.sun.jersey \
                           -DartifactId=jersey-server \
                           -Dversion=1.19.5-PP-ASM7 \
                           -Dpackaging=jar \
                           -DgeneratePom=true
    ```

* Deploy jetty-servlet
    ```
    mvn -Paspectjrt-jdk8 deploy:deploy-file -Durl=https://nexus.pulsepoint.com/repository/thirdparty-releases/ \
                           -DrepositoryId=thirdparty-releases \
                           -Dfile=jersey-servlet/target/jersey-servlet-1.20-SNAPSHOT.jar \
                           -DgroupId=com.sun.jersey \
                           -DartifactId=jersey-servlet \
                           -Dversion=1.19.5-PP-ASM7 \
                           -Dpackaging=jar \
                           -DgeneratePom=true
    ```