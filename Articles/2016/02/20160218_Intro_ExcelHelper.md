## ExcelHelper工具说明

ExcelHelper是一个基于Node.js命令行工具，专注于解决用户Excel（xls、xlsx）格式基础数据，在不同信息管理系统之间批量导入导出时进行的有规律地行列增删改操作。

同时，ExcelHelper工具还有一个文件批量重命名的子命令。它可以搜索指定路径中搜索符合以下条件的文件，即文件名或文件名的一部分与Excel表格中“原文件名”列所指定文件名一一对应的文件，并将其重命名为“目标文件名”列所指定的文件名。

ExcelHelper是一个开放源代码程序，想要了解详细信息，请前往其[Github页面][github-repo-url]。

Dillinger is a cloud-enabled, mobile-ready, offline-storage, AngularJS powered HTML5 Markdown editor.

  - Type some Markdown on the left
  - See HTML in the right
  - Magic

Markdown is a lightweight markup language based on the formatting conventions that people naturally use in email.  As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually* written in Markdown! To get a feel for Markdown's syntax, type some text into the left window and watch the results in the right.

### 背景
在学校的工作中，常常要用到多个学生信息管理系统，有时还会遇见新的系统想要尝尝鲜的情况。要将数据从一个系统导入到另一个系统，常用的方法是使用Excel文件作为通用数据交换文件。但是，这些信息管理系统的导出的数据基本上是不能马上导入另一个系统的，要使用各式各样的方法对这样Excel文件进行加工。常见的Excel文件加工方法有：

- 全手动法
- 小工具助力法
- 程序设计法

全手动法，顾名思义就是全手动地在Excel中进行行列的增删改操作，高级一点儿的，使用一些公式或者宏。小工具助力法就是使用一些网上搜集的各种“Excel文件加工小工具”，结合批处理是命令，再加上一点点儿纯手动，对Excel文件进行加工。

以上两种方法多见于一次性加工，或没有程序设计基础的人使用。我所在的学校，全校几十个班哪怕只是试用一个系统，我也不想一个一个手动来修改表格，于是便写程序来加工Excel文件。

一开始，使用的是Office PIA，这是一种微软官方的编程接口，通过代码后台调用Office程序来对Excel文件进行操作。效率较低，程序编写也有一定困难，所以后来没有再使用。后来接触了Apache POI，直接二进制读取Excel文件，运行效率大大提高，不过由于程序编写还是有些繁琐，还是没有什么好感。直到后来，在前端开发学习中认识了Node.js世界就变得很美好。

Nodej.js库非常丰富，NPM包管理十分方便，运行效率高，使用Javascript减少了语言障碍。在Node.js的基础上，ExcelHelper工具应运而生。

### 设计理念
ExcelHelper的设计，遵循了Unix编程艺术中的“[模块原则][Module-principle]”，大大降低了程序的复杂度。使程序代码清晰明了，易于维护，同时提高的程序的可靠性。

前文中也提到，工作中会遇到很多表格转换及根据表格给文件重命名的工作。这些工作简单有规律，同时又需要大量的重复运算，这是最适合计算机程序应用的情境之一。为了持久地为工作提供便捷，同时减少不必要的劳动浪费，程序的可复用性也极其重要。在程序的编写过程中，将可以重用的部分和需要根据不同的表格而更改的部分区分开，切换不同的任务时，只需切换相应的分区代码即可。同时使用版本管理工具git方便版本之间的切换。

简明易用（人性化的参数，简明的说明文档）

### 设计说明
### 使用方法
### 如何复用

Dillinger uses a number of open source projects to work properly:

* [AngularJS] - HTML enhanced for web apps!
* [Ace Editor] - awesome web-based text editor
* [Marked] - a super fast port of Markdown to JavaScript
* [Twitter Bootstrap] - great UI boilerplate for modern web apps
* [node.js] - evented I/O for the backend
* [Express] - fast node.js network app framework [@tjholowaychuk]
* [Gulp] - the streaming build system
* [keymaster.js] - awesome keyboard handler lib by [@thomasfuchs]
* [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

### Installation

You need Gulp installed globally:

```sh
$ npm i -g gulp
```

```sh
$ git clone [git-repo-url] dillinger
$ cd dillinger
$ npm i -d
$ gulp build --prod
$ NODE_ENV=production node app
```

### Plugins

Dillinger is currently extended with the following plugins

* Dropbox
* Github
* Google Drive
* OneDrive

Readmes, how to use them in your own application can be found here:

* [plugins/dropbox/README.md] [PlDb]
* [plugins/github/README.md] [PlGh]
* [plugins/googledrive/README.md] [PlGd]
* [plugins/onedrive/README.md] [PlOd]

### Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantanously see your updates!

Open your favorite Terminal and run these commands.

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma start
```

### Docker, N|Solid and NGINX

More details coming soon.

#### docker-compose.yml

Change the path for the nginx conf mounting path to your full path, not mine!

### Todos

 - Write Tests
 - Rethink Github Save
 - Add Code Comments
 - Add Night Mode

License
----

MIT


**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [github-repo-url]: <https://github.com/zc1415926/covert-xj-to-xkw>
   [Module-principle]: <http://www.cnblogs.com/chgaowei/archive/2011/07/26/2117644.html>
   
   [john gruber]: <http://daringfireball.net>
   [@thomasfuchs]: <http://twitter.com/thomasfuchs>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [marked]: <https://github.com/chjj/marked>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [keymaster.js]: <https://github.com/madrobby/keymaster>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]:  <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>


