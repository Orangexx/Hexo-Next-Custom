---
title: Next 定制化记录
abstract: 才不给你看嘞！！
message: Who am I ？
date: 2019-06-13 20:14:07
password:
categories:
- 博客
tags:
- Hexo
- Next
---
作为一个前端小白。。还带点强迫症那种，东改西改改了两三天，大致把想要的效果都改出来了，这里做一个记录。主要是记录，大家也可以当做教程用一下，有些部分不够完善也放了比较详尽的地址。

便于自己记录，博文不光是采用了根据功能记录的结构还采用了根据文件记录的结构。
**博客搭建使用** **Hexo Next Mist**
<!--more-->

## 根据文件记录
### css/_custom/custom.styl

这个文件目录在 next\source\css\_custom，一开始是空的，看命名也可以知道是让用户自定义用的。

这个文件我主要是用来做一些背景的修改，字体颜色的修改以及总体的布局。实际上字体颜色等参数修改还有另一种方式，在下一个文件会介绍。
```
// Custom styles.
//设置代码颜色
#posts code {color: #FFFFF0;background-color:#000000;}

#sidebar {
			background-color:rgba(0,0,0,40%);
            background-size: cover;
            background-position:center;
            background-repeat:no-repeat;
            p,span,a{color: #87DAFF;}
}

	
body
{
	background:url(/images/custom/background.jpg);
    background-size:cover;
    background-repeat:no-repeat;
    background-attachment:fixed;
    background-position:center;

}
.content {
			padding: 20px;
            border-radius: 10px;
            margin-top: 60px;
            background:rgba(255,251,240,85%) none repeat scroll !important;
         }
.header {
          background:rgba(0,0,0,100%) none repeat scroll !important;
        }
.footer {
          background:rgba(0,0,0,30%) none repeat scroll !important;
        }
.footer-inner{color:$footer-text-Color;}
.main-inner {
			width: 800px;
}
```

### css/_variables/custom.style

目录在next/source/css/_variables/custom，Next 标记了一些例如 $brand-color 格式的参数，而在这个文件中就可以对这些参数赋值。我主要是使用这个进行了一些颜色的设置。也可以自己来创建这种参数，然后在这个文件中进行配置。

```
$brand-color = #EE9572
$menu-textcolor = #EE9572
$grey-dark = #EE9572
$footer-text-Color = #EE9572
$site-description-color = #87DAFF
```

## 根据功能记录
### Hitokoto 调用在侧边框

![Hitokoto](https://i.loli.net/2019/06/14/5d035527c6e7464599.jpg)

具体效果就是每次刷新界面都会有不一样的句子，[**Hitokoto**](https://hitokoto.cn/)的介绍可以直接点进去看一下。
由于是前端小白。。就硬着头皮找侧边框的文件，然后添加上去，文件在 \next\layout\_macro\sidebar.swig，具体的修改是在渲染描述那行前面加了两行代码。原理就是调用了 Hitokoto 官方提供的 Script 标签，然后使用 div 用  Description 的模式展示出来，用 id 来标定文本。

```
			  			  <script src="https://v1.hitokoto.cn/?c=d&encode=js&select=%23hitokoto" defer></script>
              <div class="site-description motion-element" id="hitokoto"></div>
              <div class="site-description motion-element" itemprop="description">{{ description }}</div>
```
### 文章加密

加密方法网上主要有两种，一种是直接加脚本判断，不过只要浏览者看一下源码就能看到，而另一种是使用 [**hexo-blog-encrypt**](https://github.com/MikeCoder/hexo-blog-encrypt) 插件，说明很详细，但是在使用的时候和 next 有冲突，文档中的一些方法还用不了，我出现的问题是加密的文档没法显示目录，经过一番修改后也只是做成了加密文档的目录不会加密的效果，勉勉强强解决了，具体解决方法在此 GitHub仓库 的 [这个Issues](https://github.com/MikeCoder/hexo-blog-encrypt/issues/16) 下，由于版本不同源代码已经进行了更新，大家还是对着这解决方案自己一点点改比较好，感谢 edward-p 和 xmeng1 的分享，对于 mist 来说两位大佬的方案都要采用，其他的主题模式不太清楚。

### 字数、时间统计
此功能使用的是 next 自带的 [**symbols_count_time**](https://github.com/theme-next/hexo-symbols-count-time)，根据 GitHub 上的文档操作，先在 Hexo项目 根目录下打开命令行工具，输入指令下载插件
```
$ npm install hexo-symbols-count-time --save
```
这里有个地方要注意一下，下载完成之后需要对 Hexo 的 _config 和 Next 的 _Config 两个文件进行配置，具体配置参考 GitHub 说明文档。

### 阅读量统计
Next 自带了 busuanzi 的访客统计(其实我也记不清当时怎么做的了。。)，在 next 的 _config.yml 文件中搜索到 busuanzi_count，进行相关开关及配置即可。

这里是我这个版本的配置，大家可以根据初始状态的模板进行修改。
```
busuanzi_count:
  enable: true
  total_visitors: false
  total_visitors_icon: user
  total_views: false
  total_views_icon: eye
  post_views: true
  post_views_icon: eye
```

### 简易评论功能
简易评论功能这里使用的是 [**Valine**](https://valine.js.org/)，目前对于访客评论没有任何限制，只是会提示访客输入邮箱和博客地址。Valine 使用 LeanCloud 做评论存储和管理，需要先注册 [**LeanCloud**](https://leancloud.cn/) 并配置，然后就是对于 Next _config 的配置，根据[这篇文章](https://nobige.cn/post/20180725-forHexoAddValine/)操作就可以了(才不是我懒！！！)。

Next 评论框样式是透明的，由于和我设置了背景，倒置我这边看起来很不舒服，之后研究一番改了评论框的样式，是在这个文件中进行修改next\source\css\_common\components\comments.styl，下面的代码分别是指页边距、圆角、整体间距？背景颜色。
```
.comments { 
padding: 10px;
border-radius: 10px;
margin: 60px 20px 0;
background-color:rgba(255,239,213,85%); 
}
```

### 为搜索引擎收录（待做）

## 其他分享
### 图床工具
由于 GitHub 的速度问题，一般大家会把图片放到国内的图床上，这里推荐一个图床工具 [**PicGo**](https://molunerfinn.com/PicGo/)。

### MarkDown 编辑器
Next 介绍中有一款专门针对 Hexo 的工具 [**HexoEditor**](https://github.com/zhuzhuyule/HexoEditor)，之前我一直在用的是 [**Typora**](https://www.typora.io/)，两款都不错。



