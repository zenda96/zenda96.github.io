---
layout: display
title:  "GitHub + Jekyll 搭建个人blog"
categories: other
digest: "windows上轻松搭建blog"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>
利用一个周末的时间终于磕磕绊绊把自己blog雏形给搭建好了 在此记录一下我搭建的过程  
主要分为以下几个步骤  
1. 安装ruby
2. 安装jekyll
3. 安装bundler
4. 新建jekyll 项目 或者 下载jekyll 主题
5. 启动jekyll 服务 在线预览编辑
6. 上传到特定的github仓库  

## 1.安装ruby
从[官网](https://rubyinstaller.org/downloads/)上下载 ruby 及其开发工具  
![下载示例](../../images/other/ruby-download.png '下载示例')  
选择2.4.4-2后进行下载 得如下安装包    
![安装包](../../images/other/ruby-download-01.png '安装包')  
双击进行安装  安装过程中勾选如下图示例额的选项  之后直接按提示点击下一步
![安装说明](../../images/other/ruby-download-02.png '安装说明')   
安装后，在cmd中输入ruby -v和gem -v来看看是否安装成功，看到版本号就说明成功

## 2.安装jekyll
我们使用gem 安装jekyll 在命令行输入  
`gem install jekyll`  
所有的jekyll的gem依赖包都会被自动安装

## 3.安装bundler
我们使用gem bundler 在命令行输入  
`gem install bundler`  

## 4.新建jekyll 项目 或者 下载jekyll 主题
有两种建立自己blog的方式  
##### 方法一(新建jekyll 项目):  
`jekyll new blog  //blog为你的博客文件名`  
##### 方法二(下载jekyll 主题):  
从[jekyll主题](http://jekyllthemes.org/)上选择你自己喜欢的主题 然后下载到本地文件夹  

## 5.启动jekyll 服务
进入你的blog文件夹 输入 `jekyll serve  //开启服务器，可以按ctrl+c停止`  
Jekyll服务器默认端口是4000，所以打开浏览器输入：http://localhost:4000 就可以看到生成的博客页面。如下是我下载的jekyll主题后启动生成的页面:  
![jekyll 服务页面](../../images/other/jekyll-blog-04.png 'jekyll 服务页面')  

## 6.上传到特定的github仓库 
去自己的github账户上新建一个仓库 创建一个名为username.github.io的项目，我的用户名是zenda96，所以我需要创建 zenda96.github.io 的仓库 因为我之前创建过了 github会有不能重名的提醒 如下:  
![创建仓库](../../images/other/jekyll-blog-05.png '创建仓库')  
创建完成后 将本地的blog与此仓库关联起来 以后就不断的在本地修改预览最后推送  实时更新自己的blog啦

