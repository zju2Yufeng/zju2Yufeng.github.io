---
layout: article
title: 关于一台「404」笔记本的使用感想
tags: chromebook
---

这段时间每天都要背着电脑上下班，开始后悔为了更爽地做幻灯而买的ThinkBook 16+了，虽然有着丰富的接口、清晰且16寸的大屏幕、全尺寸不怎么好用的键盘（这一点真的是不如他的兄弟ThinkPad）、不错的机身质感，但是整机加上充电器超过2Kg的重量让我的肩膀已经不堪重负。想着换一台更加轻便的笔记本用来通勤和写写文档，考虑到刚买没多久的ThinkBook和本不富裕的钱包，只能放弃这种败家的想法。

不过几天前，在[少数派的文章](https://sspai.com/post/80882)中，看到有人买了一部2017年的Pixelbook，瞬间对Chromebook这个「404」的笔记本有了兴趣——低廉的价格、轻薄的机身——这些特点正好戳中被书包重量折磨的我，于是直接从闲鱼上淘了一台Google Pixelbook Go。

这台2019年次顶配的Pixelbook Go有着手感不错的键盘，轻薄的机身，好看且质感不错的外观，唯一的缺点可能是只配备了一块1080P分辨率的显示屏，这让习惯了高分辨率显示屏的我多少有些不适应。不过考虑到这要998的价格，还要啥自行车呢。可惜的是，Google在2022年的时候，[解散了Pixelbook团队并且取消了下一代Pixelbook项目](https://new.qq.com/rain/a/20220913A00COO00)，不知道下一代的Pixelbook Go还能不能出现。

## 开始使用ChromeOS

除了网络条件严格以外，ChromeOS系统使用十分简单，登入自己的Google账号就可以完成大部分的配置，包括Chrome浏览器的插件、书签、浏览记录也会一起同步。另外，自己的安卓手机也可以连接到Chromebook，并且用于解锁。这让我有了一种以前使用苹果生态的感觉，但是比起苹果全家桶还是少了很多的易用性。

在ChromeOS上除了特殊的网络以外，最需要解决的是输入法问题。现在可以在Chrome浏览器中安装[真文韵输入法](https://chrome.google.com/webstore/detail/%E7%9C%9F%E6%96%87%E9%9F%B5%E8%BE%93%E5%85%A5%E6%B3%95/ppgpjbgimfloenilfemmcejiiokelkni?hl=zh-CN)插件来实现中文输入。

### 一个小BUG

在Google 文档中，使用中文输入法的时候会出现候选框不跟随光标而在屏幕顶端的情况。这个情况应该是Google 文档的BUG，因为不仅仅在我的Chromebook上出现，同时也在我的windows电脑上出现了。解决的方法也很简单，就是把无障碍功能的「开启屏幕放大镜支持」勾选。

## 调教Linux系统

Chromebook可以开启Linux 系统，大大增加了这台上网本的可玩性，可以安装WPS、Zotero、typora等应用。这样，我就可以在这台Chromebook上看文献，写论文了。

不过在舒服的使用Linux之前，我们还需要配置Linux的中文环境，包括输入法的配置。这个在网上其实很有多教程，大部分都是基于Fcitx输入框架下配置Google 拼音或者搜狗输入法解决的。不过我参考的那篇[教程](https://blog.csdn.net/weixin_44054078/article/details/120105916)是比较早的版本，在**环境配置**中通过在`cros-garcon-override.conf`中添加配置来实现中文输入环境。但是，在最新的版本中，似乎这种配置方法已经被弃用。现在需要通过`environment.d`进行用户环境的配置，具体的配置方法如下：

```shell
mkdir -p ~/.config/environment.d/
vi ~/.config/environment.d/fcitx.conf
```

并且在`fcitx.conf`配置文件中加入如下的配置：

```shell
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

### 没有解决的问题

通过上述的方法，我实现了Google输入法输入中文。但是，我尝试着安装更加符合国人的搜狗输入法时，出现无法弹出候选框的问题。这个问题可能与`libqt4-declarative`框架缺失有关。但是在尝试通过`sudo apt install libqt4-declarative`安装是出现了「软件包无法定位」的报错。本着能用就用，不下折腾的原则，放弃了使用搜狗拼音的想法。

## 安卓子系统

在Chromebook上，我们可以通过**Play商店**安装安卓应用。但是这个存在这适配的问题，有些应用适配的还不错，比如Netflix，Don't Starve，而有些应用，就一言难尽了，比如那个微信。不过转念一想，可能没有微信是一件好事情呢。

## 尾巴

「轻」可能是我对这个Google Pixelbook Go的最终印象。随手打开就用，用完随手一扔。比起Windows笔电，有着更长的续航，打开就用的优点；比起Ipad，有着桌面级别的浏览器和Linux的加持；比起Macbook，有着更加便宜的价格。不过，「轻」也意味着他只能干一些轻活：码码字、浏览浏览网页、刷刷剧。对于998的价格来说，我也不奢求他能干更多的事情了。Pixelbook Go如同他的名字一样，这是一台我会想着带出去的笔记本。
