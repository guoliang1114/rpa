# Excel和数据表

Excel是UiPath的最常用的场景。本文将带领大家了了解UiPath对Excel的常用操作。例如如何打开Excel文件,读取单元格或区域，输出数据等等。  
Excel/工作薄\(Workbooks\)是基于Excel文件，能存放各种数据的容器。能够格式化，工作表，布局，合并单元格以及多个数据表等等，其实就是你所理解的Excel。  
数据表\(Data tables\)则是一种简单的电子表格，有一些行和列，表头都是可用可无的。

单元格（cell）是表格的最小单位。

范围（Range）是一组单元格，使用":"来隔开。

## Excel 操作

UiPath有多其他操作excel的组件，例如： Read Range, Write Range, Append Range, Sort Table, Read Cell 和 Write Cell, 而数据表的操作组件有For Each Row, Output Data Table, Get Row Item, Add Data Row 以及 Build Data Table。这些组件件如其名。我们挑选几个重点的来说一说。

### Excel Application Scope

Excel Application Scope是开始所有Excel世界的大门，它是一个容器，你可以用它执行要处理的excel的文件，所有的Excel的操作都需要在它内部执行。  
另外，你电脑上如果没有安装Excel，也是可以使用它来执行，但是需要将它的属性“Visible”设置为false。

我们从一个简单的例子开始。有一个Excel文件，我们需要使用UiPath打开该文件，在UiPath的output中打开出其内容,最后将其保存到新文件中。

![](/assets2.3/import1.png)

上半段如图所示，首先使用Excel Application Scope打开book1文件，然后使用Read Range来读取该文件。Excel Application Scope中指定文件目录和名称。在Read Range中，我们保持Range为“”，表示自动选择，如果需要指定可以采取类似“A1:A10”的方式，接着使用参数来接受返回的DataTable。

![](/assets2.3/import2.png)

下半段，继续使用Excel Application Scope打开book2文件，如果book2文件不存在的话，会自动创建。使用Append Range来将上半段的datatable添加到新文件。另外，图中的变量dt需要更改作用域才可以在下半段使用。

打开Excel的方式：

* 使用Excel应用：Excel必须安装。进程之间可以共享数据，数据修改可见。
* 使用文件读取：仅仅支持xlsx格式，不需要安装excel,并且在后台执行。

决定打开方式的参数就是Visible。

![](/assets2.3/import3.png)

刚刚大家已经对几个组件有了一定的认知。我们继续给大家介绍

### Write Range和Append Range

Write Range和Append Range有些类似，它们都需要datatable来作为入参，Write Range是用来写数据的，如果有数据的话会被覆盖；而Append会原有数据后添加数据,不会覆盖现有数据。

### Read Range

Read Range用来读取一个区域的数据，返回datatable。  
![](/assets2.3/import4.png)

| 参数 | 描述 | 备注 |
| :--- | :--- | :--- |
| 出参 | Datatable | 读取数据的返回值 |
| 入参（必填） | SheetName |  |
| 可选 | Range | 读取的范围，默认是自动获取所有数据 |

勾选 “Add Headers”，会将第一行也返回到datatable。

### 其他组件

| 组件名称 | Read Range | Read Cell | Read Column | Read Row | Write range | Write cell |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 入参 | Range SheetName WorkbookPath 或 Workbook object | Range SheetName WorkbookPath 或 Workbook object | Range SheetName WorkbookPath 或Workbook object | Range SheetName WorkbookPath 或 Workbook object | Data Table | String |
| 出参 | Data Table | String | IEnumerable | IEnumerable | workbook | workbook |

如果需要涉及公式，是能通过Excel应用来操作哦。

### 例子:对比Excel的两列
**目标**
对比Excel的前两列，并且把结果写入第三列：
值相等： "="
第一列值大： "a"
第二列值大："b" 

**自动化思路**

1. 读取Excel文件
2. 逐行比对列A和列B
3. 将结果写入第三行

**实现过程**

1. 使用 "Read Cell Range"来读取数据。



