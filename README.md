>display:table-cell属性指让标签元素以表格单元格的形式呈现，类似于td标签。目前IE8+以及其他现代浏览器都是支持此属性的。我们都知道，单元格有一些比较特别的属性，例如元素的垂直居中对齐，关联伸缩等。table-cell同样会被其他一些CSS属性破坏，例如float, position:absolute，所以，在使用display:table-cell与float:left或是position:absolute属性尽量不用同用。设置了display:table-cell的元素对宽度高度敏感，对margin值无反应，响应padding属性，基本上就是活脱脱的一个td标签元素了。

- 首先来看一下如何实现显示简单的垂直居中的内容。

```html
<style type="text/css">
    .parent{
        display: table; 
        width:200px; 
        height:200px; 
        text-align:center; 
        border:1px solid #ccc;
    }
    .children{
        display:table-cell; 
        vertical-align: middle;
    }
</style>
<!-- Dom结构 -->
<div class="parent">
    <span class="children">
    垂直居中的内容
</span>
</div>
```

- 元素两端对齐，正常可以用float实现，但用float会有弊端，需要清除浮动。

```html
<style type="text/css">
* {
    box-sizing: border-box;
}
.content {
    display: table;
    border: 1px solid #06c;
    padding: 15px 15px;
    max-width: 1000px;
    margin: 10px auto;
    min-width: 320px;
    width: 100%;
}
.box {
    width: 100px;
    height: 100px;
    border: 1px solid #ccc;
    text-align: center;
    display: inline-block;
    font-size: 40px;
    line-height: 100px;
}
.right {
    text-align: right;
    display: table-cell;
}
.left {
    text-align: left;
    display: table-cell;
}
</style>
<!-- Dom结构 -->
<div class="content">
    <div class="left">
        <div class="box">B</div>
    </div>
    <div class="right">
        <div class="box">A</div>
    </div>
</div>
```

- 一行平分显示几个模块，一般会用float来做，或者把每个li设置成display:inline-block;来做，并且都要设置给他们设置一个宽度，而且最痛苦的是5个li如果你设置width:20%;他们一定会掉下来，如果li都设置成display:table-cell；就不会出现这种情况，即使不设置宽度他们也会在一行显示，你在加多一行他也不会掉下来，依旧会在一样显示。

```html
<style type="text/css">
* {
    box-sizing: border-box;
}
.content {
    display: table;
    border: 1px solid #06c;
    padding: 15px 15px;
    max-width: 1000px;
    margin: 10px auto;
    min-width: 320px;
    width: 100%;
}
.content ul {
    display: table;
    width: 100%;
    padding: 0;
    border-right: 1px solid #ccc;
}
.content ul li {
    display: table-cell;
    border: 1px solid #ccc;
    text-align: center;
    height: 100px;
    border-right: none;
    line-height: 100px;
}
</style>
<!-- Dom结构 -->
<div class="content">
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
    </ul>
</div>
```

- 图片垂直居中，有时候我们需要让图片垂直水平都居中于某个元素，用常规写法比较复杂，但用table-cell则相对简单。

```html
<style type="text/css">
* {
    box-sizing: border-box;
}
.content {
    display: table;
    border: 1px solid #06c;
    padding: 15px 15px;
    max-width: 1000px;
    margin: 10px auto;
    min-width: 320px;
    width: 100%;
}
.img-box {
    height: 150px;
    width: 100px;
    border: 1px solid red;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    background-color: #4679bd;
}
</style>
<!-- Dom结构 -->
<div class="content">
    <div class="img-box">
        <img src="1.png" />
    </div>
</div>
```

- 两box实现等高对齐，不对右侧的box设置display:table-cell，只对左侧，所以就会出现左侧跟随右侧高度变化而变化，如果要实现不管两个box哪个高度产生变化另一个就跟随，只需要把右侧的box也设置成display:table－cell就可以实现了。

```html
<style type="text/css">
* {
    box-sizing: border-box;
}
.content {
    display: table;
    border: 1px solid #06c;
    padding: 15px 15px;
    max-width: 1000px;
    margin: 10px auto;
    min-width: 320px;
    width: 100%;
}
.img-box {
    height: 50px;
    width: 100px;
    border: 1px solid red;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    background-color: #4679bd;
}
.text-box {
    margin-left: 20px;
    border: 1px solid #ddd;
    padding: 10px;
    display: table-cell;  /*注意会导致外边距失效*/
}
</style>
<!-- Dom结构 -->
<div class="content">
    <div class="img-box">
        <img src="1.png" />
    </div>
    <div class="text-box">
        <span>
          王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。
      </span>
    </div>
</div>
```

- 弹性、响应式布局，只要改变浏览器宽度就会发现他们其实都是会随高度变化自动变化高度的。

```html
<style type="text/css">
* {
    box-sizing: border-box;
}
.content {
    display: table;
    border: 1px solid #06c;
    padding: 15px 15px;
    max-width: 1000px;
    margin: 10px auto;
    min-width: 320px;
    width: 100%;
}
.left-box {
    float: left;
    margin-right: 10px;
    padding-top: 5px;
}
.right-box {
    display: table-cell;
    padding: 10px;
    border: 1px solid #ccc;
    margin-right: 10px;
    vertical-align: top;
}
</style>
<!-- Dom结构 -->
<div class="content">
    <div class="img-box">
        <img src="1.png" />
    </div>
    <div class="right-box">
        <span>王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。王尼玛和陈尼玛都是年轻有为的骚年，有一天他们相遇了，然后发现都对对方一见钟情后，所以就愉快的生活在了一起。。。。。</span>
    </div>
</div>
```

- 参考文献
1、[我所知道的几种display:table-cell的应用](http://www.zhangxinxu.com/wordpress/2010/10/%E6%88%91%E6%89%80%E7%9F%A5%E9%81%93%E7%9A%84%E5%87%A0%E7%A7%8Ddisplaytable-cell%E7%9A%84%E5%BA%94%E7%94%A8/)
2、[https://www.jianshu.com/p/2479665ee1f8](https://www.jianshu.com/p/2479665ee1f8)