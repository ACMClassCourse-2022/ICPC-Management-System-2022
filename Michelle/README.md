# Michelle的学生会工作

[评测地址](https://acm.sjtu.edu.cn/OnlineJudge/problem?problem_id=1346)

## 1 背景

`Michelle`接到了花咲川学生会的协助请求，想要她帮忙写一个程序管理学生的信息。但她还有`Hello, Happy World`新曲的编曲没有完成，实在是没有时间了。你能帮帮她吗？

## 2 题目目的

本题目为`ICPC Management System`的前置作业，意在确保大家掌握结构体与部分`STL`容器的基本操作。

## 3 任务描述

在这个任务中，你需要实现一个管理系统，通过控制台输入对学生信息进行维护。

题目保证：

* 输入格式合法
* 在开始统计前只会出现`ADD`操作
* `START`操作仅出现一次

具体需要实现以下操作。

### 添加学生

```
ADD <name> <gender> <class> <score0> ... <score8>
```

向系统中添加一名学生。学生有 12 个参数，`name`、`gender`、`class`与 9 个成绩。

`name`为长度不超过 30 的字符串，由数字、大小写字母与下划线组成；`gender`为一个字母，`M`代表男性，`F`代表女性；`class`为一个整数，1<=`class`<=20；`<scorei>`为课程代号为`i`的课程的分数（一个整数），0\<=`scorei`<=100, 0<=`i`<=8。

开始统计后不能再添加学生。若已经开始统计，输出`[Error]Cannot add student now.`；若未开始统计但学生名字重复输出`[Error]Add failed.`。

本题中，添加失败只有一种情况，即学生名字重复。

### 开始统计

```
START
```

开始进行学生的成绩统计。在开始统计时，榜单应该按照顺序排列。

### 更新成绩

```
UPDATE <name> <code> <score>
```

更新学生`<name>`课程代号为`<code>`的分数为`<score>`。0<=`score`<=100，0<=`code`<=8。

若学生不存在输出`[Error]Update failed.`。

### 刷新榜单

```
FLUSH
```

刷新榜单。**注意更改学生成绩但未刷新榜单时榜单的排名不会变化**（但数据可能变化）。

### 输出榜单

```
PRINTLIST 
```

输出共 N（学生总数）行，每行以

```
<rank> <name> <gender> <class> <avg_score>
```

的格式输出，其中`rank`为`1-based`，`gender`男性输出`male`，女性输出`female`；`avg_score`为该学生所有分数的平均值，向下取整。

学生的排名由平均成绩（即`avg_score`，注意为向下取整的平均成绩）决定，平均成绩高者靠前；平均成绩相同时从 0 到 8 分别比较成绩，成绩高者靠前；依旧平局时，比较学生名字的字典序，字典序较小者靠前。

### 查询学生排名

```
QUERY <name>
```

若学生存在，以

```
STUDENT <name> NOW AT RANKING <ranking>
```

的格式输出学生的排名，`1-based`。否则，输出`[Error]Query failed.`。

### 退出程序

```
END
```

结束程序。

## 4 数据范围

学生总数为`n`，操作次数为`opt`。

对于60%数据，`n`<=100，`opt`<=3,000。​​

对于100%数据，`n`<=10,000，`opt`<=300,000​。​

## 5 提示

在这道题目中，你应该使用一个`struct`去保存所有学生的信息，并使用一个`string`到该结构体的`map`来维护学生的信息；同时，你需要使用`set`维护一个排行榜，排序标准为学生的成绩。

`map`与`set`的相关接口可以在`cpp reference`上学习。

本目录下的`data`文件夹即`Online Judge`上的测试数据点。

在`START`之后，各个指令出现的频率大致如下：

* `UPDATE` 45%
* `QUERY` 45%
* `ADD` 5%
* `FLUSH` 4.9%
* `PRINTLIST` 0.1%

如果你遇到`Time Limit Exceed`的问题，可以考虑以下两个解决方案：

* 将`map`换成`unordered_map`。这两个容器在接口上十分相似，且均实现了映射的功能，但`unordered_map`的性能较好。（相应的，`unordered_map`牺牲了容器内元素的有序性。）
* 避免使用函数的值传递，改成`const &`传递。

