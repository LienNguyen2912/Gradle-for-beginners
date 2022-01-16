# Hello Gradle - Gradle tutorial for beginners
We will talk about
- What is Gradle
- Why would you use Gradle
- Install Gradle
- Gradle project structure
- Create the first Gradle project
- Gradle task graph

## What is Gradle?
- Gradle is a build automation tool. It takes the code and packages it into a deployable unit.
- Applies to small or large project
- Gradle is written in JVM language such as Groovy and Kotlin

Below is a simple example of **build.gradle** in _Groovy_
```sh
plugins {
	id 'java'
}
jar {
    manifest {
        attributes('Main-Class': 'com.tomgregory.languageapp.SayHello')
    }
}
repositories {
    mavenCentral()
}
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.6.3'
}
```

## Why would you use Gradle
- Gradle makes building and running applications very easy and fast
- When people check out a project, they don't need to have Gradle installed. Just run 
```sh
gradlew.bat build
```
the command above is in Windows environment. Run _./gradlew build_ in case of Linux or Apple. _"gradlew"_ stands for _"gradle wrapper"_
### Java project requirements
- Compile Java classes from _.java_ into _.class_ files
- Manage all resources that live alongside code
- Package everything into a _.jar_ file
- Easily run tests
- Define dependencies

### How Gradle does
**Compile classes.** </br>
For example to compile Java: 
```sh
plugins {
	    id 'java'
} 
```
Execute a task
```sh
gradlew.bat compileJava
```
will compile _.java_ into _.class_ files. Outputs _.class_ files in the _build_ directory</br>
**Manage resources**</br>
```sh
gradlew.bat processResources
```
will copy contents of resources directories into _build/resources_ directory</br>
**Package into a _.jar_ file**</br>
Add a task _jar_</br>
```sh
gradlew.bat jar
```
will add all compiled classes and resources to a _.jar_ archive. Outputs _<project-name>-<version>.jar_ file to _build/libs_ directory</br>
**Easily run tests**</br>
Add a task _test_
```sh
gradlew.bat test
```
will compile test codes, process resources, run test cases and create a test report</br>
**Define dependencies**</br>
Use the _dependencies_ section of the _build.gradle_. When define a dependency, we must define _<group>:<name>:<version>_. This helps Gradle to download the correct depedency
```sh
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.6.3'
}
```

