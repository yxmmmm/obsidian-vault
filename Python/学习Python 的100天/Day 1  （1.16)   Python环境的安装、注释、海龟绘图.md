
|     |                                    |        |          |
| --- | ---------------------------------- | ------ | -------- |
| 序号  | **课程名称**                           | **时长** | **看完画√** |
| 1   | 必须听的正确学习方法                         | 17分48秒 | ✓        |
| 2   | python环境的安装                        | 4分32秒  | ✓        |
| 3   | pycharm软件的下载和安装                    | 6分35秒  | ✓        |
| 4   | pycharm的使用-python项目的创建和第一行python程序 | 10分17秒 | ✓        |
| 5   | Python程序格式_缩进_行注释_段注释              | 9分52秒  | ✓        |
| 6   | 简单错误如何处理                           | 6分42秒  | ✓        |
| 7   | 海龟绘图-坐标系问题-画笔的用法                   | 8分50秒  | ✓        |
| 8   | 海龟绘图-绘制奥运五环                        | 10分28秒 | ✓        |
| 9   | AI辅助工具_GithubCopilot介绍与安装流程        | 12分55秒 |          |
| 10  | GithubCopilot安装与开发游戏体验             | 13分53秒 |          |
| 11  | 大语言模型(LLM)-查询资料与解决编程报错             | 22分6秒  |          |
| 12  | 大语言模型(LLM)-Prompt提示词               | 18分12秒 |          |
| 13  | python程序的构成                        | 7分46秒  |          |
|     |                                    |        |          |

## 学习方法

原则：持之以恒，细水长流
每天固定1-2小时的高效学习，远胜于周末突击10小时。
样例每日学习计划（参考）
时段1（20分钟）：复习前一天的学习内容，浏览笔记。
时段2（40分钟）：学习新知识点（看视频/读文档），理解概念。
时段3（50分钟）：核心环节：动手实践。完成课后练习，或尝试修改代码看不同效果。
时段4（10分钟）：整理今日所学，用几句话总结到笔记中。
每周留出半天：进行综合练习，将本周学的零散知识点串联起
来，做一个小项目（如：一个简单的计算器、一个爬取天气的脚
本）。

正确利用语言大模型，要自己思考，不能过度依赖

虽然中文技术社区（CSDN、博客园、思否等）非常活跃，但最权威、最一手、最前沿的信息通常
首先来自英文世界
官方文档：Python、Django、PyTorch等所有主流技术和框架的官方文档均是英文写成，中文版
本往往存在滞后甚至误译
Stack Overflow：全球最大的程序员问答社区，你遇到的99%的技术问题都能在上面找到答案，
答案质量远高于国内多数论坛
顶级学术会议、论文：AI、算法等前沿领域的第一手资料基本都是英文

国内技术生态圈
CSDN、博客园：老牌综合性社区，文章海量，但需要甄别质量（优先看阅读量、评论点赞数高
的）。
思否（SegmentFault）：更偏向开发者社区，问答和文章质量相对较高。
掘金：近年来活跃的社区，UI现代，专栏文章质量高，是学习前沿技术的好地方。
Gitee（码云）：中国的GitHub，由于网络和合规性原因，是国内开源项目托管的首选平台。很多
国内企业和高校都在使用。

## Python环境的安装
### 方法1：
官网下载并安装，官网：python.org，初学者3.9以上版本就够用，点击Python解释器的时候要==**用管理员身份**==，安装目录可以默认也可修改，建议修改
### 方法2：
通过网盘分享的文件：python-3.11.3-amd64.exe
链接: https://pan.baidu.com/s/13qgBv72svbdgXauoP9mOjg 提取码: 14mm 
--来自百度网盘超级会员v1的分享

下载完
运行python
windows查找命令中输入cmd，进入命令行窗口，再输入：python
输入print("helloworld")
输出helloworld

交互模式(shell脚本模式)
交互模式详解
1>>>即为“提示符”
2关闭交互模式：
(1)Ctrl+Z和回车
(2)输入quit()或exit()命令
(3)直接关闭命令行窗口
⚠交互模式工作原理和Python处理文件的方式一样。除了一
点：当你输入一些值时，交互模式会自动打印输出。Py文件中
则必须使用print语句

## pycharm的使用-python项目的创建和第一行python程序
### 创建python项目

1. 选择：`New Project`

