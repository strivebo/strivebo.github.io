---
title: 如何利用GitBook写书
date: 2019-02-13 20:01:08
categories: 版本控制
tags: [blog,GitBook,GitHub] 
---

### (1) 本地操作步骤

1. 安装 Node.js、Git 等
2. 新建书籍目录，如 `F:\gitbook\firstbook-test`
3. 进入书籍目录，新建一个名称为 `SUMMARY.md` 文件，写上书籍目录，如：<!-- more -->
    ``` xml
    [简介](README.md)
    - [第一章：如何造火箭](ch1/build.md)
        - [1. 燃料学](ch1/fuel.md)
        - [2. 空气动力学](ch1/air.md)
        - [3. 总装工程学](ch1/enginer.md)
        - [小结](ch1/WRAPUP.md)
    - [第二章：如何回收火箭](ch2/recycle.md)
        - [1. 自动控制原理](ch2/ac.md)
        - [2. 二次利用要点](ch2/key.md)
    - [结束](end/SUMMARY.md)
    ```
4. 在 GitBash 下敲命令 `gitbook init`，则会按照`SUMMARY.md`文件写的自动生成对应的文件夹和文件（注：这步也可和第三步对调，先初始化，会自动生成`SUMMARY.md`和`README.md`文件）
    ``` xml
    .
    ├── README.md
    ├── SUMMARY.md
    ├── ch1
    │   ├── WRAPUP.md
    │   ├── air.md
    │   ├── build.md
    │   ├── enginer.md
    │   └── fuel.md
    ├── ch2
    │   ├── ac.md
    │   ├── key.md
    │   └── recycle.md
    └── end
        └── SUMMARY.md
    ```
    每个文件的第一行就是我们写的章节标题。
5. 这个时候，按照 Markdown 的格式逐个填充内容到文件即可。至于用什么编辑器写 Markdown 文件，随便哪个都可以。
6. 书籍编写完，就可以本地预览了，`gitbook serve` 会在 4000 端口下预览 `http://localhost:4000`

生成 pdf 格式电子书：`gitbook pdf .`，默认为`book.pdf`，如果自定义名称，可：`gitbook pdf 目录 目录/书名.pdf` ,如在当前文件夹下输出：

``` xml
$ gitbook pdf ./ ./书名.pdf
```
>注：如上操作出现报错话，试试，先使用 npm 安装上 gitbook-pdf：`npm install gitbook-pdf -g`。
>
>参考：[使用Gitbook写开源书籍，过一把作家瘾](https://www.jianshu.com/p/7476afdd9248)。
>
>由于生成 PDF 文件依赖于`ebook-convert`，故首先在该处【[ebook-convert下载链接](http://calibre-ebook.com/download)】点击下载所需要的版本。

生成 epub 或者 mobi 格式的，分别执行下面的命令即可：`gitbook epub .`、`gitbook mobi .`。

注1：如果需要定制 PDF 输出，可以使用 book.json 中的一组选项来定制 PDF 输出：
![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190127225401.png)

注2：若需要输出的 PDF 目录对应的是数字页码，参考：

1. [Change PDF generation engine to either wkhtmltopdf or phantom.js](https://github.com/GitbookIO/gitbook/issues/1470) 、

2. [Conversion to PDF with calibre should show table of content with page numbers](https://github.com/GitbookIO/gitbook/issues/1223) 

看是否能解决吧。

参考资料：

- [输出PDF](https://yuzeshan.gitbooks.io/gitbook-studying/content/output/pdfandebook.html)
- [GitBook使用](http://wiki.11ten.net/Node/gitbook%E4%BD%BF%E7%94%A8.html)
- [使用 Gitbook 打造你的电子书](https://www.jianshu.com/p/f38d8ff999cb)

### (2) 发布

好几种！

1. 可以发布到虚拟空间，也即如自己买的云服务器；
2. 可以直接发布到 GitBook 网站；
3. 可以先在 GitBook 网站新建的电子书关联 GitHub 上的新建的仓库，然后利用 Git 操作推送到 GitHub，会自动更新到 GitBook。


针对第一种：

1. 在本地写作完，可以`gitbook build`生成静态网页，即会在书籍目录下生成`_book`的目录，
2. 在使用只需要将这个目录的文件上传到我们的虚拟空间中就可以了。

针对第二种：后面再说。


针对第三种：（本人即采用该方式~）

1. 登录 GitBook 网站，创建组织，进入 Integrations --> GitHub 进行关联设置，关联 GitHub 仓库；
2. 然后本地编写的电子书籍，然后就是 Git 常见那些操作了，最后推送到 GitHub 仓库即可，GitBook 上会自动同步 GitHub 上更新的内容。

虽然 GitBook 上的所有的图书都可以通过地址`http://{author}.gitbooks.io/{book}/content`访问， 但我们有时候还是希望将图书绑定我们自己的域名上。如何做呢？操作如下：
```xml
第一步，gitbook的网站上到目标图书的setting中设置要绑定的域名，比如设置为go.lijiaocn.com；
第二步，到你的dns服务商那里，添加一条cname记录，将go.lijiaocn.com解析为www.gitbooks.io；
第三步，就是等待域名解析记录在全球范围内生效，然后就可以直接通过go.lijiaocn.com阅读图书。
等待的时候不是固定的，如果你等待了很久还是不能访问，不妨翻墙试一下。
```



**参考资料：**

- [gitbook图书绑定自定义的域名要怎样做_百度经验](https://jingyan.baidu.com/article/335530daf86c3b19cb41c3f3.html)

  > 注意：该文有个坑。在添加 CNAME 解析的时候应该是添加为 xxx.domain.com，其中 xxx 为你注册 GitBook 上的账户名。
- [Gitbook 入门教程](https://yuzeshan.gitbooks.io/gitbook-studying/content/index.html)
- [GitBook使用教程](https://jackchan1999.github.io/2017/05/01/gitbook/GitBook%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/)
- [使用Gitbook制作电子书](https://www.kancloud.cn/wizardforcel/markdown-simple-world/97377)