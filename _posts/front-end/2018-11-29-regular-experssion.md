---
layout: display
title:  "js的正则表达式"
categories: front-end
digest: "是时候来个总结了"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

### 1.什么是正则表达式 
正则表达式(regular expression)描述了一种字符串匹配的模式，可以用来检查一个字符串是否含有某种子串、将匹配的子串做替换或者从某个字符串中取出符合某个条件的子串等
### 2.正则表达式的创建方式 
- 1.字面量创建方式 
- 2.实例创建方式 

```
    var reg = /pattern/flags
    // 字面量创建方式
    var reg = new RegExp(pattern,flags);
    //实例创建方式
    
    pattern:正则表达式  
    flags:标识(修饰符)
    标识主要包括：
    1. i 忽略大小写匹配
    2. m 多行匹配，即在到达一行文本末尾时还会继续寻常下一行中是否与正则匹配的项
    3. g 全局匹配 模式应用于所有字符串，而非在找到第一个匹配项时停止
```
**字面量创建方式和构造函数创建方式的区别**

- 字面量创建方式不能进行字符串拼接以及使用变量，实例创建方式可以
```
    var regParam = 'cm';
    var reg1 = new RegExp(regParam+'1');
    var reg2 = /regParam/;
    console.log(reg1);  //   /cm1/
    console.log(reg2);  //  /regParam/
```
- 字面量创建方式特殊含义的字符不需要转义，实例创建方式需要转义
```
    var reg1 = new RegExp('\d');  //    /d/ 
    var reg2 = new RegExp('\\d')  //   /\d/
    var reg3 = /\d/;              //  /\d/
```

### 3.正则用到的元字符
```
\d : 0-9之间的任意一个数字  \d只占一个位置
\w : 数字，字母 ，下划线 0-9 a-z A-Z _
\s : 空格或者空白等
\D : 除了\d
\W : 除了\w
\S : 除了\s
 . : 除了\n之外的任意一个字符
 \ : 转义字符
 | : 或者
() : 分组
\n : 匹配换行符
\b : 匹配边界 字符串的开头和结尾 空格的两边都是边界 => 不占用字符串位数
 ^ : 限定开始位置 => 本身不占位置
 $ : 限定结束位置 => 本身不占位置
[a-z] : 任意字母 []中的表示任意一个都可以
[^a-z] : 非字母 []中^代表除了
[abc] : abc三个字母中的任何一个 [^abc]除了这三个字母中的任何一个字符

* : 0到多个
+ : 1到多个
? : 0次或1次 可有可无
{n} : 正好n次；
{n,} : n到多次
{n,m} : n次到m次

```

***特别注意:[ ]中，不会出现两位数***
```
[12]表示1或者2 不过[0-9]这样的表示0到9 [a-z]表示a到z
例如:匹配从18到65年龄段所有的人
var reg = /[18-65]/; // 这样写对么
reg.test('50')
//Uncaught SyntaxError: Invalid regular expression: /[18-65]/:Range out of order in character class
//聪明的你想可能是8-6这里不对，于是改成[16-85]似乎可以匹配16到85的年龄段的，但实际上发现这也是不靠谱的
实际上我们匹配这个18-65年龄段的正则我们要拆开来匹配
我们拆成3部分来匹配 18-19  20-59 60-65 
reg = /(18|19)|([2-5]\d)|(6[0-5])/;
```

##### 分组：
只要正则中出现了小括号那么就会形成一份分组
只要有分组，exec(match)和replace中的结果就会发生改变(后边的正则方法中再说)

##### 分组的引用 :
只要在正则中出现了括号就会形成一个分组，我们可以通过\n (n是数字代表的是第几个分组)来引用这个分组，第一个小分组我们可以用\1来表示

当我们加()只是为了提高优先级而不想捕获小分组时，可以在()中加?:来取消分组的捕获

```
var str = 'aaabbb';
var reg = /(a+)(b+)/;
var res =reg.exec(str);
console.log(res)
// ["aaabbb", "aaa", index: 0, input: "aaabbb", groups: undefined]
//全部捕获

var str = 'aaabbb';
var reg = /(a+)(?:b+)/;
var res =reg.exec(str);
console.log(res)
//["aaabbb", "aaa", "bbb", index: 0, input: "aaabbb", groups: undefined]
//只捕获第一个小分组的内容

```

#### 正则的特性
- 贪婪性
- 所谓的贪婪性就是正则在捕获时，每一次会尽可能多的去捕获符合条件的内容。如果我们想尽可能的少的去捕获符合条件的字符串的话，可以在量词元字符后加?

- 懒惰性
- 懒惰性则是正则在成功捕获一次后不管后边的字符串有没有符合条件的都不再捕获。如果想捕获目标中所有符合条件的字符串的话，我们可以用标识符g来标明是全局捕获

### 4.正则常用的一些方法

- reg.test(str)
- reg.exec(str)
- str.match(reg)
- str.replace(reg)

**reg.test(str) 用来验证字符串是否符合正则 符合返回true 否则返回false**
```
var str = 'abc';
var reg = /\w+/;
console.log(reg.test(str));  //true
```

