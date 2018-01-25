# SpringCloudLightningTalk
# Working with Github
This repository demonstrates working with GitHub and the services in the marketplace, such as Travis, CodeCoverage, VersionEye, and JitPack.

# Table of Content
* [Creating an account](#creating_account)
* [Creating a repository](#create_repo)
* [Creating a .gitignore](#gitignore)
* [Cloning a repository](#clone_repo)

## <a name="creating_account"></a>Creating an account
Go to https://github.com/ and sign up. Pick the free plan and verify your email address.

![Sign up](/images/creating_an_account.png)

## <a name="create_repo"></a>Create a new repository
Enter a repository name and initialize the repository with a README and the Apache License 2.0.

![New Repository](/images/create_repo.png)

## <a name="gitignore"></a>Create a .gitignore
Create new file, name it ".gitignore", pick the Java template, and add your IDE's files to the file.

![.gitignore](/images/gitignore.png)

## <a name="clone_repo"></a>Cloning a repository
Copy the repository URL into your clipboard and clone the repository in your IDE.

![Copy the repository URL](/images/clone_copy_url.png)

![Clone the repository in your IDE](/images/clone_ide.png)

## pom.xml and first code
Create a pom.xml in the root directory, and add JodaToJava8Converter.java in a package, and create a test in the test tree.
```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <groupId>mafoe</groupId>
    <artifactId>working-with-github</artifactId>
    <version>1.0-SNAPSHOT</version>
    <modelVersion>4.0.0</modelVersion>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.7.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <dependencies>

        <dependency>
            <groupId>joda-time</groupId>
            <artifactId>joda-time</artifactId>
            <version>2.7</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
</project>
```
