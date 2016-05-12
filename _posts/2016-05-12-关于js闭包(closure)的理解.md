---
layout: post
title: 关于js闭包(closure)的理解
date: 2016-5-08
categories: blog
tags: [js, 总结]
---

##<b>闭包</b>

闭包在各种书上的解释还是很多的，不过总的来说很难理解，今天在读[闭包的秘密](https://www.gracecode.com/posts/2385.html)这篇文时发现了非常棒的解释：

###<b><u>closure is where a function remembers what happens around it</u></b>

一般常见的使用方式就是在一个函数内定义另一个函数。外层函数中定义的变量是绑定在外层的变量对象(variable object)上。而如果内层函数需要访问外层函数的这个变量，这个变量不会被垃圾回收清除(garbage collection)。

一般的如果我们需要`记住`绑定在环境变量中的所有变量，我们可以使用`var that = this` 把`this`的所有变量放入闭包中。下面的例子很好：

		function main(link) {			link.onclick = function(e) {			var newa = document.createElement("a");			var tn = document.createTextNode("second");
 			newa.appendChild(tn);			newa.href = "#";			this.firstChild.nodeValue = "clicked";			var that = this; 
			document.body.appendChild(newa); 
			newa.onclick = function(e) {				that.firstChild.nodeValue = "reset";				this.parentNode.removeChild(this); }			 }		}
		
这段函数是点击link时link上的内容变为"clicked",并在下面产生一个新的链接内容是"second"，如果点击"second"那么"clicked"会变成"reset",并且"second"会消失

这就是典型的闭包：通过`var that = this; `内层函数得以访问外层环境变量绑定的所有变量。