**reg.exec(str) 用来捕获符合规则的字符串**
```
var str = '2017-01-05';
var reg = /-\d+/g
reg.exec(str)
//["-01", index: 4, input: "2017-01-05", groups: undefined]
exec 受分组的影响
var str = '2017-01-05';
var reg = /-(\d+)/g
reg.exec(str)
// ["-01", "01", index: 4, input: "2017-01-05", groups: undefined]

"-01" : 正则捕获到的内容
"01"  : 捕获到的字符串中的小分组中的内容
```
**exec 的特点是 当我们用exec进行捕获时，如果正则没有加'g'标识符，则exec捕获的每次都是同一个，当正则中有'g'标识符时 ， exec捕获的是下一个**
```
var str = 'abc123cba456aaa789';
var reg = /\d+/g;  //此时加了标识符g
console.log(reg.lastIndex)
// lastIndex : 0 

console.log(reg.exec(str))
//  ["123", index: 3, input: "abc123cba456aaa789"]
console.log(reg.lastIndex)
// lastIndex : 6

console.log(reg.exec(str))
// ["456", index: 9, input: "abc123cba456aaa789"]
console.log(reg.lastIndex)
// lastIndex : 12

console.log(reg.exec(str))
// ["789", index: 15, input: "abc123cba456aaa789"]
console.log(reg.lastIndex)
// lastIndex : 18

console.log(reg.exec(str))
// null
console.log(reg.lastIndex)
// lastIndex : 0

每次调用exec方法时,捕获到的字符串都不相同
lastIndex ：这个属性记录的就是下一次捕获从哪个索引开始。
当未开始捕获时，这个值为0。          
如果当前次捕获结果为null。那么lastIndex的值会被修改为0.下次从头开始捕获。
而且这个lastIndex属性还支持人为赋值
```

**str.match(reg)如果匹配成功，就返回匹配成功的数组，如果匹配不成功，就返回null**
```
//match和exec的用法差不多
var str = 'abc123cba456aaa789';
var reg = /\d+/;
console.log(reg.exec(str));
//["123", index: 3, input: "abc123cba456aaa789"]
console.log(str.match(reg));
//["123", index: 3, input: "abc123cba456aaa789"]
```
当我们进行全局匹配时，二者的不同就会显现出来了
```
var str = 'abc123cba456aaa789';
var reg = /\d+/g;
console.log(reg.exec(str));
// ["123", index: 3, input: "abc123cba456aaa789"]
console.log(str.match(reg));
// ["123", "456", "789"]

当全局匹配时，match方法会一次性把符合匹配条件的字符串全部捕获到数组中,如果想用exec来达到同样的效果需要执行多次exec方法
```

**match和exec都可以受到分组()的影响，不过match只在没有标识符g的情况下才显示小分组的内容，如果有全局g，则match会一次性全部捕获放到数组中**
```
var str = 'abc';
var reg = /(a)(b)(c)/;

console.log( str.match(reg) );
// ["abc", "a", "b", "c", index: 0, input: "abc"]
console.log( reg.exec(str) );
// ["abc", "a", "b", "c", index: 0, input: "abc"]


当有全局g的情况下
var str = 'abc';
var reg = /(a)(b)(c)/g;
console.log( str.match(reg) );
// ["abc"]
console.log( reg.exec(str) );
// ["abc", "a", "b", "c", index: 0, input: "abc"]
```

**str.replace(reg,newStr)字符串替换**  
replace的第二个参数也可以是一个函数 ，需要注意的是，如果我们需要替换replace中正则找到的字符串，函数中需要一个返回值去替换正则捕获的内容

```
var str = 'a111bc222de';
var res = str.replace(/\d/g,'Q')
console.log(res)
// "aQQQbcQQQde"

第二个参数是函数时
reg = /([^?&#+]+)=([^?&#+]+)/g;
str = 'https://www.baidu.com?a=1&b=2'
str.replace(reg,function($0,$1,$2,$3,$4){
            console.log($0,$1,$2,$3,$4)
})

第一个参数是匹配到的内容
之后的参数分别是 匹配到的分组内容
最后的参数是 str

//a=1 a 1 22 https://www.baidu.com?a=1&b=2
//b=2 b 2 26 https://www.baidu.com?a=1&b=2
//"https://www.baidu.com?undefined&undefined"
```

### 零宽断言

用于查找在某些内容(但并不包括这些内容)之前或之后的东西，如\b,^,$那样用于指定一个位置，这个位置应该满足一定的条件(即断言)，因此它们也被称为零宽断言

**在使用正则表达式时，捕获的内容前后必须是特定的内容，而我们又不想捕获这些特定内容的时候，零宽断言就可以派上用场了。**

- 零宽度正预测先行断言 (?=exp)
- 零宽度负预测先行断言 (?!exp)
- 零宽度正回顾后发断言 (?<=exp)
- 零宽度负回顾后发断言 (?<!exp)

**(?=exp) 这个简单理解就是说字符出现的位置的右边必须匹配到exp这个表达式**

```
var str = "i'm singing and dancing";
var reg = /\b(\w+(?=ing\b))/g
var res = str.match(reg);
console.log(res)
// ["sing", "danc"]

注意一点，这里说到的是位置，不是字符。
var str = 'abc';
var reg = /a(?=b)c/;
console.log(res.test(str));  // false

// 这个看起来似乎是正确的，实际上结果是false
reg中a(?=b)匹配字符串'abc' 字符串a的右边是b这个匹配没问题,接下来reg中a(?=b)后边的c匹配字符串时是从字符串
'abc'中a的后边b的前边的这个位置开始匹配的，
这个相当于/ac/匹配'abc',显然结果是false了
```

**(?!exp) 这个就是说字符出现的位置的右边不能是exp这个表达式**
```
var str = 'nodejs';
var reg = /node(?!js)/;
console.log(reg.test(str)) // false
```

**(?<=exp) 这个就是说字符出现的位置的前边是exp这个表达式**
```
var str = '￥998$888';
var reg = /(?<=\$)\d+/;
console.log(reg.exec(str)) //888
```

**(?<!exp) 这个就是说字符出现的位置的前边不能是exp这个表达式**
```
var str = '￥998$888';
var reg = /(?<!\$)\d+/;
console.log(reg.exec(str)) //998
```

来一张思维导图

![正则表达式思维导图]({{"images/work/reg-expression.jpeg"|absolute_url}})




