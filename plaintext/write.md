Write a plaintext file
======================

#### Python example
```python
path = r'C:\my_output_file.txt'
text = 'some text line'

with open(path, 'w', encoding='utf-8', newline='\n') as out_file:
    out_file.write(text + '\n')          # variant 1 (before Python v3.6)
    out_file.write('{}\n'.format(text))  # variant 2 (before Python v3.6)
    out_file.write(f'{text}\n')          # variant 3 (since Python v3.6)
```


#### Scala example
```scala
import java.io.{File, FileOutputStream, OutputStreamWriter}

val path = """C:\my_output_file.txt"""
val text = "some text line"

val writer = new OutputStreamWriter(new FileOutputStream(new File(path)), "UTF-8")
writer.write(s"$text\n")
writer.close()
```

```scala
// since Scala 2.13
import java.io.{File, FileOutputStream, OutputStreamWriter}
import scala.util.Using

val path = """C:\my_output_file.txt"""
val text = "some text line"

Using(new OutputStreamWriter(new FileOutputStream(new File(path)), "UTF-8")) {
  writer => writer.write(s"$text\n")
}
```
