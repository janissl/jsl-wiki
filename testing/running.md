Running from terminal
=====================

#### Python example (using the unittest module)
```powershell
# Prerequisite: your test modules (test_*.py) are located in $project_dir/tests directory
cd $project_dir
python -m unittest discover -s tests
```

#### Scala example (using sbt)

```sbt
// Add the lines below to your build.sbt file
libraryDependencies ++= Seq(
  "org.scalacheck" %% "scalacheck" % "1.14.2" % Test,
  "com.novocode" % "junit-interface" % "0.11" % Test
)

testOptions in Test += Tests.Argument(TestFrameworks.JUnit, "-a", "-v", "-s")
```


```sbt
// cd to your project's directory and run the following command:
sbt test
```
