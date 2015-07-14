---
layout: post
title: Hello world
category: "code"
tags: ["git"]
---

一些Markdown语法的例子：

这是一个段落，前后有一个以上的空行，<a href="#">这是一个链接</a>在段落中。

##这是h2，由2个井号包着##

这是h2下面的内容，这是h2下面的内容。这是h2下面的内容，这是h2下面的内容。这是h2下面的内容，这是h2下面的内容。这是h2下面的内容，这是h2下面的内容。这是h2下面的内容，这是h2下面的内容。这是h2下面的内容，这是h2下面的内容。

### 这是h3，由3个井号包着 ###

这是h3下面的内容；  
这是h3下面的内容；  
这是h3下面的内容。

#### 这是h4，由4个井号包着 ####

#####这是h5，由5个井号包着#####

这是h5下面的内容，_这是em强调，2边由1个下划线或者星号包着_，**这是strong强调，2边由2个下划线或者星号包着**。

	this is <a href="#">code</a>
	this is <span>code</span>
			this is code
		this is code
	this is code
	this is code
	this is code
	this is code

这是一个段落里面有`一块代码`在里面，用反引用包着代码。

{% highlight ruby linenos %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget } format.json { render json: @widget } format.json { render json: @widget }
  end
end
{% endhighlight %}


