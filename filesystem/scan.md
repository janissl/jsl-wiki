Recursively scan directory for files
====================================

#### Python example
```python
import os

def scan_dir(dir_path):
    with os.scandir(dir_path) as it:
        for entry in it:
            if entry.is_file():
                yield entry.path
            elif entry.is_dir():
                yield from scan_dir(entry.path)

path = r'C:\mydir'
scan_dir(path)
```

#### Scala example
```scala
// up to Scala 2.12
import java.io.File
import java.nio.file.{DirectoryStream, Files, Paths}
import scala.jdk.CollectionConverters.IterableHasAsScala


def listFiles(directory: String, acc: List[File]): List[File] = {
  val directoryStream = Files.newDirectoryStream(Paths.get(directory))

  val fileList = directoryStream.asScala.flatMap(p => {
    if (p.toFile.isDirectory) listFiles(p.toString, acc) ++ acc
    else p.toFile :: acc
  }).toList

  directoryStream.close()

  fileList
}

val path = """C:\mydir"""
listFiles(path, List.empty[File])
```

```scala
// since Scala 2.13
import java.io.File
import java.nio.file.{DirectoryStream, Files, Paths}
import scala.jdk.CollectionConverters.IterableHasAsScala
import scala.util.Using

def listFiles(directory: String, acc: List[File]): List[File] = {
  Using(Files.newDirectoryStream(Paths.get(directory))){ directoryStream =>
    directoryStream.asScala.flatMap(p =>
      if (p.toFile.isDirectory) listFiles(p.toString, acc) ++ acc
      else p.toFile :: acc
    ).toList
  }.getOrElse(List.empty[File])
}

val path = """C:\mydir"""
listFiles(path, List.empty[File])
```
