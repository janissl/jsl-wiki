Literal string interpolation
============================

#### Python example

```python
hostname = 'localhost'
ip_address = '127.0.0.1'

# Option 1 (%)
print('%s uses the IP address %s' % (hostname, ip_address))

# Option 2 ({})
print('{} uses the IP address {}'.format(hostname, ip_address))

# Option 3 ({0}, {1}...)
print('{1} uses the IP address {0}'.format(ip_address, hostname))

# Option 4 (parameters)
print('{a} uses the IP address {b}'.format(a=hostname, b=ip_address))

# Option 5 (**kwargs)
params = {'hostname': 'localhost',
          'ip_address': '127.0.0.1'}
print('{hostname} uses the IP address {ip_address}'.format(**params))

# Option 6 (f-strings)
print(f'{hostname} uses the IP address {ip_address}')
```

#### Scala example

```scala
// Include variables in strings using s""
val hostname = "localhost"
val ipAddress = "127.0.0.1"
s"$hostname uses the IP address $ipAddress"
//res1: String = localhost uses the IP address 127.0.0.1

// Escape double quotes with triple double quotes
val person = """{"name":"James"}"""
//person: String = {"name":"James"}

// Display a double with two decimal places using f""
val ratio = 6.7854
f"The current ratio is $ratio%.2f."
//res2: String = The current ratio is 6.79.

// Retain backslash-escaped characters (useful for e.g. regular expressions) using raw""
import scala.util.matching.Regex
val word = "window"
val pattern = raw"\b$word\b".r

pattern findFirstIn "This is Windows OS"
//res3: Option[String] = None

pattern findFirstIn "Window closed"
//res4: Option[String] = None

pattern findFirstIn "Open a window"
//res5: Option[String] = Some(window)

pattern findFirstIn "All windows are open"
//res6:  Option[String] = None
```