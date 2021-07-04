# `Koltin`的必备基础知识

[toc]

## 基础知识

### 代码注释

代码注释的方法同`C++`

### 输出

输出是`Java`代码的简化版本, 可以直接`println()`

### 数学运算

运算符的操作方法同`C++`, 主要的区别在于**`Kotlin`的取余操作可以对浮点数进行操作** 

#### 位运算符

`Kotlin`所支持的是`shl`和`shr`操作, 分别对应算术左移和右移

#### 常用的数学函数

由`kotlin.math`所对应的标准库支持

#### 递增和递减

采用同`C++`方式的递增和递减, 以及简化的`*=`, `+=`等运算符

### 命名数据

* 常量数据

  ```kotlin
  val constant: T = data
  ```

  常量无法被再次赋值, 由于`Kotlin`采用引用的方式进行索引内存和变量名, 这里`val`仅仅意味着其中的`binding`无法改变, 但是却能够改变其中的内容

  同样的, 如果你想要这个常量在编译的时候就可以进行赋值, 可以采用如下方式:

  ```kotlin
  const val reallyConstant: T = data
  ```

  > Tips: 在使用编译时常量的时候只能初始化赋值为`String`, `Int`, `Double`等基本数据类型

* 变量

  ```kotlin
  var variableNum: T = data
  ```

  采用`var`关键字进行声明一个变量, 这种类型允许你自由的改变数据而不用担心出错



## 类型和运算符

### 类型转换

和`C++`不同的是, `Kotlin`不允许直接采用隐式类型转换, 所以每一种类型转换都必须要进行显示的声明(针对的两种不同的类型)

### 运算时采用不同的数据类型

运算过程中如果有不同类型的数据类型, `Kotlin`会进行隐式的类型转换, 将低精度的数据类型转换为高精度

### 类型

如果运算符右边的值有确定的类型, 那么`Kotlin`可以自动推导出左边的类型



`String`再`Kotlin`中

`char`类型必须要采用单引号, `String`类型必须采用双引号, 对于`Kotlin`中的字符串可以采用加法, `+=`等运算, 但是要注意`+=`运算实际上是产生了一个新的对象, 和以前的对象已经不再相同了.

### `String` templates

引入了string template方便格式化输出, 例如:

```kotlin
val message: String = "My name is $name"
```

`$`符号在这里的作用就是占位符的作用, 但是不提供一些个性化的模板

### 多行的字符串

`Kotlin`提供了一种简洁的方式来表达多行字符串

```kotlin
val bigString = """
	|xxxxxx
	|xxxxxx
	|xxxx
	""".trimMargin()
```

在这里我们采用三个双引号来表示多行字符串, 采用管道符`|`防止字符串出现前导的空格



### Pair和Triples

它们分别代表了二元组和三元组, 我们通常采用如下方式来生成二元组和三元组:

```kotlin
val coor: Pair<T, T> = Pair(a, b)
val coor = a to b
val x = coor.first
val y = coor.second
val (x, y) = coor
```

我们分别对下面的几种方式进行说明:

1. 最基本的泛型Pair, 和C++的用法相同
2. `Kotlin`特色方式, 这种方式形式为`key to value`, 这种的方法在之后的Map中得到广泛应用
3. 对最后一种方式我们通常称为元组的解包

对于`Triple`, 它的使用方法基本和`Pair`相同



### 数字的类型

`Kotlin`是完全面向对象的, 在`c`族编程语言当中会存在基本数据类型, 类似`Java`会存在自动包装机制. 对于`Kotlin`所有的类型都为对象, 我们给出如下的表示方式:

| Type     | Size |
| -------- | ---- |
| `Bytes`  | 1    |
| `Short`  | 2    |
| `Int`    | 4    |
| `Long`   | 8    |
| `Float`  | 4    |
| `Double` | 8    |

这样一来你就可以可以大致选取自己所需要的数据类型



### Any, Unit和Nothing类型

`Any`可以认为是除了`nullable`类型之外所有其它类型的父类, 因此可以将整数声明为`Any`类型, 例如:

```kotlin
val num: Any = 10
```

`Unit`仅仅代表`Unit`对象, 和`Java`中的`void`类型很像, 所有函数没有显式返回值的都会返回`Unit`

```kotlin
fun add(x: Int, y: Int): Unit {
    print("${x + y}")
}
```

`Nothing`表示一个函数既没有返回值, 也永远不会完成

```kotlin
fun doNothing(): Nothing {
    while (true) {
        //
    }
}
```



## 基础控制流

### 比较运算符

通用逻辑和`C++`相同, 同理比较字符串`String`是否相等, 以及短回路原则都同样适用

### if表达式

这一点和`C++`程序不同, `if`在这里不是一条语句, 而是一个带有返回值的表达式, `if`表达式的最后一句话返回`if`表达式的值. 其次注意`if`表达式中的域是封闭的, 也就是说在`if`中定义的变量, 外部是不可见的



