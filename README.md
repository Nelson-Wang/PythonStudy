# PythonStudy
import re
# pip 包管理工具
'''
13934453290adffsbxfgsgsgjsss
'''
r'''
re.match函数
原型：match(pattern, string, flags=0)
参数：
pattern：匹配的正则表达式
sting：要匹配的字符串
flags：标志位，用于控制正则表达式的匹配方式，值如下
re.I          忽略大小写
re.L          做本地户识别
re.M          多行匹配，影响~和$
re.S          是.匹配包括换行符在内的所有字符
re.U          根据Unicode字符集解析字符，影响\w  \W  \b  \B
re.X          使我们以更灵活的格式理解正则表达式      
功能：尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，返回None
'''
# www.baidu.com
print(re.match("www", "www.baidu.com"))
print(re.match("www", "www.baidu.com").span())
print(re.match("www", "ww.baidu.com"))
print(re.match("www", "baidu.com.www"))
print(re.match("www", "wwW.baidu.com"))
print(re.match("www", "wwW.baidu.com", flags=re.I))
# 扫描整个字符串，返回从起始位置成功的匹配

print("---------------------------------------------")
'''
re.search()函数
原型：search(pattern, string, flags=0)
参数：
pattern：匹配的正则表达式
sting：要匹配的字符串
flags：标志位，用于控制正则表达式的匹配方式
功能：扫描整个字符串，并返回第一个成功的匹配
'''
print(re.search("sunck", "man is sunck! sunck is a good man !"))

print("---------------------------------------------")

'''
re.findall函数
原型：findall(pattern, string, flag=0)
参数：
pattern：匹配的正则表达式
sting：要匹配的字符串
flags：标志位，用于控制正则表达式的匹配方式
功能：扫描整个字符串，并返回结果列表
'''
print(re.findall("sunck", "man is sunck! Sunck is a good man !", flags=re.I))

import re

print("-----------匹配单个字符与数字------------")
r'''
.               匹配除换行符以外的任意一个字符
[0123456789]    []是字符集合，表示匹配方括号中所包含的任意一个字符
[sunck]         匹配's' 'u' 'n' 'c' 'k'中任意一个字符
[a-z]           匹配任意小写字母
[A-Z]           匹配任意大写字母
[0-9]           匹配任意数字，类似[0123456789] 
[0-9a-zA-Z]     匹配任意的数字和字母
[0-9a-zA-Z_]    匹配任意的数字和字母和下划线
[^sunck]        匹配除了sunck这几个字母以外的所有字符，中括号里的^称为脱字符，表示不匹配集合中的字符
[^0-9]          匹配所有的非数字字符
\d              匹配数字，效果同[0-9]
\D              匹配非数字字符，效果同[^0-9]
\w              匹配数字，字母和下划线，效果同[0-9a-zA-Z_]
\W              匹配非数字，字母和下划线，效果同[^0-9a-zA-Z_]
\s              匹配任意的空白符(空格，换行，回车，换页，制表)，效果同[ \f\n\r\t]
\S              匹配非任意的空白符(空格，换行，回车，换页，制表)，效果同[^ \f\n\r\t]
'''
print(re.search(".", "sunck is a good man 6"))
print(re.search("[0123456789]", "sunck is a good man 6"))
print(re.search("[sunck]", "sunck is a good man 6"))
print(re.findall("[^0-9]", "sunck is a good man 6"))
print(re.findall("\d", "sunck is a good man 6"))
print(re.findall("\D", "sunck is a good man 6"))
print(re.findall("\w", "sunck is a good man 6"))
print(re.findall(".", "sunck is a good man\n 6", flags=re.S))

print("-------------锚字符（边界字符）--------------")
r'''
^        行首匹配，和在[]里的^不是一个意思
$        行尾匹配

\A       匹配字符串开始，它和^的区别是，\A只匹配整个字符串的开头，即使在re.M模式下也不会匹配其它行的行首
\Z       匹配字符串结束，它和$的区别是，\Z只匹配整个字符串的结束，即使在re.M模式下也不会匹配其它行的行尾

\b       匹配一个单词的边界，也就是指单词和空格间的位置
         'er\b'可以匹配never，不能匹配nerve
\B       匹配单词的非边界
'''
print(re.search("^sunck", "sunck is a good man"))
print(re.search("man$", "sunck is a good man"))

print(re.findall("^sunck", "sunck is a good man\nsunck is a good man", flags=re.M))
print(re.findall("\Asunck", "sunck is a good man\nsunck is a good man", flags=re.M))
print(re.findall("man$", "sunck is a good man\nsunck is a good man", flags=re.M))
print(re.findall("man\Z", "sunck is a good man\nsunck is a good man", flags=re.M))

print(re.search(r"er\b", "never "))
print(re.search(r"er\b", "nerve"))
print(re.search(r"er\B", "never"))
print(re.search(r"er\B", "nerve"))

