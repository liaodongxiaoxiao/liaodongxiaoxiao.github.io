---
layout: post
title:  Android SDK 历史版本
categories: [Android,SDK]
tags:	[Android,SDK]
---
### 0. Android 历史版本

> 以下内容参考于 [Wikipedia](https://en.wikipedia.org/wiki/Android_version_history){:target="_blank"}

 版本 | API Level | Version Code | 发布日期 
 :------ | :-------: | :----------- | :-----------
  1.0 | 1 | [`BASE`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#BASE) | 2008-09-23
  1.1 | 2 | [`BASE_1_1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#BASE_1_1)  | 2009-02-09
  1.5 | 3 | [`CUPCAKE`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#CUPCAKE)  | 2009-04-27
  1.6| 4 | [`DONUT`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#DONUT)  | 2009-09-15
  2.0| 5 | [`ECLAIR`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#ECLAIR)  | 2009-10-26
  2.0.1 | 6 | [`ECLAIR_0_1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#ECLAIR_0_1)  | 2009-12-03
  2.1.x | 7 | [`ECLAIR_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#ECLAIR_MR1)  | 2010-01-12
  2.2.x | 8 | [`FROYO`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#FROYO)  | 2010-05-20
  2.3-2.3.2| 9 | [`GINGERBREAD`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#GINGERBREAD)  | 2010-12-06
  2.3.3-2.3.4 | 10 | [`GINGERBREAD_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#GINGERBREAD_MR1)  | 2011-02-09
  3.0.x| 11 | [`HONEYCOMB`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#HONEYCOMB)  | 2011-02-22
  3.1.x | 12 | [`HONEYCOMB_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#HONEYCOMB_MR1)  | 2011-05-10
  3.2.x| 13 | [`HONEYCOMB_MR2`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#HONEYCOMB_MR2)  | 2011-07-15
  4.0-4.0.2 | 14 | [`ICE_CREAM_SANDWICH`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#ICE_CREAM_SANDWICH)  | 2011-10-18
  4.0.3-4.0.4| 15 | [`ICE_CREAM_SANDWICH_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#ICE_CREAM_SANDWICH_MR1)  | 2011-12-16
  4.1-4.1.1 | 16 | [`JELLY_BEAN`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#JELLY_BEAN)  | 2012-07-09
  4.2-4.2.2 | 17 | [`JELLY_BEAN_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#JELLY_BEAN_MR1)  | 2012-11-13
  4.3| 18 | [`JELLY_BEAN_MR2`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#JELLY_BEAN_MR2)  | 2013-07-24
  4.4| 19 | [`KITKAT`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#KITKAT)  | 2013-10-31
  4.4W | 20 | [`KITKAT_WATCH`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#KITKAT_WATCH)  | 2014-06-25
  5.0 | 21 | [`LOLLIPOP`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#LOLLIPOP)  | 2014-11-12
  5.1 | 22 | [`LOLLIPOP_MR1`](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#LOLLIPOP_MR1)  | 2015-03-09
  6.0 | 23 | [`M` (Marshmallow)](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#M)  | 2015-10-05
  7.0 | 24 | [`N` (Nougat)](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#N)  | 2016-08-01
  7.1 | 25 | [`N_MR1` (Nougat MR1)](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html#N_MR1)  | 2016-10-04

### 1. Java代码中使用
{% highlight java %}
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
	...
}
{% endhighlight %}