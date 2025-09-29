# kotlin 变量

var: 用此关键字声明的变量表示可变变量，即可读且可写。相当于 Java 中普通变量
val: 用此关键字声明的变量表示不可变变量，即可读且不可写。相当于 Java 中用 final 修饰的变量

```格式
var a:Int=10
val b:Int=5
```

## 声明可空变量

```
var a:Int?=0
val b:Int?=5
```

## 常量

在 val 关键字前面加上 const 关键字

```
const val a=6
```

声明常量的三种正确方式

1. 在顶层声明
2. 在 object 修饰的类中声明，在 kotlin 中称为对象声明，它相当于 Java 中一种形式的单例类
3. 在伴生对象中声明

```kt
// 1. 顶层声明
const val NUM_A : String = "顶层声明"
// 2. 在object修饰的类中
object TestConst{    
    const val NUM_B = "object修饰的类中"
    }
// 3. 伴生对象中
class TestClass{    
    companion object {        
        const val NUM_C = "伴生对象中声明"    
        }
        }

fun main(args: Array<String>) {    
    println("NUM_A => $NUM_A")    
    println("NUM_B => ${TestConst.NUM_B}")    
    println("NUM_C => ${TestClass.NUM_C}")
    }

```

# 数值类型

```md
- Byte=> 字节 => 8 位
- Short => 短整型 => 16 位
- Int => 整型 => 32 位
- Long => 长整型 => 64 位
- Float => 浮点型 => 32 位
- Double => 双精度浮点型 => 64 位
- Boolean => 布尔类型 =>true ,false
- Char => 字符 => 字符变量用单引号（‘ ’）表示
- String => 字符串 =>
- Array => 数组 =>
```

## 两个数值的比较

判断两个数值是否相等（\==）,判断两个数值在内存中的地址是否相等（===）
## 显示转换
```
  toByte() => 转换为字节型
  
  toShort() => 转换为短整型
  
  toInt() => 转换为整型
  
  toLong() => 转换为长整型
  
  toFloat() => 转换为浮点型
  
  toDouble() => 转换为双精度浮点型
  
  toChar() => 转换为字符型
  
  toString() => 转换为字符串型
```

## 位运算符
Kotlin中对于按位操作，和Java是有很大的差别的。Kotlin中没有特殊的字符，但是只能命名为可以以中缀形式调用的函数，下列是按位操作的完整列表(仅适用于整形（Int）和长整形（Long）)：
  
  - shl(bits) => 有符号向左移 (类似Java的&lt;&lt;)
  - shr(bits) => 有符号向右移 (类似Java的&gt;&gt;)
  - ushr(bits) => 无符号向右移 (类似Java的&gt;&gt;&gt;)
  - and(bits) => 位运算符 and (同Java中的按位与)
  - or(bits) => 位运算符 or (同Java中的按位或)
  - xor(bits) => 位运算符 xor (同Java中的按位异或)
  - inv() => 位运算符 按位取反 (同Java中的按位取反)

## 字符串字面量
在Kotlin中， 字符串字面量有两种类型：

- 包含转义字符的字符串 转义包括（\t、\n等）,不包含转义字符串的也同属此类型
- 包含任意字符的字符串 由三重引号（""" …. """）表示

## 数组的创建
- arrayOf()
创建一个数组，参数是一个可变参数的泛型对象
```
var arr2 = arrayOf("0","2","3",'a',32.3f)
```
- arrayOfNulls()
用于创建一个指定数据类型且可以为空元素的给定元素个数的数组
```
var arr3 = arrayOfNulls<Int>(3)
```
- 工厂函数（Array()）
1. 使用一个工厂函数Array()，它使用数组大小和返回给定其索引的每个数组元素的初始值的函数。
2. Array() => 第一个参数表示数组元素的个数，第二个参数则为使用其元素下标组成的表达式
```
var arr4 = Array(5,{index -> (index * 2).toString() })
```

## 原始类型数组
Kotlin还有专门的类来表示原始类型的数组，没有装箱开销，它们分别是：
  
1.  ByteArray => 表示字节型数组
2.  ShortArray => 表示短整型数组
3.  IntArray => 表示整型数组
4.  LongArray => 表示长整型数组
5.  BooleanArray => 表示布尔型数组
6.  CharArray => 表示字符型数组
7.  FloatArray => 表示浮点型数组
8.  DoubleArray => 表示双精度浮点型数组

```
var intArr: IntArray = intArrayOf(1,2,3,4,5)
```

# 控制语句
# if

在 Kotlin 中，if 是表达式（而非单纯的语句），这意味着它可以有返回值。其返回值取决于分支中最后一个表达式的结果 —— 如果分支的最后是一个变量，那么整个 if 表达式就会返回该变量的值
## 三元运算符
- 在Kotlin中其实是不存在三元运算符(condition ? then : else)这种操作的
- 因为if语句的特性(if表达式会返回一个值)故而不需要三元运算符
```
var num:Int = if(num1>2) 3 else 1
```
# for
- Kotlin废除了Java中的for(初始值;条件；增减步长)这个规则。但是Kotlin中对于for循环语句新增了其他的规则，来满足刚提到的规则。
- for循环提供迭代器用来遍历任何东西
- for循环数组被编译为一个基于索引的循环，它不会创建一个迭代器对象

## 新增规则
1. 递增
- 关键字 until  
- 范围 until[n,m) 大于等于n,小于m
```
//  循环5次，且步长为1的递增
for(i in 0 until 5){
  print("$i")
}
```
2. 递减
-关键字 downTo
- 范围 downTo[n.m] 
```
 // 循环5次，且步长为1的递减
 for (i in 15 downTo 11){
     print("i => $i \t")
 }
```

3. 符号（' .. '） 表示递增的循环的另外一种操作
- 符号 ..
- 范围 ..[n,m] 
```
//循环6次,步长为1增加
for(i in 20 .. 25){
  print($i)
}
```

