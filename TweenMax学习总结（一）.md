# TweenMax学习总结（一）

### 初识TweenMax

* 缘于在学习JavaScript的时候，做了一个回到顶部的demo：https://jiangnanmax.github.io/JS_back_to_top/ 只是使用缓动函数简单的实现了回到顶部的功能，没有任何动画特效，觉得甚是乏味。在网上找各种回到顶部的插件，最后找到了一个动画特效比较酷炫的插件，做了些改进，查看效果请点击链接：https://jiangnanmax.github.io/Back_To_Top/ 发现这个插件使用了一个TweenMax.js的动画库，然后只要几行简单的代码就能实现各种酷炫的动画效果，十分社会，遂学之。

* 和其它的库类似，TweenMax动画库也依赖于jQuery库，以上两个文件都放在了Github上：https://github.com/JiangNanMax/TweenMax 

### 引用TweenMax库

```
<script src="js/jquery.min.js"></script>
<script src="js/TweenMax.js"></script>  
```

### 创建一个动画实例

```
$(function () {
        var t = new TimelineMax();

    });
```

### to()方法：用来添加动画

* 方法介绍和参数说明

```
// TweenMax.to()是最常用的方法，它允许你定义对象的各个目标值
t.to("元素选择器或对象",持续时间,对象(描述运动的方向参数等),(可选)动画延迟发生时间可写数字,"-=0.5","+=0.5")
/*
	1. 传入一个元素选择器或对象
	
	2. 设定动画的持续时间
	
	3. 对象
		
		{变化的属性:值}
		
	4. (可选)动画延迟发生时间
		
		可写数字，“-=0.5”，“+=0.5“
*/
```

### 实例演示

* 页面布局

```
<body>
	<div id="div1"></div>
</body>
```

```
<style>
        html,body{
            margin: 0;
            padding: 0;
        }

        #div1{
            width: 100px;
            height: 100px;
            background-color: #8D121A;
            position: absolute;
            left: 0;
            top: 100px;
        }
</style>
```

* 执行单个动画

```
<script>
	$(function(){
		var t =new TimelineMax();
		t.to("#div1", 1, {left:300});
	});
</script>
```

* 执行组合动画,其中第三个参数内的动画效果同时进行

```
<script>
	$(function(){
		var t =new TimelineMax();
		t.to("#div1", 1, {left:300,width:300});
	});
</script> 
```

* 执行一个队列的动画，其中队列中的动画会依次进行

```
<script>
	$(function(){
		var t =new TimelineMax();
		
		t.to("#div1", 1, { left: 300 });
		t.to("#div1", 1, { width: 300 });
		t.to("#div1", 1, { height: 300 });
		t.to("#div1", 1, { top: 300 });
		t.to("#div1", 1, { rotationZ: 180 });
		t.to("#div1", 1, { opacity: 0 });
	});
</script>
```

* 添加第四个参数，设置动画播放的延迟时间

 ```
 <script>
	$(function(){
		var t =new TimelineMax();
		
		t.to("#div1", 1, { left: 300 }, 1); //第一个动画延迟1s后执行
		t.to("#div1", 1, { width: 300 }); //第二个动画没有添加延迟，因此轮到它的时候立即执行
	});
</script>
 ```
 
 ```
 <script>
	$(function(){
		var t =new TimelineMax();
		
		t.to("#div1", 1, { left: 300, width: 300 }, 1); //第一个动画延迟1s后执行
		t.to("#div1", 1, { width: 300 }, 1); //第二条动画也是延迟一秒执行,会和第一条动画同时延迟一秒执行
	});
</script>
 ```
 
* 延迟执行第二个动画

 ```
 <script>
	$(function(){
		var t =new TimelineMax();
		
		t.to("#div1", 1, { left: 300, width: 300 }, 1); //第一个动画延迟1s后执行
		t.to("#div1", 1, { width: 300 }, 3); //实现第一条动画完成后,延迟一秒,执行第二条动画
	});
</script>
 ```
 
