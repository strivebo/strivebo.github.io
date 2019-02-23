---
title: 利用GitBook制作电子书，发布于网络并绑定个性域名
date: 2019-02-21 20:01:08
categories: 版本控制
tags: [Blog,GitBook,GitHub] 
---

## 1. 制作电子书

[GitBook](https://github.com/GitbookIO/gitbook) 是一个使用 GitHub/Git 和 Markdown 来制作电子书的命令行工具（Node.js 库）。另外，有一个网站 [http://gitbook.com](http://link.zhihu.com/?target=http%3A//gitbook.com) 可以帮助用户更好的使用 Gitbook，它是使用 GitBook 格式创建和托管图书的在线平台。它提供托管，协作功能和易于使用的编辑器。Gitbook 与 [http://gitbook.com](http://link.zhihu.com/?target=http%3A//gitbook.com) 的关系类似 Git 和 GitHub，一个是工具，另一个是基于工具创建的网站。<!-- more -->

> 注：GitBook 平台在今年的 4 月 9 日发布了新的版本 v2。新的版本官网已经变成 [`www.gitbook.com`](https://www.gitbook.com/?t=11) （旧的地址为 [`legacy.gitbook.com`](https://legacy.gitbook.com/) ）。新旧版本有很多的不一样，网上很多资料都是针对旧版。 比如新版不再支持把每本书作为一个 `Git Repository`  来进行版本管理。更多 v2 的重大改变可以看 [这里](https://docs.gitbook.com/v2-changes/important-differences)。

你可以利用 Git 命令管理电子书版本，如果你是 GitHub 的重度使用者，还可以把你的 GitBook 帐户和 GitHub 帐户关联起来，这样不论在任何一方修改了内容，都可以互相同步。下面是制作电子书和使用步骤。

**(1) 安装Node.js**

由于 GitBook 是基于 Node.js 开发的，所以依赖 Node.js 环境。如果您的系统中还未安装 Node.js，请点击 [Node.js下载页面](https://nodejs.org/en/download/)，根据你所使用的系统下载对应的版本。如果已安装则略过本步骤。

Windows 版和 Mac 版的 Node.js 都是常规的安装包，连续下一步安装即可。Linux 版可以通过 yum、apt-get 之类的工具安装，也可以通过源码包安装。

 **(2) 安装GitBook命令行工具**

打开“命令提示符”（Mac 系统打开“终端”）输入以下命令全局安装 gitbook-cli：

``` markdown
npm install gitbook-cli -g
```

`gitbook-cli` 是 GitBook 的一个命令行工具。它将自动安装所需版本的 GitBook 来构建一本书。

执行下面的命令，查看 GitBook 版本，以验证安装成功。

``` markdown
gitbook --version
```

 **(3) 新建GitBook项目**

新建一个目录，并进入该目录使用 gitbook 命令初始化电子书项目。

``` markdown
gitbook init
```

初始化后的目录中会出现 `README.md` 和 `SUMMARY.md` 两个基本文件，如果你希望将书籍创建到一个新目录中，可以通过运行 `gitbook init ./directory` 这样做。当然你也可以自己手动创建这两个文件。`README.md` 是电子书的介绍，`SUMMARY.md` 是电子书的目录结构。

> 注意：一个 GitBook 项目至少要包含 README.md 和 SUMMARY.md，书本的第一页内容是从文件 README.md 文件中提取的。如果这个文件名没有出现在 SUMMARY.md 文件中，则它会被添加为章节的第一个条目。而由于一些托管在 GitHub 上的书会将 README.md 作为项目的介绍而不是书的介绍，从 gitbook v2 起，可以在 book.json 中指定某个文件作为 README。如：
>
> ``` json
> {
> 	"structure": {
> 		"readme": "introduction.md"
> 	}
> }
> ```
> 
> *以下为个人实践：如果不想要书籍的目录默认把 README.md 文作为书籍第一章，可以新建 introduction.md 文件（名称随意），并 readme 指定该文件，则书籍第一章为 introduction.md 内容。但是有个注意的是，如果在 summary.md 文件某个目录中有指定了 README.md 文件作为章节内容，则书籍第一章不会是 introduction.md 内容，而是 README.md 内容。*

**(4) 编辑书籍内容**

GitBook 使用 `SUMMARY.md` 来定义书本的章节和子章节的结构。它用来生成书本内容的预览表。它的格式是一个简单的链接列表。另外可以在里面添加一些 Markdown 格式的标题和分割线。例如：

``` xml
# 概要
- [章节 1](chapter1.md)
- [章节 2](chapter2.md)
- [章节 3](chapter3.md)

# 基础
- [章节 1](chapter1/README.md)
  - [1.1 a](chapter1/a.md)
  - [1.2 b](chapter1/b.md)
---
- [章节 2](chapter2/README.md)
  - [2.1 c](chapter2/c.md)
  - [2.2 d](chapter2/d.md)

# 进阶
- [章节 3](chapter3/README.md)
```

接下来就可以在相应的 MD 文件里书写内容了。文件内容编写使用 Markdown 语法格式。另外，GitBook 的目录，限定为三级。

> 注：`README.md` 和 `SUMMARY.md` 这两个文件你也可以自己手动新建和编写。

**(5) 预览电子书**

写完内容，可以通过以下方式来预览电子书：

``` markdown
gitbook serve
```

`gitbook serve` 命令实际上是先调用 `gitbook build`  编译书籍，然后启动一个 web 服务器，监听在本地的 4000 端口。在浏览器中输入 `http://localhost:4000`，即可预览查看。

> 注：`gitbook build` 命令会在当前文件夹中生成 `_book `文件夹（生成 HTML 版本的电子书），用户可以将这个文件夹内容托管到网上，从而实现内容的发布。

这里有个问题记录下，我在 `gitbook serve` 后报错，如下：

``` xml
Template render error: (F:\JavaEE-tutorial\ch1\02-Java基本语法.md) [Line 434, Column 22]
  expected variable end
```

根据错误，我有找到对应位置的内容：

``` java
scores = new int[][]{{1, 2, 3},{3, 4, 5},{6} };
```

即这行这里的数字 1 前面连续的花括号问题，后面尝试解决了：只要这两个花括号不要连续就行，比如空一格 `{ {` 就不会有错了。另外，我还发现 MD 源文章的标题不能使用半角下的圆括号 `（`、`)`，否则预览电子书的时候点击对应文章的目录没有反应。另外我也发现在基于 Hexo 博客搭建编写的文章里出现了连续花括号同样会报错，解决方法只要不连续就行。

**(6) 生成电子书** 

生成 PDF 格式电子书：`gitbook pdf .`，默认为 `book.pdf`，如果自定义名称，可：`gitbook pdf 目录 目录/书名.pdf`，如在当前文件夹下输出：

``` markdown
gitbook pdf ./ ./书名.pdf
```

> 注意：如上操作出现报错话，试一试先使用 npm 安装上 gitbook-pdf：`npm install gitbook-pdf -g`。参考：[使用Gitbook写开源书籍，过一把作家瘾](https://www.jianshu.com/p/7476afdd9248)。
>
> 另外，由于生成 PDF 文件依赖于 `ebook-convert`，故首先在该处 [ebook-convert下载链接](http://calibre-ebook.com/download) 点击下载所需要的版本。

需要在当前目录生成 epub 或者 mobi 格式的，分别执行下面的命令即可：`gitbook epub .`、`gitbook mobi .`。

如果需要定制 PDF 输出，可以使用 book.json 中的一组选项来定制 PDF 输出：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190127225401.png)

若想要输出的 PDF 目录对应的是数字页码，可以试试下面解决方式：

- [Change PDF generation engine to either wkhtmltopdf or phantom.js](https://github.com/GitbookIO/gitbook/issues/1470) 
- [Conversion to PDF with calibre should show table of content with page numbers](https://github.com/GitbookIO/gitbook/issues/1223) 

**(7) 使用插件**

Gitbook 本身功能丰富，但同时可以使用插件来进行个性化定制。Gitbook 插件里已经有 100 多个插件，可以在 `book.json` 文件的 `plugins` 和 `pluginsConfig` 字段添加插件及相关配置，添加后别忘了进行安装。

安装插件的方式非常简单，只需要将所需要的插件添加到 `book.json` 中，如：

``` json
{
    "plugins": ["mathjax"]
}
```

然后执行：`gitbook install ./`，即可安装在当前目录。以下是我的配置：

``` json
{
	
	"structure": {
		"readme": "introduction.md"
	},
	
	"plugins": [
        "github",
        "github-buttons",
		"splitter",
		"latex-codecogs",
		"atoc",
		"-highlight", 
		"prism",
		"prism-themes"
    ],
    "pluginsConfig": {
        "github": {
            "url": "your url"
        },
		
		"atoc": {
            "addClass": true,
            "className": "atoc"
        },
		"sharing": {
            "douban": false,
            "facebook": false,
			"qzone": true,
			"weibo": true
		},
		"prism": {
			"css": [
				"prism-themes/themes/prism-darcula.css"
			]
		}
    }
}
```

Gitbook 默认带有 5 个插件：

- highlight
- search
- sharing
- font-settings
- livereload

如果要去除自带的插件， 可以在插件名称前面加 `-`。

常用插件：

- [exercises](https://plugins.gitbook.com/plugin/exercises)：在文档中增加交互练习内容，目前只支持 JS 语言。
- [quiz](https://github.com/chudaol/gitbook-plugin-quiz)：在文档中增加测验内容，支持单选、多选、排序。
- [include-codeblock](https://plugins.gitbook.com/plugin/include-codeblock)：使得 GitBook 能引用外部独立文档。
- [localized-footer](https://github.com/noerw/gitbook-plugin-localized-footer#readme)：为 GitBook 的每个页面添加页脚内容。
- [page-footer-ex](https://plugins.gitbook.com/plugin/page-footer-ex)：为文档添加修改时间和版权声明页脚。
- [search-pro](https://plugins.gitbook.com/plugin/search-pro)：为 GitBook 添加多字节字符搜索，实现中文搜索（默认只能搜索英文）。
- [sharing-plus](https://plugins.gitbook.com/plugin/sharing-plus)：GitBook 默认分享工具的增强版，加入了中国常用的社交网站。
- [changyan](https://github.com/codepiano/gitbook-plugin-changyan)：为 GitBook 页面添加畅言评论框。
- [iframely](https://plugins.gitbook.com/plugin/iframely)：在页面中嵌入常见视频网站内容。
- [bibtex-indexed-cite](https://plugins.gitbook.com/plugin/bibtex-indexed-cite)：使用 bibtex 格式，自动生成参考文献。

参考：

- [常用的插件都有哪些 · GitBook学习笔记](https://yangjh.oschina.io/gitbook/faq/Recommand.html)
- [Gitbook 的使用和常用插件](https://zhaoda.net/2015/11/09/gitbook-plugins/)

参考文章：

- [输出PDF | gitbook入门教程](https://yuzeshan.gitbooks.io/gitbook-studying/content/output/pdfandebook.html)
- [GitBook使用](http://wiki.11ten.net/Node/gitbook%E4%BD%BF%E7%94%A8.html)
- [GitBook学习笔记](https://yangjh.oschina.io/gitbook/)
- [使用 Gitbook 打造你的电子书 - 知乎](https://zhuanlan.zhihu.com/p/34946169)
- [Gitbook 的使用和常用插件](https://zhaoda.net/2015/11/09/gitbook-plugins/)



## 2. 发布于网络

### (1)  在gitbook.com上发布和管理书籍

以上所有的步骤都是在本地进行的，如果需要实现电子书的版本管理，或者把电子书发布到网络上，还可以通过 Git 命令将本地的项目托管到 GitBook.com 上。

首先进入 [GitBook.com](https://www.gitbook.com/) 注册一个账号，选择“Create an organization”创建一个 Organization。另外，从官网可以看到：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190219145307.png)

一个组织下免费用户只能有 2 个协作者，一个公开空间，一个私有空间。如果想要创建多本公开图书，创建多个组织就行，再在每个组织下创建公开图书。

再创建完 Organization 后，在选择 “Creat a new Space” 创建一个 Space（旧版叫 Book），然后就可以在线写书了。

访问之前先进行几个设置，先到 Organization –> “Settings” –> “Your Organization URL” 设置你的 url，比如 `strivebo`，再打开电子书，进入 “Domains” –> “GitBook URL” –> 设置域名 `https://strivebo.gitbook.io/` 的后部分，比如设置为 `javaee`，这样就可以使用 `https://strivebo.gitbook.io/javaee` 在线访问了。

### (2) 在github.com上发布和管理书籍

如果你喜欢使用 GitHub 管理电子书。还可以把您的 GitBook 帐户和 GitHub 帐户关联起来，这样两者的修改内容就可以互相同步了。你可以在 Account Settings 中的 Github 设置选项中去进行绑定。

完成关联后即可设置同步电子书项目了。以电子书项目“JavaEE-tutorial”为例，进入某个电子书的设置页面，切换到“Integrations”选项卡。在“GitHub”中设置和添加需要同步的仓库。如图（下图为已经添加了 GitHub 仓库）：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221143040.png)

> 注：其中设置过程中，有个选择 ”Which content should be used for the first synchronization ?“，我们这里选择“I write my content on GitHub“选项，即选择 GitHub 内容自动同步到 GitBook。

添加完成会自动导入你添加的 GitHub 仓库内容。以后你上传到 GitHub 的内容就会自动同步到 GitBook 了。

另外，你也可以托管到 Github Pages，这个就不细讲了。我的 GitHub Page 用来搭建个人博客了，如果想要了解如何使用 GitHub Page 可以找我写的搭建博客的文章看看。

忘了说，你还可以发布到虚拟空间，也就是自己买的云服务器，使用步骤：

1. 在本地写作完，`gitbook build` 生成静态网页，即会在书籍目录下生成 `_book` 的目录，
2. 在使用只需要将这个目录的文件上传到我们的虚拟空间中就可以了。



## 3. 绑定域名

虽然 GitBook 上的所有的图书都可以通过地址`http://{OrganizationUr}.gitbooks.io/{Gitbook Ur}/`访问， 但我们有时候还是希望将图书绑定我们自己的域名上。

如何做呢？以腾讯云操作如下：

第一步，GitBook 的网站上进入你的电子书的，打开 “Domains” –> “Custom Domain” 设置你的个性域名，比如我设置了一个二级域名 `javaee.strivebo.com`；

第二步，进入腾讯云 [云解析](https://console.qcloud.com/cns/domains)，如下操作，选择一级域名，点击「分配其子域名至项目」：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170338.png)

然后在弹出的对话框填入二级域名前缀，项目名称，选择「默认项目」如图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170539.png)

第三步，打开「协作子域名」选择刚刚添加的二级域名，点击解析，添加一条 CNAME 记录，将 `javaee.strivebo.com` 解析为 `strivebo.gitbooks.io.`，如下图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170902.png)

第四步，就是等待域名解析记录在全球范围内生效，然后就可以地址栏输入 `javaee.strivebo.com` 阅读图书了。等待的时候不是固定的，如果你等待了很久还是不能访问，不妨翻墙试一下。

> 注意：在添加 CNAME 解析的时候记录值，记得后面 `.io` 还有一个 `.`，如果你不加，这里在添加完解析会默认给加上。

参考阅读：[云解析 子域名分项目管理 - 操作指南 - 文档平台 - 腾讯云](https://cloud.tencent.com/document/product/302/7800)