4. 设置步长 step
```
for(i in 10 until 16 step 2)
for(i in 10 .. 16 step 2)
for(i in 10 downTo 4 step 2)
```

## 迭代
- for循环提供一个迭代器用来遍历任何东西。
- for循环数组被编译为一个基于索引的循环，它不会创建一个迭代器对象
1. 遍历字符串
```
for(i in "abcdef"){
  print("$i\t")
}
```
2. 遍历数组
```
var arrayList =arrayOf(10,1,2,3)
for(i in arrayList){
  print("$i\t")
}
```

3. 使用数组的indices属性遍历
```
var arrayList =arrayOf(10,1,2,3)
for(i in arrayList.indices){
  println("array[$i]"+arrayList[i])
}

```

4. 使用数组的withIndex()方法遍历
```
var arrayList =arrayOf(1,2,3,4,5)
for((index,val) in arrayList.withIndex()){
  println("Index-$index\t vslue-$val")
}
```

5. 迭代器遍历
其一般和while循环一起使用
```
var arrayList=arrayOf(1,2,false,9)
var iterator:Iterator<Any> =arrayList.iterator()
while(iterator.hasNext()){
  println(iterator.next())
}
```

6. foreach遍历
```
 val array = arrayOf(2,'a',3,false,9)
 array.forEach { println(it) }
```

# when
Kotlin 的 when 语句是一种强大的条件判断结构，类似于 Java 的 switch，但功能更灵活、语法更简洁，支持更多样的匹配逻辑。它既可以作为语句（执行逻辑），也可以作为表达式（有返回值），是 Kotlin 中替代复杂 if-else 链的优选方案。
## 基本语法
```
when (变量/表达式) {
    条件1 -> 逻辑1  // 满足条件1时执行逻辑1
    条件2 -> 逻辑2  // 满足条件2时执行逻辑2
    else -> 默认逻辑  // 所有条件都不满足时执行（可选）
}
```

```
val 结果 = when (变量/表达式) {
    条件1 -> 结果1  // 满足条件1时返回结果1
    条件2 -> 结果2  // 满足条件2时返回结果2
    else -> 默认结果  // 必须覆盖所有可能，否则编译报错
}
```
## 用法
1. 支持多值匹配（用逗号分隔）
```
val num = 3
when (num) {
    1, 3, 5 -> println("奇数")  // num为1、3、5时都执行
    2, 4, 6 -> println("偶数")
    else -> println("不在1-6范围内")
}
// 输出：奇数
```
2. 支持范围匹配
```
val score = 85
when (score) {
    in 90..100 -> println("优秀")
    in 80 until 90 -> println("良好")  // until 是左闭右开范围
    in 60 until 80 -> println("及格")
    !in 0..100 -> println("分数无效")
    else -> println("不及格")
}
// 输出：良好
```

3. 支持类型匹配（is 关键字）
```
fun printType(value: Any) {
    when (value) {
        is String -> println("是字符串，长度：${value.length}")  // 自动转成String
        is Int -> println("是整数，值的两倍：${value * 2}")       // 自动转成Int
        is Boolean -> println("是布尔值：$value")
        else -> println("未知类型")
    }
}

printType("hello")  // 输出：是字符串，长度：5
printType(100)      // 输出：是整数，值的两倍：200
```

4.  支持表达式作为分支条件
```
val x = 10
val y = 20
when (x) {
    y - 10 -> println("x 等于 y-10")  // 表达式 y-10 的结果是10，与x匹配
    y -> println("x 等于 y")
    else -> println("不匹配")
}
// 输出：x 等于 y-10
```

5. 不带参数的 when
when 可以不带参数，此时每个分支是一个布尔表达式，执行第一个结果为 true 的分支（类似多条件 if-else）：
```
val age = 17
val hasId = true

when {
    age >= 18 && hasId -> println("可以独立办理业务")
    age < 18 && hasId -> println("需监护人陪同")
    !hasId -> println("请先办理身份证")
    else -> println("条件不满足")
}
// 输出：需监护人陪同
```
# 可空类型
在 Kotlin 中，默认情况下，所有变量和参数都是非空类型（Non-null），即不能赋值为 null。如果需要允许变量为 null，必须在类型后添加 ? 显式声明为可空类型（Nullable）
```
// 非空类型（默认）：不能赋值为 null
val str: String = "hello"
str = null  // 编译报错：非空类型不能赋值为 null

// 可空类型（显式声明 ?）：可以赋值为 null
val nullableStr: String? = "world"
nullableStr = null  // 合法：可空类型允许赋值为 null
```
##  安全调用运算符 ?.
如果对象为 null，?. 会直接返回 null，而不会抛出异常；如果对象非 null，则正常调用方法 / 属性。
## let 操作符
let 函数可以配合 ?. 使用，仅当可空变量非 null 时执行代码块，避免冗余的 if 判断
```
val nullableStr: String? = "hello"

// 仅当 nullableStr 非 null 时，执行 lambda 表达式（it 代表非空的变量）
nullableStr?.let { 
    println("长度：${it.length}")  // 输出：长度：5
}

val nullStr: String? = null
nullStr?.let { 
    println(it)  // 不会执行，因为 nullStr 为 null
}
```
##  Elvis 运算符 ?:
当左侧表达式为 null 时，使用右侧的默认值；如果左侧非 null，则使用左侧的值。常用于为可空类型提供 “兜底” 值。
```
val nullableStr: String? = null

// 如果 nullableStr 为 null，使用默认值 "default"
val str = nullableStr ?: "default"  
println(str)  // 输出：default

// 结合安全调用使用
val length = nullableStr?.length ?: -1  // 为 null 时返回 -1
println(length)  // 输出：-1
```
## 非空断言 !!.
强制认定可空类型 “一定非 null”，如果实际为 null，会直接抛出 NullPointerException。谨慎使用，仅在确定变量不可能为 null 时使用
## 安全转换 as?
将对象转换为目标类型，如果转换失败（如类型不匹配），返回 null 而不是抛出 ClassCastException。
```
val obj: Any? = "123"

// 安全转换为 String：成功则返回字符串，失败返回 null
val str = obj as? String  
println(str)  // 输出：123

val num = obj as? Int  // 转换失败，返回 null
println(num)  // 输出：null
```