### 循环

#### while循环

使用方法同`C++`



## 高级控制流

### Ranges序列

* 闭区间序列: `m..n`递增序列, `m downTo n`递减序列
* 开区间序列: `m until n` 递增序列

### for循环

除了基础的for循环之外, 也添加了`for in`(`step`指定步长), 同样也要注意循环变量只在循环内部可见, 并且**循环变量不可见**, 甚至你还可以使用`repeat(n)`方法指定重复的次数



### when表达式

它很像`switch`语句, 但是要远比`switch`语句强大

* ```kotlin
  when (singleValue) {
      case1, case2 -> do_something()
      case3, case4 -> do_anotherthing()
      ....
      else -> do_default()
  }
  ```

  上面的语句并非标准写法, 只是表达一种意思, 首先它不需要`C++`语句中的`break`, `->`就代表了一件事情的发生, 由于`when`是一个表达式, 因此**每种情况的最后一句话代表了一个返回值**

* 我们甚至可以在每种情况中采用`Ranges`

  ```kotlin
  when (hour) {
      in 0..5 ->
      in 6..11 ->
      else ->
  }
  ```

  采用`in`作为是否存在其中的标识

* 甚至可以不需要单值, 直接进行`when`

  ```kotlin
  when {
      num % 2 == 0 -> do_sth()
      else -> do_default()
  }
  ```



## 函数

首先明白一点, 函数中所有的形参类型均为`val`, 也就是不可变, 因此你无法修改一个函数的形参, **本质上来讲, 其实是你无法更改指向的指针**

函数的使用用法很像`C++`, 如下给出一个模板通例:

```kotlin
fun function(x: T1, y: T2): T3 {
    // do_sth
}
```

但是`kotlin`可以不断简化, 一行的函数可以直接写`=`, 还有提供函数默认值等等

其次不得不提的是函数重载, 这种形式和`C++`并无不同, 主要区别重载在于两个点:

* 形参类型
* 形参数目





## 可空性

这应该是`kotlin`独具特色的一点了吧, 如何对一个对象进行判空, 并引入了`nullable`可空类型



### 引入可空类型

可空类型既可以来表示一个值, 也可以用来表示`null`, 即当前没有值. 就好比一个盒子, 里面可以装东西, 也可以不装东西. 而非空类型保证盒子里面一定有东西. `kotlin`采用`T?`来表示可空类型, 并且可空类型一定要注意显式声明, 它是不可被推断的.



### 判空

可空类型仅在一些受限的场合下可以使用, 很重要的一点是**你无法直接对可空类型进行一些操作**, 因此首先进行判空是很重要的.

* 非空断言`Not-null assertion`(`!!`)

  如果你能够非常肯定的表示你的可空类型值不为空, 你可以在变量之后添加`!!`

  ```kotlin
  var num: Int? = 10
  val numBigger = num!! + 10
  // 这里就表明了你十分肯定num是个非空类型
  ```

* 智能转换

  也就是我们自行对可空类型进行`if else`检查, 然后再进行对应的操作

* 安全调用

  如果我们想要使用可空类型进行一些方法调用, 可以采用安全调用`?.`
  
* `let()`函数

  ```kotlin
  var author: Int?
  author?.let {
      // author在函数中成为非空类型
  }
  ```

* `Elvis`运算符(`?:`)

  ```kotlin
  var nullableInt: Int? = 10
  var num = nullableInt ?: 10
  ```

  这个运算符表明的意思是可空值不为空就选择这个值, 否则就选用运算符后的默认值, 和C++三目运算符效果很像.

  

## 数组和列表(Array & Lists)

### 数组

#### 基本使用方法

`kotlin`中的Arrays代表了`Java`中基础的`array`类型(类似`String[]`这种), 在连续的存储空间中存储多个值. 这里数组的含义和C++并无不同

* 创建数组`arrayOf()`, 产生的类型为`Array<T>`, `T`表示泛型; 同样我们还可以采用`Array(size: Int) { init }`的方式创建数组, 这里面用到了lambda表达式
* 创建基本数据类型的数组, `intArrayOf()`等用来创建基本数据类型数组, 在编译过程中这些数组会被转换成`T[]`
* 上述的数组都自带方法进行相互转换`toxxxx()`方法即可

#### 数组迭代

* 采用`for in`循环的方式, 方法同C++
* 采用lambda表达式, `args.forEach {}`



### Lists

`List`在`Kotlin`中也是一个接口**Interface**, 它有一些具体的实现如: `ArrayList`, `LinkedList`等, 一般来说数组比列表效率更高, 这在`C++`以及人尽皆知, 但是`List`可以动态扩容(dynamically-sized), 而数组只能是固定的尺寸.

