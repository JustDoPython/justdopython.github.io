---
layout: post
title: 弃繁就简！一行代码搞定 Python 日志！
category: python
tagline: by 闲欢
tags: 
  - python
  - 日志
---

写了这么多年的 Python ，我一直都是使用 Python 自带的 logging 模块来记录日志，每次需要写一些配置将日志输出到不同的位置，设置不同日志输出格式，或者将日志进行分文件和压缩等。这个日志模块没什么问题，直到我无意中发现了一个神器，我才发觉原来记日志可以这么简单的！这个神器就是 loguru 。

<!--more-->

### 安装

这个库的安装方式很简单，直接使用 pip 就可以，我使用 Python 3 版本，安装命令如下：

```
pip3 install loguru
```

### 小试牛刀

安装完毕之后，我们就可以使用了，最简单的使用方式：

```python

from loguru import logger

logger.debug('this is a debug message')

```

无需任何配置，即取即用。上例是打印一条 debug 级别的日志，输出结果如下：

```python

2021-03-16 22:17:23.640 | DEBUG    | __main__:<module>:8 - this is a debug message

```

这条输出日志信息包含了日期、时间、日志级别、日志代码行数以及日志内容信息。可以说最基本的内容都囊括了，当然你还可以打印 warning、info、error、critical、success 等级别。输出的日志在 console 中还带有高亮颜色，并且每个级别的日志颜色不一样，简直不要太酷！


### 日志文件

#### 写文件

在loguru中，输出日志文件只需要一个 add() 函数即可：

```python

logger.add('hello.log')

logger.debug('i am in log file')

```

这时候，在 console 中会正常打印日志信息，在同级目录下会生成一个日志文件 hello.log ，我们打开日志文件，可以看到内容如下：

```python

2021-03-16 21:20:31.460 | DEBUG    | __main__:<module>:12 - i am in log file

```

当然，我们还可以加一些参数，来指定文件中日志输出的格式、级别：

```python

log = logger.add('world.log', format="{time} | {level} | {message}", level="INFO")

logger.debug('i am debug message')
logger.info('i am info message')

```

对应的文件输出信息如下：

```python 

2021-03-16T22:47:53.226998+0800 | INFO | i am info message

```

我们设置了文件只记录 info 级别的信息，所以 debug 级别的日志信息并没有写入日志文件。

我们也可以给日志文件名称加信息：

```python

logger.add('hello_{time}.log')

```

上面的代码运行后，会生成一个带时间的日志文件。


#### 停止写入文件

当我们不再需要将日志写入文件时，我们随时可以停止：

```python

id = logger.add('world.log', format="{time} | {level} | {message}", level="INFO")
logger.info('this is a info message')
logger.remove(id)
logger.info('this is another info message')

```

add() 方法会返回一个日志文件的 id ，当我们需要停止写入信息时，我们使用 remove() 方法，传入 id ，即可。上面代码运行后，日志文件记录的信息如下：

```python

2021-03-16T22:47:53.227389+0800 | INFO | this is a info message

```

在调用 remove() 方法后，其后面的日志信息并没有写入日志文件中。


#### 滚动记录日志文件

我们可以配置 rotation 参数，来指定日志文件的生成方式，跟通常的日志记录一样，我们可以设置按照文件大小、时间、日期等来指定生成策略。

```python

# 超过200M就新生成一个文件
logger.add("size.log", rotation="200 MB")
# 每天中午12点生成一个新文件
logger.add("time.log", rotation="12:00")
# 一周生成一个新文件
logger.add("size.log", rotation="1 week")

```

#### 指定日志文件的有效期

我们还可以通过 retention 参数来指定日志文件的保留时长：

```python

logger.add("file.log", retention="30 days") 

```

通过上面的配置，可以指定日志文件最多保留30天，30天之前的日志文件就会被清理掉。

#### 配置压缩文件

为了节省空间，我们可能存在压缩日志文件的需求，这个 loguru 也可以实现：

```python

logger.add("file.log", compression="zip") 

```