# 函数
## 函数声明
```
fun basis(){
  //something...
}
```
## 成员函数
成员函数是指在类或对象中的内部函数
```
class Test{
  fun foo(){
    //...
  }
}
```

## 函数使用
```
// 普通的使用
basis()
// 如果函数有返回值
val x = basis()

// 成员函数的使用：先初始化对象，在根据对象使用`中缀符号(.)`调用其成员函数
Test().foo()
// 如果函数有返回值
val x = Test().foo()
```

## 函数的返回值
在Kotlin中，函数的返回值类型可以分为：
- Unit类型：该类型即无返回值的情况，可以省略。
- 其他类型： 显示返回类型的情况
```
fun unitFun(): Unit{
  println("Unit")
  return 

   // return Unit 可省略
    // 或者 return  可省略
}

//等价于
fun unitFun(){
  print("Unit")
}

```
函数具有返回值，返回值类型不能省略，并且return也不能省略
```
fun returnFun() : Int{
    return 2
}
```

## 函数的参数
### 1.基本参数声明
函数参数的基本格式为：参数名: 类型，多个参数用逗号分隔。
参数在函数体内可直接使用，其作用域仅限于函数内部。
```
// 定义一个接收两个Int参数的函数
fun sum(a: Int, b: Int): Int {
    return a + b // 直接使用参数a和b
}

// 调用函数时传入参数
fun main() {
    val result = sum(3, 5) // 传入3和5作为参数值
    println(result) // 输出：8
}
```
### 2. 默认参数
Kotlin 允许为参数指定默认值，调用函数时可省略该参数（使用默认值），减少函数重载的需求。
```
// 为name参数设置默认值"Guest"
fun greet(name: String = "Guest", message: String = "Hello") {
    println("$message, $name!")
}

fun main() {
    greet() // 省略所有参数，使用默认值：Hello, Guest!
    greet("Alice") // 只传第一个参数：Hello, Alice!
    greet(message = "Hi", name = "Bob") // 显式指定参数名，顺序可交换：Hi, Bob!
}
```

### 3. 命名参数
调用函数时，可通过参数名 = 值的形式指定参数，增强代码可读性（尤其参数较多或类型相同时）
```
fun printUserInfo(name: String, age: Int, city: String) {
    println("Name: $name, Age: $age, City: $city")
}

fun main() {
    // 不使用命名参数（需按顺序传递）
    printUserInfo("Alice", 25, "Beijing")
    
    // 使用命名参数（顺序可任意）
    printUserInfo(age = 30, name = "Bob", city = "Shanghai")
}
```

### 4.可变参数
用vararg修饰的参数允许接收可变数量的同类型参数（类似 Java 的...），一个函数最多只能有一个可变参数

```
// 定义可变参数函数：计算多个Int的和
fun sumAll(vararg numbers: Int): Int {
    var total = 0
    for (num in numbers) { // numbers是一个数组，可迭代
        total += num
    }
    return total
}

fun main() {
    val result1 = sumAll(1, 2, 3) // 传入3个参数：6
    val result2 = sumAll(10, 20, 30, 40) // 传入4个参数：100
    println(result1) // 6
    println(result2) // 100
}
```
传递数组给可变参数：需用*（展开运算符）将数组 “展开” 为单个元素
```
fun main() {
    val nums = intArrayOf(5, 6, 7)
    val result = sumAll(1, 2, *nums) // 等价于 sumAll(1, 2, 5, 6, 7)
    println(result) // 21
}
```
## 单表达式函数
单表达式函数省略了传统函数的花括号 {} 和 return 关键字，直接用 = 连接函数声明与表达式：
```
// 传统函数写法
fun add(a: Int, b: Int): Int {
    return a + b
}

// 单表达式函数写法
fun add(a: Int, b: Int): Int = a + b
```

