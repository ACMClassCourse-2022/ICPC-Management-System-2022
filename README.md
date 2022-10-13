# :trophy:ICPC Management System

> ACM班 2022级 程序设计课程第二次大作业

## 📖目录

- [简介](#简介)
  - [背景](#背景)
  - [作业目标](#作业目标)
- [作业说明](#作业说明)
  - [分数组成](#分数组成)
  - [截止时间](#截止时间)


- [作业要求](#作业要求)
  - [术语解释](#术语解释)
  - [指令说明](#指令说明)
  - [输入格式](#输入格式)
  - [输出格式](#输出格式)

- [FAQ](#FAQ)

## 🎈简介

### 背景

**ICPC** （国际大学生程序设计竞赛）由 ICPC 基金会举办的一项旨在展示大学生创新能力、团队精神和在压力下编写程序、分析和解决问题能力的年度竞赛，是最具影响力的大学生计算机竞赛。在 ICPC 比赛中，每个队伍尝试在错误提交次数最少的情况下解答出最多的问题，获胜者为正确解答题目最多且总罚时最少的队伍。

### 作业目标

我们想通过本次作业达到以下目标：

- 学会使用STL库
- 加深对于字符串处理的掌握
- 加深对于时间复杂度的理解
- 提高模拟水平
- 学会处理边界情况
- 规范代码风格

因此，你需要实现一个 ICPC 比赛后台系统，通过队伍的提交情况对比赛结果进行维护，具体要求实现的操作见**作业要求**。

## 📝作业说明

### 🛎分数组成

为了让大家在更好地熟悉c++ STL相关操作，B班同学需要先完成前置作业**T1**和**T2**。A班同学不做要求。所以AB班的分数组成略有差别：

#### A班

|                    得分项                     | 分数占比 |
| :-------------------------------------------: | :------: |
| 通过**1732. ICPC Management System (2022 A)** |   80%    |
|                  Code Review                  |   20%    |

#### B班

|                    得分项                     | 分数占比 |
| :-------------------------------------------: | :------: |
|      通过STL练习**1383. 聪老师不想摸鱼**      |    5%    |
|  通过前置作业**1346. Michelle的学生会工作**   |   15%    |
| 通过**1731. ICPC Management System (2022 B)** |   60%    |
|                  Code Review                  |   20%    |

下面是需要说明的几点：

- 题目ICPC Management System(2022-B)的所有测试点的时间限制是ICPC Management System(2022-A)的**4倍**。
- Code Review 也是大作业中重要的一部分，在Code Review 中我们会**严格审查你的代码风格**， TA 建议使用[谷歌标准](https://zh-google-styleguide.readthedocs.io/en/latest/)或[ISO标准](https://isocpp.org/wiki/faq/coding-standards)，你也可以选择其他标准或使用你自己的标准。如果你没有使用 TA 建议的标准，请在 code review 时展示你参考的风格指南。如果使用自己的标准，请**在开始完成作业之前先完成你自己的风格指南**，并全程参考完成代码。

### ⏱截止时间

#### A班

- ICPC Management System(2022-A) ：//todo

#### B班

- STL练习 ：**//todo**
- 前置作业 ：//todo
- ICPC Management System(2022-B) ：//todo

## 🚀作业要求

### 术语解释

由于本次作业涉及到很多专用术语，为了更好地理解后面的指令说明，我们先会对作业中用到的术语进行解释。

- **比赛时间**：我们用一个整数 $duration_time$ 表示比赛的持续时间，比赛时间是一个闭区间$[1,duration\_time]$，因此，我们可以用该区间中的某个整数，表示比赛过程中的某个时间（点）。


- **队伍**：每一支参赛队伍都有自己唯一的队伍名称，队名格式为20个字符内（含）的大小写字母、数字及下划线的组合。

- **榜单**：按照排名从前到后显示每支队伍的状态。榜单的输出规则见输出格式//todo。

- **封榜**：封榜后，对于任意一支队伍，**所有封榜前该队伍未通过的题目**，封榜后的排行榜上并不显示实时的提交结果，而只显示出封榜时间段内该队伍对题目的提交次数，封榜后至少有一次提交的题目将变成冻结状态（封榜前通过的题目，封榜后再次提交不会被冻结）。

- **滚榜**：滚榜环节中，首先在排行榜上选择一支排名最靠后且有冻结状态题目的队伍，并选择该队伍编号最小的一道冻结状态的题目进行解冻，显示该队伍对这道题目的所有提交结果（无需输出），并重新计算排名，更改排行榜上的排名状态。之后重复这项操作直到所有队伍都不存在仍处于冻结状态的题目。这样，我们就得到了当前正确的榜单。

- **提交**：队伍提交一份解答，经评测机评测后，后台获得这次提交的基本信息。未封榜时的提交会实时更新队伍的状态（如通过题目数量等），但**并不会**更新榜单上队伍的排名。

- **评测状态**：某次提交之后，后台获取的信息之一。可能有以下情况：

  - Accepted
  - Wrong_Answer
  - Runtime_Error
  - Time_Limit_Exceed


  除了 Accepted 算做通过外，剩下的状态均不算做通过。

- **刷新榜单**：更新榜单上队伍的排名。

- **罚时**：一种比较两队伍排名的参数。一个队伍对于某道题目的罚时我们定义为$P = 20X + T$。其中$X$ 为该队伍第一次正确提交前的提交次数，$T$ 为该队通过此题的时间，即第一次正确提交的时间。某队伍的罚时我们定义为该队伍对于其所有通过的题目的罚时之和。

- **排名**：比赛的排名由多个参数共同决定：首先，通过题目数多的队伍排名靠前；当两队通过题目数相同时，我们两队的罚时，罚时小者排名靠前；依旧平局时，我们比较两队通过时间最大的题目的通过时间，最大通过时间较小的一队排名靠前，相同则比较通过时间第二大的题目，依旧相同则比较通过时间第三大的题目……以此类推；如果依旧平局则比较两支队伍名称的字典序，字典序较小的队伍排名靠前。**注意**：以上所有因素均不包含冻结状态的题目，显而易见，封榜后直到滚榜前排行榜上的排名不会发生改变。

### 指令说明

所有的指令格式由下方的代码框给出，全大写部分代表命令，中括号[]内的小写部分代表对应参数（括号并不会出现在输入中）。

```css
# 添加队伍
ADDTEAM [team_name]

# 开始比赛
START DURATION [duration_time] PROBLEM [problem_count]

# 提交题目
SUBMIT [problem_name] BY [team_name] WITH [submit_status] AT [time]

# 刷新榜单
FLUSH

# 封榜
FREEZE

# 滚榜
SCROLL

# 查询队伍排名
QUERY_RANKING [team_name]

# 查询队伍提交情况
QUERY_SUBMISSION [team_name] WHERE PROBLEM=[problem_name] AND STATUS=[status]

# 结束比赛
END
```

- 添加队伍
  - `ADDTEAM [team_name]`
    - 向系统中添加队伍。
      - 成功添加输出`[Info]Add successfully.\n`
      - 若比赛已开始，输出`[Error]Add failed: competition has started.\n`
      - 若比赛未开始但队伍名重复，输出`[Error]Add failed: duplicated team name.\n`


- 开始比赛
  - `START DURATION [duration_time] PROBLEM [problem_count]`
    - 开始比赛，比赛时间 count 为闭区间 [1, duration_time] ，题号范围为前 problem_count 个大写英文字母。
      - 成功开始则输出`[Info]Competition starts.\n`
      - 若比赛已开始，输出`[Error]Start failed: competition has started.\n`

**保证以下全部操作均在开始比赛之后出现**

- 提交题目

  - `SUBMIT [problem_name] BY [team_name] WITH [submit_status] AT [time]`
    - 保证输入合法，记录 team_name 在 time 时刻对题目 problem_name 的一次提交，评测状态为 submit_status 。 submit_status 可能有以下情况：Accepted，Wrong_Answer，Runtime_Error，Time_Limit_Exceed。除了 Accepted 算做通过外，剩下的状态均不算做通过。保证 time 按照提交出现的顺序单调上升。
      - 本条指令无输出

- 刷新榜单

  - `FLUSH`
    - 刷新当前榜单
      - 输出`[Info]Flush scoreboard.\n`

- 封榜

  - `FREEZE`
    - 进行封榜操作。
      - 成功则输出`[Info]Freeze scoreboard.\n`
      - 若已封榜但未滚榜，则输出`[Error]Freeze failed: scoreboard has been frozen.\n`

- 滚榜

  - `SCROLL`

    - 刷新当前榜单并进行滚榜操作。

      - 成功则输出`[Info]Scroll scoreboard.\n`，接下来首先输出滚榜前的榜单，接着每一行输出每一次滚榜时**导致排名变化**的解冻，每行的输出格式如下：

        ```css
        [team_name1] [team_name2] [solved_number] [penalty_time]
        ```

        team_name1 表示题目解冻导致排名上升的队伍， team_name2 表示排名被 team_name1 取代的队伍， solved_number 和 penalty_time 为 team_name1 新的解题数和罚时；最后输出滚榜后的榜单。

- 查询队伍排名

  - `QUERY_RANKING [team_name]`

    - 查询对应队伍排名。

      - 若队伍不存在，则输出`[Error]Query ranking failed: cannot find the team.\n`

      - 若队伍存在，则输出`[Info]Complete query ranking.\n`。此时若处在封榜状态，则需要输出一行`[Warning]Scoreboard is frozen. The ranking may be inaccurate until it were scrolled.\n`。不论是否封榜，输出上一次刷新榜单后的队伍排名，格式如下：

        ```css
        [team_name] NOW AT RANKING [ranking]
        ```

- 查询队伍提交情况

  - `QUERY_SUBMISSION [team_name] WHERE PROBLEM=[problem_name] AND STATUS=[status]`

    - 查询对应队伍的满足条件的最后一次提交。

      以下是可参考以下合法示例：

      ```css
      QUERY_SUBMISSION Team_Rocket WHERE PROBLEM=ALL AND STATUS=ALL
      // 查询Team_Rocket的最后一次提交

      QUERY_SUBMISSION Team_Plasma WHERE PROBLEM=ALL AND STATUS=Accepted
      // 查询Team_Plasma的最后一次状态为Accepted的提交

      QUERY_SUBMISSION Pokemon_League WHERE PROBLEM=A AND STATUS=ALL 
      // 查询Pokemon_League的最后一次对题目A的提交

      QUERY_SUBMISSION Opelucid_Gym WHERE PROBLEM=M AND STATUS=Runtime_Error 
      // 查询Opelucid_Gym队的最后一次对M题状态为Runtime_Error的提交
      ```

      - 若队伍不存在，则输出`[Error]Query submission failed: cannot find the team.\n`

      - 若队伍存在`[Info]Complete query submission.\n`

        - 若无满足条件的提交，输出`Cannot find any submission.\n`

        - 若有满足条件的提交，输出一行表示最后一次满足条件的提交，格式如下：

          ```css
          [team_name] [problem_name] [status] [time]
          ```

          [problem_name] 为该次提交的题目编号， [status] 为该次提交的状态，[time] 为该次提交的时间。保证询问中的 [problem_name] 与 [status] 合法。

- 结束比赛

  - `END`
    - 结束比赛。
      - 输出`[Info]Competition ends.\n`。保证结束比赛时排行榜不处于封榜状态，且之后没有任何操作。

### 输入格式

- 程序开始运行后，会读入若干个指令，直到读入`END`指令为止。
- 保证命令格式合法（但不保证命令所执行的内容合法，具体可参见上文）


### 输出格式

某些指令需要输出榜单，榜单输出格式要求如下：

- 输出$N$（队伍总数）行，每行以

  ```css
  队名 排名 解题数 总罚时 A B C ...
  ```

  的格式表示一支队伍的情况，其中“A B C ...”表示每一题的情况，有以下三种可能：

  ```css
  +x 该题未被冻结且已经通过。x表示该题第一次通过前错误的次数，如果x为0，则显示“+”而不是“+0”。

  -x 该题未被冻结但没有通过。x表示该题错误的次数，如果x为0，则显示“.”而不是“-0”。

  -x/y 该题被冻结。x表示封榜前错误的次数，y表示封榜后的提交次数。如果x为0，则显示“0/y”而不是“-0/y”。；
  ```

## FAQ

- 提交时间单调上升不是严格的，可能出现相同时间。
- 滚榜时每次选择队伍依照的排名是动态变化的
- 封榜后的提交可以被查询提交情况查询到
- 第一次刷新榜单前的排名的依据是队伍名称的字典序