## Installing Gradle (Windows)
- Validate that Java is installed. Don't worry if you've got a different Java version installed because Gradle supports version 8 and above.
```sh
java -version
```
![java](https://user-images.githubusercontent.com/73010204/149618756-b980b17f-7ba6-44c8-8172-5b314b1df47f.PNG)</br>
- Go to https://gradle.org/releases/
- Scroll down and choose the most recent Gradle release. At the current time, this was **7.3.3**. Chose the _binary-only_. Click the link to download the Gradle.zip file to your computer</br>
![install](https://user-images.githubusercontent.com/73010204/149618923-8c6fe1ea-b3cb-455b-8189-250b9364a034.png)</br>
- Create a new directory on your hard drive, name it _Gradle_, copy and extracted the downloaded zip file above. In my case, I created _C:\Gradle_</br>
![3](https://user-images.githubusercontent.com/73010204/149619048-bbc7d24f-1058-4a07-8606-78a148a73061.PNG)</br>
- In the extracted folder, go into the bin directory, copy the path, in my case it is _C:\Gradle\gradle-7.3.3\bin_, configure your PATH variable so that you can run Gradle commands from wherever you are in the command prompt.
- Go to the start menu, type _environment_, hit Enter. On the dialog appears, click _Environment variables_, then under _System variables_ double click the _Path_ variable, click _New_ then paste in the location of your Gradle _bin_ directory which you copied earlier. Hit Enter and OK again and again.</br>
![4](https://user-images.githubusercontent.com/73010204/149619286-82018534-77b7-45a5-aa62-483c81c47bc8.png)</br>
- Now let's validate our Gradle installation
```sh
gradle --version
```
![installDone](https://user-images.githubusercontent.com/73010204/149619394-fee975dd-120e-4dff-a604-587bc716a661.PNG)</br>

## Gradle project structure
![structure](https://user-images.githubusercontent.com/73010204/149620105-82c73324-7c9e-42e0-a866-f3c99ec18caa.png)</br>
- **build.gradle** is the Gradle build script file. Normally lives in the top level of your project. It is the main build configuration file where we define how Gradle build should work including plugins, dependencies...
- **Gradle directory** contains the code configurating for the Gradle wrapper
- **gradlew** is the Gradle wrapper script for Windows version
- **gradlew.bat** is the Gradle wrapper script for Linux/MacOS version
- **settings.gradle** contains additional configurations outside of the build.gradle. Importantly it contains the specify for the project name

#### The Gradle expected Java project layout
![structureAfter](https://user-images.githubusercontent.com/73010204/149622913-d5df7d78-cdeb-4370-a5ee-b3530538d2fe.PNG)

Although everything is configurable, TRY to use the default.

## Create the first Gradle project - Hello Gradle
We will create an application that outputs _Hello_ if users input _en_ as parameter, and outputs _こんにちは！_ if users input _jp_
### Gradle init
Create a directory for the project, name it _hello-gradle_</br>
Navigate into the directory, create a Gradle project
```sh
gradle init
```
Select type of project to generate: **1** </br>
Select build script DSL: **1** </br>
Project name: **<enter>** to let it be default</br<
![init](https://user-images.githubusercontent.com/73010204/149620942-99ac8722-4031-4665-a175-dcc6f8449274.png)</br>
**Try interacting with the project**
```sh
gradlew.bat tasks
```
![tasks](https://user-images.githubusercontent.com/73010204/149621325-eb459302-4eb1-44d6-bc2b-7ef963684a1b.png)</br>
Now the gradle project structure will be</br>
![structureInit](https://user-images.githubusercontent.com/73010204/149621440-87c1f723-fadf-45fb-85f1-c9fbad06346a.PNG)</br>
※ If you get some errors relative to proxy, check the proxy configuration in _C:\Users\yourname\.gradle\gradle.properties_. Make sure you are using the correct proxy or just delete all if you don't use proxy.
### Add the Java code
Add a directory _src/main/java_ for the main application code</br>
Add directories for the Java package _com/liennt/hellogradleapp_
Create a new file _HelloGradle.java_ having the below content
```sh
package com.liennt.hellogradleapp;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;

public class HelloGradle {
    public static void main(String[] args) throws IOException {
        String language = args[0];

        InputStream resourceStream = HelloGradle.class.getClassLoader().getResourceAsStream(language + ".txt");
        assert resourceStream != null;
        BufferedReader bufferedInputStream = new BufferedReader(new InputStreamReader(resourceStream, StandardCharsets.UTF_8));

        System.out.println(bufferedInputStream.readLine());
    }
}
```
### Adding the resources
Create a new directory under the _src/main_ callled _resources_</br>
Add a file en.txt with contents _Hello!_
Add a file jp.txt with contents _こんにちは！_</br>
### Building the application
Open _build.gradle_, insert this plugin configuration
```sh
plugins {
    id 'java'
}
```
**Compile the Java classes.**
```sh
gradlew.bat compileJava
```
Compiled outputs are in _build/classes/java/main_.</br>
**Process resources**
```sh
gradlew.bat processResources
```
Look for output in _build/resources/main._ </br>
**Generate the jar file**
```sh
gradlew.bat jar
```
Look for the _.jar_ in the build/libs</br>
![build](https://user-images.githubusercontent.com/73010204/149648430-7f2af55f-3ca4-4866-96ca-cf1a8347ae99.PNG)</br>
**Running the application**
```sh
java -jar build/libs/hello-gradle.jar en
```
You’ll see an error which says _no main manifest attribute._</br>
![err](https://user-images.githubusercontent.com/73010204/149648492-f6e941e5-9fca-4460-bd34-641040a85f27.png)</br>
Add this jar configuration to the end of _build.gradle_:
```sh
jar {
    manifest {
        attributes('Main-Class': 'com.liennt.hellogradleapp.HelloGradle')
    }
}
```
Build the jar file again
```sh
gradlew.bat jar
```
Rerun the application
```sh
java -jar build/libs/hello-gradle.jar en
```
You should see the expected text output.</br>
![out](https://user-images.githubusercontent.com/73010204/149648562-327ddc30-0e77-4a85-94d7-40051fea2cf3.png)</br>
We 've just built successfully the first Java application with Gradle! Great!</br>
**Testing the application**</br>
Test sources should live in _src/test_, so under _src_ create new directories _test/java/com/liennt/hellogradleapp_ then add a new file _HelloGradleTest.java_. Edit it as below
```sh
package com.liennt.hellogradleapp;

import org.junit.jupiter.api.Test;
import java.io.IOException;

public class HelloGradleTest {
    @Test
    public void testHelloGradle() throws IOException {
        HelloGradle.main(new String[]{"en"});
    }
}
```
Try running the tests
```sh
gradlew.bat test
```
You'll get an error here saying that it can’t find the _org.junit.jupiter.api_ package.</br>
Add this dependency configuration block to build.gradle, after the plugins:
```sh
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.6.3'
}
```
Add this repositories configuration block, putting it just before the dependencies to let Gradle know where to download the dependencies
```sh
repositories {
    mavenCentral()
}
```
Rerun the test command:
```sh
gradlew.bat test
```
The build should be successful and you will get the test report located in _ build/reports/tests/test/index.html._</br>
![test1](https://user-images.githubusercontent.com/73010204/149648828-520d3b0d-fec1-456c-baa2-986d2368545b.png)</br>
_You'll see 0 tests have been run._ Add this test configuration block below the dependencies block:
```sh
test {
    useJUnitPlatform()
}
```
This configures tests to use the Junit 5 platform.</br>
Rerun the test again
```sh
gradlew.bat test
```
Open the test report again in a browser, located in _build/reports/tests/test/index.html._ You should now see that 1 test was run, with a 100% success rate.</br>
![test2](https://user-images.githubusercontent.com/73010204/149648896-69af08df-0f96-4b6d-8a61-1d83192f5807.png)</br>
**Well done! We have just built, run and tested the first Java project with Gradle!**

## Gradle tasks
Gradle tasks defines a unit of work</br>
A task is invoked from the command line. For example, to execute the _build_ task, we invoke
```sh
gradlew.bat build
```
To clear/ delete the _build_ folder, just run
```sh
gradlew.bat clean
```
To see avaiable tasks, run</br>
```sh
gradlew.bat tasks
```
We can create our own custom tasks</br>
A task can depend on other task following to the **task plugin graph**. Dependence on an other task means the other task completes first</br>
For example, _build_ task depends on _assemble_ and _check_ task, so when we invoke _gradlew build_ the _build_ task actually does nothing but build aggregates _assemble_ and _check_ tasks
### Task plugin graph
![taskgraph](https://user-images.githubusercontent.com/73010204/149661900-b9e09f0e-709e-4e95-989c-840528c7d765.PNG)</br>
Following to the graph
- Some tasks perform actions and some are aggregates. Aggreate tasks combine multiple tasks using task dependencies.
- Use _gradlew.bat build_ when we need to build and test the whole project.
- Use _gradlew.bat assemble_ or _gradlew.bat jar_ when we need to build the project without testing it
- Use _gradlew.bat check_ or _gradlew.bat test_ when we need to excute testing the project without re-assembling it

## Congratulation
We have created a simple Java project in Gradle and understand the key aspects of Gradle configuration.

## Reference
tomgregory.com