# 类
关键字 class
```
class Test {
// 属性...
 ...
// 构造函数
 ...
// 函数
 ...
// 内部类
 ...
 ...
}
```
## 构造函数
在 Kotlin 中，类的构造函数分为两种：主构造函数（primary constructor）和次构造函数（secondary constructor）。它们的作用是初始化类的实例，但使用场景和语法有所不同。
### 主构造函数
主构造函数是类头的一部分，类名的后面跟上构造函数的关键字以及类型参数。
```
class Test constructor(num : Int){
    ...
}
```
等价于
```
/*
   因为是默认的可见性修饰符且不存在任何的注释符
   故而主构造函数constructor关键字可以省略
*/
class Test(num: Int){
    ...
}
```
###  构造函数中的初始化代码块
- 构造函数中不能出现其他的代码，只能包含初始化代码。包含在初始化代码块中。
- 关键字：init{…}
```

class Test constructor(var num : Int){
    init {
        num = 5
        println("num = $num")
    }
}

```
### 次构造函数
当类需要多种初始化方式时，可以定义次构造函数。次构造函数用 constructor 关键字声明，必须直接或间接调用主构造函数。
```
class Person(val name: String, var age: Int) {
    // 次构造函数1：只传name，age默认20
    constructor(name: String) : this(name, 20) {
        println("次构造函数1调用：默认年龄20")
    }
    
    // 次构造函数2：无参，name默认"Unknown"，age默认0
    constructor() : this("Unknown") {  // 间接调用主构造函数（通过次构造函数1）
        println("次构造函数2调用：无参初始化")
    }
    
    init {
        println("主构造函数初始化块")
    }
}

// 使用
fun main() {
    val p1 = Person("Bob", 30)  // 调用主构造函数
    val p2 = Person("Charlie")  // 调用次构造函数1
    val p3 = Person()           // 调用次构造函数2
}
```
执行顺序：init块 会在所有构造函数（主 / 次）执行时优先执行，且按定义顺序执行。
### 无主构造函数无主构造函数的情况：如果类没有显式定义主构造函数，那么所有次构造函数无需调用 this(...)，但此时类默认的无参主构造函数会被隐藏。
```
class Car {
    var brand: String
    
    // 次构造函数（此时无主构造函数）
    constructor(brand: String) {
        this.brand = brand
    }
}
```
## 类的实例化
创建一个类的实例，需要调用类的构造函数，就像它是一个常规函数一样\
```
var test = Test()
var test1 = Test(1,2)
```
## 属性
Kotlin 中的「属性」是对数据的封装，它不仅包含数据的存储，还包含对数据的访问逻辑（getter）和修改逻辑（setter）。这与 Java 中单纯的「字段（Field）」+「getter/setter 方法」的模式不同 ——Kotlin 直接将这些整合为一个「属性」概念，大幅简化了代码。
```
class Person {
    // 只读属性（val）：只有 getter，没有 setter
    val name: String = "Tom"
    
    // 可变属性（var）：有 getter 和 setter
    var age: Int = 20
}
```
## 字段
Kotlin 中没有直接声明「字段」的语法，字段通常指 后备字段（Backing Field），它是属性用于存储实际数据的变量，由 Kotlin 自动生成和管理。
### 当属性需要存储数据时，Kotlin 会隐式创建后备字段 如:
- 声明属性时指定了初始值（如 var age: Int = 20）。
- 在自定义访问器（getter/setter）中使用 field 关键字引用时。
### field 关键字
在自定义访问器中，field 用于引用当前属性的后备字段，避免访问器递归调用自身
```
class Person {
    var age: Int = 0
        set(value) {
            // 使用 field 引用后备字段，存储实际值
            if (value >= 0) {
                field = value // 正确：修改后备字段
            } else {
                println("年龄不能为负数")
            }
        }
        get() {
            // 使用 field 获取后备字段的值
            return field + 1 // 示例：返回值加 1
        }
}

fun main() {
    val p = Person()
    p.age = -5 // 打印 "年龄不能为负数"，age 保持 0
    p.age = 20
    println(p.age) // 输出 21（因为 getter 中加了 1）
}
```
## 
## 可见性修饰符
修饰符          | 可见范围                                       |
| ------------ | ------------------------------------------ |
| `public`（默认） | 所有地方可见（不限制访问）                              |
| `private`    | 仅在**声明它的作用域内**可见（如类内部、文件内部）                |
| `protected`  | 与 `private` 类似，但**子类可以访问父类的 protected 成员** |
| `internal`   | 仅在**同一模块（Module）**  内可见

## 继承
在 Kotlin 中，类的继承遵循单继承原则（一个类只能有一个直接父类），且对继承有严格的显式声明要求（默认禁止继承，需主动开启）
## 1. open 关键字
```
open class Person { 
    // ...
}
```
## 2. :关键字
子类通过 : 继承父类（类似 Java 的 extends），且必须在构造函数中显式初始化父类构造函数。
### (1) 父类有主构造函数时
若父类有主构造函数，子类需在主构造函数中通过参数传递给父类构造函数
```
// 父类：有主构造函数
open class Person(val name: String, val age: Int) {
    fun introduce() {
        println("我叫 $name，今年 $age 岁")
    }
}

// 子类：继承 Person，主构造函数参数需传递给父类
class Student(name: String, age: Int, val studentId: String) : Person(name, age) {
    // 子类可以添加自己的属性和方法
    fun study() {
        println("$name 正在学习")
    }
}

fun main() {
    val student = Student("小明", 18, "2023001")
    student.introduce()  // 调用父类方法：我叫 小明，今年 18 岁
    student.study()      // 调用子类方法：小明 正在学习
}
```
### (2) 父类只有次构造函数时
若父类没有主构造函数，只有次构造函数，子类需在自己的次构造函数中用 super 调用父类的次构造函数
```
// 父类：无主构造函数，只有次构造函数
open class Person {
    var name: String = ""
    var age: Int = 0

    // 次构造函数
    constructor(name: String, age: Int) {
        this.name = name
        this.age = age
    }
}

// 子类：无主构造函数，次构造函数需调用父类次构造函数
class Student : Person {
    var studentId: String = ""

    // 子类次构造函数：用 super 调用父类次构造函数
    constructor(name: String, age: Int, studentId: String) : super(name, age) {
        this.studentId = studentId
    }
}
```
当父类没有主构造函数、只有次构造函数时，子类可以有主构造函数，但需要在子类的主构造函数中显式调用父类的某个次构造函数
```
// 父类：无主构造函数，只有两个次构造函数
open class Person {
    var name: String = ""
    var age: Int = 0

    // 次构造函数1：接收 name
    constructor(name: String) {
        this.name = name
    }

    // 次构造函数2：接收 name 和 age
    constructor(name: String, age: Int) {
        this.name = name
        this.age = age
    }
}

// 子类：有主构造函数，需调用父类的次构造函数
class Student(
    name: String, 
    age: Int, 
    val studentId: String  // 子类自己的属性
) : Person(name, age) {  // 主构造函数中调用父类的次构造函数（name, age）
    // 子类可以添加自己的方法
    fun getInfo() {
        println("姓名：$name，年龄：$age，学号：$studentId")
    }
}

fun main() {
    val s = Student("小李", 20, "2023003")
    s.getInfo()  // 输出：姓名：小李，年龄：20，学号：2023003
}
```
## 3. override 关键字
Kotlin 中，父类的方法 / 属性默认是 final（不可重写），需用 open 标记可重写成员；子类重写时必须用 override 关键字显式声明。
```
open class Person(val name: String) {
    // 用 open 标记，允许被重写
    open fun introduce() {
        println("我是 $name")
    }
    open val role:String="Person"
}

class Student(name: String, val studentId: String) : Person(name) {
    // 用 override 重写父类方法
    override fun introduce() {
        // 可通过 super 调用父类的实现
        super.introduce()
        println("我的学号是 $studentId")
    }
    override val role:String= "学生"
}

fun main() {
    val s = Student("小红", "2023002")
    s.introduce() 
    // 输出：
    // 我是 小红
    // 我的学号是 2023002
}
```
## 4.final 关键字
若子类重写了父类成员后，不希望自己的子类再重写，可以用 final 标记。
```
open class Person {
    open fun work() {
        println("工作中")
    }
}

open class Teacher : Person() {
    // 重写父类方法，但用 final 禁止子类再重写
    final override fun work() {
        println("教书")
    }
}

class MathTeacher : Teacher() {
    // 错误：无法重写 final 方法
    // override fun work() { }  // 编译报错
}
```
##  继承中的初始化顺序
子类初始化时，父类会先于子类完成初始化
## abstract 关键字 (抽象类)
抽象类是一种特殊的 open 类（无需显式加 open），可包含抽象成员（无实现，必须被子类重写）和具体成员
```kotlin
// 抽象类：默认可被继承
abstract class Animal {
    // 抽象方法：无实现，子类必须重写
    abstract fun sound()

    // 具体方法：有实现，子类可选择重写
    open fun eat() {
        println("进食中")
    }
}

// 子类必须重写抽象方法
class Dog : Animal() {
    override fun sound() {
        println("汪汪叫")
    }

    // 可选重写具体方法
    override fun eat() {
        println("狗吃骨头")
    }
}
```

