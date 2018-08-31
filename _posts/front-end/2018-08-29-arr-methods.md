---
layout: display
title:  "forEach map filter some every 五个数组方法"
categories: front-end
digest: "js几种常见的数组循环方法"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>


forEach() 方法对数组的每一个元素执行一次提供的函数 不能强制中止循环 除非抛出异常
map()     方法创建一个新数组，其结果是该数组都执行一次函数，原函数保持不变
filter()  方法创建一个新数组，使指定函数测试数组的每一个元素，并放回一个通过元素的新数组
some()    方法测试该数组有元素通过了指定函数的测试，如果有返回true，否则，返回false
every()   方法测试该数组是否全部通过指定函数测试，全部通过返回true，否则，返回false 可以强制中止循环

forEach 遍历数组 没有返回值
理论上这个方法是没有返回值的，仅仅是遍历数组中的每一项，不对原来数组进行修改；但是可以自己通过数组的索引来修改原来的数组；
```
  var arr = [1,2,3,4]
  arr.forEach((el,index)=>{
    arr[index] = (el+1)
  })
```

map 创建并返回新数组
map的回调函数中支持return返回值；return的是什么，相当于把数组中的这一项变为什么（并不影响原来的数组，只是相当于把原数组克隆一份，把克隆的这一份的数组中的对应项改变了）
```
  var arr = [1,2,3,4]
  arr.map((el,index)=>{
    return el+1
  })
```

filter 过滤并创建返回新数组 
```
  //返回所有大于10的数组元素
  var arr = [1,2,3,4]
  arr.filter((value)=>{
      return value>10
  })
```

some 返回 true 或者 false
```
  //判断当前数组  是否至少有一个元素  大于10的元素
  var arr = [1,2,3,4]
  arr.some((value)=>{
      return value>10
  })
```

every 返回 true 或者 false
```
  //判断当前数组  是否全部元素  大于10
  var arr = [1,2,3,4]
  arr.every((value)=>{
      return value>10
  })
```


