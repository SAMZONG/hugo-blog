---
title: Python 基础
tags: 
    - Python
categories: 
    - Python
abbrlink: 26724
date: 2016-11-11 00:32:13
---

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/><meta name="exporter-version" content="Evernote Mac 6.10 (454269)"/><meta name="author" content="Alex LU"/><meta name="created" content="2016-09-29 02:27:16 +0000"/><meta name="source" content="desktop.mac"/><meta name="updated" content="2016-09-29 06:27:40 +0000"/><title>Python学习笔记(1) --Python基础</title></head><body>
<ol>
<li>输出： print
<ol>
<li>python2：print 'Hello Python'</li>
<li>python3: print(‘Hello Python')</li>
<li>python(‘10+20=‘,10+20)</li>
</ol>
</li>
<li>输入：
<ol>
<li>python2：raw_input()</li>
<li>python3: input()</li>
</ol>
</li>
<li>python的语法比较简单，采用缩进的方式：</li>
</ol>
<div style="-en-codeblock: true; box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-top-left-radius: 4px; border-top-right-radius: 4px; border-bottom-right-radius: 4px; border-bottom-left-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.14902); background-position: initial initial; background-repeat: initial initial;">
<div>a = 100</div>
<div>if a &gt;= 0:</div>
<div>     print(a)</div>
<div>else:</div>
<div>     print(-a)</div>
<div><br/></div>
<div>&amp; diff &amp;</div>
<div>a = 100</div>
<div>if a &gt;=0:</div>
<div>print(a)</div>
<div>else:</div>
<div>print(-a)</div>
</div>
<ol start="4">
<li># 开头为注释；: 结尾，缩进的语句视为代码块；Python大小写是敏感的，约定俗成：4个空格的缩进，可以吧tab设置为4个空格。</li>
<li>Python 的数据类型
<ol>
<li>整数：python可以处理任意大小的整数</li>
<li>浮点数：也就是小数，之所以称之为浮点数，因为按照科学计数法表示时，一个浮点数的小数点位置是可变的</li>
<li>字符串：字符串是以’’和”” 包括起来的任意文本，例如’abc’,”xyz”；如果字符内部同时包含’和”，可以使用\转义字符来标识。
<ol>
<li>如果字符串内部有很多换行，用\n不好阅读，python支持使用’’’…’’' 的格式表示多行‘</li>
<li>r’…'  python可以使用r’’表示’'以内的字符不转义;多行: r’’’…’''</li>
</ol>
</li>
<li>布尔值：布尔值和布尔代数表示的完全一致，一个布尔值只有True和False，python支持直接使用True和False表示布尔值，注意大小写，另外最好不要生命变量时使用True等，布尔值，经常用于在条件判断之中。
<ol>
<li>and : 与运算，所有运算结果都是True，and的结果才是True</li>
<li>or：或运算，只有1个运算结果为True，or的结果就是True</li>
<li>not：他是一个单目运算符，取相反的值</li>
</ol>
</li>
<li>空值：python里的一个特殊值，用None表示，注意None不能理解为0，因为0是有意义的，而None是一个特殊的空值</li>
</ol>
</li>
<li>python的变量
<ol>
<li>命名规则：必须是大小写英文，数字和_的组合，且不能用数字开头；</li>
<li>赋值符号：’=’；等于的符号是’==’</li>
<li>动态语言：变量本身类型不固定的语言称之为动态语言，反之是静态语言，静态语言在定义变量时必须制定变量的数据类型，如果赋值的时候类型不匹配，就会报错；</li>
<li>变量在计算机内存中的表示：a=1,指的是python在内存中创建了整数1，然后在内存创建了变量a，并把它指向了整数1</li>
</ol>
</li>
<li>python的常量
<ol>
<li>定义：常量就是不能改变的变量，在python中，通常使用全部大写的变量名表示常量</li>
<li>整数的除法是精确的，因为除法计算结果是浮点数，例如 9/3 结果为3.0 ; 另外一种除法是’//‘ 地板除，两个整数的除法任然是整数；余数运算’%’</li>
</ol>
</li>
<li>字符编码：字符串是一种数据类型，但是字符串还涉及到一个编码问题，Python3的字符串是支持多语言的
<ol>
<li>ord(‘')函数 获取字符的整数表示；</li>
<li>chr(‘')函数 把编码转换成对应的字符；</li>
<li>python的字符串类型是str，在内存中以Unicode表示，一个字符对应若干字节，但是如果要在网络传输或者保存到磁盘，就要把str转化为单位的bytes；
<ol>
<li>python对于bytes的数据类型用带b前缀的单引号或双引号表示：</li>
<li>另外，Unicode表示的str可用encode()函数，指定编码为bytes。 ‘ABC’ .encode(‘utf-8')</li>
<li>decode() 可以吧bytes转变为str。b'ABC' .decode('ascii')</li>
<li>要计算str包含了多少个字符使用 len()函数： len(‘hello’) ,结果为5</li>
</ol>
</li>
<li style="-en-codeblock: true; box-sizing: border-box; padding: 8px; font-family: Monaco, Menlo, Consolas, &quot;Courier New&quot;, monospace; font-size: 12px; color: rgb(51, 51, 51); border-top-left-radius: 4px; border-top-right-radius: 4px; border-bottom-right-radius: 4px; border-bottom-left-radius: 4px; background-color: rgb(251, 250, 248); border: 1px solid rgba(0, 0, 0, 0.14902); background-position: initial initial; background-repeat: initial initial;">#!/usr/bin/env python3<br/>
# -*- coding: utf-8 -*-</li>
</ol>
</li>
<li>格式化： 如何处理格式化输出字符串，在python中使用的格式化方式和C语言是一致的，用’%’实现：
<ol>
<li>%d 表示整数</li>
<li>%f 表示浮点数</li>
<li>%s 表示字符串，如果不确定用什么，用%s，它会把任何数据类型转换为字符串</li>
<li>%x 表示十六进制整数</li>
<li>%% 表示一个普通的%</li>
</ol>
</li>
<li>数据类型list和tuple
<ol>
<li>list是python内置的一种数据类型：列表，list是一个有序的集合，可以随时添加和删除其中元素。
<ol>
<li>classmates = [‘Michael’,’Bob’,’Tracy’]， 可以用len()函数获取这个list的元素的个数</li>
<li>可以用索引来访问list中的每一个位置的元素，记住索引的第一个位置是0：</li>
<li>当索引超出范围的时候，python会报出IndexError错误，记得最后一个索引是len(classmates) -1</li>
<li>如果直接取出最后一个索引可用classmates[-1],以此类推</li>
</ol>
</li>
<li>list是一个可变的有序列表，所以可以去追加，插入指定位置，删除，替换等操作，支持不同数据类型，支持嵌套list
<ol>
<li>追加: classmates.append(‘Adam')</li>
<li>插入指定位置: classmates.insert(2,’Jack')</li>
<li>删除list末尾的元素： classmates.pop()</li>
<li>删除指定位置的元素: classmates.pop(1)</li>
<li>替换元素：classmates[1]=‘Sarch’ ， 直接给相应位置的元素重新赋值即可</li>
<li>list的元素支持不同的数据类型, L = [‘abc’,23,23.4]</li>
<li>list的元素支持嵌套另外一个list： s = [‘abc',123,[‘XYZ’,2.34]]，注意这个时候len(s)的元素是3个</li>
<li>list也可以没有元素，就是一个空的list，它的长度为0</li>
</ol>
</li>
<li>tuple：元组，也是一种有序列表，但是tuple一旦初始化就不能修改，他没有append()也没有insert()，这样的方法，其他获取元素的方式和list一样，也不能赋值成为另外的元素：
<ol>
<li>classmates = (‘Michael’,’Bob’,’Tracy’) 注意list用的是’[]’，而tuple用的是’()’</li>
<li>tuple 有个问题，当你定义1个元素的时候，tuple的()和数学公式中的小括号混淆 ，因此python规定，这种情况下面，当定义只有1个tuple时必须增加一个逗号’,’来消除歧义。</li>
<li>tuple的元素也可以为list或者tuple，tuple的元素不会改变，但是list是一个可以改变的有序数列，所以当tuple中包含list时，这个tuple是’可变的'</li>
</ol>
</li>
<li>取出特定元素： L[[‘Apple’,’Google’,’Microsoft’],[‘Java’,’Python’,’C’]] ; L[1][1] = ‘Python'</li>
</ol>
</li>
<li>条件判断
<ol>
<li>if：根据python的缩进规则，如果if语句的判断是True，就会执行下面的语句，否则什么都不做</li>
<li>else：也可以个if添加else，意思就是，如果if的判断是false，不要执行if的内容，执行else的内容</li>
<li>elif：如果要嵌套多级判断条件的话，使用elif，elif 是else if的缩写</li>
<li>if语句执行有个特点，它是自上而下的判断，如果某个判断的结果是True，那么执行该判断对应的语句，就会忽略掉剩下的所有elif和else，if判断条件还可以简写: if x: 只要x是非零数值、非空字符串、非空list等，就判断为True，</li>
</ol>
</li>
<li>iput(): 需要注意的地方，默认input的返回类型是str，由于str不能直接整数比较，所以在碰到明明输入200，但是不能和201对比时，记住先要把str转化为整数，python提供了int()函数, 转化数据类型为int类型，但是如果输入’abc’则会得到1个ValueError的错误</li>
<li>循环
<ol>
<li>for…in ： 依次把list或者tuple的每个元素迭代出来，for x in … ：循环就是把每个元素带入变量x，然后执行缩进的语句：</li>
<li>range()函数：用来生成一个整数序列，再通过list()函数转换为list，例如range(5)生成：0,1,2,3,4
<ol>
<li>list(range(5)) = [0,1,2,3,4]</li>
<li>计算1+...+100的结果： for x in range(101): sum = sum +x</li>
</ol>
</li>
<li>while 循环： 只要条件满足，就不断循环，条件不足时退出循环：
<ol>
<li>计算100以内所有奇数之和： sum = 0,n = 99, while n &gt; 0: sum =sum +n; n = n-2</li>
</ol>
</li>
<li>break: 在循环中，break语句可以提前退出循环，当程序执行满足break条件的时候，就会退出循环</li>
<li>continue: 在循环过程中，也可以通过continue语句，跳过当前的这次循环。</li>
<li>注意：循环是让计算机做重复任务的有效方法，break语句可以在循环过程总直接退出循环，continue语句可以提前结束本轮循环，并直接进入下一轮循环，这两个语句通常必须配合if语句使用，但是尽量不要滥用这两个语句，因为当break和continue使用过多会导致代码执行逻辑分支过多，容易出错。</li>
</ol>
</li>
<li>dict和set
<ol>
<li>dict： python内置了字典：dict的支持，全称：dictionary，在其他语言中也称之为map，使用键值存储，具有极快的查找速度。</li>
<li>对比list处理方式：会过滤整个list的元素，这导致list越长，耗时越长；dict实现时，只需要创建key-values对应表，直接根据名字查找，无论这个表有多大，查找速度都不会变慢，但是内存消耗会大，典型用性能(内存空间)换时间。</li>
<li>dict的初始化: d {‘Michael’:95,’Bob’:75,’Tracy’:85}  # 注意dict使用的是大括号’{}‘</li>
<li>dict的数据插入： d [‘Adam’] = 67 </li>
<li>由于dict是根据key检索，所以key是固定的，一个key只能对应1个value,所以当对1个key多次放入value时，后面的值会把前面的值冲掉： （类似变量）</li>
<li>但是如果查询的key不存在,dict会报错，KeyError，可以用in 判断key是否存在: ‘key’ in d  : True/False</li>
<li>通过dict的get方法，如果key不存在，可以返回None，或者自己指定的值，d.get(‘Key’) , d.get(‘key’,-1)</li>
<li>d.pop('key’): 删除1个key，注意当key被删除是，相应的value也会被删除。</li>
<li>另外注意：dict内部存放的顺序和key放入的顺序是没有关系的：</li>
<li>dict应在需要高速查找的地方，正确使用dict非常重要，要牢记1点，dict的key必须是不可变的对象，因为dict是根据key来计算value的位置，如果每次计算相同的key得到的结果不一样，那么dict内部就完全混乱了，这个通过key计算位置的算法称之为Hash算法。</li>
<li>要保证hash的准确性，作为key的对象就不能改变，在python中，字符串·整数等都是不可变的，但是list是可以变的所以不能作为key</li>
<li>set： set和dict类似，也是一组key的集合，但是不存储value，由于key不能重复，所以，在set中，没有重复的key值。</li>
<li>要创建一个set，需要提供一个list作为输入集合。 s = set([1,2,3])   : s = {1,2,3}</li>
<li>注意set也不是有序的，而且重复在set存在的元素会被自动过滤： s = set([1,2,3,1,2,3,1,2,3])  s = {1,2,3}</li>
<li>通过s.add(key) 可以增加元素到set中，可以重复添加，但是不会有效果</li>
<li>通过s.remove(key) 可以删除元素</li>
<li>set 可以看成数学意义上的无序和无重复元素的集合，因此两个set可以做数学意义上的交集、并集能操作：
<ol>
<li>s1 = set([1,2,3]), s2 = set([2,3,4]) ,交集： s1 &amp; s2 = {2,3} ; s1 | s2 = {1,2,3,4}</li>
</ol>
</li>
<li>set和dict的区别仅在于有没有存储对应的value，但是set和dict的原理是一样的，所以，同样不可以放置可变对象，因为无法判断两个对象是否相等，也就无法保证set内部的不会重复元素</li>
<li>不可变对象：str是不变对象，list是可变对象；对于可变对象，例如list，对list进行操作，list的内部会发生变化</li>
<li>a = ‘abc’ , a.replace(‘a’,’A’) # 这个操作是把所有小写的a替换成大写的A，但是注意a的值并没有发生改变，要牢记a是变量，’abc'才是字符对象。</li>
</ol>
</li>
</ol>
</body>
</html>
