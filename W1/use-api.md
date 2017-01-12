# 加强难度：用API实时查询天气

## 为什么我不可以？

`20170111` 晚上，在PY103的微信群，我们的bug达人liumang同学发现了开智网页端的一个封面bug，W2 or W3的任务是把这个命令行实时化，变成一个可用的真·天气查询系统。

看到这里，我就一直有个想法，为什么现在的我做不到呢？为什么不试试看呢？就算做不出来又如何？

Just do IT吧！就这么干了吧！

还是老思路，分解任务，然后开动！

## update weather代码

原来的代码需要重构一下了，看看哪些可以用的。

`help`模块，保留！

`quit`模块，保留！

`check`模块，肯定要重写！

这个模块的主要问题在于我要实现2个步奏：

1. 从网上下载数据

2. 把数据整理成我需要的格式

`history`模块，这个估计会最头痛，花的时间最多。因为写第一版的时候，怎么方便怎么来，所以需要完全重写。

这个模块我给自己提了几个要求，按照以下格式来进行：

|    时间    | 地点   |  py天气  |
| --------   | -----:  | :----:  |
| 2017-01-12   | 北京 |   晴     |

如果这样子的话，意味着一个查询需要3个元素。原来的list格式已经不适用了，我需要用dict格式。

好了，大致清楚了，开工吧。

## 第三方模块 requests

首先我需要一个下载url response的第三方库。

研究了一下，从`urllib` 和 `requests` 两个第三方库中选择了 `requests`，或许唯一的原因是官方文档写得很中二，可读性很强。
以下是官方文档的地址，大家感受一下中二魂吧！

[requests官方文档][1]
这个官方文档我喜欢！

我预先装了一个超级大的第三方库集合，如果没有安装这个库的，可以按以下步奏安装：

```
pip install requests
```

## API的选择之随机

随机选了心知天气的API，需要注册，免费版送每天4000次的基础查询，对我来说足够了。

先看一下官方文档：[心知天气API文档][2]

这里有一个概念，API KEY。意思是用来验证API请求合法性的一个唯一字符串，通过API请求中的key参数传入。

用人话说就是一个钥匙，你有这个钥匙才给你返回数据。这里给了一个范例：

```
https://api.thinkpage.cn/v3/weather/now.json?key=fgw2indvrjndyky3&location=beijing&language=zh-Hans&unit=c
```

key的意思是我们的合法性字符串，注册后就查得到了，fqw这一大串就是我的合法性字符串了。

location是查询地点，可以用中文也可以用英文，这个是我们的用户需要输入的。

language是指语言选项，默认中文；unit指的是温度采用摄氏度还是华氏度，默认摄氏度。这两个默认的可以不管，不加入参数，那么只有1个是用户需要输入的，那就是查询地点。

这时候我看了requests的官方文档，发现这么一个功能：

> 你也许经常想为 URL 的查询字符串(query string)传递某种数据。如果你是手工构建 URL，那么数据会以键/值对的形式置于 URL 中，跟在一个问号的后面。例如， `httpbin.org/get?key=val`。 Requests 允许你使用`params`关键字参数，以一个字典来提供这些参数。举例来说，如果你想传递`key1=value1`和 `key2=value2`到`httpbin.org/get`，那么你可以使用如下代码：
```
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.get("http://httpbin.org/get", params=payload)
```

简单来说我可以构建一个字典，然后从字典读取我需要的关键字。那么我需要构建这么一个字典：
{’key':'我的密钥’;'lacation':'用户输入'}
OK，我决定把这段命名为’check_date'。

## 开搞
现在我有了`check_date`这个字典了，我用一个很简单的方法来构建这个字典：

```
check_date['key'] = '巴拉巴拉我的那串密钥'
user_input = input("请输入指令或您要查询的城市名：")
check_date['location'] = user_input
```

之所以使用user_input这个变量，是为了方便我在if中和`help`、`quit`等做比对。

