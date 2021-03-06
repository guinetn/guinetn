---
title: gradle.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Command line
#-#

gradle [option...] [task...]

#-# Options

Option                   Description
------                   -----------
-?, -h, --help           Shows a help message.
-a, --no-rebuild         Do not rebuild project dependencies.
--all                    Shows additional detail in the task listing.
-b, --build-file         Specifies the build file.
-c, --settings-file      Specifies the settings file.
--console                Specifies which type of console output to generate (plain/auto/rich).
--continue               Continues task execution after a task failure.
--configure-on-demand    Only relevant projects are configured in this build run.
-D, --system-prop        Sets a system property of the JVM, for example -Dmyprop=myvalue.
-d, --debug              Log in debug mode (includes normal stacktrace).
-g, --gradle-user-home   Specifies the Gradle user home directory (defaults to ~/.gradle).
--gui                    Launches the Gradle GUI.
-I, --init-script        Specifies an initialization script.
-i, --info               Set log level to info.
-m, --dry-run            Runs the build with all task actions disabled.
--offline                Specifies that the build should operate without accessing network resources.
-P, --project-prop       Sets a project property of the root project, for example -Pmyprop=myvalue.
-p, --project-dir        Specifies the start directory for Gradle (defaults to current directory).
--parallel               Build projects in parallel.
--max-workers            Sets the maximum number of workers that Gradle may use.
--profile                Profiles build execution time and generates a report in the buildDir/reports/profile directory.
--project-cache-dir      Specifies the project-specific cache directory (defaults to .gradle in the root project dir).
-q, --quiet              Log errors only.
--recompile-scripts      Forces scripts to be recompiled, bypassing caching.
--refresh-dependencies   Refresh the state of dependencies.
--rerun-tasks            Specifies that any task optimization is ignored.
-S, --full-stacktrace    Print out the full (very verbose) stacktrace for any exceptions.
-s, --stacktrace         Print out the stacktrace also for user exceptions (e.g. compile error).
-t, --continuous         Enables continuous building - Gradle will automatically re-run when changes are detected.
-u, --no-search-upwards  Don't search in parent directories for a settings.gradle file.
-v, --version            Prints version info.
-x, --exclude-task       Specifies a task to be excluded from execution.


#-# Tasks

Task                     Description
----                     -----------
projects                 List the sub-projects of the selected project, displayed in a hierarchy.
tasks                    List the main tasks of the selected project.


#-# Environment variables

Variable                 Description
--------                 -----------
GRADLE_OPTS              Specifies command-line arguments to use to start the JVM.
GRADLE_USER_HOME         Specifies the Gradle user home directory (defaults to ~/.gradle).
JAVA_HOME                Specifies the JDK installation directory to use.



#-#
#-# Plugins
#-#

#-# Usage

apply plugin: '<plugin-name>'


#-# Base plugins

Plugin             Description
-----              -----------
base               Adds the standard lifecycle tasks and configures reasonable defaults for the archive tasks.
java-base          Adds the source sets concept to the project. Does not add any particular source sets.
groovy-base        Adds the Groovy source sets concept to the project.
scala-base         Adds the Scala source sets concept to the project.
reporting-base     Adds some shared convention properties to the project, relating to report generation.


#-# Language plugins

Plugin             Auto applies       Description
-----              ------------       -----------
java               java-base          Adds Java compilation, testing and bundling capabilities to a project.
groovy             java, groovy-base  Adds support for building Groovy projects.
scala              java, scala-base   Adds support for building Scala projects.
antlr              java               Adds support for generating parsers using Antlr.
assembler          -                  Adds native assembly language capabilities to a project.
c                  -                  Adds C source compilation capabilities to a project.
cpp                -                  Adds C++ source compilation capabilities to a project.
objective-c        -                  Adds Objective-C source compilation capabilities to a project.
objective-cpp      -                  Adds Objective-C++ source compilation capabilities to a project.
windows-resources  -                  Adds support for including Windows resources in native binaries.


#-# Integration plugins

Plugin             Auto applies       Description
-----              ------------       -----------
application        java, distribution Adds tasks for running and bundling a Java project as a command-line application.
ear                -                  Adds support for building J2EE applications.
jetty              war                Deploys your web application to a Jetty web container embedded in the build.
maven              -                  Adds support for publishing artifacts to Maven repositories.
osgi               java-base          Adds support for building OSGi bundles.
war                java               Adds support for assembling web application WAR files.


#-# Java Plugin

