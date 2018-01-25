# SpringCloudLightningTalk
# Working with Github
This repository demonstrates working with GitHub and the services in the marketplace, such as Travis, CodeCoverage, VersionEye, and JitPack.

# Table of Content
* [Creating an account](#creating_account)
* [Creating a repository](#create_repo)
* [Creating a .gitignore](#gitignore)
* [Cloning the repository](#clone_repo)
* [Adding the pom.xml](#pom.xml)
* [First code](#first_code)
* [Adding a test](#add_test)
* [Travis CI](#travis)
* [Codecov](#codecov)

## <a name="creating_account"></a>Creating an account
Go to https://github.com/ and sign up. Pick the free plan and verify your email address.

![Sign up](/images/creating_an_account.png)

## <a name="create_repo"></a>Creating a repository
Enter a repository name and initialize the repository with a README and the Apache License 2.0.

![New Repository](/images/create_repo.png)

## <a name="gitignore"></a>Creating a .gitignore
Create new file, name it ".gitignore", pick the Java template, and add your IDE's files to the file.

![.gitignore](/images/gitignore.png)

## <a name="clone_repo"></a>Cloning the repository
Copy the repository URL into your clipboard and clone the repository in your IDE.

![Copy the repository URL](/images/clone_copy_url.png)

![Clone the repository in your IDE](/images/clone_ide.png)

## <a name="pom.xml"></a>Adding the pom.xml
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

## <a name="first_code"></a>First code

```java
package mafoe;

import org.joda.time.DateTime;

import java.time.ZoneId;

/**
 * Converts Joda time objects to javax.time objects.
 *
 * @author EMAFOER
 */
public class JodaToJava8Converter {

	public static java.time.ZonedDateTime convertTimestamp(DateTime jodaDateTime) {

		String zoneId = jodaDateTime.getZone().getID();
		return java.time.ZonedDateTime.of(
				jodaDateTime.getYear(),
				jodaDateTime.getMonthOfYear(),
				jodaDateTime.getDayOfMonth(),
				jodaDateTime.getHourOfDay(),
				jodaDateTime.getMinuteOfHour(),
				jodaDateTime.getSecondOfMinute(),
				jodaDateTime.getMillisOfSecond() * 1000 * 1000,
				ZoneId.of(zoneId));
	}
}
```

## <a name="add_test"></a>Adding a test

```java
package mafoe;

import org.joda.time.DateTime;
import org.junit.Test;

import java.time.ZonedDateTime;

import static org.junit.Assert.*;

/**
 * @author EMAFOER
 */
public class JodaToJava8ConverterTest {

	@Test
	public void testConvertTimestamp() {

		DateTime jodaTime = DateTime.parse("2010-06-30T01:20+02:00");
		ZonedDateTime zonedDateTime = JodaToJava8Converter.convertTimestamp(jodaTime);
		assertEquals("2010-06-30T01:20+02:00", zonedDateTime.toString());
	}
}
```

## <a name="travis"></a>Travis CI
From Travis CI's homepage: 
> Test and Deploy with Confidence
> Easily sync your GitHub projects with Travis CI and you’ll be testing your code in minutes!

In the settings, add the Travis CI service to your repository:

![Add Travis CI service](/images/add_travis.png)

Add a file named ".travis.yml" into the root directory:

```
language: java

jdk:
- oraclejdk8
```

Go to https://travis-ci.org/auth?redirectUri=https%3A%2F%2Ftravis-ci.org%2Fprofile and sign in with GitHub, then authorize travis-ci.

Switch the new repository to "on" on the page you're being redirected to. Click on "More Options" -> "Trigger Build" to trigger a build automatically, or push a change to GitHub to trigger an automatic build.

At the top of the travis build page, there is a badge. Click it and select "Markdown" code. Copy the markdown to clipboard...

![Copy Travis badge markdown](/images/travis_badge.png)

... and add it to the README.MD:

![Add Travis badge to README.MD](/images/add_travis_badge_to_readme.png)

The result should look like this:

![Badge embedded in README.MD](/images/travis_badge_final.png)

## <a name="codecov"></a>Codecov

From Codecov's GitHub marketplace page:

> Codecov provides highly integrated tools to group, merge, archive and compare coverage reports. 

Visit https://github.com/marketplace/codecov and set up a free trial for "Open Source". "Install for free".

Login and authorize Codecov. Add the new repository.

Edit your pom.xml to add the cobertura plugin into the build/plugins block:

```
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>cobertura-maven-plugin</artifactId>
    <version>2.7</version>
    <configuration>
        <formats>
            <format>html</format>
            <format>xml</format>
        </formats>
        <check />
    </configuration>
</plugin>
```

Edit the .travis.yml (Codecov easily integrates with Travis CI) to look like this:

```yaml
language: java

jdk:
  - oraclejdk8

script: "mvn cobertura:cobertura"

after_success:
- bash <(curl -s https://codecov.io/bash)
```

Your next travis build should start automatically after pushing your changes, and should send coverage information to Codecov.
