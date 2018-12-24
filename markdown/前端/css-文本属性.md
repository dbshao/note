text-indent
>通过使用 text-indent 属性，所有元素的第一行都可以缩进一个给定的长度，甚至该长度可以是负值。

text-align 
>text-align 是一个基本的属性，它会影响一个元素中的文本行互相之间的对齐方式。它的前 3 个值相当直接，不过第 4 个和第 5 个则略有些复杂。
值 left、right 和 center 会导致元素中的文本分别左对齐、右对齐和居中

word-spacing
>word-spacing 属性可以改变字（单词）之间的标准间隔。其默认值 normal 与设置值为 0 是一样的。
word-spacing 属性接受一个正长度值或负长度值。如果提供一个正长度值，那么字之间的间隔就会增加。为 word-spacing 设置一个负值，会把它拉近

letter-spacing
>letter-spacing 属性与 word-spacing 的区别在于，字母间隔修改的是字符或字母之间的间隔。
与 word-spacing 属性一样，letter-spacing 属性的可取值包括所有长度。默认关键字是 normal（这与 letter-spacing:0 相同）。输入的长度值会使字母之间的间隔增加或减少指定的量

text-transform

  none
    uppercase
    lowercase
    capitalize
>默认值 none 对文本不做任何改动，将使用源文档中的原有大小写。顾名思义，uppercase 和 lowercase 将文本转换为全大写和全小写字符。最后，capitalize 只对每个单词的首字母大写。
作为一个属性，text-transform 可能无关紧要，不过如果您突然决定把所有 h1 元素变为大写，这个属性就很有用。不必单独地修改所有 h1 元素的内容，只需使用 text-transform 为你完成这个修改：

text-decoration
none
    underline
    overline
    line-through
    blink
>不出所料，underline 会对元素加下划线，就像 HTML 中的 U 元素一样。overline 的作用恰好相反，会在文本的顶端画一个上划线。值 line-through 则在文本中间画一个贯穿线，等价于 HTML 中的 S 和 strike 元素。blink 会让文本闪烁，类似于 Netscape 支持的颇招非议的 blink 标记。
none 值会关闭原本应用到一个元素上的所有装饰。通常，无装饰的文本是默认外观，但也不总是这样。例如，链接默认地会有下划线。如果您希望去掉超链接的下划线，可以使用以下 CSS 来做到这一点

white-space
![2018-11-27_142759.png](https://upload-images.jianshu.io/upload_images/66256-3f6ccb70b99a2bd4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![2018-11-27_142917.png](https://upload-images.jianshu.io/upload_images/66256-c609164daebb23cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




