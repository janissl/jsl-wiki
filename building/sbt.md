Build Scala executables using sbt
=================================

#### A minimal build.sbt example

```sbt
name := "my-project"
version := "0.1"

scalaVersion := "2.12.13"
scalacOptions ++= Seq("-language:implicitConversions", "-deprecation")

libraryDependencies ++= Seq(
  "com.novocode" % "junit-interface" % "0.11" % Test
)

testOptions in Test += Tests.Argument(TestFrameworks.JUnit, "-a", "-v", "-s")
```

#### Create a single JAR file without dependencies
```shell
sbt package
```
Creates a JAR file containing the files in _./src/main/resources_ and the classes compiled from _./src/main/scala_ and _./src/main/java_.

Outputs a JAR to *./target/scala-{scalaVersion}}/{projectName}_{scalaVersion}-{projectVersion}.jar*.


#### Delete all generated files
```shell
sbt clean
```

#### Create a single JAR file with dependencies (a fat JAR)
```shell
sbt assembly
```
Requires the __sbt-assembly__ plugin.

Outputs a JAR to *./target/scala_{scalaVersion}/{projectName}-assembly-{projectVersion}.jar*

Add the following line in the file _./project/plugins.sbt_ (check for the latest version on https://github.com/sbt/sbt-assembly).
```sbt
addSbtPlugin("eed3si9n" % "sbt-assembly" % "0.15.0")
```

Add the following line in the beginning of __build.sbt__.
```sbt
enablePlugins(AssemblyPlugin)
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


#### Create a single JAR file and download all dependencies as separate JARs
```shell
sbt pack
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
packResourceDir += (baseDirectory.value / "src/main/resources/" -> "")
```