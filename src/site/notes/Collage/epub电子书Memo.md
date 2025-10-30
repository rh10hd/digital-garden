---
{"dg-publish":true,"permalink":"/collage/epub-memo/","created":"2025-10-30T08:33:03.000+08:00"}
---

## 概览

之前在[[Collage/Kindle的一点随想\|Kindle的一点随想]]里提过最近都在使用kindle看书，那么找书就成了一项重要工作，我原以为找完书用Calibre导出再放进kindle就好了，可是没想到有些书在kindle里“水土不服”，不是大小不适配kindle就是注释无法在kindle正常显示，于是我又走上了“制作”电子书的道路，现在特意记录一下。

我使用的工具是[Calibre](https://calibre-ebook.com/)自带的编辑图书和[Sigil](https://sigil-ebook.com/)，这两款应该是目前最主流的电子书编辑／管理工具了，使用起来也比较容易。测试工具是Mac自带的Books和Calibre的阅读。

## 问题类型及解决方案

### 注释问题汇总

打开一本书我一般都会直接搜索关键词：footnote, note去检索里面的注释是否正常，而我遇到的注释有问题的书主要有这么几类：

- 注释无法跳转
- 注释和正文混排
- 弹窗注释弹出后立刻消失
- 无注释

下面会记录我是如何解决的这些问题的。

#### 注释无法跳转

注释无法跳转一般是因为没有指定锚点，只要加上唯一的id即可

引文：

`<sup><a id="footnoten1" href="#notebackn1">[1]</a></sup>`

注释：

`<p class="calibre_5><a id="notebackn1" href="#footnoten1"></a></p>`

#### 注释和正文混排

注释和正文混排我遇到的最普遍的情况就是使用了`<aside>`标签，部分阅读器（包括Kindle端的koreader）或者阅读软件会将其当作正文内容处理。虽然在阅读上无障碍，但是容易干扰阅读，尤其是当注释过长的时候，如下图：

![正文和注释混排.png](/img/user/Collage/%E6%AD%A3%E6%96%87%E5%92%8C%E6%B3%A8%E9%87%8A%E6%B7%B7%E6%8E%92.png)

如果是这样，最省事的方法就是直接改用能够识别`<aside>`标签的阅读器或者阅读软件，iOS端推荐使用自带的Books，非常强大的阅读工具，兼容性非常优秀，我几乎所有的电子书（epub格式）它都能正常处理，缺点就是支持的格式太少了，甚至连txt都不支持。

Android端推荐使用Moon Reader（静读天下），Android端上非常优秀阅读软件，和Books可以相媲美，支持的格式还更多，免费版有广告，买断10.99刀。

另外推荐一款iOS，Android，Windows，Mac和Linux都适用且开源免费的阅读软件[Readest](https://readest.com/)，支持云同步，也能够正常阅读`<aside>`的书籍。免费版提供500m的云空间，还有premium版，有条件的话就支持一下开发者们吧。

当然如果注释不多的话，可以自己手动改或者采用脚本更改。我就选择了最省事的方法，因为不想折腾。

#### 弹窗注释弹出后立刻消失

把鼠标放在注上，会有弹窗出现然后立刻消失，这一般是css有问题，在`sytlesheet.css`（可能会叫其他名字）找到对应的脚注格式更改即可。

![脚注格式代码.png](/img/user/Collage/%E8%84%9A%E6%B3%A8%E6%A0%BC%E5%BC%8F%E4%BB%A3%E7%A0%81.png)

我在`hover:`后增加了一个`after`所有注释即恢复正常。

#### 无注释

无注释一般有两个情况，一个是制作人员没有添加锚点，且把注释放在比较隐蔽的地方，此时参考添加锚点的方法补充注释即可，另一种则是书本本身并无注释，此时无能为力，建议放弃。

### 其他排版问题

记录一下我觉得还不错的注释排版：

```
<hr class="calibre4"/>
  <p class="calibre_"><span class="calibre5"><a id="notebackn21" href="#noten21">[1]</a> 原文是ball breaker，直译为打破睾丸的人。</span></p>
  <p class="calibre_"><span class="calibre5"><a id="notebackn22" href="#noten22">[2]</a> 原文为ballsy。</span></p>
  <p class="calibre_"><span class="calibre5"><a id="notebackn23" href="#noten23">[3]</a> 露西尔·鲍尔（Lucille Ball），Ball人名音译为鲍尔。</span></p>
  <div class="mbp_pagebreak" id="calibre_pb_160"></div>
```

![longshot20251030173854.png](/img/user/Collage/longshot20251030173854.png)

该书是范妮·弗拉格的《油炸绿番茄》。