## 枚举类
枚举类用于表示固定数量的常量集合（如星期、颜色、状态等），每个常量都是枚举类的实例。Kotlin 的枚举类比 Java 更灵活，支持属性、方法甚至匿名类实现。
### 基本声明
```
// 简单枚举类：表示星期
enum class Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```
###  带属性和方法的枚举类
```
// 带属性的枚举类：表示颜色及对应的RGB值
enum class Color(
    val rgb: Int  // 枚举常量的属性
) {
    // 每个常量都是枚举类的实例，需传入属性值
    RED(0xFF0000),
    GREEN(0x00FF00),
    BLUE(0x0000FF);  // 注意：最后一个常量后需加分号（如果有方法）

    // 枚举类的方法
    fun isDark(): Boolean {
        // RGB值越接近0，颜色越暗
        return rgb < 0x808080
    }
}

fun main() {
    println(Color.RED.rgb)  // 输出：16711680（0xFF0000的十进制）
    println(Color.BLUE.isDark())  // 输出：true（BLUE的RGB值较低）
}
```
### 枚举的常用方法
- values()：返回所有枚举常量的数组（按声明顺序）
- name：枚举常量的名称（如 RED.name 为 "RED"）
- ordinal：枚举常量的声明顺序索引（从 0 开始）
- valueOf(String)：根据名称获取枚举常量（名称必须完全匹配，否则抛异常）
```
fun main() {
    // 遍历所有枚举常量
    for (day in Day.values()) {
        println("${day.ordinal}: ${day.name}")
    }
    // 输出：0: MONDAY, 1: TUESDAY, ..., 6: SUNDAY

    // 通过名称获取枚举常量
    val friday = Day.valueOf("FRIDAY")
    println(friday)  // 输出：FRIDAY
}
```
###  枚举常量的匿名类
枚举常量可以通过匿名类重写方法，实现每个常量的个性化行为：
```
enum class Operation {
    // 每个常量用匿名类重写方法
    PLUS {
        override fun calculate(a: Int, b: Int) = a + b
    },
    MINUS {
        override fun calculate(a: Int, b: Int) = a - b
    },
    MULTIPLY {
        override fun calculate(a: Int, b: Int) = a * b
    };

    // 抽象方法：每个常量必须实现
    abstract fun calculate(a: Int, b: Int)
}

fun main() {
    println(Operation.PLUS.calculate(3, 5))   // 输出：8
    println(Operation.MINUS.calculate(10, 4)) // 输出：6
}
```

## 接口
接口用于定义行为规范（方法和属性），本身不实现具体逻辑，由类实现（implements）。Kotlin 接口类似 Java 8+ 的接口，支持抽象方法、默认方法（带实现）和属性，但接口不能有后备字段（存储数据）。
### 基本声明
用 interface 关键字声明接口，可包含抽象方法和默认方法：
```
// 定义接口：表示"可点击"的行为
interface Clickable {
    // 抽象方法（无实现，实现类必须重写）
    fun click()

    // 默认方法（有实现，用 "fun 方法名() { ... }"）
    fun showHint() {
        println("点击以交互")
    }
}
```

### 实现接口
类通过 : 实现接口（类似继承），可实现多个接口（用逗号分隔）。实现接口时，必须重写所有抽象方法，默认方法可选择重写。
```
// 实现 Clickable 接口
class Button : Clickable {
    // 必须重写抽象方法 click()
    override fun click() {
        println("按钮被点击")
    }

    // 可选重写默认方法 showHint()
    override fun showHint() {
        println("点击按钮提交")
    }
}

fun main() {
    val button = Button()
    button.click()    // 输出：按钮被点击
    button.showHint() // 输出：点击按钮提交
}
```
### 接口中的属性
接口可以声明属性，但不能有后备字段（无法存储数据），因此属性必须是：

