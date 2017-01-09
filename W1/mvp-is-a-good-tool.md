## 转码

由于我自己的锅（其实也没法子甩锅给别人啊！），我直接从github把第一周的weather_info.txt文件下载下来了。但是文件是这样的：

![此处输入图片的描述][1]
好吧，大家肯定看出来了，我下载的是HTML格式的~这个要怎么做呢？比较还是有点阅历的，这个肯定是要用爬虫利器正则表达式来洗稿啊！

问题在于我以前要么让公司的程序员小伙伴帮忙，要么就是去网上找相应的网站进行一些常规的洗稿。不过俗话说“**不要怂，就是干**”！立刻call程序员小伙伴肿么能够最快学会正则表达式。他直接扔了这本书给我。只好花一天时间自学啦！~

![学习正则表达式][2]

不过周日晚上，看了微信群里的聊天记录，我总觉得不对劲。因为居然没人讨论正则表达式，莫非他们都提前掌握了这个技能？这不科学！立刻问一下，果然，我获取文件的方式出了问题。

这个，只能用麦当劳的新品来表达我的心情了：

![此处输入图片的描述][3]

果然是耿教练说的醉点啊！对资料视而不见。好了，我用正确的方式取回了`weather_info.txt`。

不过现在我还是需要把`txt`转码为`dict`。

首先添加了以下这行代码：
```
# -*- coding: utf-8 -*-
```
运行了读取`weather_info.txt`的代码，出现以下错误：
```
#UnicodeDecodeError: 'gbk' codec can't decode byte 0xb4 in position 9: illegal multibyte sequence
```
看来还需要将gbk文件转为utf-8。那么现在问题来了，我要怎么做呢？
很快地，我将问题归纳为“python读取txt显示gbk错误如何解决”。OK，很快地，我就找到了转码的代码了。
```
import codecs
f = codecs.open('weather_info.txt', 'r','utf-8') 
```
看看相应的pydoc解释吧：

> codecs.open(filename, mode='r', encoding=None, errors='strict',buffering=1)
> Open an encoded file using the given mode and return aninstance of StreamReaderWriter, providing transparentencoding/decoding. The default file mode is 'r', meaning to open thefile in read mode.

搞定！可以正常读取啦！不过我又作死了。看看下面的代码：

```
import codecs
f = codecs.open('weather_info.txt', 'r','utf-8') 
f = f.readlines()
# 转码
dict_weather={}
for i in f:
	i = i.split(',')
	dict_weather[i[0]] = i[1]
```
我用`readlines`直接读取了整个文件，结果就是，读取速度很慢！我用肉体都可以感受到3秒的延迟啊。后来，经过@VyGiBe 同学的指点，果断删除了`f = f.readlines()`。完美，prefer！

OK，我们已经完成了第一步，把`weather_info.txt`转化为了`dict_weather`这个字典。

## 输入 help 输出 帮助文本
这是最简单了啦！我要不做个大新闻，用`def`来做吧~

代码如下：
```
def weather_help():
	print("\t 以下为相关操作说明；\n\t 输入城市名，查询该城市的天气；\n\t 输入 help，获取帮助文档；\n\t 输入 history，获取查询记录；\n\t 输入 quit，退出天气查询系统。")
```
以后我只要输入`weather_help()`就可以引用这个模块了。

### 输入 history 输出 查询记录
这个项目，似乎首先有查询记录了才能够test这个部分。好吧，我先跳过。

我会回来的。下一步，进入最主要的功能，查询！！啊，一看，还有5分钟就有别的事情，我做个简单的部分吧。

输入 quit 退出程序。

### 输入 quit 退出程序
这个，用 if……then……就OK啦！
```
elif user_input == "quit":
	print("感谢使用，更多精彩内容欢迎关注我的博客！")
	exit()
```
其实我的博客还没做好，这个我怎么会乱说呢？不过按照这个进度，我肯定可以在这周做出来的，所以，先吹个牛逼。吧~~

### 输入 相关城市 输出 字典中的天气（中等）
好了，最后一部分了。我忽然想到一个问题,如果用户很无聊地输入一个不存在的城市，那么我要如何知道呢？我需要一个预先判断，判断这个键是否存在。

那么我提示了一个问题：python中如何判断某个键在字典中存在？
搜索得到的反馈是以下代码：
```
dict_weather.has_key(in_put)
```
如果存在返回 True，不存在返回 False。

但是运行后就报了以下错误：
> AttributeError: 'dict' object has no attribute 'has_key'

这不科学啊！不存在？？？ARE YOU KID ME?我至少看到好几个回答都这么写的，不可能他们都中奖了吧？回到一手文件看看这么说的。输入`pydoc -m has_key()`，也依旧木有，还给了一些可能的相临解释。看来是真的没有了。

我冷静思考了一下，确定了几个事实：
 1. 这个函数曾经存在过——不如不可能那么多人使用。
 2. 这个函数已经不存在了。

那么结论很明显了：这个函数被移除了。想想上周的PY2 TO PY3，我只是学了一些主要的变化，比如`print`等，是不是还有不主要的变化呢？

> Removed. dict.has_key() – use the in operator instead.

果然，用has_key搜索，找到了。我再改写一下就可以了：
```
elif user_input in dict_weather:
    print(user_input,dict_weather[user_input])
```
测试了一下，果然可以了。那么还有什么被我落下了呢？对了，history。我用清单法，把我之前列的项目过了一遍，接着完成这部分。

### 输入 history 输出 查询记录
一开始我的思路是，建立一个新字典，然后一旦输入history，则print整个字典。让我放弃的原因是我阅读了字典的特性，有两个方面不符合我的需求：
1. 字典是无序的
2. 两个键不能一样，换言之，键是unique的。

那么有序、“键”可以一样，那是什么呢？列表啊！我只要做一个列表，然后每次查询之后的城市写入列表就OK拉！思路有了，那么写代码就简单了。
```
check_history = []
elif user_input == "history":
	for list_history in check_history:
		print(list_history,dict_weather[list_history])
elif user_input in dict_weather:
	check_history.append(user_input)
	print(user_input,dict_weather[user_input])
```
此处还有一个坑，我稍后道来。

## 扫尾工作

### 如果用户胡乱输入怎么办？
这个问题想得到就可以立刻解决了。加一个else，前面全不匹配，来这里打屁屁。
```
else:
	print("你所输入的指令或城市不存在,如需帮助请输入 help ！")
```

### 输入一次后就退出了？
test后发现了这个问题，也是发现了就可以解决的。来个无限循环吧：
```
while True:
	user_input = input("请输入指令或您要查询的城市名：")
	if :
	elif：
	elif：
	else：
```
用`quit`让用户自己退出就可以了。

不过我在这里犯了一个错误，那就是把`check_history = []`写在了while循环里面，导致每一次循环都被重置。还好发现不对后，在每一行加了`print（check_history)`，追踪到了问题。


  [1]: http://ojf2yfe6b.bkt.clouddn.com/bug1.jpg
  [2]: https://img3.doubanio.com/lpic/s26372295.jpg
  [3]: http://img1.lukou.com/static/p/blog/medium/0009/71/54/11/9715411.jpg