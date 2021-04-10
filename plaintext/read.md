Read a plaintext file
=====================

#### Python example

```python
path = r'C:\my_input_file.txt'

with open(path, encoding='utf-8') as file:
    for line in file:
        print(line.strip())
```

#### Scala example

```scala
import scala.io.Source

val path = """C:\my_input_file.txt"""

val source = Source.fromFile(path, "UTF-8")
source.getLines.foreach(println)
source.close
```

```scala
// since Scala 2.13

import scala.io.Source
import scala.util.Using

val path = """C:\my_input_file.txt"""

Using(Source.fromFile(path, "UTF-8")) { source => source.getLines.foreach(println) }
```