* 通过play()方法和stop()方法来控制动画的播放与停止

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html,body{
            margin: 0;
            padding: 0;
        }

        #div1{
            width: 100px;
            height: 100px;
            background-color: #8D121A;
            position: absolute;
            left: 0;
            top: 100px;
        }
    </style>
</head>
<body>
<input type="button" id="play" value="播放">
<input type="button" id="stop" value="停止">
<input type="button" id="reverse" value="反向播放">
<div id="div1"></div>

<script src="js/jquery-2.1.4.min.js"></script>
<script src="js/TweenMax.js"></script>

<script>
    $(function () {
        var t = new TimelineMax();

        t.to("#div1", 1, {left: 300}, 1);
        t.to("#div1", 2, {width: 300}, "+=1");
        t.to("#div1", 2, {height: 300}, "+=1");
        t.to("#div1", 2, {top: 600});
        t.to("#div1", 2, {rotationZ: 360});
        t.to("#div1", 2, {opacity: 0});
        t.stop();

        //通过play()方法和stop()方法来控制动画的播放与停止
        $("#play").click(function () {
            t.play();
        });

        $("#stop").click(function () {
            t.stop();
        });


    });
</script>

</body>
</html>
```

* 通过reverse()方法让动画反向执行

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html,body{
            margin: 0;
            padding: 0;
        }

        #div1{
            width: 100px;
            height: 100px;
            background-color: #8D121A;
            position: absolute;
            left: 0;
            top: 100px;
        }
    </style>
</head>
<body>
<input type="button" id="play" value="播放">
<input type="button" id="stop" value="停止">
<input type="button" id="reverse" value="反向播放">
<div id="div1"></div>

<script src="js/jquery-2.1.4.min.js"></script>
<script src="js/TweenMax.js"></script>

<script>
    $(function () {
        var t = new TimelineMax();

        t.to("#div1", 1, {left: 300}, 1);
        t.to("#div1", 2, {width: 300}, "+=1");
        t.to("#div1", 2, {height: 300}, "+=1");
        t.to("#div1", 2, {top: 600});
        t.to("#div1", 2, {rotationZ: 360});
        t.to("#div1", 2, {opacity: 0});
        t.stop();

        //通过play()方法和stop()方法来控制动画的播放与停止
        $("#play").click(function () {
            t.play();
        });

        $("#stop").click(function () {
            t.stop();
        });

        //通过reverse()方法让动画反向执行
        $("#reverse").click(function () {
            t.reverse();
        });

    });
</script>

</body>
</html>
```

* 动画运动结束后的回调函数：onComplete()； 动画反向运动结束后的回调函数：onReverseComplete()

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        html,body{
            margin: 0;
            padding: 0;
        }

        #div1{
            width: 100px;
            height: 100px;
            background-color: #8D121A;
            position: absolute;
            left: 0;
            top: 100px;
        }
    </style>
</head>
<body>
<input type="button" id="play" value="播放">
<input type="button" id="stop" value="停止">
<input type="button" id="reverse" value="反向播放">
<div id="div1"></div>

<script src="js/jquery-2.1.4.min.js"></script>
<script src="js/TweenMax.js"></script>

<script>
    $(function () {
        var t = new TimelineMax();

        t.to("#div1", 1, {left: 300,onComplete:function () {
                alert("left:300px");
            },onReverseComplete:function () {
                alert("lef:0px");
            }}, 1);
        t.to("#div1", 2, {width: 300}, "+=1");
        t.to("#div1", 2, {height: 300}, "+=1");
        t.to("#div1", 2, {top: 600});
        t.to("#div1", 2, {rotationZ: 360});
        t.to("#div1", 2, {opacity: 0});
        t.stop();

        //通过play()方法和stop()方法来控制动画的播放与停止
        $("#play").click(function () {
            t.play();
        });

        $("#stop").click(function () {
            t.stop();
        });

        //通过reverse()方法让动画反向执行
        $("#reverse").click(function () {
            t.reverse();
        });

        //onComplete()：运动结束后触发的函数
        //onReverseComplete()：反向运动结束后触发的函数
        //对应补充如上：
    });
</script>

</body>
</html>
```