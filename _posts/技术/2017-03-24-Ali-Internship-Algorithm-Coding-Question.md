---
layout: post
title: 某次实习阿里算法工程师在线笔试解析
category: 技术
tags: 编程
keywords:
description:
---

### 1. 题目介绍（大致记忆）
输入一组数字，要求每个数字只能够进行前向或者后向的翻转，这组数字之间可以改变顺序，保证最后组合的输出数字最大。（只能凭记忆记住这么多内容😢）

输入数字使用空格进行区分，例如输入是“123 43 9 76 1341”，其中的数字“123”可以翻转为“321”；

最后输出结果为：“976433211431”。

要求不能使用系统的sys库。

>另外还有一些性能的要求，不记得了。。。

### 2. Python 代码

在本次答题中，要求时间是40分钟。

由于紧张情绪，而且不知道后面还有没有题目，没有认真审题就开始草草来答了，最后的还是fail了，比较可惜。

后续重新收拾心情，整理思路，最后使用了一点小技巧，使用python自带的sort()排序方法进行排序。

完整Python代码如下，解决问题的思路在代码的备注中进行了介绍：

```
# -*- coding: utf8 -*-
# --Author:littleroach110--

# input_number 用于记录从键盘的输入
# number_list 用于将input_number按照空格进行拆分到列表
input_number = raw_input("Please input number separate by space:\n")
number_list = input_number.split()

# 用于记录将输入的字符，按照高位到地位，存入到二维列表changed_number中
changed_number = []

for each_number in number_list:
    # number_split 用于临时存储，按照高位到地位拆分的数字
    number_split = []
    each_number = int(each_number)

    # 拆分过程
    while each_number:
        number_split.append(each_number%10)
        each_number = each_number/10

    # 判断是否将一个长数字串进行翻转
    # 确定字符串长度，将最高位和最低位进行比较
    # 如果比较的两位数字相等，则以此向内侧数字靠近，进行比较
    # 通过flag进行循环判断
    number_len = len(number_split)
    half_len = number_len / 2
    flag = 1
    start_num = 0
    end_num = number_len-1

    while flag and half_len:
        if(number_split[start_num] > number_split[end_num]):
            flag = 0

        elif(number_split[start_num] < number_split[end_num]):
            number_split.reverse()
            flag = 0

        else:
            half_len = half_len - 1
            start_num = start_num + 1
            end_num = end_num - 1

    changed_number.append(number_split)

# 使用系统自带的sort()命令，对存储的切分、单项切分数字串已排序的列表，进行排序
# 默认的sort()命令，会依次比较二维列表的 第一位、第二位数据的大小，进行排序
# 用于不能使用调用sys资源以及使用系统命令，即不能使用sys.stdout.write('.')来控制输出
# 正常print输出，会产生换行或者空格，则使用新建字符串的方法，现将数字保存在字符串中，最后一起输出
changed_number.sort()
number_string = ''

for number_str in changed_number[::-1]:
    for number in number_str:
        number_string = number_string + str(number)

print number_string
```

运行结果如下：

```
C:\Python27\python.exe F:/*****/img_handle/ali.py
Please input number separate by space:
21312314 4234123 3554234 63 65634 254234 12341 4342 63411 4134
65634634116343424324553432452431442341234132131214321
```

### 3. 经验总结

* 在线笔试，还是需要多积累点经验，不能怯场；

* Python自带的sort()库很好用，后续需要通读sort()源代码，届时会重新写一篇文章，介绍sort()源代码

* 把数字拆分成数字列表的方法，比较好用，用于后续的组合分析