通过上面的配置，我们指定了日志文件的压缩格式为 zip 。


### 异常捕获

loguru 不仅可以记录日志，还可以捕获异常信息，这个
可以帮助我们更好地追溯错误原因。

在 loguru 模块中，我们通常有两种异常捕获方式：通过 catch 装饰器捕获和通过 exception 方法捕获。

#### catch 装饰器捕获异常

我们来看一个例子：

```python

@logger.catch
def a_function(x):
    return 1 / x

a_function(0)

```

输出信息如下：

```
021-03-16 23:10:28.124 | ERROR    | __main__:<module>:32 - An error has been caught in function '<module>', process 'MainProcess' (25939), thread 'MainThread' (140735895298944):
Traceback (most recent call last):
  File "/Users/cxhuan/Library/Application Support/JetBrains/IntelliJIdea2020.3/plugins/python/helpers/pydev/pydevconsole.py", line 483, in <module>
    pydevconsole.start_client(host, port)
    │            │            │     └ 62146
    │            │            └ '127.0.0.1'
    │            └ <function start_client at 0x10fd596a8>
    └ <module 'pydevconsole' from '/Users/cxhuan/Library/Application Support/JetBrains/IntelliJIdea2020.3/plugins/python/helpers/py...
  
    ......
  
> File "/Users/cxhuan/Documents/python_workspace/mypy/loguru/logurustudy.py", line 32, in <module>
    a_function(0)
    └ <function a_function at 0x11021e620>
  File "/Users/cxhuan/Documents/python_workspace/mypy/loguru/logurustudy.py", line 30, in a_function
    return 1 / x
               └ 0
ZeroDivisionError: division by zero

```

上面的代码中，我特意造了一个 1 除以 0 的异常，我们可以看到日志输出信息非常详细，将每一步调用的错误信息都详细的列出来，并且还把参数的值也打印出来了，还有非常直观的指向性，简直是异常分析神器！

#### exception 方法捕获异常

我们直接看例子：

```python

def b_function1(x):
    try:
        return 1 / x
    except ZeroDivisionError:
        logger.exception("exception!!!")

b_function1(0)

```

运行上面代码，输出信息如下：

```python

2021-03-16 23:16:07.602 | ERROR    | __main__:b_function1:40 - exception!!!
Traceback (most recent call last):
  File "/Users/cxhuan/Library/Application Support/JetBrains/IntelliJIdea2020.3/plugins/python/helpers/pydev/pydevconsole.py", line 483, in <module>
    pydevconsole.start_client(host, port)
    │            │            │     └ 62254
    │            │            └ '127.0.0.1'
    │            └ <function start_client at 0x118d216a8>
    └ <module 'pydevconsole' from '/Users/cxhuan/Library/Application Support/JetBrains/IntelliJIdea2020.3/plugins/python/helpers/py...
  File "/Users/cxhuan/Library/Application Support/JetBrains/IntelliJIdea2020.3/plugins/python/helpers/pydev/pydevconsole.py", line 411, in start_client
    process_exec_queue(interpreter)
    │                  └ <_pydev_bundle.pydev_ipython_console.InterpreterInterface object at 0x118d36240>
    └ <function process_exec_queue at 
    0x118d21400>
    
    ......
    
  File "/Users/cxhuan/Documents/python_workspace/mypy/loguru/logurustudy.py", line 42, in <module>
    b_function1(0)
    └ <function b_function1 at 0x11913b598>
> File "/Users/cxhuan/Documents/python_workspace/mypy/loguru/logurustudy.py", line 38, in b_function1
    return 1 / x
               └ 0
ZeroDivisionError: division by zero

```

同样地，也是很详细和直观地打印了错误详情。


### 总结

有需求就有实现，但是能把众多人的需求实现得这么优雅、简洁的，我只服这个 loguru 的作者。而且还附加了许多非常有用的功能，简直是个鬼才！如果你觉得今天分享的神器有用，点个“**在看**”支持一下吧！


> 示例代码：(https://github.com/JustDoPython/python-examples/tree/master/xianhuan/loguru)