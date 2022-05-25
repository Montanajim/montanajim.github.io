# Ant Vs Maven Vs Gradle



# Ant Vs Maven vs Gradle

from [Baeldung](https://www.baeldung.com/ant-maven-gradle#:~:text=While%20Ant%20gives%20flexibility%20and,the%20framework%20to%20do%20it.)

## Introduction

In this article, we'll explore three Java build automation tools that dominated the JVM ecosystem – Ant, Maven, and Gradle.

We'll introduce each of them and explore how Java build automation tools evolved.

## Apache Ant

In the beginning, Make was the only build automation tool available beyond homegrown solutions. Make has been around since 1976 and as such, it was used for building Java applications in the early Java years.

However, a lot of conventions from C programs didn't fit in the Java ecosystem, so in time Ant took over as a better alternative.

Apache Ant (“Another Neat Tool”) is a Java library used for automating build processes for Java applications. Additionally, Ant can be used for building non-Java applications. It was initially part of Apache Tomcat codebase and was released as a standalone project in 2000.

In many aspects, Ant is very similar to Make, and it's simple enough so anyone can start using it without any particular prerequisites. Ant build files are written in XML, and by convention, they're called build.xml.

Different phases of a build process are called “targets”.

Here is an example of a build.xml file for a simple Java project with the HelloWorld main class:
```xml
<project>
    <target name="clean">
        <delete dir="classes" />
    </target>

    <target name="compile" depends="clean">
        <mkdir dir="classes" />
        <javac srcdir="src" destdir="classes" />
    </target>
    
    <target name="jar" depends="compile">
        <mkdir dir="jar" />
        <jar destfile="jar/HelloWorld.jar" basedir="classes">
            <manifest>
                <attribute name="Main-Class" 
                  value="antExample.HelloWorld" />
            </manifest>
        </jar>
    </target>
    
    <target name="run" depends="jar">
        <java jar="jar/HelloWorld.jar" fork="true" />
    </target>
</project>
```

This build file defines four targets: clean, compile, jar and run. For example, we can compile the code by running:

ant compile
This will trigger the target clean first which will delete the “classes” directory. After that, the target compile will recreate the directory and compile the src folder into it.

The main benefit of Ant is its flexibility. Ant doesn't impose any coding conventions or project structures. Consequently, this means that Ant requires developers to write all the commands by themselves, which sometimes leads to huge XML build files that are hard to maintain.

Since there are no conventions, just knowing Ant doesn't mean we'll quickly understand any Ant build file. It'll likely take some time to get accustomed to an unfamiliar Ant file, which is a disadvantage compared to the other, newer tools.

At first, Ant had no built-in support for dependency management. However, as dependency management became a must in the later years, Apache Ivy was developed as a sub-project of the Apache Ant project. It's integrated with Apache Ant, and it follows the same design principles.

However, the initial Ant limitations due to not having built-in support for dependency management and frustrations when working with unmanagable XML build files led to the creation of Maven.

### Apache Maven

Apache Maven is a dependency management and a build automation tool, primarily used for Java applications. Maven continues to use XML files just like Ant but in a much more manageable way. The name of the game here is convention over configuration.

While Ant gives flexibility and requires everything to be written from scratch, Maven relies on conventions and provides predefined commands (goals).

Simply put, Maven allows us to focus on what our build should do, and gives us the framework to do it. Another positive aspect of Maven was that it provided built-in support for dependency management.

Maven's configuration file, containing build and dependency management instructions, is by convention called pom.xml. Additionally, Maven also prescribes a strict project structure, while Ant provides flexibility there as well.

Here's an example of a pom.xml file for the same simple Java project with the HelloWorld main class from before:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
      http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>mavenExample</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <description>Maven example</description>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

However, now the project structure has been standardized as well and conforms to the Maven conventions:

>+---src
>|   +---main
>|   |   +---java
>|   |   |   \---com
>|   |   |       \---baeldung
>|   |   |           \---maven
>|   |   |                   HelloWorld.java
>|   |   |                   
>|   |   \---resources
>|   \---test
>|       +---java
>|       \---resources

As opposed to Ant, there is no need to define each of the phases in the build process manually. Instead, we can simply call Maven's built-in commands.

For example, we can compile the code by running:

mvn compile
At its core, as noted on official pages, Maven can be considered a plugin execution framework, since all work is done by plugins. Maven supports a wide range of available plugins, and each of them can be additionally configured.

One of the available plugins is Apache Maven Dependency Plugin which has a copy-dependencies goal that will copy our dependencies to a specified directory.

To show this plugin in action, let's include this plugin in our pom.xml file and configure an output directory for our dependencies:
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-dependency-plugin</artifactId>
            <executions>
                <execution>
                    <id>copy-dependencies</id>
                    <phase>package</phase>
                    <goals>
                        <goal>copy-dependencies</goal>
                    </goals>
                    <configuration>
                        <outputDirectory>target/dependencies
                          </outputDirectory>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```
This plugin will be executed in a package phase, so if we run:

mvn package
We'll execute this plugin and copy dependencies to the target/dependencies folder.

There is also an existing article on how to create an executable JAR using different Maven plugins. Additionally, for a detailed Maven overview, have a look at this core guide on Maven, where some Maven's key features are explored.

Maven became very popular since build files were now standardized and it took significantly less time to maintain build files, comparing to Ant. However, though more standardized than Ant files, Maven configuration files still tend to get big and cumbersome.

Maven's strict conventions come with the price of being a lot less flexible than Ant. Goal customization is very hard, so writing custom build scripts is a lot harder to do, compared with Ant.

Although Maven has made some serious improvements regarding making application's build processes easier and more standardized, it still comes with a price due to being a lot less flexible than Ant. This lead to the creation of Gradle which combines the best of both worlds – Ant's flexibility and Maven's features.

### Gradle
Gradle is a dependency management and a build automation tool that was built upon the concepts of Ant and Maven.

One of the first things we can note about Gradle is that it's not using XML files, unlike Ant or Maven.

Over time, developers became more and more interested in having and working with a domain-specific language – which, simply put, would allow them to solve problems in a specific domain using a language tailored for that particular domain.

This was adopted by Gradle, which is using a DSL based either on Groovy or Kotlin. This led to smaller configuration files with less clutter since the language was specifically designed to solve specific domain problems. Gradle's configuration file is by convention called build.gradle in Groovy, or build.gradle.kts in Kotlin.

Notice that Kotlin offers better IDE support than Groovy for auto-completion and error detection.

Here is an example of a build.gradle file for the same simple Java project with the HelloWorld main class from before:

apply plugin: 'java'
```gradle
repositories {
    mavenCentral()
}

jar {
    baseName = 'gradleExample'
    version = '0.0.1-SNAPSHOT'
}

dependencies {
    testImplementation 'junit:junit:4.12'
}
```
We can compile the code by running:

Gradle classes
At its core, Gradle intentionally provides very little functionality. Plugins add all useful features. In our example, we were using java plugin which allows us to compile Java code and other valuable features.

Gradle gave its build steps name “tasks”, as opposed to Ant's “targets” or Maven's “phases”. With Maven, we used Apache Maven Dependency Plugin, and it's a specific goal to copy dependencies to a specified directory. With Gradle, we can do the same by using tasks:

task copyDependencies(type: Copy) {
   from configurations.compile
   into 'dependencies'
}
We can run this task by executing:

gradle copyDependencies
5. Conclusion
In this article, we presented Ant, Maven, and Gradle – three Java build automation tools.

Not surprisingly, Maven holds the majority of the build tool market today.

Gradle, however, has seen good adoption in more complex codebases, for the following reasons:

* Lots of open-source projects such as Spring are using it now
* It is faster than Maven for most scenarios, thanks to its incremental builds
* It offers advanced analysis and debugging services

However that Gradle seems to have a steeper learning curve, especially if you're not familiar with Groovy or Kotlin.