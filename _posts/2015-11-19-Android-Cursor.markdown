---
layout: post
title:  "Android Cursor的正确遍历方法"
date:   2015-11-19 11:09:25 +0800
categories: [Android Development Notes,Android Tips]
---
之前在项目中，我在维护代码时，发现一个bug，遍历出的结果很奇怪。
本来查出10条数据，然通过上述代码遍历会丢数据。
在没debug，这段代码时，我排除了好多假设，花了我好久的时间。
而且每次遍历的数据条数都在变。
同事遍历Cursor是这样写的:
{% highlight java %}
if(cursor ==null) {
	Log.w(TAG,"....");
}else{
	while(cursor.moveToNext()){
		//do someting ....
	}
}
{% endhighlight %}
找了好久才发现，这段遍历的方式不对。他就没有把Cursor移动到起始位置。
正确的遍历方式是这样的：
{% highlight java %}
//cursor不为空，moveToFirst为true说明有数据
if(cursor!=null&&cursor.moveToFirst()){
	do{
		//do something
	}while(cursor.moveToNext);
}
{% endhighlight %}
或者：
{% highlight java %}
if(cursor!=null&&cursor.moveToFirst()){
	while (!result.isAfterLast()) {
		//do something
	}
}
{% endhighlight %}