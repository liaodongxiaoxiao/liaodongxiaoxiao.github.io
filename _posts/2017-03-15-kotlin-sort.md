---
layout: post
title:  Kotlin 集合排序
categories: [Kotlin,sort]
tags:	[Kotlin]
---
## 0. 写在前边
> 最近在工作间隙，试了一把Kotlin。一发车就根本停不下来，各种语法糖，各种炫酷的写法...
> 
> 闲话少叙，分享一下学习中遇到的**集合排序问题**
<div style="width:100%" align="center">
	<img src="{{ site.BASE_PATH}}/img/cool_img_001.jpg" alt="NB" style="width: 200px;"/>
</div>

## 1. 先构造一个业务类Person 及 Person集合

{% highlight java %} 
//定义一个Person类，有name 和 age 两属性
data class Person(var name: String, var age: Int)

var personList: MutableList<Person> = mutableListOf()
personList.add(Person("Jim", 12))
personList.add(Person("A-Lin", 12))
personList.add(Person("Tom", 11))
personList.add(Person("Mary", 14))

{% endhighlight %}

## 2. 使用 sortBy 排序
{% highlight java %} 
fun main(args: Array<String>) {
    //构造personlist...

    println("----排序前----")
    personList.forEach(::println)
    println("----排序后----")
    //按年龄排序
    personList.sortBy ({ it.age })
    //或者写成
    //personList.sortBy(Person::age)
    personList.forEach(::println)
 }
{% endhighlight %}
运行结果如下：
{% highlight java %}
----排序前----
Person(name=Jim, age=12)
Person(name=A-Lin, age=12)
Person(name=Tom, age=11)
Person(name=Mary, age=14)
----排序后----
Person(name=Tom, age=11)
Person(name=Jim, age=12)
Person(name=A-Lin, age=12)
Person(name=Mary, age=14)
{% endhighlight %}

> **sortBy** 为正序排列，跟其对应的降序方法为 **sortByDescending**

{% highlight java %}
personList.sortByDescending({ it.age })

//运行的结果为
----排序后----
Person(name=Mary, age=14)
Person(name=Jim, age=12)
Person(name=A-Lin, age=12)
Person(name=Tom, age=11)

{% endhighlight %}

## 3. 使用 sortWith 排序
> 实际情况下，我们的业务需求往往需要根据多个条件来排序，这时我们就需要用到 **sortWith** 方法

{% highlight java %}
//先根据age 升序排列，若age相同，根据name升序排列
personList.sortWith(compareBy({ it.age }, { it.name }))
// 运行结果如下：
----排序后----
Person(name=Tom, age=11)
Person(name=A-Lin, age=12)
Person(name=Jim, age=12)
Person(name=Mary, age=14)
{% endhighlight %}
> **sortWith** 方法中，传入的  **compareBy({属性1},{属性2},...)**参数， compareBy（） 这里的参数个数是可变的，但是都是默认的升序排列。所以我们还可以根据自己的实际需求，给**sortWith**传入一个**Comparator**对象，来达到一个更高级更复杂的逻辑
{% highlight java %}
//构造一个Comparator对象，完成排序逻辑：先按age降序排列，若age相同，则按name升序排列
val c1: Comparator<Person> = Comparator { o1, o2 ->
        if (o2.age == o1.age) {
            o1.name.compareTo(o2.name)
        } else {
            o2.age - o1.age
        }
    }
personList.sortWith(c1)

// 运行结果如下：
----排序后----
Person(name=Mary, age=14)
Person(name=A-Lin, age=12)
Person(name=Jim, age=12)
Person(name=Tom, age=11)

{% endhighlight %}

## 4. 通过 data class 实现 Comparable 接口来排序
重新构造 Person 类
{% highlight java %}
data class Person(var name: String, var age: Int) : Comparable<Person> {
    override fun compareTo(other: Person): Int {
        if (this.age == other.age) {
            return this.name.compareTo(other.name)
        } else {
            return other.age - this.age
        }
    }

}
{% endhighlight %}
调用 list.sorted()方法排序
{% highlight java %}
//sorted 方法返回排序好的list
val sorted = personList.sorted()
sorted.forEach(::println)
//运行结果如下：
----排序后----
Person(name=Mary, age=14)
Person(name=A-Lin, age=12)
Person(name=Jim, age=12)
Person(name=Tom, age=11)
{% endhighlight %}

### --- The End ---