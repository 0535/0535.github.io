---
layout: post
title: Notepad++正则表达式使用规范指导
category: 资源
tags: 正则
keywords: 正则
---

## 规则

| 表达式        | 说明           |
| ------------- |:-------------:|
| `\t`      | 制表符 |
| `\n`      | 新行      |
| `|` | `"ab|bc" 匹配 "ab" 或者 "bc"` |
| `[]` | 匹配任何单个字符 `"[ab]" 匹配 "a" 或者 "b". "[0-9]" 匹配任意数字`      |
| `[^]` | 匹配列表之外的单个字符 `"[^ab]" 匹配 "a" 和 "b" 以外的字符. "[^0-9]" 匹配任意非数字字符`      |
| `.`       | 匹配任意字符      |
| `*` | 匹配任意次(0次，或者多次) `"be*" 匹配 "b", "be" 或者 "bee"`      |
| `+` | 匹配至少一次(1次，或者多次) `"be+" 匹配 "be" 或者 "bee" 但是不匹配 "b"`      |
| `?` | 匹配0次或者1次 `"be?" 匹配 "b" 或者 "be" 但是不匹配 "bee"`      |
| `^` | 匹配行的开始 `"^A" 仅仅匹配以 "A" 开头的行`      |
| `$` | 匹配行的结尾 `"e$" 仅仅匹配以 "e" 结尾的行`      |
| `()` | 用作表达式的分组      |
| `\` | 转义字符 `"\\"匹配"\"`      |


## 案列

**换位**

```
str[11]abc[993]; ----->>>>abc[11]; 
查找串：str\[([0-9]+)\]abc\[([0-9]+)\] 
替换串：abc[\1] 
```

**字符串替换**

```
替换指定内容到行尾:每次遇到“abc”，则替换“abc”以及其后到行尾的内容为“abc efg” 
文本
abc aaaaa 
123 abc 444 
效果
abc efg 
123 abc efg 
查找串“abc.*” 
替换串“abc efg”
```

**数字替换**

```
文本
asdadas123asdasdas456asdasdasd789asdasd 
效果
asdadas[123]asdasdas[456]asdasdasd[789]asdasd 
查找串([0-9]+)
替换串[\1]
```

**每一行行尾的指定字符**

```
12345 1265345 ---->>123456 1265
查找串“345$” 
替换串“”
```

**数据库**

```
上海市---->>INSERT INTO province_info(province_name) VALUES ('上海市');
查找串(.*)
替换串INSERT INTO province_info\(province_name\) VALUES \('\1'\);
```
**英文部分截图**

```
can not be deleted because ---->>无法被deleted因为
查找串can not be ([^ ]*) because 
替换串无法被\1因为 

abandon[2''b9nd2n]v.抛弃，放弃 ---->>”abandon”,”[2''b9nd2n]“,”v.抛弃，放弃”, 
查找串(^[a-zA-Z\-]+)(\[.*\]+)(.*) 
替换串”\1″,”\2″,”\3″, 

<a href="http://xxxx.com/hotels/xi'an-hotel-detail-109312/">Zailushang Apartment Hotel</a>
<a href="http://xxxx.com/hotels/hang zhou-hotel-detail-109312/">Zailushang Apartment Hotel</a>
href中的＂'＂和＂空格＂、 ＂%20＂查找替换成＂-＂
查找目标 : (href=".*)('| |%20)(.*")
替换为(p) : $1-$3 注：跟\1-\3效果一样
```

## 特殊表达式

| 表达式        | 说明           |
| ------------- |:-------------:|
| `(.+)`      | 匹配任何一行内容 |
| `^[ \t]*\n`      | 匹配空行 空行仅包括空格符、制表符、回车符，且必须以这三个符号之一作为一行的开头，并且以回车符结尾 |
| `[\u4e00-\u9fa5]`      | java、C#、JS中匹配中文 |
| `[一-龥]`      | 正常查找到所有的中文字 |
| `[一-龥！-～]`      | 匹配中文 略微有问题 |
| `[！-～]`      | 匹配中文标点符号 |




链接：[正则表达式入门教程](https://deerchao.net/tutorials/regex/regex.htm)

