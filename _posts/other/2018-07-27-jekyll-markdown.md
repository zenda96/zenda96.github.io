---
layout: display
title:  "jekyll 里的 markdown 语法"
categories: other
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

# 1.标题

代码:
{% highlight markdown %}
    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题
{% endhighlight %}
效果:
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
# 2.字体
{% highlight markdown %}
*倾斜的字体*
**加粗的字体**
***斜体加粗字体***
~~删除线字体~~
换行符  一行结束后输入两个空格
{% endhighlight %}
效果:  
*倾斜的字体*  
**加粗的字体**  
***斜体加粗字体***  
~~删除线字体~~  
# 3.引用
{% highlight markdown %}
>引用内容1
>>引用内容2
>>>引用内容3
{% endhighlight %}
>引用内容1
>>引用内容2
>>>引用内容3

# 4.分割线
{% highlight markdown %}
---
***
{% endhighlight %}
---
***
# 5.图片
{% highlight markdown %}
![图片alt](图片地址 '图片标题')
![blockchain](https://www.baidu.com/img/bd_logo1.png?where=super "百度logo")
{% endhighlight %}
![blockchain](https://www.baidu.com/img/bd_logo1.png?where=super "百度logo")
# 6.超链接
{% highlight markdown %}
[超链接名称](超链接 '超链接title')
[百度](https://www.baidu.com "百度")
{% endhighlight %}
[百度](https://www.baidu.com "百度")

# 7.列表
{% highlight markdown %}
无序列表用 - + * 任何一种都可以 后面带有空格
- 列表内容
+ 列表内容
* 列表内容
{% endhighlight %}

- 列表内容
1. 列表内容
2. 列表内容
3. 列表内容

# 8.表格
{% highlight markdown %}
第二行 表示对齐方式  ---默认左对齐  :--左对齐 --:右对齐  :-:居中对齐
表头|表头|表头
--- |:--:|:--:
内容|内容|内容
内容|内容|内容
{% endhighlight %}

表头|表头|表头
--- |:--:|:--:
内容|内容|内容
内容|内容|内容
# 9.代码
{% highlight markdown %}
单行代码    `代码内容`

多行代码    ```
           代码内容
           ```
{% endhighlight %}
单行代码    `alert("hello world")`

多行代码    
```
    function a(){
        alert("hello world")
    }
```