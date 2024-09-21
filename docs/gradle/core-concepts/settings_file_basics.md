---
sidebar_position: 4
tags:
    - gradle
    - build tool
    - settings
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Settings File Basics

Settings file is the **entry point** of every Gradle project.
The primary purpose of the _settings file_ is to add subprojects to your build.
Gradle supports single and multi-project builds.
- Settings file is optional for single-project builds.
- Settings file is mandatory and declares all subprojects for multi-project builds.

## Settings script

The settings file is a script. It is either a `settings.gradle` file written in Groovy
or a `settings.gradle.kts` file in Kotlin.
The _Groovy DSL_ and _Kotlin DSL_ are the only accepted languages for Gradle scripts.
The settings file is typically found in the root directory of the project:
<Tabs>
  <TabItem value="kotlin" label="Kotlin" default>
        ```kotlin title="settings.gradle.kts"
        rootProject.name = "root-project"   (1)

        include("sub-project-a")            (2) 
        include("sub-project-b")
        include("sub-project-c")
        ```
  </TabItem>
  <TabItem value="groovy" label="Groovy">
        ```groovy title="settings.gradle"
        rootProject.name = 'root-project'   (1)

        include('sub-project-a')            (2)
        include('sub-project-b')
        include('sub-project-c')
        ```
  </TabItem>
</Tabs>

(1) Define the project name.  
(2) Add subprojects.

