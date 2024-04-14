---
sidebar_position: 6
tags:
    - gradle
    - build tool
    - dependency management
---

# Dependency Management Basics

Dependency management is an automated technique for declaring and resolving external resources required by a project.
Dependencies refer to JARs, plugins, libraries, or source code the support building your project.

## Version Catolog

Version catalog provide a way to centralize your dependency declaration in a
`libs.versions.toml` file.
The catalog makes sharing dependencies and version configurations between subprojects simple.
It also allows teams to enforce versions of libraries and plugins in large projects.

The version catalog typically contains four sections:
1. [versions] to declare the version numbers that plugins and libraries will reference.
2. [libraries] to define the libraries used in the build files.
3. [bundles] to define a set of dependencies.
4. [plugins] to define plugins.

```toml
[versions]
androidGradlePlugin = "7.4.1"
mockito = "2.16.0"

[libraries]
googleMaterial = { group = "com.google.android.material", name = "material", version = "1.1.0-alpha05" }
mockitoCore = { module = "org.mockito:mockito-core", version.ref = "mockito" }

[plugins]
androidApplication = { id = "com.android.application", version.ref = "androidGradlePlugin" }
```
This file is located in the `gradle` directory so that it can be used by Gradle and IDEs automatically.
The version catalog should be checked into source control: `gradle/libs.versions.toml`.

## Declaring Your Dependencies

To add dependency to the project, specify a dependency in the `dependencies` block
of your `build.gradle(.kts)` file.
```kotlin
plugins {
   alias(libs.plugins.androidApplication)  (1)
}

dependencies {
    // Dependency on a remote binary to compile and run the code
    implementation(libs.googleMaterial)    (2)

    // Dependency on a remote binary to compile and run the test code
    testImplementation(libs.mockitoCore)   (3)
}

```
(1) Applies the Android Gradle plugin to the project, which adds several features that
are specific to building Android apps.  
(2) Adds the Material dependency to the project. Material Design provides components
for creating a user interface in an Android App. This library will be used to compile and
run the Kotlin source code in the project.  
(3) Adds the Mockito dependency to the project. Mockito is a mocking framework for testing
Java code. This library will be used to compile and run the _test_ source code in the project.

Dependencies in Gradle are grouped by configurations.
- The `material` library is added to the `implementation` configuration, which is used
for compiling and running _production_ code.
- The `mockito-core` library is added to the `testImplementation` configuration, which is used
for compiling and running _test_ code.

:::note

There are many more configurations available.

:::

## Viewing Project Dependencies

You can view dependency tree of your project in terminal using the
`./gradlew :app:dependencies` command:
```bash
$ ./gradlew :app:dependencies
Starting a Gradle Daemon (subsequent builds will be faster)

> Task :app:dependencies

------------------------------------------------------------
Project ':app'
------------------------------------------------------------

annotationProcessor - Annotation processors and their dependencies for source set 'main'.
No dependencies

compileClasspath - Compile classpath for source set 'main'.
\--- com.google.guava:guava:31.1-jre
     +--- com.google.guava:failureaccess:1.0.1
...
implementation - Implementation dependencies for the 'main' feature. (n)
\--- com.google.guava:guava:31.1-jre (n)

mainSourceElements - List of source directories contained in the Main SourceSet. (n)
No dependencies

runtimeClasspath - Runtime classpath of source set 'main'.
\--- com.google.guava:guava:31.1-jre
     +--- com.google.guava:failureaccess:1.0.1
...
testCompileClasspath - Compile classpath for source set 'test'.
...
\--- org.junit.jupiter:junit-jupiter:5.9.2
     +--- org.junit:junit-bom:5.9.2
```

