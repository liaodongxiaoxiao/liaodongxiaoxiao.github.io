---
layout: post
title:  Android EditText 用法总结
categories: [Android,EditText]
tags:	[Android Tips]
---
> Android *EditText* 是开发过程中最常用的控件之一
> 以下是EditText常用的方法总结

## 1. 用Shape设置EditText只有一条底线背景的样式

<div style="width:100%" align="center">
	<img src="{{ site.BASE_PATH}}/img/android_edittext_tips_00.png" alt="NB" style="width: 200px;"/>
   
</div>

#### 1.1在 *res/drawable* 目录下定义一个 *editview_selector.xml* 文件
{% highlight xml %} 
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 获得焦点时的图片背景 -->
    <item android:state_focused="true">
	  <layer-list>
         <item>
          <shape>
            <solid android:color="@color/colorPrimaryDark"/>
          </shape>
         </item>
         <item android:bottom="2dp">
            <shape>
               <solid android:color="#ffffff"/>
            </shape>
         </item>
        </layer-list>
    </item>
    <!-- 默认情况下 -->
    <item>
        <layer-list>]
            <item>
                <shape>
                    <solid android:color="@color/colorPrimary"/>
                </shape>
            </item>
            <item android:bottom="1dp">
                <shape>
                    <solid android:color="#ffffff"/>
                </shape>
            </item>
        </layer-list>
    </item>
</selector>

{% endhighlight %}
#### 2.在 *layout* 布局文件中设置EditText的背景
{% highlight xml %}
<EditText
    ...
    android:background="@drawable/editview_selector"
    ...
/>
{% endhighlight %}

## 2.