Task name             Description
---------             -----------
compileJava           Compiles production Java source files using javac.
processResources      Copies production resources into the production classes directory.
classes               Assembles the production classes directory.
compileTestJava       Compiles test Java source files using javac.
processTestResources  Copies test resources into the test classes directory.
testClasses           Assembles the test classes directory.
jar                   Assembles the JAR file
javadoc               Generates API documentation for the production Java source, using Javadoc
test                  Runs the unit tests using JUnit or TestNG.
uploadArchives        Uploads artifacts in the archives configuration, including the JAR file.
clean                 Deletes the project build directory.
cleanTaskName         Deletes files created by specified task.
assemble              Assembles all the archives in the project.
check                 Performs all verification tasks in the project.
build                 Performs a full build of the project.
buildNeeded           Performs a full build of the project and all projects it depends on.
buildDependents       Performs a full build of the project and all projects which depend on it.
buildConfigName       Assembles the artifacts in the specified configuration.
uploadConfigName      Assembles and uploads the artifacts in the specified configuration.

# Directory structure convention
src/main/java           // Production Java source
src/main/resources      // Production resources
src/test/java           // Test Java source
src/test/resources      // Test resources
src/sourceSet/java      // Java source for the given source set
src/sourceSet/resources // Resources for the given source set

# Customize directory structure
sourceSets {
  main {
    java {
      srcDir 'src/java'
    }
    resources {
      srcDir 'src/resources'
    }
  }
}



#-#
#-# Repositories
#-#

repositories {
  // Maven central repository
  mavenCentral()

  // Remote Maven repository
  maven {
    url "http://repo.mycompany.com/maven2"
  }

  // Remote Maven repository with authentication
  maven {
    credentials {
      username "user"
      password "password"
    }
    url "http://repo.mycompany.com/maven2"
  }

  // Ivy repository
  ivy {
    url "http://repo.mycompany.com/repo"
  }

  // Local repository
  flatDir {
    dirs "libs"
  }
}



#-#
#-# Dependencies
#-#

#-# Dependency scopes

Scope          Description
-----          -----------
compile        Dependencies required to compile the production source of the project.
runtime        Dependencies required by production classes at runtime. Also includes the compile time dependencies.
testCompile    Dependencies required to compile the test source of the project. Also includes the compiled production classes and the compile time dependencies.
testRuntime    Dependencies required to run the tests. Also includes the compile, runtime and test compile dependencies.


#-# Module dependencies

# Declaring dependencies with group-name-version strings
dependencies {
  compile 'org.apache.solr:solr-core:1.4.1'
  compile 'org.springframework:spring-core:3.0.5'
  testCompile 'junit:junit:4.8'
}

# Declaring dependencies with Groovy map syntax
dependencies {
  compile group: 'org.apache.solr', name: 'solr-core' version: '1.4.1'
  compile group: 'org.springframework', name: 'spring-core', version: '3.0.5'
  testCompile group: 'junit', name: 'junit', version: '4.8'
}


#-# Dynamic versions

dependencies {
  compile 'org.springframework:spring-core:3.0.+'
  testCompile 'junit:junit:4.8+'
}


#-# File dependencies

# Declaring a dependency explicitly on a locally managed module
dependencies {
  compile files('lib/hacked-vendor-module.jar')
}

# Depending recursively on all of the files under lib
dependencies {
  compile fileTree('lib')
}


#-# Project dependencies

# Declaring dependencies on subprojects
dependencies {
  compile project(':projectA')
  compile project(':projectB')
}

# Declaring an explicit configuration dependencies on a subproject
dependencies {
  compile project(path: ':projectA', configuration: 'published')
  compile project(':projectB')
}


#-# Internal dependencies

# Depending on the Gradle API
dependencies {
  compile gradleApi()
  // other dependencies...
}

# The configuration of a typical Groovy build
apply plugin: 'groovy'
// Repository declaration
dependencies {
  groovy 'org.codehaus.groovy:groovy:2.0.5'
  // other dependencies...
}

# Depending on Gradle’s internal version of Groovy
apply plugin: 'groovy'
dependencies {
  groovy localGroovy()
  // other dependencies...
}


#-# Example

dependencies {
  compile 'org.apache.solr:solr-core:1.4.1'

  compile group: 'org.hibernate', name: 'hibernate-core', version: '3.6.7.Final'
  testCompile group: 'junit', name: 'junit', version: '4.+'

  compile project(':projectA')

  runtime files('libs/a.jar', 'libs/b.jar')
  runtime fileTree(dir: 'libs', include: '*.jar')
}



#-#
#-# Tasks
#-#

#-# Defining tasks

Every task is composed of two stages: configuration and execution.

By looking at the following three tasks we can see that there are a few slight differences when
it comes to what is executed when.

// This task will output the defined message when calling it explicitly: 'gradle taskOne'
// but it will also display the message when we call 'gradle tasks' due to the fact that
// the printing is defined in the configuration stage and Gradle has to configure all the
// specified tasks in the build script before the actual build is started.
task taskOne {
  def message = "Hello world!" // configuration stage
  println message // configuration stage
}

