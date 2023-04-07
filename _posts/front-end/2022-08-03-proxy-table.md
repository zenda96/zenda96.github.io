---
layout: display
title:  "webpack 的 proxyTable 配置"
categories: front-end
digest: "通过设置代理解决跨域问题"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

跨域问题大家在前后端分离的前端开发的过程中肯定都遇到过  
通常有两种方法  
一种是 chrome 浏览器可以设置跨域  
另外一种就是在 webpack 里面设置代理了 更多说明请参考[官方文档](https://webpack.js.org/configuration/dev-server/#devserver-proxy "官方文档") 如下:  
假设我们的后端接口地址为   localhost:3000 我们可以在 config/index.js 里这样设置代理  

{% highlight javascript %}
module.exports = {
    //...
    devServer: {
        proxy: {
        '/api': 'http://localhost:3000'
        }
    }
};
{% endhighlight %}

使用的vue-cli开发 同样提供了 proxyTable 和下面的操作一样  
以`/api/users`开头的请求都会被重新代理到 `http://localhost:3000/api/users`  
如果不想始终传递 /api ，则需要重写路径  

{% highlight javascript %}

module.exports = {
  //...
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        pathRewrite: {'^/api' : ''}
      }
    }
  }
};
{% endhighlight %}


在https上运行并且使用无效证书的后端服务 得如下修改配置:  

{% highlight javascript %}

module.exports = {
  //...
  devServer: {
    proxy: {
      '/api': {
        target: 'https://other-server.example.com',
        secure: false
      }
    }
  }
};
{% endhighlight %}


多个路径代理同一后端地址  
{% highlight javascript %}

module.exports = {
  //...
  devServer: {
    proxy: [{
      context: ['/auth', '/api'],
      target: 'http://localhost:3000',
    }]
  }
};
{% endhighlight %}