- 抽象的（由实现类提供具体值）；
- 或提供自定义访问器（无后备字段）。
```
interface Named {
    // 抽象属性（实现类必须重写）
    val name: String

    // 带自定义访问器的属性（无后备字段）
    val description: String
        get() = "名称：$name"  // 依赖抽象属性 name
}

class Person(override val name: String) : Named {
    // 已重写 name，description 继承接口的默认实现
}

fun main() {
    val p = Person("张三")
    println(p.name)        // 输出：张三
    println(p.description) // 输出：名称：张三
}
```
## 数据类（Data Classes）
数据类的核心作用是专门用于存储数据（如模型对象、DTO 等）。Kotlin 会为数据类自动生成一系列常用方法（如 equals()、hashCode()、toString() 等），避免了 Java 中手动编写模板代码的繁琐。
### 声明与基本要求
数据类用 data class 关键字声明，且必须满足以下条件：

- 主构造函数至少包含一个参数；
- 主构造函数的参数必须是 val 或 var（即必须是属性，不能是普通参数）；
- 数据类不能是 abstract、open、sealed 或 inner；
```
// 简单数据类：存储用户信息
data class User(
    val id: Int,
    val name: String,
    var age: Int  // 可变属性
)
```

### 自动生成的方法
Kotlin 会为数据类自动生成以下方法（基于主构造函数的属性）：

- toString()：格式为 类名(属性1=值1, 属性2=值2, ...)；
- equals()：比较所有主构造函数的属性值是否相等；
- hashCode()：基于主构造函数的属性生成哈希值；
- componentN()：按主构造函数参数顺序生成的解构函数（用于解构声明）；
- copy()：用于复制对象并修改部分属性（不改变原对象）。
```
fun main() {
    val user1 = User(1, "Alice", 25)
    val user2 = User(1, "Alice", 25)
    val user3 = User(2, "Bob", 30)

    // 1. toString()：自动生成格式化字符串
    println(user1)  // 输出：User(id=1, name=Alice, age=25)

    // 2. equals()：比较属性值（而非引用）
    println(user1 == user2)  // 输出：true（属性完全相同）
    println(user1 == user3)  // 输出：false

    // 3. 解构声明（通过 componentN() 函数）
    val (id, name, age) = user1  // 对应 component1(), component2(), component3()
    println("id: $id, name: $name, age: $age")  // 输出：id: 1, name: Alice, age: 25

    // 4. copy()：复制并修改部分属性（原对象不变）
    val user4 = user1.copy(age = 26)  // 仅修改 age
    println(user4)  // 输出：User(id=1, name=Alice, age=26)
    println(user1)  // 原对象不变：User(id=1, name=Alice, age=25)
}
```

## 封装类(Sealed Class)
密封类用于表示受限的类层次结构（即一个值只能是有限的几种类型，不能是其他类型）。它是枚举类的扩展：枚举常量是单例，而密封类的子类可以有多个实例。

### 声明与特色
- 用 sealed class 关键字声明；
- 密封类的直接子类必须定义在同一个文件中（Kotlin 1.1 后允许在同一包内的不同文件，但通常建议同文件以保持关联性）；
- 密封类本身是抽象的，不能实例化；
- 密封类的子类可以是普通类、数据类、对象（单例）或其他密封类。
```
// 密封类：表示网络请求结果
sealed class Result

// 成功状态（数据类，可携带数据）
data class Success(val data: String) : Result()

// 失败状态（数据类，可携带错误信息）
data class Failure(val error: String) : Result()

// 加载状态（单例，无额外数据）
object Loading : Result()
```
### 核心优势：when 表达式的完整性检查
使用 when 表达式处理密封类时，如果覆盖了所有子类，就不需要写 else 分支，编译器会在编译时检查是否有遗漏，避免逻辑错误。
```
fun handleResult(result: Result) {
    when (result) {
        is Success -> println("成功：${result.data}")  // 处理成功
        is Failure -> println("失败：${result.error}")  // 处理失败
        Loading -> println("加载中...")                // 处理加载
        // 无需 else 分支：编译器知道已覆盖所有可能的子类
    }
}

fun main() {
    handleResult(Loading)        // 输出：加载中...
    handleResult(Success("数据")) // 输出：成功：数据
    handleResult(Failure("网络错误")) // 输出：失败：网络错误
}
```
## 嵌套类（Nested Classes）
默认情况下，Kotlin 中定义在类内部的类是嵌套类，它与外部类相互独立，不持有外部类的实例引用，因此无法访问外部类的非静态成员（属性或方法）
```
class Outer {
    private val outerProp = "外部类的属性"
    
    // 嵌套类：不使用 inner 关键字
    class Nested {
        fun nestedMethod() {
            // 错误：嵌套类不能访问外部类的非静态成员
            // println(outerProp) 
            
            println("这是嵌套类的方法")
        }
    }
}
```
调用嵌套类的属性或方法的格式为：外部类.嵌套类().嵌套类方法/属性。在调用的时候嵌套类是需要实例化的
```
fun main() {
    // 创建嵌套类实例：无需外部类实例
    val nested = Outer.Nested()
    nested.nestedMethod()  // 输出：这是嵌套类的方法
}
```

## 内部类
如果需要在嵌套类中访问外部类的实例成员，需用 inner 关键字声明为内部类。内部类持有外部类的实例引用，因此可以访问外部类的所有成员（包括私有成员）
```
class Outer {
    private val outerProp = "外部类的属性"
    private fun outerMethod() = "外部类的方法"
    
    // 内部类：用 inner 关键字声明
    inner class Inner {
        fun innerMethod() {
            // 可以访问外部类的所有成员（包括私有）
            println("访问外部类属性：$outerProp")
            println("调用外部类方法：${outerMethod()}")
        }
    }
}
```

