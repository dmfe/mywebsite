---
sidebar_position: 5
tags:
    - gradle
    - build tool
    - build file
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Build File Basics

A build script details build configuration, tasks, and plugins.
Every Gradle build comprises at least one build script.
In the build file, two types of dependencies can be added:
1. The libraries and/or plugins on which Gradle and the build script depend.
2. The libraries on which the project sources depend.

## Build script

The build script is either a `build.gradle` file written in Groovy or a
`build.gradle.kts` file in Kotlin.
Example of the build script:
<Tabs>
  <TabItem value="kotlin" label="Kotlin" default>
        ```kotlin title="settings.gradle.kts"
        plugins {
            id("application")               (1)
        }

        application {
            mainClass = "com.example.Main"  (2)
        }
        ```
  </TabItem>
  <TabItem value="groovy" label="Groovy">
        ```groovy title="settings.gradle"
        plugins {
            id 'application'                (1)
        }

        application {
            mainClass = 'com.example.Main'  (2)
        }
        ```
  </TabItem>
</Tabs>

(1) Add plugins.  
(2) Use convention properties.

### 1. Add plugins

Plugins extend Gradle's functionality and can add more tasks to a project.
Adding a plugin to a build is called _applying_ a plugin:
```kotlin
plugins {
  id("application")
}
```
The application plugin facilitates creating an executable JVM application.
Applying the [Application plugin](https://docs.gradle.org/current/userguide/application_plugin.html#application_plugin)
also implicitly applies the [Java plugin](https://docs.gradle.org/current/userguide/java_plugin.html#java_plugin).
The `java` plugin adds Java compilation along with testing and bundling capabilities to a project.

### 2. Use convention properties

A plugin adds tasks to a project. It also adds properties and methods to a project.
The `application` plugin defines tasks that package and distribute an application,
such as the `run` task.
The Application plugin provides a way to declare the main class of a Java application,
which is required to execute the code.
```kotlin
application {
    mainClass = "com.example.Main"
}
```

