Build Scala executables using sbt
=================================

The most common sbt commands
----------------------------

#### Open sbt shell
```shell
sbt
```

#### Run Scala interpreter or REPL
```shell
[sbt] console
```
To close the Scala console, press Ctrl+D or type
```shell
:quit
```

#### Compile the main sources
```shell
[sbt] compile
```


#### Run the main class
```shell
[sbt] run <argument>*
```

#### Delete all generated files in target folder
```shell
[sbt] clean
```


#### Reload build definition after modification
```shell
reload
```


#### A minimal build.sbt example
```sbt
lazy val root = (project in file("."))
  .settings(
    name := "my-project",
    version := "0.1",
    scalaVersion := "2.12.13",

    scalacOptions ++= Seq(
      "-language:implicitConversions", "-deprecation", "-unchecked",
      "-encoding", "utf8",  // if you have "UTF-8" encoded literal strings in your source code
      "-release", "8"  // if the compilation must be preformed for a specific Java version which differs from the current one
    )
  )
```

#### Create a single JAR file without dependencies
```shell
[sbt] package
```
Creates a JAR file containing the files in _./src/main/resources_ and the classes compiled from _./src/main/scala_ and _./src/main/java_.

Outputs a JAR to *./target/scala-{scalaVersion}}/{projectName}_{scalaVersion}-{projectVersion}.jar*.

Using plugins to build JAR executables
--------------------------------------
#### Create a single JAR file with dependencies (a fat JAR)
```shell
[sbt] assembly
```
Requires the __sbt-assembly__ plugin.

Outputs a JAR to *./target/scala_{scalaVersion}/{projectName}-assembly-{projectVersion}.jar*

Add the following line in the file _./project/plugins.sbt_ (check for the latest version on https://github.com/sbt/sbt-assembly).
```sbt
addSbtPlugin("eed3si9n" % "sbt-assembly" % "0.15.0")
```

Add _enablePlugins_ method in __build.sbt__.
```sbt
lazy val root = (project in file("."))
  .enablePlugins(AssemblyPlugin)
  .settings(???)
```

To exclude some dependencies, specify them as "provided" in __build.sbt__.
```shell
libraryDependencies += "org.apache.spark" %% "spark-core" % "2.4.7" % "provided"
```

To include also directories with unmanaged dependencies (like DLL, SO files), add the following lines in __build.sbt__.
```sbt
unmanagedResourceDirectories in Compile += baseDirectory.value / "{directoryName}"
includeFilter in (Compile, unmanagedResourceDirectories) := ".dll,.so"
```

Specify the merging strategy in __build.sbt__ (a simple example).
```sbt
assemblyMergeStrategy in assembly := {
  case PathList("META-INF", xs @ _*) => MergeStrategy.discard
  case x => MergeStrategy.first
}
```

#### Create a single JAR file with no dependencies and download all dependencies as separate JARs
```shell
[sbt] pack
```
Requires the __sbt-pack__ plugin.

Creates a distributable package in _./target/pack_ folder.
All dependent JARs including __scala-library.jar__ are collected in _./target/pack/lib_ folder.
Generates program launch scripts _./target/pack/bin/{appName}_.

Add the following line in the file _./project/plugins.sbt_ (check for the latest version on https://github.com/xerial/sbt-pack)
```sbt
addSbtPlugin("org.xerial.sbt" % "sbt-pack" % "0.13")
```

Add the following line in the beginning of __build.sbt__.
```sbt
enablePlugins(PackPlugin)
```

To copy resource files/directories to _./target/pack_ folder, add the following line in __build.sbt__.
```shell
packResourceDir += (baseDirectory.value / "src/main/resources" -> "")
```

To also create a tar.gz and a zip archive of your Scala application, execute the following command:
```shell
[sbt] packArchive
```

NOTES
-----
* For building Spark applications, only use AssemblyPlugin if you have dependencies other than Spark and testing libraries.
  Otherwise your dependencies may not be found at runtime.
* When building Spark application, the major and minor version of Scala must match the version with which your current Apache Spark installation has been built.
  Otherwise, running the application will result in a ClassNotFoundException.
  Both versions can be checked using spark-shell command.

---
References:
1. [sbt Reference Manual](https://www.scala-sbt.org/1.x/docs/)
1. [sbt-pack plugin](https://github.com/xerial/sbt-pack)
