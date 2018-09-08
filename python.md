# Python

## Import 

[thanks](https://medium.com/@peterchang_82818/python-import-from-as-cheatsheet-tutorial-example-beginner-help-module-function-def-5f03b02a1dbe)

Example, we have a lib called `module.py`

```text
# module.py

def fun1(n):
  return n+1
```

There are four way to import `module.py`

**1- import**

```text
import module

module.fun1(1000) #1001
```

#### **2- from**

```text
from module import fun1

fun1(1000) #1001
```

**3- import \***

```text
from module import *

fun1(1000) #1001
```

**4- import as**

```text
import module as lib

lib.fun1(1000) #1001
```



