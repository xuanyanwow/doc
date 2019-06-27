# 依赖注入

Dependency Injection  依赖注入

EasySwoole实现了简单版的IOC，使用 IOC 容器可以很方便的存储/获取资源，实现解耦。

使用依赖注入，最重要的一点好处就是有效的分离了对象和它所需要的外部资源，使得它们松散耦合，有利于功能复用，更重要的是使得程序的整个体系结构变得非常灵活。

在我们的日常开发中，创建对象的操作随处可见以至于对其十分熟悉的同时又感觉十分繁琐，每次需要对象都需要亲手将其new出来，甚至某些情况下由于坏编程习惯还会造成对象无法被回收，这是相当糟糕的。但更为严重的是，我们一直倡导的松耦合，少入侵原则，这种情况下变得一无是处。于是前辈们开始谋求改变这种编程陋习，考虑如何使用编码更加解耦合，由此而来的解决方案是面向接口的编程。

> 注意：在服务启动后，对IOC容器的获取/注入仅限当前进程有效。不对其他worker进程产生影响。

## 方法列表

### getInstance

```php
$di = Di::getInstance();
```

### set

函数原型：set($key, $obj,...$arg)

- key：键名

- obj:要注入内容。支持注入对象名，对象实例,闭包，资源，字符串等各种常见变量。

- $arg:若注入的内容为is_callable，则可以设置该参数以供callable执行时传入。

```php
$di->set('test',new TestClass());
$di->set('test',TestClass::class);

// set的时候储存的是[类名, 方法名]的数组，需要自己手动调用call_user_func()执行 (不要因错误与异常章节的demo而误解会自动执行)
$di->set('test', [TestClass::class,'testFunction']);

// set的时候传递了类名，get的时候才去new对象，并且将可变变量传递进构造函数，返回实例化后的对象
$di->set('test', TestClass::class, $arg_one, $arg_tow);
```

> Di的set方法为懒惰加载模式，若set一个对象名或者闭包，则该对象不会马上被创建。

### get

```php
$db = $db->get('test');
```

### delete

```php
$di->delete('test');
```

### clear

清空 IoC 容器的所有内容。