另外，`requests.get`返回的是一个多格式文件，我在这里踩了一个坑：
```
{"results":[{"location":{"id":"WX4FBXXFKE4F","name":"北京","country":"CN","path":"北京,北京,中国","timezone":"Asia/Shanghai","timezone_offset":"+08:00"},"now":{"text":"晴","code":"0","temperature":"3"},"last_update":"2017-01-12T11:40:00+08:00"}]}
```
我一开始认为是dict文件，按dict写了半天，后来用`print(type())`查了一下才知道不是，这是一种多格式文本，你可以用它来构建json、str等等格式。
如果你print这个变量，会出现以下结果：
```
<response:200>
```
查询了一下，这个编码代表返回成功。那么再一想，这个可以用来验证城市是否存在啊！于是就开写了：
```
elif weather_now.status_code == 200 :
		user_input_city()
		# 如果查询有正确返回，则进入处理模块
```
## 处理数据

在处理模块，我把返回的文件转了`str`格式，然后用`split`切片。
```
def user_input_city():
	m = weather_now.text
	m = m.split("\"")
	print(time_now,m[11],m[33])
	# 返回查询结果
	check_history[len(check_history) + 1] = [time_now,m[11],m[33]]
	# 写入历史字典
# 这个模块用于数据处理并返回处理结果和写入历史文件
```
这部分写得极为不优雅，主要是因为我一开始用的是以下代码
```
def user_input_city():
	weather_now = weather_now.text
	weather_now = m.split("\"")
	print(time_now,weather_now[11],weather_now[33])
	check_history[len(check_history) + 1] = [time_now,weather_now[11],weather_now[33]]
# 这个模块用于数据处理并返回处理结果和写入历史文件
```
由于局部变量和全局变量名称一致，导致报错。这里留一个疑问期待以后解决，那就是变量的命名问题，我现在感觉自己的命名过于随意化了。出了报错后，我把局部变量的`weater_now`都改成了`m`。

另一个残留问题是，我知道一个list的value，如何去查找它的序列号，也就是反差。这个部分我先搁置，后面有了方法再补充。我这次是直接用人手数的，很不优雅。

PS：做梦的时候想到的方法，那就是把list用for……in……转为dict，然后通过字典互换的形式实现，唯一的问题是字典的key必须唯一，如果list中有2个或以上的相同value如何处理。

## 历史记录查询
 ```
 	elif user_input == "history":
		k=len(check_history)
		if k == 0:
			print("无查询记录")
		# 字典key数量为0，则返回查无记录
		else:
			print(k)
			for number in range(k):
				number2 = check_history[number+1]
				print(number2[0],number2[1],number2[2])
		#字典key数量为1或以上，则输出查询结果
```

这部分其实很简单了，只要有一个思路，很快就可以搞定了。

运行了一下，正常，OK，撒花，收工。历时3小时。

## 个人体悟

### 不要怂，就是干

出现第一个`优化我的程序使之可以实时查询`时，我的第一个想法是，我做不到。

因为这个超纲了，这个依旧是学生时代做作业的态度啊！就像大妈说的，3个月内你可以提问，3个月后你怎么办？何况我学python不就是为了数据处理吗？那么我有什么理由一定要等任务出来呢？顶多做不出来，又不丢人。

那么不要怂，之后就是干。何况我把任务分解了，进一分有进一分的欢喜啊！

### 睡前思考

果然大科学家说梦中好杀人是真的。

睡前思考，起来了干。这次模式我喜欢。而且梦中还真的解决了一些问题呢。比如用dict给list排序。比我之前的手数强多了。

### 完成第一
这次用了许多取巧的办法，估计代码可读性也不是很强。有些要自己写注释才看得懂，太囧了。不过至少完成了目标，接下来才是优化。巴菲特有一句话我很喜欢：

> 跑第一的前提是你跑完全程！

但跑完全程的前提是你报名比赛了！所以，我先完成报名比赛（完成我的程序，之后再做优化（快速迭代）。


  [1]: http://cn.python-requests.org/zh_CN/latest/
  [2]: http://www.thinkpage.cn/doc


