---
title: 博客搭建日志及博客文章管理说明
date: 2019-02-13 20:01:08
categories: Blog
tags: [blog] 
summary_img: /cover_images/001.jpg
---
博客搭建日志及博客文章管理说明。<!-- more -->

<h4 align="center">
    博客搭建日志
</h4>


- 基于Hexo+GitHub Page搭建博客及备份笔记
- NexT主题的配置修改指南及添加第三方服务
- 使用七牛云作为图床获取外链方式总结（已更换为使用PicGO+腾讯云COS）

<h4 align="center">
    博客文章管理
</h4>


关于 Front-matter：

``` markdown
---
title: 标题
date: 2018-04-29 20:01:08
categories: 分类
tags: [标签1,标签2] 
summary_img: 文章的封面路径,如/source/cover_images/001.jpg 图片必须在source文件夹下
description: 
comments: false #是否运行评论,默认true
---
```

代码片段 - Java 代码：

``` java
class Hello{
    public static void main(String[] args){
        System.out.print("hello world");
    }
}
```

未标识语言的代码片段：

``` 
#include<iostream>
int main(){
    std:cout<<"hello world";
}
```



音乐播放：

``` xml
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=1&height=66"></iframe>
```

``` html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=1&height=66"></iframe>
```



参考链接：

- [Hexo 图片插入](http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/)
- [Hexo-NexT搭建个人博客（五）——插入封面](https://neveryu.github.io/2017/07/15/hexo-next-five/) 