#### 基本使用方法

* 创建一个列表

  ```kotlin
  val list = listOf() // 产生不可更改的列表
  val arrayList = arrayListOf() // 可变列表
  val mutableList = mutableListOf() // 可变列表
  ```

* **CURD**(主要针对可变列表)

  ```kotlin
  arrayList.isEmpty() // 判断表是否为空
  // size属性, first(), last()方法获取元素
  // 由于运算符重载的原因, 因此可以采用[]方法访问元素
  arrayList[2]
  // 数组切片, 切片产生的列表是新生成的, 和之前的列表无关
  arrayList.slice(1..2)
  // 检查元素是否在列表中
  arrayList.contain(2)
  // CURD
  add
  remove
  removeAt
  indexOf
  
  ```

* 列表的迭代, 基本和数组一致, 还可以使用`withIndex()`进行迭代, 从而包含下标信息

  ```kotlin
  for ((index, num) in numbers.withIndex()) {
      
  }
  ```

### 可空序列

* 序列可空`val nums: ArrayList<Int>?`
* 元素可空`val nums: ArrayList<Int?>`



## 表和集合(Maps & Sets)

### 表

#### 基本操作

* 创建表

  ```kotlin
  val map = mapOf(a to A, b to B) // 实际上是Pair对, 产生不可修改的map
  val mutableMap = mutableMapOf() // 可变表
  val hashMap = hashMapOf() // 哈希表
  val hashMap = HashMap<T1, T2>() // H链式ash表
  ```

* **CRUD**

  1. 采用下标方式的访问或者`get`方法
  2. 采用下标方式的增加更新或者`put`方法
  3. 采用`remove`进行移除

### 集合

无序唯一存在值的集合, 具有离散数学集合性质, 基本使用方式同上述, 不再赘述

需要注意的一点是类似`Python`的解包运算符, 将数组转化为集合

```kotlin
val someSet = mutableSetOf(*array)
```



## Lambda表达式

lambda表达式是没有名字的函数, 你可以将它分配给一个变量, 然后到处传递它

### Lambda基础

lambda被称为匿名函数, 又或者是闭包, 因为**它能在自己的域内关闭变量和常量**, 通俗地来讲就是:

* lambda能够具有上下文环境, 就像一个嵌套函数一样
* 定义在lambda内部地变量和常量无法被外部所访问, 具有闭包性

```kotlin
// examples
var lambda: (Int, Int) -> Int
// 这个例子表明了这个lambda函数接受两个Int型参数, 返回Int

lambda = { a: Int, b: Int -> Int
          a * b
}
// 由于lambda表达式自动返回最后一行作为返回值
```

但是有以下几点需要注意:

* lambda不知此参数名赋值, 也就是某个形参等于实参这种赋值方式
* lambda表达式要注明形参列表和返回值

### 精简语法

* 由于上面我们对`lambda`这个函数进行类型声明, 因此我们可以直接省略所有的类型声明

	```kotlin
	lambda = {a, b -> 
		a * b         
	}
```

* `it`关键字针对只有一个参数的时候, 可以直接使用`it`作为参数



### Lambda作为参数

```kotlin
fun opOnNum(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    val result = operation(a, b)
    println(result)
    return result
}

opOnNum(4, 2, lambda) // 如果是你传入的为lambda表达式, 那么直接传入即可

fun add(x: Int, y: Int): Int {
    return x + y;
}

opOnNum(1, 2, ::add) // 如果传入的是函数, 需要进行引用

opOnNum(10, 20, { a, b ->
	a + b
}) // 直接传入labmda表达式

// 如果lambda表达式在最后一个位置, 我们甚至可以直接, 将lambda表达式提出来写
opOnNum(10, 20) {a, b -> 
	a + b
}
```

> 当然咯, 如果`Unit`, `Nothing`也可以作为lambda的返回类型, 这里也不再一一赘述

由于lambda表达式具有上下文环境和闭包特性, 因此你可在lambda表达式内访问外部变量, 而内部变量无法被外部所访问.

### 内置lambda表达式

* `sort`函数

  ```kotlin
  val prices = arrayOf(10, 20, 30)
  prices.sortWith(compareBy {
      it % 10
  })
  ```

* `forEach`进行迭代

* `filter`可以迭代筛选`boolean`值为真的对象

* `map`进行迭代, 操作所有对象

* `fold`相当于对前后元素进行迭代操作, 需要传入第一个值

* `reduce`直接将第一个元素作为初始值



## 类

### 构建类

`Kotlin`中的类的构建方式和C++有所不同, 首先是它的主构造函数:

```kotlin
class Type(val para1: T, var para2 : T)
```

可以看到`kotlin`的主构造函数直接在括号中进行声明, 其中`para1`会作为类的一个属性, 对于`val`和`var`则表示了这个参数是否可变, 











