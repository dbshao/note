####CSS定位属性


![CSS 框模型概述](https://upload-images.jianshu.io/upload_images/66256-d35c36e6b8560e0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![CSS 定位属性](https://upload-images.jianshu.io/upload_images/66256-75bdb4c78d96ca6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####相对定位
![相对定位](https://upload-images.jianshu.io/upload_images/66256-dac29aa47c0d15ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####绝对定位
>设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位，包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

![绝对定位](https://upload-images.jianshu.io/upload_images/66256-8f5480929f994725.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





#####浮动
![浮动](https://upload-images.jianshu.io/upload_images/66256-c77eae6a1b598334.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.news {
  background-color: gray;
  border: solid 1px black;
  }

.news img {
  float: left;
  }

.news p {
  float: right;
  }

<div class="news">
<img src="news-pic.jpg" />
<p>some text</p>
</div>
```
这种情况下，出现了一个问题。因为浮动元素脱离了文档流，所以包围图片和文本的 div 不占据空间。

如何让包围元素在视觉上包围浮动元素呢？需要在这个元素中的某个地方应用 clear：
![ct_css_positioning_floating_clear_div.gif](https://upload-images.jianshu.io/upload_images/66256-1a2c82802119a5d8.gif?imageMogr2/auto-orient/strip)
```
不幸的是出现了一个新的问题，由于没有现有的元素可以应用清理，所以我们只能添加一个空元素并且清理它。

.news {
  background-color: gray;
  border: solid 1px black;
  }

.news img {
  float: left;
  }

.news p {
  float: right;
  }

.clear {
  clear: both;
  }

<div class="news">
<img src="news-pic.jpg" />
<p>some text</p>
<div class="clear"></div>
</div>

这样可以实现我们希望的效果，但是需要添加多余的代码。常常有元素可以应用 clear，但是有时候不得不为了进行布局而添加无意义的标记。

不过我们还有另一种办法，那就是对容器 div 进行浮动：

.news {
  background-color: gray;
  border: solid 1px black;
  float: left;
  }

.news img {
  float: left;
  }

.news p {
  float: right;
  }

<div class="news">
<img src="news-pic.jpg" />
<p>some text</p>
</div>

这样会得到我们希望的效果。不幸的是，下一个元素会受到这个浮动元素的影响。为了解决这个问题，有些人选择对布局中的所有东西进行浮动，然后使用适当的有意义的元素（常常是站点的页脚）对这些浮动进行清理。这有助于减少或消除不必要的标记。

事实上，W3School 站点上的所有页面都采用了这种技术，如果您打开我们使用 CSS 文件，您会看到我们对页脚的 div 进行了清理，而页脚上面的三个 div 都向左浮动。
```