print("-------------匹配多个字符--------------")
r'''
说明：下方的x、y、z、n、m均为假设的普通字符，不是正则表达式的元字符
(xyz)      匹配小括号内xyz(作为一个整体去匹配)
x?         匹配0个或者1个x
x*         匹配0个或者任意多个x（.*表示0个或者任意多个字符，换行符除外）
x+         匹配至少一个x
x{n}       匹配确定的n个x(是一个非负整数)
x{n,}      匹配至少n个x
x{n,m}     匹配至少n个最多m个x，注意：n<=m
x|y        |表示或，匹配的是x或y
'''
print(re.findall(r"(sunck)", "sunck is a good sunckman"))
print(re.findall(r"a?", "aaa"))     # 非贪婪匹配（尽可能少的匹配）
print(re.findall(r"a*", "aaabaa"))  # 贪婪匹配（尽可能多的匹配）
print(re.findall(r".*", "aaabaa"))
print(re.findall(r"a+", "aaabaa"))  # 贪婪匹配（尽可能多的匹配）
print(re.findall(r"a{3}", "aaaaabaaa"))
print(re.findall(r"a{3,}", "aaaaabaaa"))
print(re.findall(r"a{3,4}", "aaaaabaaaaaabaa"))
print(re.findall(r"((s|S)unck)", "sunck--Sunck"))


# 需求，提取sunck……man
str = "sunck is a good man!sunck is a nice man!sunck is a very handsome man"
print(re.findall(r"(sunck.*?man)", str))


print("-------------------特殊-----------------")
r'''
*?   +?   x?   最小匹配  通常都是尽可能多的匹配，可以使用这种方法解决贪婪匹配

(?:x)          类似(xyz)，但表示是一个组  

'''

# 注释：/* part1  */     /*  part2  */
print(re.findall(r"//*.*?/*/", r"/* part1  */     /*  part2  */"))
               # 第二个/为了转义*

import re

'''
字符串切割
'''
str1 = "sunck   is a good man"
print(str1.split(" "))
print(re.split(r" +", str1))

'''
re.finditer函数
原型：finditer(pattern, string, flags=0)
参数：
pattern：匹配的正则表达式
sting：要匹配的字符串
flags：标志位，用于控制正则表达式的匹配方式
功能：与findall类似，扫描整个字符串，返回的是一个迭代器
'''
str3 = "sunck is a good man! sunck is a nice man! sunck is a handsome man!"
d = re.finditer("(sunck)", str3)
# 防止数据过大占满内存
while True:
    try:
        l = next(d)
        print(l)
    except StopIteration as e:
        break



'''
字符串的替换和修改
re.sub(pattern, repl, string, count=0, flags=0)
re.subn(pattern, repl, string, count=0, flags=0)

参数：
pattern:正则表达式（规则）
repl:指定的用来替换的字符串
string:目标字符串
count:最多替换次数
flags:标志位，用于控制正则表达式的匹配方式

功能：在目标字符串中以正则表达式的规则匹配字符串，再把他们替换成指定的字符串。可以指定替换的次数，如果不指定，替换所有的
匹配字符串

区别：前者返回一个被替换的字符串，后者返回一个元组，第一个元素被替换的字符串，第二个元素表示被替换的次数
'''
str5 = "sunck is good good good man"
print(re.sub(r"(good)", "nice", str5))
print(type(re.sub(r"(good)", "nice", str5)))

print(re.subn(r"(good)", "nice", str5))
print(type(re.subn(r"(good)", "nice", str5)))



'''
分组：
概念：除了简单的判断是否匹配之外，正则表达式还有提取子串的功能。我们用()表示的就是提取分组

'''
str6 = "010-53247654"
m = re.match(r"(?P<first>\d{3})-(?P<last>\d{8})", str6)
# 使用序号获取对应组的信息，group(0)一直代表原始字符串
# ?P<first> 给分组起名
print(m.group(0))
print(m.group(1))
print(m.group("first"))
print(m.group(2))
print(m.group("last"))
# 查看匹配的各组的情况
print(m.groups())



'''
编译：当我们使用正则表达式时，re模块会干两件事
1、编译正则表达式，如果正则表达式本身不合法，会报错
2、用编译后的正则表达式去匹配对象

compile(pattern , flags=0)
pattern   要编译的正则表达式
'''
pat = r"(^1[3578]\d{9}$)|(^1(47)\d{8}$)"
print(re.match(pat, "13699999949"))
# 编译成正则对象
re_telephone = re.compile(pat)
print(re_telephone.match("13699999949"))


# 模块调用
# 对象调用
# re.match(pattern, string, flags=0)
# re_telephone.match(string)
# re.search(pattern, string, flags=0)
# re_telephone.search(string)
# re.findall(pattern, string, flags=0)
# re_telephone.findall(string)
# re.split(pattern, string, flags=0)
# re_telephone.split(string)
# re.subn(pattern, repl, string, count=0, flags=0)
# re_telephone.subn(repl, string)
