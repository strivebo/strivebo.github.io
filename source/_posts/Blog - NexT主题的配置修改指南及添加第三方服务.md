---
title: NexT主题的配置修改指南及添加第三方服务
date: 2019-02-13 20:01:08
categories: Blog
tags: [blog]
---

## 写在前面

(1) 什么是 Hexo：[官网传送门](https://hexo.io/zh-cn/docs/)

(2) Hexo 官网：[Hexo.io](https://hexo.io/ )

(3) Hexo 主题的选择：

- 官网：[Themes | Hexo](https://hexo.io/themes/)
- GitHub：[Themes · hexojs](https://github.com/hexojs/hexo/wiki/Themes )
- 知乎：[有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)




## 1. NexT主题的配置修改

选来选去一直决定不下来选哪个主题合适，在尝试了好多个意向主题之后，最后还是决定选 GitHub 最高 star 的主题 NexT 了。那么多人在用，综合来说，普遍大众应该还是很认可的。

- [NexT](https://theme-next.org/) | [NexT主题 - GitHub](https://github.com/iissnan/hexo-theme-next)

关于这个主题的相关配置、优化等操作网上很容易找到非常详的细资料。建议直接看官方文档吧：[主题配置 - NexT 使用文档](http://theme-next.iissnan.com/theme-settings.html)。

这里主要记录下 NexT 的配置过程我有遇到的问题。先来欣赏使用的 NexT 该主题的 DEMO 网站吧，这是一个：

- [吴小龙同學](http://wuxiaolong.me/)

这是 NexT 主题 GitHub 上其 wiki 页面关于主题设置教程：[主题配置参考 · iissnan/hexo-theme-next Wiki](https://github.com/iissnan/hexo-theme-next/wiki/%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%8F%82%E8%80%83)

关于 NexT主题的修改：

- 还是很全面的： 2016-04-07 [Hexo站点、NexT主题修改全记录](http://www.lzblog.cn/2016/04/07/Hexo%E7%AB%99%E7%82%B9%E3%80%81NexT%E4%B8%BB%E9%A2%98%E4%BF%AE%E6%94%B9%E5%85%A8%E8%AE%B0%E5%BD%95/)

这个主题相关的设置网上一搜是真的太多了，下面列举一些：

- [Hexo+nexT主题搭建个人博客](http://www.wuxubj.cn/2016/08/Hexo-nexT-build-personal-blog/#)


- [Hexo搭建GitHub博客（三）- NexT主题配置使用](https://zhiho.github.io/2015/09/29/hexo-next/)
- [hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html) 
- [浅谈tag标签分类和目录分类的区别以及如何SEO优化妙用！](http://www.brightmoonseo.com/basic/link/1187.html) 



### (1) 关于文章所属「分类」和「标签」的设置

之前我使用的别的主题，只要在 source 文件夹下新建的文章前面按如下格式表明所属分类和标签：

```
title: 自学编程成功概率有多少可能
date: 2017-05-26 19:57:47
tags: [编程,感悟]
categories: 技术 
```

但是在 NexT 主题下的设置的步骤如下：

1) 先`hexo new page categories`新建 categorier 文件夹，其中会自动生成一个`index.md`文件，修改（即添加一行）为：

```
---
title: categories
date: 2018-01-23 17:14:51
type: "categories"
---
```
同理，「标签」也一样，`hexo new page tags`，生成 tags 文件夹，其中会自动生成一个`index.md`文件，修改为：
```
---
title: tags
date: 2018-01-23 17:14:51
type: "tags"
---
```

2) 然后写的博客文章，表明所属「分类」和拥有哪些「标签」，官方文档所说的格式如下：

```
categories:
- Diary
tags:
- PS3
- Games
```

但是我亲测，如下也是可以的：
```
categories: 技术
tags: [编程,感悟]
```

另外，对于 NexT 这个主题，对于「关于」这个菜单和上面新建分类和标签一样，也是需要手动创建文件夹的，`hexo new page about`，这样会生成 about 文件夹，同时自动生成`index.md`文件，然后可以在这个`.md`文件中写上自我个人介绍。（亲测过，`index.md`这个文件的名字不能修改，否则「关于」菜单出错）

关于这部分的设置，官方文档称其为「Front-matter」，「Front-matter」 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数       | 描述                 | 默认值       |
| :--------- | -------------------- | ------------ |
| layout     | 布局                 |              |
| title      | 标题                 |              |
| date       | 建立日期             | 文件建立日期 |
| updated    | 更新日期             | 文件更新日期 |
| comments   | 开启文章的评论功能   | true         |
| tags       | 标签（不适用于分页） |              |
| categories | 分类（不适用于分页） |              |
| permalink  | 覆盖文章网址         |              |

### (2) 添加本地添加搜索菜单

1) 安装 `hexo-generator-searchdb` 插件：`npm install hexo-generator-searchdb --save` 

2) 打开站点配置文件找到 Extensions 在下面添加（其实，新增以下内容到任意位置即可）

```
search:
      path: search.xml
      field: post
      format: html
      limit: 10000
```

3) 打开主题配置文件找到 Local search，将 enable 设置为 true，启动本地搜索功能，这样就能在页面可以看到搜索菜单了：

```
# Local search
local_search:
  enable: true
```

### (3) 添加字数统计、阅读时长

 第一步：安装 word_count 插件，在博客根目录下打开终端：`npm install hexo-wordcount --save`

 第二步：在主题配置文件 `Blog\themes\next\config.yml` 中打开 wordcount 统计功能：

```
# Post wordcount display settings
    # Dependencies: https://github.com/willin/hexo-wordcount
    post_wordcount:
        item_text: true
        wordcount: true
        min2read: true
```

如果仅仅只是打开开关，部署之后会发现文章的【字数统计】和【阅读时长】后面没有对应的 xxx 字，xx 分钟等字样，只有光秃秃的数字在那里。

解决方案：

找到 \themes\next\layout\_macro\post.swig 文件，将“字”、“分钟” 字样添加到如下位置即可。

```
<span title="{{ __('post.wordcount') }}">
     {{ wordcount(post.content) }} 字
</span>

    ...
<span title="{{ __('post.min2read') }}">
     {{ min2read(post.content) }} 分钟
</span>
```

然后才可以看到显示：`阅读时长 ≈ 2 分钟`，但若是不需要显示 `≈` ，就修改这个地方：

```
{% if theme.post_wordcount.item_text %}
        <span class="post-meta-item-text">{{ __('post.min2read') }} &asymp;</span>
 {% endif %}
```

把这里的` &asymp;`删除即可。

另外，如侧边栏友情链接小图标，可以到 [图标库](https://fontawesome.com/icons?from=io) 找到自己喜欢的图标然后复制到相应代码中，也可以到这里找：[Font Awesome，一套绝佳的图标字体库和CSS框架](http://fontawesome.dashgame.com/)。

参考：[Hexo添加字数统计、阅读时长、友情链接](http://www.crocutax.com/2017/05/11/Hexo%E6%B7%BB%E5%8A%A0%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1%E3%80%81%E9%98%85%E8%AF%BB%E6%97%B6%E9%95%BF%E3%80%81%E5%8F%8B%E6%83%85%E9%93%BE%E6%8E%A5/)

### (4) 设置友情链接

在主题配置文件添加，示例：

``` 
# title
links_title: Links
links:
  MacTalk: http://macshuo.com/
  Title: http://example.com/
```

### (5) 设置侧边栏头像

编辑主题的 `_config.yml`，新增字段 `avatar`， 值设置成头像的链接地址。

其中，头像的链接地址可以是：

1. 完整的互联网 URL，例如：`https://avatars1.githubusercontent.com/u/32269?v=3&s=460`
2. 站点内的地址，例如：
   - `/uploads/avatar.jpg` 需要将你的头像图片放置在 `站点的 source/uploads/`（可能需要新建`uploads`目录）
   - `/images/avatar.jpg` 需要将你的头像图片放置在 `主题的 source/images/` 目录下。

### (6) 设置订阅微信公众号

> 注：此特性在版本 5.0.1 中引入，要使用此功能请确保所使用的 NexT 版本在此之后。

在每篇文章的末尾显示微信公众号二维码，扫一扫，轻松订阅博客。将公众号二维码存放于博客`source/uploads/`目录下。然后编辑 主题配置文件，示例如下：

``` 
# Wechat Subscriber
wechat_subscriber:
  enabled: false
  qcode: /uploads/wechat.jpg
  description: 欢迎扫描二维码关注公众号一起成长~
```

### (7) 开启打赏

越来越多的平台（微信公众平台，新浪微博，简书，百度打赏等）支持打赏功能，付费阅读时代越来越近，特此增加了打赏功能，支持微信打赏和支付宝打赏。 只需要主题配置文件中填入微信和支付宝收款二维码图片地址即可开启该功能。打赏功能配置示例：

``` 
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /path/to/wechat-reward-image
alipay: /path/to/alipay-reward-image
```

我的操作：把收款二维码存放在了 NexT 主题的`source/uploads/`目录下，然后配置如下：

``` 
# Reward  赞赏  
reward_comment: 觉得文章对您有帮助请我喝杯咖啡吧^_^ 
wechatpay: /uploads/wechatpay.jpg
alipay: /uploads/alipay.jpg
```

 ### 遇到的问题

我在配置过程中有被官方文档坑了，目前猜测是官方文档没及时更新原因。在此，我记录下遇到的坑：

#### 1）菜单图标问题

问题：「首页」、「分类」、「标签」等这些菜单旁边的图标都显示是问号，未显示正常图标，我按照官方示例配置是这样的：

``` 
menu:
  home: / 
  categories: /categories/  
  tags: /tags/  
  archives: /archives/  
  about: /about/    
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #公益: /404/ || heartbeat

# Enable/Disable menu icons.    
menu_icons:
  enable: true
  home: home
  about: user
  categories: th
  tags: tags
```

网上很多文章写的都是上面那样的配置，但后来找到原因了，真正的配置是下面这样的：

```
menu:
  home: / || home
  archives: /archives || archive
  categories: /categories || th
  tags: /tags || tags
  about: /about || user
  
menu_icons:
  enable: true
```

原来 NexT 这个主题中的「菜单设置」被注释掉的那些配置样例，才是正确的配置。OS：官方文档真是坑人啊。

#### 2）友情链接图标设置问题

问题：「友情链接」图标未正常显示。

官方文档包括网上很多文章写的都是如下：

```
social:
  GitHub: https://github.com/yourname
  邮箱: mailto:test@gamil.com
social_icons:
  enable: true
  icons_only: false
  transition: false
  GitHub: github
  邮箱: envelope
```

但正确配置其实是如下，和菜单配置类似：

```
social:
  GitHub: https://github.com/yourname || github
  邮箱: mailto:test@gamil.com || envelope
social_icons:
  enable: true
  icons_only: false
  transition: false
```



## 2. 第三方服务及其他修改

添加第三方服务，官网文档：[第三方服务集成 - NexT 使用文档](https://theme-next.iissnan.com/third-party-services.html)。

- 评论系统
- 数据统计与分析
- 内容分享服务
- 搜索服务
- 其他服务

### (1) 在线联系（DaoVoice）★

非常全面的一个 NexT 主题优化指南：  [hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)（含全站总字数、DaoVoice 在线联系等等）。

首先在 [DaoVoice](https://account.daocloud.io/signin) 注册账号，注册完成后会得到一个 app_id，记下这个 app_id 的值，然后打开 `/themes/next/layout/_partials/head.swig`，写下如下代码：

``` 
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

接着打开主题配置文件，在最后写下如下代码：

``` 
# Online contact 
daovoice: true
daovoice_app_id: 这里填你的获得的 app_id
```

> *注1：安装成功后可以在 DaoVoice 控制台上的聊天设置里设置聊天窗口样式。*
>
> *注2：我的 DaoVoice 账户注册使用的 GitHub 账户。*

### (2) 评论（Disqus）——已更换为 Valine（注：登录LeanCloud）★

Disqus 官网：https://disqus.com/ （本人使用的是谷歌账号注册和登录）

~~NexT 主题添加评论，我采用了 Disqus 评论~~，参考：[Hexo 集成 Disqus 评论](http://www.cylong.com/blog/2017/03/26/hexo-next-disqus/)。在完成网站注册和配置后，打开 NexT 主题配置文件 `config.yml` 文件。

①大于等于 5.1.1 版本，将 disqus 下的 enable 设定为 true，同时提供你的 shortname，count 用于指定是否显示评论数量：

``` 
disqus:
  enable: true
  shortname:
  count: true
```

②小于 5.1.1 版本，设定 disqus_shortname 的值即可：

``` 
disqus_shortname: shortname
```

接下来就可以进入后台管理设置你的评论了。

***——update：2019-02-14 已弃用 Disqus 评论。参考知乎：[Hexo（NexT 主题）评论系统哪个好？ - 知乎](https://www.zhihu.com/question/267598518)，采用了  Valine，不用登陆就可以用。*** 

***Valine 设置步骤：***

1. 先需要去注册一个账号：[Leancloud官网，点我注册](https://leancloud.cn/)

   注册完以后需要创建一个应用，名字可以随便起，然后 **进入应用 -> 设置 -> 应用key**，获取你的 appid 和 appkey。

2. 拿到你的 appid 和 appkey 之后，打开**主题配置文件** 搜索 valine，填入 appid 和 appkey。

我的配置：

   ``` 
valine:
    enable: true
    appid: MhbxUrTu9FJ0T1iq1HupHO29-gzGzoHsz    
    appkey: PMMgr6Xmfk6n1aKfuKzLwe5p 
    notify: false # mail notifier , https://github.com/xCss/Valine/wiki
    verify: false # Verification code
    placeholder: Just go go # comment box placeholder
    avatar: mm # gravatar style   
    guest_info: nick,mail,link # custom comment header
    pageSize: 10 # pagination size
   ```

 注：记得在 Leancloud -> 设置 -> 安全中心 -> Web 安全域名，把你的域名加进去。

### (3) 添加访问次数和阅读次数（注： 登录LeanCloud）★

①打开 LeanCloud 官网，进入 [注册页面](https://leancloud.cn/login.html#/signup) 注册。完成邮箱激活后，点击头像，进入`控制台`页面，创建一个新应用(类型为`JavaScript SDK`)，点击应用进入；

②创建名称为 `Counter` 的 Class；

③修改配置文件，编辑网站根目录下的 `_config.yml` 文件，添加如下：

```
leancloud_visitors:
  enable: true
  app_id: 你的app_id
  app_key: 你的app_key
```

其中，app_id 和 app_key 在你所创建的应用的`设置->应用Key`中。

注：为了保证应用的统计计数功能仅应用于自己的博客系统，你可以在`应用->设置->安全中心`的`Web安全域名`中加入自己的博客域名，以保证数据的调用安全。

参考：

- [为NexT主题添加文章阅读量统计功能](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)
- [Hexo之NexT主题优化（4）-添加文章访问数和站点访问数](http://happywayq.com/Hexo%E7%9A%84NexT%E4%B8%BB%E9%A2%98%E4%BC%98%E5%8C%96-%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E8%AE%BF%E9%97%AE%E6%95%B0%E5%92%8C%E7%AB%99%E7%82%B9%E8%AE%BF%E9%97%AE%E6%95%B0/)
- [Hexo的NexT主题个性化：添加文章阅读量](http://www.jeyzhang.com/hexo-next-add-post-views.html)

### (4 动态背景、点击出现桃心效果、去除文章底部带#号的标签

参考：[2018最新版Hexo博客Next主题6.0配置优化](https://blog.csdn.net/qq_32454537/article/details/79482896)

### (5) 如何更改标题和文章等字体

参考：[常见问题 - NexT 使用文档](https://theme-next.iissnan.com/faqs.html)

### (6) 添加自定义菜单  

参考：[hexo高阶教程：next主题优化之加入网易云音乐、网易云跟帖、炫酷动态背景、自定义样式，打造属于你自己的定制化博客](https://juejin.im/post/58eb2fd2a0bb9f006928f8c7)

### (7) 添加音乐/视频

**1）添加音乐**

可以进入 [网易云音乐](https://music.163.com/) 的官网，打开需要的音乐，点击「生成外链播放器」生成外链，直接拿来用就行。iframe 插件可以在代码中设置宽高等参数，auto 为自动播放。flash 不可以自己设置参数。示例：

``` html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=1&height=66"></iframe>
```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=1&height=66"></iframe>

**2）添加视频**

打开视频网站，比如优酷、YouTube 等。以优酷为例，打开某个视频后，点击「分享」，再复制 iframe 代码粘贴到 Markdown 文章即可。示例：

``` html
<iframe height=498 width=510 src='http://player.youku.com/embed/XMTU0ODEwMzM3Ng==' frameborder=0 'allowfullscreen'></iframe>
```

### (8) 页面宽度/标题样式等设置

参考：

- [Hexo--Next主题优化](http://www.heqiangfly.com/2016/01/12/blog-optimize-next-theme/)
- [hexo框架基于next主题定制](http://www.aisun.org/2017/10/hexo-next+dingzhi/)（这篇文章把 NexT 主题各种配置讲解的很全面。）

### (9) 设置文章封面图片

如果只是插入本地图片作为文章封面，即在博客首页的时候会显示文章的封面图片，进入这篇文章的详细页面后，将不显示这张图片。

按如下方式操作：

1）修改 `\themes\next\layout\_macro\post.swing` 文件。将如下代码复制：

```js
{% if post.summary_img  %}
  <div class="out-img-topic">
    <img src={{ post.summary_img }} class="img-topic">
  </div>
{% endif %}
```

添加到下图所示的位置:

![](https://neveryu.github.io/images/hexo-next-five-1.png)

2）在新建的文章添加一个字段属性：`summary_img`。`summary_img` 的值是图片的路径，如： 

```html
---
title: CSS 各种Hack手段
date: 2017-06-25 03:25:24
categories: 前端
tags: [CSS]
comments: false
summary_img: /images/css-hack-1.png
---
```

当然也可以不设置`summary_img`的图片路径，即也就不会显示封面图。

**PS：这里有个注意点，亲测，图片存放的文件夹只能新建在 `source` 目录下。**

参考文章：

- [Hexo 图片插入](http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/)
- [Hexo-NexT搭建个人博客（五）——插入封面](https://neveryu.github.io/2017/07/15/hexo-next-five/) 

### (10) 网页加载进度条★

打开 `/themes/next/layout/_partials/head.swig` 文件，在文件末尾添加如下代码：

``` 
<!-- 网页加载条 -->
<script src="https://neveryu.github.io/js/src/pace.min.js"></script>
```

然后，打开 `/themes/source/css/_custom/custom.styl` 文件，在文件末尾添加如下代码：

```
/*网页加载条*/
/* This is a compiled file, you should be editing the file in the templates directory */
.pace {
  -webkit-pointer-events: none;
  pointer-events: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}

.pace-inactive {
  display: none;
}

.pace .pace-progress {
  background: #1e92fb;
  position: fixed;
  z-index: 2000;
  top: 0;
  right: 100%;
  width: 100%;
  height: 3px;
}

.pace .pace-progress-inner {
  display: block;
  position: absolute;
  right: 0px;
  width: 100px;
  height: 100%;
  box-shadow: 0 0 10px #e90f92, 0 0 5px #e90f92;
  opacity: 1.0;
  -webkit-transform: rotate(3deg) translate(0px, -4px);
  -moz-transform: rotate(3deg) translate(0px, -4px);
  -ms-transform: rotate(3deg) translate(0px, -4px);
  -o-transform: rotate(3deg) translate(0px, -4px);
  transform: rotate(3deg) translate(0px, -4px);
}

.pace .pace-activity {
  display: block;
  position: fixed;
  z-index: 2000;
  top: 15px;
  right: 15px;
  width: 14px;
  height: 14px;
  border: solid 2px transparent;
  border-top-color: #e90f92;
  border-left-color: #e90f92;
  border-radius: 10px;
  -webkit-animation: pace-spinner 400ms linear infinite;
  -moz-animation: pace-spinner 400ms linear infinite;
  -ms-animation: pace-spinner 400ms linear infinite;
  -o-animation: pace-spinner 400ms linear infinite;
  animation: pace-spinner 400ms linear infinite;
}

@-webkit-keyframes pace-spinner {
  0% { -webkit-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); transform: rotate(360deg); }
}
@-moz-keyframes pace-spinner {
  0% { -moz-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -moz-transform: rotate(360deg); transform: rotate(360deg); }
}
@-o-keyframes pace-spinner {
  0% { -o-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -o-transform: rotate(360deg); transform: rotate(360deg); }
}
@-ms-keyframes pace-spinner {
  0% { -ms-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -ms-transform: rotate(360deg); transform: rotate(360deg); }
}
@keyframes pace-spinner {
  0% { transform: rotate(0deg); transform: rotate(0deg); }
  100% { transform: rotate(360deg); transform: rotate(360deg); }
}
/*网页加载条 END*/
```

参考：[Hexo-NexT搭建个人博客（五） | Never_yu's Blog](https://neveryu.github.io/2017/07/15/hexo-next-five/)

另外，还看到一个方法，参考：[Hexo-NexT配置超炫网页效果 - 简书](https://www.jianshu.com/p/9f0e90cc32c2)

> 编辑主题配置文件搜索`pace`，将其值改为`ture`就可以了，选择一款你喜欢的样式。
>
> ```
> # Progress bar in the top during page loading.
> pace: ture
> # Themes list:
> #pace-theme-big-counter
> #pace-theme-bounce
> #pace-theme-barber-shop
> #pace-theme-center-atom
> #pace-theme-center-circle
> #pace-theme-center-radar
> #pace-theme-center-simple
> #pace-theme-corner-indicator
> #pace-theme-fill-left
> #pace-theme-flash
> #pace-theme-loading-bar
> #pace-theme-mac-osx
> #pace-theme-minimal
> # For example
> # pace_theme: pace-theme-center-simple
> pace_theme: pace-theme-minimal
> ```



### 第三方服务整合的比较全面的DEMO欣赏

- [博採眾長](https://lruihao.cn/)

  > 「关于」页面特别地还有个网易音乐播放，不错，另外，博客最底部的优化的不错，打算借鉴。

- [Vincent Qin](https://www.vincentqin.tech/)

- [wustxiao's blog](http://wustxiao.cn/2017/10/06/Hexo-Next%E4%B8%BB%E9%A2%98-%E6%96%87%E7%AB%A0%E6%B7%BB%E5%8A%A0%E9%98%85%E8%AF%BB%E6%AC%A1%E6%95%B0%EF%BC%8C%E8%AE%BF%E9%97%AE%E9%87%8F%E7%AD%89/)

- [Zack's Blog](http://www.aisun.org/)

- [进击的学霸的博客](https://l-cw.github.io/)



## 3. 主题制作

- [从零开始制作 Hexo 主题](http://www.ahonn.me/2016/12/15/create-a-hexo-theme-from-scratch/)
- [写一个自己的Hexo主题](https://segmentfault.com/a/1190000006057336)



---

*update：2018-01-30*

*update：2019-02-13 标题由「Hexo之NexT主题的配置及遇到的问题」改为了「NexT主题的配置修改指南及添加第三方服务」；增加了很多内容，如「2.第三方服务及其他修改」这节内容；其他地方做了一些删减和修改。* 

*update：2019-02-14 添加和修改了部分内容。*  