![image-20211021192726595](https://www.itbaizhan.com/wiki/imgs/image-20211021192726595.png)

选择路径（尽量不要包含中文），项目名：`mypro01`

![image-20211021194007827](https://www.itbaizhan.com/wiki/imgs/image-20211021194007827.png)

> ⚠️关于解释器设置（了解即可）：
> 
> 1. Project Interpreter部分是选择新建项目所依赖的python库，第一个选项会在项目中建立一个venv（virtualenv）目录，这里存放一个虚拟的python环境。这里所有的类库依赖都可以直接脱离系统安装的python独立运行。
>     
> 2. Existing Interpreter关联已经存在的python解释器，如果不想在项目中出现venv这个虚拟解释器就可以选择本地安装的python环境。
>     
> 3. 那么到底这两个该怎么去选择呢，这里建议选择New Environment 可以在Base Interpreter选择系统中安装的Python解释器，这样做的好处如下：
>     
>     - python项目可以独立部署
>     - 防止一台服务器部署多个项目之间存在类库的版本依赖问题发生

### 开发和运行项目

打开项目后，右键单击项目，创建Python文件`mypy01`

![image-20211021194530961](https://www.itbaizhan.com/wiki/imgs/image-20211021194530961.png)

运行py文件，使用右键单击编辑区，选择`Run mypy01`即可。

![image-20211021194723320](https://www.itbaizhan.com/wiki/imgs/image-20211021194723320.png)

### 其他设置

1. 字体大小：
    
    `File→Setting→Editor→Font`把字体调大一些
    
2. 主题风格：
    
    `File→Setting→Apperence→Dragula(黑色主题)、InteliJ light(白色主题)`

### 缩进
Python用缩进来表示程序块的层次关系
单个缩进用单个制表符或四个空格

### 注释
在Pycharm中想要将一段代码注释掉，只需要选定代码，CTRL+/

用来解释代码，不属于代码本身，运行时不会去执行注释
##### 单行注释
 注释前加#，代表注释
##### 段注释（多行注释）
使用连续三个单引号或三个双引号，引号之间的为注释
⚠️三个连续引号，其实就是定义了一个字符串。只不过，没有变量指向，会被当做垃圾回收（关于本句话的含义，后面讲完面向对象再看）

`#我是单行注释`
`print('单行注释演示')`


`'''`
`我是多行注释`
`三个单引号实现多行注释`
`作者:`
`时间：`
`'''`
`print('三个单行引号实现多行注释')`
`"""`
`三个双引号实现多行注释`
`作者:`
`时间:`
`"""`
`print('双引号实现多行注释')`


选中代码 ctrl+？ 加注释和取消注释 

## 错误处理
遇到错误要像看到美女一样开心😄


## 海龟绘图
### 测试turtle的使用

`import turtle       #导入turtle模块`

`turtle.showturtle()    #显示箭头`

`turtle.write("高淇")    #写字符串`

`turtle.forward(300)   #前进300像素`

`turtle.color("red")    #画笔颜色改为red`

`turtle.left(90)      #箭头左转90度`

`turtle.forward(300)`

`turtle.goto(0,50)    #去坐标（0,50）`

`turtle.goto(0,0)`

`turtle.penup()     #抬笔。这样，路径就不会画出来`

`turtle.goto(0,300)`

`turtle.pendown()    #下笔。这样，路径就会画出来`

`turtle.circle(100)    #画圆`

`turtle.done()      #程序结束，保持窗口存在`


## 奥运五环
### 课堂练习，画出奥运五环

![](https://www.itbaizhan.com/wiki/imgs/%E5%A5%A5%E8%BF%90%E4%BA%94%E7%8E%AF.gif)

建立源文件`draw_olympic.py`，整体输入下面代码：

i`mport turtle`

`#最好的老师：兴趣   第二个好老师：耻辱`

`#第一个圈`

`turtle.width(10)`

`turtle.color("blue")`

`turtle.circle(50)`

`#第二个圈`

`turtle.penup()`

`turtle.goto(80,0)`

`turtle.pendown()`

`turtle.color("black")`

`turtle.circle(50)`

`#第三个圈`

`turtle.penup()`

`turtle.goto(160,0)`

`turtle.pendown()`

`turtle.color("red")`

`turtle.circle(50)`

`#第四个圈`

`turtle.penup()`

`turtle.goto(40,-60)`

`turtle.pendown()`

`turtle.color("yellow")`

`turtle.circle(50)`

`#第五个圈`

`turtle.penup()`

`turtle.goto(110,-60)`

`turtle.pendown()`

`turtle.color("green")`

`turtle.circle(50)`

`turtle.done()  #程序结束，保持窗口`