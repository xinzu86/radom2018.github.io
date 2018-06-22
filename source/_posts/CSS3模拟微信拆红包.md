---
title: CSS3模拟微信拆红包
date: 2016/07/04 
updated: 2016/07/04 
categories:
- CSS3
tags:
- 拆红包 
- CSS3 
---

近期项目做活动页面，其中要实现一个类似微信拆红包效果，试着用CSS3实现了红包以及拆红包的动画。

###### HTML

```html
<!--微信红包-->
<div style="position:fixed;left:0;top:0;right:0;bottom:0;z-index:3;background-color:rgba(0,0,0,.5);">
<article class="redPacketsBox">
    <a href="javascript:;" class="closeRp">×</a>
    <!--拆开前-->
    <div class="rpBefore flex item-center" id="js-rpBefore">
        <div>
            <p>直播间主持人<br />给你发了一个红包</p>
        </div>
    </div>
    <!--拆开后-->
    <div class="rpAfter" id="js-rpAfter">
        <div class="hd flex item-center">
            <div class="">
                <p>恭喜你获得优惠券<br />App专享</p>
                <p class="hd-yuan">5元</p>
            </div>
        </div>
        <div class="ft">
            <button type="button" name="" class="button">去App使用</button>
            <p style="margin:5px 0 10px;">请使用微信授权登录</p>
            <button type="button" name="" class="button">继续观看鉴定会</button>
        </div>
    </div>
    <div>
        <button type="button" name="" class="bombBox" id="js-bomb"><span class="bombBox-inner">拆</span></button>
    </div>
</article>
</div>
```
###### CSS3

``` CSS
.redPacketsBox{position:fixed;left:50%;top:50%;z-index:9;margin:-200px 0 0 -150px;width:300px;min-height:400px;background-color:#EC514C;border-radius:5px;
    -webkit-animation: redPackets .8s ease-out;
    animation: redPackets .8s ease-out;
}
@-webkit-keyframes redPackets {
    0% {-webkit-transform: scale(.2);}
    50% {-webkit-transform: scale(1);}
    80% {-webkit-transform: scale(.8);}
    100% {-webkit-transform: scale(1);}
}
.redPacketsBox .closeRp{position:absolute;left:5px;top:5px;width:18px;height:18px;line-height:18px;text-align:center;color:#D24235;font-size: 22px;text-decoration: none;font-weight: bold;}
.redPacketsBox .rpBefore{min-height:240px;padding:20px;background-color:#FA6059;border-bottom: 1px solid #E5443F;color:#f7df95;font-size:22px;text-align:center;line-height:1.5;
    box-shadow: 0px 1px 0px -1px rgba(0,0,0,0.1);
    border-radius:10px 10px 50% 50% / 10px 10px 15% 15%;
}
.redPacketsBox .bombBox{position:absolute;left:50%;top:230px;margin-left:-45px;background-color:#F7DF95;width:90px;height:90px;padding:5px;
    border:none;outline:none;
    border-radius:100%;
    box-shadow: 0 1px 5px 1px rgba(0,0,0,.1);
}
.redPacketsBox .bombBox-inner{display:block;width:78px;height:78px;line-height:78px;font-size:36px;font-weight:bold;text-align:center;border:1px solid #E9BF6B;border-radius:100%;}
.redPacketsBox .rpAfter{display:none;text-align:center;padding:20px;}
.redPacketsBox .rpAfter .hd{min-height:260px;line-height:1.5;color:#f7df95;font-size:22px;}
.redPacketsBox .rpAfter .ft .button{width: 100%;box-sizing:border-box;height: 34px;font-size:16px;}
.redPacketsBox .rpAfter .hd-yuan{font-size:50px;margin-top:20px;}
.redPacketsBox .rotateY{
    -webkit-animation:bomb .6s infinite alternate;
            animation:bomb .6s infinite alternate;
}
@-webkit-keyframes bomb {
    from { -webkit-transform: rotateY(180deg); }
    to { -webkit-transform: rotateY(360deg); }
}
```
###### Javascript 点击事件

``` javascript
var _bomb = document.getElementById('js-bomb'),
  _rpBefore = document.getElementById('js-rpBefore'),
  _rpAfter = document.getElementById('js-rpAfter');
_bomb.onclick = function() {
  _bomb.className = 'bombBox rotateY';
  setTimeout(function() {
    _bomb.style.display = 'none';
    _rpBefore.style.display = 'none';
    _rpAfter.style.display = 'block';
  }, 2000)
}

```
附上项目实现截图，以及线上<a href="https://jsfiddle.net/srju7vqx/">demo</a>

<img src="../../../../images/20160704173920.png" alt="" />