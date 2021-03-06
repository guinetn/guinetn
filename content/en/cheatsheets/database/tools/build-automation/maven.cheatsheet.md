---
title: maven.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Commands
#-#

#-# General command structure

mvn -P<profile> <command> <scope>


#-# Simple stuff

mvn help
mvn compile
mvn validate
mvn verify
mvn test
mvn clean
mvn clean package
mvn clean install
mvn clean deploy


#-#
#-# Dependencies
#-#

#-# Scope

Scope         Description
-----         -----------
compile       Compile dependencies are available in all classpaths of a project and are propagated to dependent projects. (default)
provided      Similar to compile, but indicates you expect the JDK or a container to provide the dependency at runtime.
runtime       Indicates that the dependency is not required for compilation, but is for execution. It is in the runtime and test classpaths, but not the compile classpath.
test          Indicates that the dependency is not required for normal use of the application, and is only available for the test compilation and execution phases.
system        This scope is similar to provided except that you have to provide the JAR which contains it explicitly. The artifact is always available and is not looked up in a repository.
import        Indicates that the specified POM should be replaced with the dependencies in that POM's <dependencyManagement> section. Since they are replaced, dependencies with a scope of import do not actually participate in limiting the transitivity of a dependency.


#-#
#-# Artifacts
#-#

mvn archetype:create                           # Create pom.xml

mvn archetype:create -DgroupId=<group> \       # Create JAR
                     -DartifactId=<new id>

mvn archetype:create -DgroupId=<group> \       # Create WAR
                     -DartifactId=<new id> \
                     -DarchetypeArtifactId=maven-archetype-webapp

mvn install:install-file <params>              # Install dependencies



#-#
#-# Releasing
#-#

mvn deploy:deploy-file <params ...>

# Useful release options:
#
#    -P <profile>
#    -Dusername=<user>
#    -Dpassword=<password>
#
mvn release:prepare
mvn release:clean
mvn release:perform