// In order to have a task execute something when called we need to specify a task Action.
// The easiest way to specify a task action is via the Task#doLast() method.
task taskTwo {
  def message = "Hello world!" // configuration stage
  doLast {
    println message // execution stage (when the task is called)
  }
}

// The '<<' is just a shortcut to doLast.
// This implementation has the drawback of not having a configuration stage so this is good for
// really small tasks, but for tasks other than 'Hello world!' you might consider using doLast.
task taskThree << {
  def message = "Hello world!" // execution stage (when the task is called)
  println message // execution stage (when the task is called)
}


#-# Adding behaviour to existing tasks

task hello << { println 'Hello Earth'   }
hello.doFirst { println 'Hello Venus'   }
hello.doLast  { println 'Hello Mars'    }
hello <<      { println 'Hello Jupiter' } // << is an alias for doLast


#-# Extra task properties

task myTask { ext.myProperty = 'myValue' }
task printTaskProperty << { println myTask.myProperty}


#-# Locating tasks

# Accessign tasks as properties
task hello
println hello.name
println project.hello.name

# Accessing tasks via the tasks collection
task hello
println tasks.hello.name
println tasks['hello'].name

# Accessing tasks by path
println tasks.getByPath('hello').path
println tasks.getByPath(':hello').path
println tasks.getByPath('projectA:hello').path
println tasks.getByPath(':projectA:hello').path


#-# Configuring tasks

task copy(type: Copy) {
  description 'Copies resources to the target directory.'
  from 'resources'
  into 'target'
  include('**/*.txt', '**/*.xml', '**/*.properties')
}


#-# Task dependencies

# Adding dependency on a task from another project
project('projectA') {
  task taskX(dependsOn: ':projectB:taskY') << {
    println 'taskX'
  }
}
project('projectB') {
  task taskY(dependsOn: ':projectA:taskX') << {
    println 'taskY'
  }
}

# Adding dependency using task object
task taskX << { println 'taskX' }
task taskY << { println 'taskY' }
taskX.dependsOn taskY

# Adding dependency using closure
task taskX << { println 'taskX' }
taskX.dependsOn {
  tasks.findAll { task -> task.name.startsWith('lib') }
}
task lib1 << { println 'lib1' }
task lib2 << { println 'lib2' }
task lib3 << { println 'lib3' }


#-# Ordering tasks

The primary difference between a task ordering and a task dependency is that an ordering
does not influence which tasks will be executed, only the order in which they will be executed.

# Must run after
task taskX << { println 'taskX' }
task taskY << { println 'taskY' }
taskY.mustRunAfter taskX

# Should run after
task taskX << { println 'taskX' }
task taskY << { println 'taskY' }
taskY.shouldRunAfter taskX


#-# Replacing tasks

task taskX << { println 'taskX' }
task taskX(overwrite: true) << { println 'I am the new one.' }


#-# Skipping tasks

# Using a predicate
task hello << { println 'Hello world!' }
hello.onlyIf { !project.hasProperty('skipHello') }

# Using StopExecutionException
task hello << { println 'Hello world!' }
hello.doFirst {
  if (true) { throw new StopExecutionException() }
}


#-# Disabling tasks

task disableMe << { println 'This should not be printed if the task is disabled' }
disableMe.enabled = false


#-# Task rules

tasks.addRule('Pattern: ping <id>') { String taskname ->
  if (taskname.startsWith('ping')) {
    task(taskname) << {
      println 'Pinging: ' + (taskName - 'ping')
    }
  }
}


#-# Finalizer tasks

# Adding a task finalizer
task taskX << { println 'taskX' }
task taskY << { println 'taskY' }
taskX.finalizedBy taskY

# Task finalizer for a failing task
task taskX << {
  println 'taskX'
  throw new RuntimeException()
}
task taskY << {
  println 'taskY'
}
taskX.finalizedBy taskY


#-# Define default tasks

defaultTasks 'clean', 'run'



#-#
#-# Multi-project builds
#-#

#-# Configuration (settings.gradle)

# Define the list of subprojects
include 'projectA', 'projectB'


#-# Tasks (build.gradle)

# Define tasks to run on all projects
allprojects {
  task projectName << { task -> println "I'm $task.project.name" }
}

# Define tasks to run on all subprojects
subprojects {
  task projectName << { println "I am a subproject" }
}

# Define tasks to run on a specific project
project(':projectA').projectName << {
  println "I have a specific project name task"
}


#-#
#-# Gotchas
#-#

#-# Publishing the fat jar for a Spring Boot application, not classes only jar

Spring Boot's bootRepackage task is setup as a dependency of the assemble task.
In order to end up with the fat jar on nexus or whatever, the publish task has to depend on assemble.

publish {
  dependsOn assemble
}



