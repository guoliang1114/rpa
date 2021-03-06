# 2.1 流控制、序列、分支

## 变量

在开始本节之前需要先说明UiPath中的变量，你可以随意的在文本框中使用和定义变量。定义的变量有4种属性。

Name： 变量名称

Value： 变量值

Scope:  变量作用域

Type： 变量类型

## 数据类型

**String**

任何文本，例如 “Hello World!” , “AG221fk”

**int32**

整形，例如 201, 33167

**Double**

浮点数，例如 22.01，444.99

**Boolean**

布尔值，True或者False

**Datetime**

日期时间，例如new DateTime\(2017, 12, 21\)

**DataTable**

数据表。

**Generic Value**

各种数据类型，可以保存数值，字符，日期等。这也是UiPath的内置类型，有了它我们流程参数处理起来就更舒服了。

##Arguments
参数，是为了方便在workflow之间传值。

## Flow Decision和IF

控制流程是定义规则和自动决定工作流程的过程。在UiPath中，你可以通过拖拽的方式搭建工作流。一般是通过使用if / else决定，循环等来实现。这一点和很多语言和工具都是类似的。

在UiPath中有两种方式来实现流控制。一种是Flow Decision,另外一种是IF。分别对应流控制（FlowChart）和序列。它们看起来不一样，但是工作原理是一致的。让我们先举个例子：设计一个工作流，判断某一年是否为闰年。大家都知道闰年的判断依据是该年份是否为4的倍数。

**使用Flow Decision实现**

![](/assets2.1/import1.png)

1. input dialog输入框
   在这个输入框中，我们提示用户输入年份，根据用户输入的年份来判断是否为闰年。并需要创建一个类型为Int32的变量year来接受用户输入的值。
2. Decision使用Flow Decision，它的输出有两条，一条为True，另一条为false。Decision有一个核心的参数是Condition。该参数的返回值是true或者false。这里我们需要判断是否为闰年，其实就是年份除以4是后的余数是否为0，表达式为“year mod 4 = 0”
3. 闰年，如果decision为true，弹出对话框提供用户为闰年。
4. 非闰年，如果decision为false，弹出对话框提供用户为非闰年。

**使用IF实现**

![](/assets2.1/import2.png)  
1. input dialog输入框  
   在这个输入框中，我们提示用户输入年份，根据用户输入的年份来判断是否为闰年。并需要创建一个类型为Int32的变量year来接受用户输入的值。  
2. IF，有三个需要填写，一个条件，两条输出。条件写：year mod 4 = 0，输入Then和Else。  
3. Then，闰年，弹出对话框提供用户为闰年。  
4. Else，非闰年，弹出对话框提供用户为非闰年。

总的来说，IF适合简单的判断,因为输出只有then和else。当然你也可以嵌套IF。

## LOOP

循环，循环是最常用于自动执行重复任务的结构。循环是大多数项目中必不可少的元素。在UiPath中有几种重复某些任务的方法。  
1. 最简单的是流程图模式，用连接线连出一个循环模型。  
2. 使用While  
3. 使用Do While/while  
4. 使用For Each

**使用流程图模式来构建循环**  
我们对上节中提到的流程稍微修改-只有当用户输入为闰年的时候流程才会终止，否则会不断的循环判断。

![](/assets2.1/import3.png)

**While和Do While**  
while和do while两种方式其实差不多，区别在于执行动作的先后。看看UiPath给出的两者图就一目了然了。

![](/assets2.1/import4.png)

![](/assets2.1/import5.png)

当然你可以接着使用闰年这个例子来体验一下这三种方式。

**For Each**  
foreach的循环有些不同。

![](/assets2.1/import6.png)

它通过遍历项目列表，一次一个项目执行操作。

for each我们可以举一个例子，比如需要输出某个文件夹下的文件清单。

![](/assets2.1/import7.png)

1. 首先使用select folder来让用户选择目录，并创建一个变量selectedFolder来接收这个目录信息。
2. 使用Assign来赋值，创建新的变量filelist，其类型为List &lt; String &gt;,使用UiPath的库Directory.GetFiles\(selectedFolder\)来获取目录信息。
3. 使用foreach来循环filelist，并把每一个item输出到控制台。
   例如:

![](/assets2.1/import8.png)

## 小结

为了更好的理解本节内容，我们使用一个例子来回顾。设计一个猜数字的游戏。计算机选择0到1000之间的随机数，我们将尝试猜测它。它会根据你的猜测提示 - 更高或更低，直到你猜出答案。

整个过程：  
1. 计算机生成0-1000的随机数  
2. 用户输入数字  
3. 判断，反馈

整个demo做起来应该比较简单。

![](/assets2.1/import9.png)

取0-1000的随机值的函数为: new Random\(\).Next\(0,1000\)。其他节点非常清晰。另外可以考虑其他的方法。