- 调用内部类的属性或方法的格式为：外部类().内部类().内部类方法/属性。在调用的时候外部类、内部类都是需要实例化的
- 如果内部类与外部类有同名成员，可通过 this@外部类名 显式引用外部类的实例，避免歧义
```
class Outer {
    val name = "Outer"
    
    inner class Inner {
        val name = "Inner"
        
        fun printNames() {
            println("内部类的 name：$name")  // 访问内部类自己的 name
            println("外部类的 name：${this@Outer.name}")  // 显式访问外部类的 name
        }
    }
}

fun main() {
    Outer().Inner().printNames()
    // 输出：
    // 内部类的 name：Inner
    // 外部类的 name：Outer
}
```
## 匿名内部类
Kotlin 中的匿名内部类是一种不需要显式声明类名就能创建对象实例的方式，主要用于实现接口或继承类并重写其方法
### 基本语法
在 Kotlin 中，使用 object 关键字创建匿名内部类：
```
interface OnClickListener {
    fun onClick()
    fun onLongClick(): Boolean
}

val clickListener = object : OnClickListener {
    override fun onClick() {
        println("点击事件触发")
    }
    
    override fun onLongClick(): Boolean {
        println("长按事件触发")
        return true
    }
}
```
### 匿名对象
在 Kotlin 中，还可以创建不实现任何接口或继承任何类的匿名对象：
```
val obj = object {
    val name = "匿名对象"
    fun printName() {
        println(name)
    }
}

obj.printName() // 输出：匿名对象
```

## 类型别名（Type Aliases） 
类型别名允许为已有的类型创建一个替代名称，主要用于简化复杂类型的书写，或为语义不明确的类型提供更清晰的名称。它不会创建新类型，只是原类型的 "别名"。
### 关键字 typealias

# Lambda表达式
## 基本语法
```
{ 参数列表 -> 函数体 }
```
- 参数列表：用逗号分隔的参数，可指定类型（通常可省略，由编译器推断）
- ->：分隔参数列表和函数体
- 函数体：包含具体逻辑，最后一行表达式的结果会自动作为返回值（无需显式return）

无参数的 Lambda
```
// 无参数，函数体为打印语句
val greet: () -> Unit = { println("Hello, Lambda!") }

// 调用Lambda（通过invoke()或直接加括号）
greet()  // 输出：Hello, Lambda!
greet.invoke()  // 等价写法
```
带参
```
val sum: (Int,Int) -> Int= {a,b->a+b}
```
## 简化规则
### 1.省略参数类型（类型推断）
```
//完整写法 (a:Int,b:Int)->Int={a*b}
val multiply={a,b->a*b}
```
### 2单个参数的it关键字
如果 Lambda 只有一个参数，可省略参数列表，用it代替该参数：
```
// 完整写法：{ s: String -> println(s) }
val printString: (String) -> Unit = { println(it) }  // it代表唯一参数

printString("Hello, it!")  // 输出：Hello, it!
```
### 3. 作为最后一个参数时的位置简化
如果 Lambda 是函数的最后一个参数，可将其移到函数括号外面；如果函数只有一个 Lambda 参数，甚至可以省略括号：
```
// 定义一个接收Lambda的函数
fun doSomething(action: (String) -> Unit) {
    action("执行Lambda")
}

// 简化写法：Lambda移到括号外
doSomething { message ->
    println("收到：$message")  // 输出：收到：执行Lambda
}

// 进一步简化（因只有一个参数，用it）
doSomething {
    println("收到：$it")  // 输出：收到：执行Lambda
}
```
## Lambda 在集合操作中的典型应用
```
val numbers = listOf(1, 2, 3, 4, 5)

// 1. forEach：遍历集合
numbers.forEach { println(it) }  // 依次打印1-5

// 2. filter：筛选元素（保留偶数）
val evenNumbers = numbers.filter { it % 2 == 0 }  // 结果：[2, 4]

// 3. map：转换元素（每个数乘2）
val doubled = numbers.map { it * 2 }  // 结果：[2, 4, 6, 8, 10]

// 4. any：判断是否有满足条件的元素（是否有大于3的数）
val hasLargeNumber = numbers.any { it > 3 }  // 结果：true
```
## Lambda 与闭包
Lambda 可以访问并修改其外部作用域的变量，这种特性称为 "闭包"：
```
var count = 0

// Lambda访问并修改外部变量count
val increment: () -> Unit = { count++ }

increment()
increment()
println(count)  // 输出：2（count被Lambda修改了两次）
```

# 集合
## 一、核心概念：可变 vs 不可变
1.  **不可变集合 (Read-Only Interfaces)**
    *   **特点**： 只有查询元素的能力，无法添加、删除或修改元素。
    *   **接口**： `Collection`, `List`, `Set`, `Map`
    *   **优势**： 确保了线程安全，避免了意外的修改，是函数式编程的理想选择。

2.  **可变集合 (Mutable Interfaces)**
    *   **特点**： 在不可变集合接口的基础上，增加了增删改元素的能力。
    *   **接口**： `MutableCollection`, `MutableList`, `MutableSet`, `MutableMap`
    *   **优势**： 当你需要动态修改集合内容时使用。

| 集合类型 | 不可变接口 | 可变接口 | 描述 |
| --- | --- | --- | --- |
| **List** | `List<T>` | `MutableList<T>` | 有序集合，可包含重复元素 |
| **Set** | `Set<T>` | `MutableSet<T>` | 无序集合，不包含重复元素 |
| **Map** | `Map<K, V>` | `MutableMap<K, V>` | 键值对集合，键唯一 |

## 二、集合的创建

#### 1. List 的创建
```kotlin
// 不可变 List
val readOnlyList = listOf("a", "b", "c") // 类型推断为 List<String>

// 可变 List
val mutableList = mutableListOf("a", "b", "c") // MutableList<String>
val arrayList = arrayListOf(1, 2, 3) // ArrayList<Int> (也是可变)

// 空 List
val emptyList = emptyList<String>()

// 使用构造器 (适用于可变List)
val constructedList = MutableList(5) { index -> "Item $index" } // 创建5个元素的列表
```

