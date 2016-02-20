# ExcelHelper工具说明

ExcelHelper是一个基于Node.js命令行工具，专注于解决用户Excel（xls、xlsx）格式基础数据，在不同信息管理系统之间批量导入导出时进行的有规律地行列增删改操作。

同时，ExcelHelper工具还有一个文件批量重命名的子命令。它可以搜索指定路径中搜索符合以下条件的文件，即文件名或文件名的一部分与Excel表格中“原文件名”列所指定文件名一一对应的文件，并将其重命名为“目标文件名”列所指定的文件名。

ExcelHelper是一个开放源代码程序，想要了解详细信息，请前往其[Github页面][github-repo-url]。

## 背景
在学校的工作中，常常要用到多个学生信息管理系统，有时还会遇见新的系统想要尝尝鲜的情况。要将数据从一个系统导入到另一个系统，常用的方法是使用Excel文件作为通用数据交换文件。但是，这些信息管理系统的导出的数据基本上是不能马上导入另一个系统的，要使用各式各样的方法对这样Excel文件进行加工。常见的Excel文件加工方法有：

- 全手动法
- 小工具助力法
- 程序设计法

全手动法，顾名思义就是全手动地在Excel中进行行列的增删改操作，高级一点儿的，使用一些公式或者宏。小工具助力法就是使用一些网上搜集的各种“Excel文件加工小工具”，结合批处理是命令，再加上一点点儿纯手动，对Excel文件进行加工。

以上两种方法多见于一次性加工，或没有程序设计基础的人使用。我所在的学校，全校几十个班哪怕只是试用一个系统，我也不想一个一个手动来修改表格，于是便写程序来加工Excel文件。

一开始，使用的是Office PIA，这是一种微软官方的编程接口，通过代码后台调用Office程序来对Excel文件进行操作。效率较低，程序编写也有一定困难，所以后来没有再使用。后来接触了Apache POI，直接二进制读取Excel文件，运行效率大大提高，不过由于程序编写还是有些繁琐，还是没有什么好感。直到后来，在前端开发学习中认识了Node.js世界就变得很美好。

Nodej.js库非常丰富，NPM包管理十分方便，运行效率高，使用Javascript减少了语言障碍。在Node.js的基础上，ExcelHelper工具应运而生。

## 设计理念
ExcelHelper的设计，遵循了Unix编程艺术中的“[模块原则][Module-principle]”，大大降低了程序的复杂度。使程序代码清晰明了，易于维护，同时提高的程序的可靠性。

前文中也提到，工作中会遇到很多表格转换及根据表格给文件重命名的工作。这些工作简单有规律，同时又需要大量的重复运算，这是最适合计算机程序应用的情境之一。为了持久地为工作提供便捷，同时减少不必要的劳动浪费，程序的可复用性也极其重要。在程序的编写过程中，将可以重用的部分和需要根据不同的表格而更改的部分区分开，切换不同的任务时，只需切换相应的分区代码即可。同时使用版本管理工具git方便版本之间的切换。

一目了然的参数设计，简洁清晰的在线帮助，配合参数审核错误信息提示功能，使用户的使用更加方便，即使命令输入错误，也不会让用户感到不知所措。

## 设计说明
### 命令行程序
使用命令行程序这一种程序形式，不仅简化了程序结构，增加程序的稳定性，同时也能使程序更加专注于业务逻辑，减少GUI对用户的干扰。
### 子命令设计理念
本程序使用了git风格的子命令，将不同的业务逻辑分享开，使得程序结构清晰。每个子命令功能单一，功能专注，效率高。同时，各个子命令又使用同一个主命令作为入口，使得整个程序分而不散，保持了程序的统一性、完整性。
### 文件列表及说明
ExcelHelper的项目文件列表如下：
<pre>
root
|--commands
	|--excel-transformer.js
	|--file-renamer.js
	|--image-resizer.js
|--node_modules
|--.gitignore
|--excelhelper.js
|--package.json
|--readme.md
</pre>

commands目录中有三个文件，excel-transformer.js为transform子命令处理Excel文件转换的核心逻辑代码；file-renamer.js是rename子命令中文件批量重命名功能的代码；image-resizer.js文件是在rename子命令执行时，重命名的文件是jpg或png的图片文件时，对图片进行缩放的代码。
node_modules是一个文件夹，存放了整个项目所引用的包。想要了解项目引用了哪些包，及项目的其它信息，可以查看package.json文件。.gitignore是版本管理系统git所使用的文件，它标记了哪些文件是需要在git中忽略的文件。excelhelper.js是程序入口文件，负责调度子命令，输出帮助信息，同时对使用的子命令有其引入的参数进行检查和处理的逻辑。readme.md是项目文档，使用markdown格式书写。
### 子命令详细设计说明
transform子命令引入了shelljs、node-xlsx、fs、progress包；rename子命令引入了shelljs、node-xlsx、progress包，;rename子命令的图片重命名部分还引入了images、match-extension两个包。

