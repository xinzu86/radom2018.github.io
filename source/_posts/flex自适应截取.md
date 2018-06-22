---
title: flex自适应截取
date: 2016/07/04 
updated: 2016/07/04 
categories:
- bug
tags:
- flex 
- ellipsis 
---
随着移动智能设备的越发普及，智能设备的软硬件也是炉火纯青，我们在做H5页面的时候，通常都会首选display:flex弹性模盒来布局，float基本抛之脑后。flex给我们带来好处的同时，也带来不少坑。最近在做项目时碰到页面效果如下（两个文字都要根据设备不同宽度做自就适应截取）：

<img src="../../../../images/flexEllipsis_01.png" alt="" />

###### CSS   
``` css
/* 弹性伸缩布局 */
.flex {
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
}
.flex-1 {
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  flex: 1;
}
/* 截取省略 */
.ellipsis {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
```

###### HTML 场景一

``` html
<div class="flex">
    <h2 class="ellipsis">主标题主标题主标题主标题主标题主标题主标题</h2>
    <p class="ellipsis">辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息</p>
</div>
```

###### HTML 场景二


``` html
<div class="flex">
    <img src="//image.huigoumai.com/20150327478d60ea86997338f3e45fa79a5bd4ad?imageView2/2/w/486/format/webp" width="100" height="100" alt="" />
    <div class="flex flex-1">
        <h2 class="ellipsis">主标题主标题主标题主标题主标题主标题主标题</h2>
        <p class="ellipsis">辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息</p>
    </div>
</div>
```

效果如下：

<img src="../../../../images/20160704155635.png" alt="" />

场景二的代码效果居然没能实现自适应截取。经过一翻折腾，最终试出来了，需在父元素使用了flex-1的情况下，重复加上截取样式，得知flex-1样式会引响到子元素ellipsis。

``` html
<div class="flex">
    <img src="//image.huigoumai.com/20150327478d60ea86997338f3e45fa79a5bd4ad?imageView2/2/w/486/format/webp" width="100" height="100" alt="" />
    <div class="flex flex-1 ellipsis">
        <h2 class="ellipsis">主标题主标题主标题主标题主标题主标题主标题</h2>
        <p class="ellipsis">辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息辅助信息</p>
    </div>
</div>
```

附上项目实现截图，以及线上<a href="https://jsfiddle.net/3v68ocuy/">demo</a>