#### 2. Set 的创建
```kotlin
// 不可变 Set (自动去重)
val readOnlySet = setOf(1, 2, 3, 3, 2) // 结果为 [1, 2, 3]

// 可变 Set
val mutableSet = mutableSetOf("x", "y", "z")
val hashSet = hashSetOf("x", "y") // HashSet<String>
val linkedSet = linkedSetOf("x", "y") // 保持插入顺序
```

#### 3. Map 的创建
```kotlin
// 不可变 Map
val readOnlyMap = mapOf(1 to "Apple", 2 to "Banana", 3 to "Orange")

// 可变 Map
val mutableMap = mutableMapOf("name" to "Tom", "age" to "25")
val hashMap = hashMapOf("a" to 1, "b" to 2)

// 使用 Pair 创建
val mapWithPairs = mapOf(Pair("key1", "value1"), Pair("key2", "value2"))
```

## 三、集合的操作（强大之处）

#### 1. 转换操作 (Transformations)
*   `map { ... }`： 将每个元素转换为新的形式。
    ```kotlin
    val numbers = listOf(1, 2, 3)
    val squared = numbers.map { it * it } // [1, 4, 9]
    ```
*   `filter { ... }`： 过滤满足条件的元素。
    ```kotlin
    val evenNumbers = numbers.filter { it % 2 == 0 } // [2]
    ```
*   `flatMap { ... }`： 将每个元素转换为一个集合，最后将所有集合“拍平”成一个集合。
    ```kotlin
    val list = listOf("Hello", "World")
    val letters = list.flatMap { it.toList() } // [H, e, l, l, o, W, o, r, l, d]
    ```
*   `zip`： 合并两个集合，返回一个 `Pair` 列表。
    ```kotlin
    val listA = listOf("a", "b", "c")
    val listB = listOf(1, 2, 3)
    val zipped = listA.zip(listB) // [(a, 1), (b, 2), (c, 3)]
    ```
*   `associateWith / associateBy`： 从集合元素构建 Map。
    ```kotlin
    val keys = listOf("a", "b", "c")
    val map1 = keys.associateWith { it.length } // {a=1, b=1, c=1}
    val map2 = keys.associateBy { it.uppercase() } // {A=a, B=b, C=c}
    ```

#### 2. 聚合操作 (Aggregations)
*   `sum(), average(), count(), min(), max()`： 统计计算。
*   `reduce { acc, value -> ... }` / `fold(initial) { acc, value -> ... }`： 从第一项（或初始值）开始累积值。
    ```kotlin
    val numbers = listOf(1, 2, 3, 4)
    val sumReduce = numbers.reduce { acc, i -> acc + i } // 10
    val sumFold = numbers.fold(10) { acc, i -> acc + i } // 20 (10 + 1+2+3+4)
    ```

#### 3. 分组操作 (Grouping)
*   `groupBy { ... }`： 根据条件将集合分组为一个 Map。
    ```kotlin
    val words = listOf("one", "two", "three", "four", "five")
    val byLength = words.groupBy { it.length }
    // {3=[one, two], 4=[four, five], 5=[three]}
    ```

#### 4. 检索元素 (Retrieving)
*   `elementAt(index)`, `first(), last()`
*   `find { ... }`： 返回第一个满足条件的元素（等同于 `firstOrNull`）。
*   `firstOrNull(), lastOrNull()`： 安全地获取元素，避免异常。

#### 5. 排序操作 (Sorting)
*   `sorted()`, `sortedDescending()`
*   `sortedBy { ... }`： 根据指定选择器函数的结果进行自然排序。
*   `sortedWith(comparator)`： 使用自定义比较器排序。
    ```kotlin
    val list = listOf("apple", "banana", "cherry")
    val sortedByLength = list.sortedBy { it.length } // [apple, banana, cherry] (5,6,6)
    val sortedDesc = list.sortedDescending() // [cherry, banana, apple]
    ```

#### 6. 去重操作 (Distinct)
*   `distinct()`： 返回列表中所有不重复的元素。

## 四、集合的遍历

```kotlin
val fruits = listOf("Apple", "Banana", "Orange")

// 1. for-in 循环
for (fruit in fruits) {
    println(fruit)
}

// 2. forEach 高阶函数
fruits.forEach { fruit ->
    println(fruit)
}

// 3. 带索引的遍历
for ((index, fruit) in fruits.withIndex()) {
    println("$index: $fruit")
}

// 4. 遍历 Map
val map = mapOf(1 to "one", 2 to "two")
for ((key, value) in map) {
    println("$key -> $value")
}
map.forEach { (key, value) -> println("$key -> $value") }
```

## 五、序列 (Sequences) - 用于大型集合

对于包含大量元素（万级以上）的集合，使用 `asSequence()` 将其转换为**序列**可以避免创建中间集合，显著提升性能。

*   **操作方式**： `集合.asSequence().filter { ... }.map { ... }.toList()`
*   **与集合操作的区别**：
    *   **集合 (Eager Evaluation)**： 每一步操作（`filter`, `map`）都会立即执行并生成一个新的中间集合。
    *   **序列 (Lazy Evaluation)**： 不会立即计算，而是将操作记录下來。只有当终端操作（如 `toList()`, `first()`）被调用时，所有操作会按顺序**逐个元素**地应用（“垂直”执行）。

**使用场景**： 数据量大或操作链长时，使用序列优化性能。

```kotlin
// 集合： 会创建两个中间列表
listOf(1, 2, 3, 4)
        .filter { println("filter $it"); it % 2 == 0 } // [2, 4]
        .map { println("map $it"); it * it } // [4, 16]

// 输出：
// filter 1
// filter 2
// filter 3
// filter 4
// map 2
// map 4

// 序列： 无中间集合，逐个元素执行所有操作
listOf(1, 2, 3, 4)
        .asSequence()
        .filter { println("filter $it"); it % 2 == 0 }
        .map { println("map $it"); it * it }
        .toList() // 终端操作

// 输出：
// filter 1
// filter 2
// map 2
// filter 3
// filter 4
// map 4
```

---