## 使用说明

### 查看帮助
如果你不知道Excelhelper如何使用，或其中有哪些子命令，可以使用：

```
node excelhelper -h
```

你可以得到如下的帮助信息：

<pre>
D:\Web\WebstormProjects\covert-xj-to-xkw> node excelhelper -h
Commands:
  transform  Building an Excel file from a source Excel file.
  rename     rename files referencing the excel file
  
Options:
  -h, --help  Show help                                                [boolean]

Examples:
  To get ditail by using: excelhelper [Commands] -h

Made by zc1415926,
Find more at https://github.com/zc1415926/covert-xj-to-xkw
</pre>

可以看到ExcelHelper有两个git风格子命令，下面分别介绍这两个子命令。

### transform子命令说明

transform子命令的帮助信息可以由以下命令获取：

```
node excelhelper transform -h
```

获取到的帮助信息如下：
<pre>
Options:
  -s, --source  Full path of the source Excel file.          [string] [required]
  -d, --dest    Directory in which your output file put.                [string]
  -h, --help    Show help                                              [boolean]
</pre>

在使用transform子命令时，为参数-s传入需要转换的Excel文件的路径（必选），为参数-d传入转换完成的目标文件所要存储的目录（可选），如果-d参数为空，程序则会自动在源文件所有目录下新建一个*transformed*目录，将转换完成的文件存入其中，或在已有的*transformed*目录中存储目标文件。

### rename子命令说明
transform子命令的帮助信息可以由以下命令获取：

```
node excelhelper rename -h
```

获取到的帮助信息如下：
<pre>
Usage: excelhelper rename -e [ExcelFilePath] -p [PhotoDirctory]

Options:
  -e, --excel  Full path of the reference Excel file.        [string] [required]
  -d, --dir    Directory path in which your file contain.    [string] [required]
  -w, --width  How width do you want your photos to resize to.(Ratio keeping) 
                                                                        [string]
  -h, --help   Show help                                               [boolean]

Examples:
  params -e X:\path\myExcel.xls -p X:\dirctory\photos

Made by zc1415926,
Find more at https://github.com/zc1415926/covert-xj-to-xkw
</pre>

使用rename子命令时，为参数-e传入存储批量重命名所需的“原文件名”、“目标文件名”的Excel参考文件路径（必选），为参数-d传入需要批量重命名的文件所在目录（必选），如果你正在重命名的文件是jpg或png格式的文件，其扩展名包含于JPG、jpg、jpeg、png、PNG几种之中，则可以使用-w参数在给文件重命名的同时，对图片进行缩放操作，传入一个要缩放至的宽度值，程序就会按此值保持长宽比地缩放图片（可选）。

**如何指定Excel参考文件中“原文件名”及“目标文件名”对应列的列号呢？**由于这一个文件批量重命名任务中，Excel参考文件中“原文件名”及“目标文件名”对应列的列号基本不变。所以，程序在file-renamer.js文件中使用*COL_NUM_LOOKING_FOR*和*COL_NUM_RENAME_TO*两个从0开始的，表示列号的变量来分别存储对应“原文件名”及“目标文件名”对应列的列号。这两个变量会在“如何复用”一节再次提到。


## 如何复用
关于Excel文件的处理，可以修改excel-transformer.js中的原表格读取代码和生表格生成代码。关于文件重命名的功能，通常请况下，你可以只改变file-renamer.js文件中使用*COL_NUM_LOOKING_FOR*和*COL_NUM_RENAME_TO*两个变量的值达到复用代码的目的，如果你想修改重命名图片文件时缩放图片的代码，可以在image-resizer.js文件中进行。

## 展望
ExcelHelper还有很多的不足之处，亟待改进，还没有实现的功能也有很多。当同时有较多的Excel文件需要转换或是有组文件需要批量重命名时，可以将参数列表提前写入一个json文件中，由程序执行时读取，执行一次就可以完成所有的任务，不必每次修改原来执行命令。

License
----

MIT


[github-repo-url]: <https://github.com/zc1415926/covert-xj-to-xkw> "Github页面"

[Module-principle]: <http://www.cnblogs.com/chgaowei/archive/2011/07/26/2117644.html> "模块原则"