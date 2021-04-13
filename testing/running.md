Running tests from terminal
===========================

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
  "org.scalacheck" %% "scalacheck" % "1.15.2" % Test,
  "org.scalatest" %% "scalatest" % "3.2.7" % Test
)

Test / testOptions ++= Seq(
  Tests.Argument(TestFrameworks.ScalaTest, "-oD"),
  Tests.Argument(TestFrameworks.ScalaCheck, "-verbosity", "1")
)
```

#### Compile and run all tests
```sbt
// cd to your project's directory and run the following command:
sbt test

// Alternatively, you can also start sbt shell and run commands in it:
sbt
test
```


#### Only run failed or new tests
```sbt
testQuick
```

---
References:
1. [Using ScalaTest with sbt](https://www.scalatest.org/user_guide/using_scalatest_with_sbt)
1. [ScalaCheck: Property-based testing for Scala](https://www.scalacheck.org/)
1. [SBT - Testing](https://www.scala-sbt.org/1.x/docs/Testing.html)
