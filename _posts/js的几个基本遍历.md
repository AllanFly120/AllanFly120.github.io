---
layout: post
title: js数组遍历的方法
date: 2016-5-08
categories: blog
tags: [js, 总结]
---
##<b>js数组遍历的方法</b>##
<u>除了for以外的用法</u>

####` every`

1. 对于数组的每个元素进行运行如果都返回`true`，最后返回`true`
2. 判断数组元素是不是都大于2

		var arr = [1, 2, 3, 4, 5, 6, 7]

		var res = arr.every(funtion(item, index, array){
			return item > 2;
		});
		return res //res = false

-
####`filter`
返回过滤后的结果

		var res = arr.filter(funtion(item, index, array){
			return item > 2;
		});


-
####` foreach`

		var res = arr.foreach(function(item, index, arr){
			//do something
		});
		
-
####`map`

1. 数组对每个元素运行，完毕后返回新结果。常用于处理大量输入统一函数  

		var res = arr.map(function(item, index, arr){
			return item * 2;
		});
		alert(res); //[2, 4, 6, 8, 10, 12, 14]

-
####`some`

1. 与every对应，不过只要有一项返回`true`，则返回`true`

		var res = arr.some(funtion(item, index, array){
					return item >= 7;
				});
				return res //res = true

-
####`reduce`

1. 这个不算遍历方法不过也非常常用
2. 有reduce和reduceRight,基本一样只不过reduceRight是从右边开始
3. 传入方程prev, curr, index当前序号, array

		var res = arr.reduce(funtion(prev, curr, index, array){
					return prev + curr;
				});
				return res //res = 