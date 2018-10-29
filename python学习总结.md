# 中文request异常

```
print(response.text.encode('GBK','ignore').decode('GBk'))
```

# 正则
    s1 = http://konnectapt.com/wp-content/themes/goodnews5/css...
    pattern = re.compile('//(.*?)/')
    datatime = "".join(pattern.findall(s1))
    print(datatime)
# list去重 #
    new = list(set(new))

# 匹配IP #
	matchObj = re.match(r'((25[0-5]|2[0-4]\d|((1\d{2})|([1-9]?\d)))\.){3}(25[0-5]|2[0-4]\d|((1\d{2})|([1-9]?\d)))', url, re.M | re.I)
# 无法update #
1. 查看拼写
2. 设置text格式
3. 元组里内容都为str类型

# 多线程与代理IP #
0911dnstoip

# 获取变量名 #
	获取变量名
	import sys
	def append(list_, name):
		list_.append((name, sys._getframe().f_back.f_locals[name]))
	>>> mylist = []
	>>> myvar = 12
	>>> append(mylist, 'myvar')
	>>> mylist
	[('myvar', 12)]
# python安装whl #
python -m pip install ***.whl

# pip 需要配置系统环境变量，置顶 #