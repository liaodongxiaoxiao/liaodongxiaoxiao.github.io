---
layout: post
title:  Android DialogFragment 用法总结
categories: [Android,DialogFragment]
tags:	[Android Tips]
---
> Android *DialogFragment* 用总结

### 1. 设置不显示默认的Title

{% highlight java %} 
	@Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        //不显示默认title
        Window window = getDialog().getWindow();
        if (window != null) {
            window.requestFeature(Window.FEATURE_NO_TITLE);
        }
        View view = inflater.inflate(R.layout.fragment_setting_auth, container, false);
        ButterKnife.bind(this, view);
        return view;
    }

{% endhighlight %}
### 2.设置Dialog背景透明
{% highlight java %}
	@Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                                 Bundle savedInstanceState) {
         //不显示默认title
         Window window = getDialog().getWindow();
         if (window != null) {
             window.setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));
         }

         return inflater.inflate(R.layout.fragment_user_feedback, container, false);
    }
        
{% endhighlight %}

### 3.设置点击Dialog以外的部分不取消
{% highlight java %}

	@Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {

        //...
        //点击Dialog以外的部分不取消
        getDialog().setCanceledOnTouchOutside(false);
        //...

        return inflater.inflate(R.layout.fragment_user_feedback, container, false);
    }


{% endhighlight %}

### 4.设置DialogFragment关闭时监听事件

#### 4.1 通过实现DialogInterface.OnDismissListener接口

- 自定义AFragment 继承 DialogFragment，重写onDismiss方法 [1](https://stackoverflow.com/questions/23786033/dialogfragment-and-ondismiss)
{% highlight java %}
public class AFragment extends DialogFragment {
    ...

    @Override
    public void onDismiss(final DialogInterface dialog) {
        super.onDismiss(dialog);
        //判断调用该Fragment的Activity实现了DialogInterface.OnDismissListener接口
        if (getActivity() instanceof DialogInterface.OnDismissListener) {
            ((DialogInterface.OnDismissListener) getActivity()).onDismiss(dialog);
        }//若是Fragment调用了本Fragment 
        else if (getParentFragment() instanceof DialogInterface.OnDismissListener) {
            ((DialogInterface.OnDismissListener) getParentFragment()).onDismiss(dialog);
        }
    }
    ...

}
{% endhighlight %}

- 调用AFragment 的Activity或Fragment 实现DialogInterface.OnDismissListener接口

### 4.2 自定义接口，关闭Dialog，向父Activity或Fragment传值

> 思路同 4.1 ，只是做一个扩展

- 自定义接口
{% highlight java %}
public interface DialogCloseListener {
     void handleDialogClose(int tag,String msg);
}
{% endhighlight %}

- 自定义BFragment 继承 DialogFragment，重写onDismiss

{% highlight java %}
...
 @Override
    public void onDismiss(final DialogInterface dialog) {
        super.onDismiss(dialog);
        if (getActivity() instanceof DialogCloseListener) {
            ((DialogCloseListener) getActivity()).handleDialogClose(tag,msg);
        }//若是Fragment调用了本Fragment 
        else if (getParentFragment() instanceof DialogCloseListener) {
            ((DialogCloseListener) getParentFragment()).handleDialogClose(tag,msg);
        }
...
{% endhighlight %}

- 在调用BFragment 的Activity或Fragment 实现DialogCloseListener接口



### the end

