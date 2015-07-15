---
layout: post
title: 用 css 实现的跟随滚动浮层在 ie6 下的 bug
category: "bug"
tags: ["css"]
---

这两天我用 ie6 测试了一下本站右侧内容块的跟随滚动情况，发现了一个莫名其妙的 bug，如下图所示，红框所在的块是用 css 实现的跟随滚动浮层，即不管浏览器右侧的上下滚动条怎么滚动，这个内容块都会固定在浏览器显示区的同一位置，但红框所在的内容出错了，没有固定在它该固定的位置上：

以下是其实现代码（只列出跟随滚动部分的代码）：

	<!-- 样式的代码 -->
	<style>
	.dFolA{position:fixed; top:10px; _position:absolute; _top:expression(document.documentElement.scrollTop+document.body.scrollTop+10);}
	</style>
	<!-- HTML 的代码 -->
	<div class="dFolA">红框所在块的内容代码</div>

其具体实现方法讲解可以看一下我之前写过的文章：跟随滚动的浮层实例；

而另一块跟随滚动浮层却没有问题，能够正常跟随滚动，如下图蓝框所示：

以下是其实现代码（只列出跟随滚动部分的代码）：

	<!-- 样式的代码 -->
	<style>
	.dFolB{position:fixed;bottom:10px;_position:absolute;_top:expression(document.documentElement.scrollTop+document.body.scrollTop+documentElement.clientHeight-this.offsetHeight-10);}
	</style>
	<!-- HTML 的代码 -->
	<div class="dFolB">蓝框所在块的内容代码</div>

我观察了很久，以为红框没有跟随滚动是因为 css 样式有问题，每一个字母都过了一篇，没有任何错误，那为什么蓝框正常，而红框不正常呢？然后我试了一下对调红蓝框的跟随滚动样式，发现红框正常了，蓝框不正常。这样可以证明问题不是其它代码引起，而是滚动的样式造成的。这时候我对比了一下两边的代码，发现不同之处是蓝框的样式代码有更多的 expression 计算公式，有计算浏览器的和自身高度的代码，请看上面蓝框样式代码的下划线部分。难道要加上这些？接下来我试了改动红框的跟随滚动代码，如下所示：

	<!-- 样式的代码 -->
	<style>
	.dFolA{position:fixed; top:10px; _position:absolute; _top:expression(document.documentElement.scrollTop+document.body.scrollTop+this.offsetHeight-this.offsetHeight+10);}
	</style>
	<!-- HTML 的代码 -->
	<div class="dFolA">红框所在块的内容代码</div>

不同之处在于增加了下划红部分代码，这部分代码是让公式加上同时也减去相同的值，并没有改变它总体计算下来的值，目的只是为了让 expression 增加红框块的高度计算。没想到接下来测试就正常了。ie6 居然存在这样的 bug，真的是无语。不过还好，最后还是解决了，任务完成。

(完)










