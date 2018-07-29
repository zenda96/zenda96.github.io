---
layout: display
title:  "使用 Jekyll 写blog"
categories: other
digest: "编写你的第一篇blog"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

## Jekyll 究竟是什么？([中文文档](https://www.jekyll.com.cn/)|[英文文档](https://jekyllrb.com/docs))
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。

好了  介绍了怎么把我们的blog搭建好以后 我们要开始写第一篇blog了 先来看看blog的目录结构吧~
![目录结构](../../images/other/write-blog-01.png '目录结构')  
来看看这些都有什么用:  

文件/目录    |相关描述
------------|:-----:
_config.yml |保存配置数据
_drafts     |drafts 是未发布的文章
_includes   | _includes里的文件可以被重用  通过 `{\% include footer.html \%}`  来把文件 _includes/footer.html 包含进来
_layouts    | layouts 是要发布的每篇文章外部使用的模板 
_posts      | 发布的文章。文件格式必须要符合: YEAR-MONTH-DAY-title.MARKUP
_data       | 存储网站数据 文件以.yml或者.yaml结束 如 members.yml 通过`site.data.members`即可访问
_site       | Jekyll 完成转换后就会将生成的页面放在这里（默认） 最好将这个目录放进你的 .gitignore 文件中 
index.html  | 网站的入口地址
其他目录     |如 css 还有 images 文件夹 favicon.ico 等文件都将被完全拷贝到生成的 site 中

## 开始编写第一篇文章
这里我们为了分类文章  规范url  我们在 _config.yml 中添加一行代码 `permalink: /:categories/:title` 这样我们每发布的一篇文章就会按照`/文章分类/文章标题` 的形式生成对应的url  
进入_posts目录 按照命名格式 新建文件 2018-07-27-jekyll-markdown.md
![新建post文件](../../images/other/write-blog-02.png '新建post文件')  
正是头信息开始让 Jekyll 变的很酷。任何只要包含 YAML 头信息的文件在 Jekyll 中都能被当做一个特殊的文件来处理。头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。下面是一个基本的例子:
```
    ---
    layout: post  //选择一个合适的布局
    title: Blogging Like a Hacker  // 文章名字
    ---
```
执行`jekyll build``jekyll server`
之后就可以用markdown语法编写文章正文内容咯  
访问 `http://localhost:4000/other/jekyll-markdown`进行本地开发预览

## Jekyll 中可以用到的变量

#### 全局(Global)变量  

变量       |描述
---------   |:--:
site      |来自_config.yml文件，全站范围的信息 + 配置  
page      |页面专属的信息 + YAML 头文件信息 通过 YAML 头文件自定义的信息都可以在这里被获取
content   |被 layout 包裹的 Post 或者 Page 渲染生成的内容 并且没定义在 Post 或者 Page 文件中的变量
paginator |在_config.yml文件中 paginate 配置选项被设置了的时候  这个变量就可用了

#### 全站(site)变量

变量       |描述
---       |:--:
site.time |当前时间  
site.pages|所有 Pages 的清单
site.posts|一个按照时间倒叙的所有 Posts 的清单
site.related_posts |如果当前被处理的页面是一个 Post，这个变量就会包含最多10个相关的 Post
site.categories.CATEGORY |所有的在 CATEGORY 类别下的帖子
site.tags.TAG | 所有的在 TAG 标签下的帖子
site.[CONFIGURATION_DATA] | 所有的通过命令行和 _config.yml 设置的变量都会存到 site 如果你设置了 url: http://mysite.com  这个变量就被存储在了 site.url 

#### 页面(page)变量

变量       |描述
---       |:--:
page.content|页面内容的源码
page.title|页面的标题
page.excerpt|页面摘要的源码
page.url|帖子以斜线打头的相对路径  如 /2008/12/14/my-post.html
page.date|帖子的日期
page.id|帖子的唯一标识码 在RSS源里非常有用
page.categories|所属的 Categories  能在 YAML 头文件信息 中被设置
page.tags|所有 tags  Tags 是在YAML 头文件信息中被定义的
page.path|Post 或者 Page 的源文件地址 可以在 YAML 头文件信息 中被改写

#### 分页器(Paginator)

变量       |描述
---       |:--:
paginator.per_page|每一页Posts的数量
paginator.posts|这一页可用的Posts
paginator.total_posts|Posts 的总数
paginator.total_pages|Pages 的总数
paginator.page|当前页号
paginator.previous_page|前一页的页号
paginator.previous_page_path|前一页的地址
paginator.next_page|下一页的页号
paginator.next_page_path|下一页的地址
