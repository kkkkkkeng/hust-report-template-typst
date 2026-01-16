*这是一份用于华中科技大学实验报告、课程作业等的Typst模板*

---

该模板集成了封面生成、自动排版、代码块高亮、智能图表编号以及参考文献管理等功能，旨在让你专注于实验内容的撰写，而无需操心排版问题。

#### 使用方法

1. 确保系统安装了以下字体

   - 中文字体：宋体 (SimSun), 黑体 (SimHei), 楷体 (KaiTi)

   - 英文字体：Times New Roman

   - 代码字体： Consolas

​	如果你是windows系统，则系统已自带这些字体，无需额外安装

2. 前往[Typst Web App](https://typst.app/)，或者使用 `vscode`与`tinymist`插件组合。确保目录组织如下。

   ```text
   Project/
   ├── assets/
   │   └── HUSTGreen.svg   <-- 请务必放入华科校名矢量图
   ├── template.typ        <-- 你的模板文件
   ├── main.typ            <-- 你的报告主文件
   └── ref.bib             <-- (可选) 参考文献库
   ```

   如果你是其他学校的学生，想使用这个模板，只需要前往template.typ中修改校名的图片为自己学校，并同步修改页眉等信息即可。

3. 在`main.tpy`插入如下代码

   ```typst
   #import "template.typ": *
   #import "@preview/lovelace:0.3.0": pseudocode-list //伪代码的实现需要用到该函数
   #show: report.with(
     type: "课程实验报告", //校名下方的标题
     course_name: ("课程名称", "人工智能导论"), //课程名称,必须以(标签，内容)方式传参,可选,默认为none
     title: ("实验题目", "基于CNN的动物识别系统"), //实验题目,同上
     class_name: "CS2410", //专业班级
     student_id: "U202488888", //学号
     name: "张三", //学生姓名
     instructor: "李四", //指导教师
     date: datetime.today().display("[year]年[month]月[day]日"), //自动获取当前日期，可手动修改
     school: "计算机科学与技术学院", //学院
     header_text: "华中科技大学课程实验报告", //页眉文字
     appendix: //可选，在[]中填写附录内容,默认为none
     [
       = 原始代码
   
       == 模块一
     ],
     bibliography-file:none //可选,填写参考文献的文件地址，不需要则填写none,默认为none
     //"ref.bib",
   )
   ```

4. 开始编写你的代码。下面是一些基本用法。

   ````Typst
   = 引言
   用 `=` 可以区分多级标题。
   
   == 有序列表
   有序列表以 `+` 开头，
   + 第一
   + 第二
   
   == 无序列表
   无序列表以 `-`开头,列表均可利用缩进进行嵌套。例如
   - One
     - 这里是子列表
     - 111
   - Two
   
   = 第一章
   所有图片、表格、公式、伪代码均会按照“章节-序号”自动编号。
   
   == 图片插入
   插入图片的格式如下,可在figure之后用`< >`包裹对figure的命名，然后用`@name`的方式来引用这个figure，就像这样@HUST，或者@this_is_a_table
   
   #figure(
     caption: "华中科技大学(黑)",
     image("assets/HUSTBlack.svg", width: 80%),
   )<HUST>
   
   == 表格插入
   表格的基本用法如下，
   
   #figure(
     caption: "这里是表格的名字",
     table(
       columns: (1fr, 2fr, 1fr),
       //建立一个三列，宽度为1:2:1的表格
       [1], [2], [3],
       [a], [b], [c],
     ),
   )<this_is_a_table>
   
   == 公式插入
   行内公式的插入如下,直接用`$`包裹即可，例如$F = m a$和$O(N^2)$, $cal(O)(N log N)$,单个字母间的空格表示相乘。用`""`包裹表示以原文呈现。
   
   单行公式的插入,在开头`$`之后和结尾`$`之前多一个空格即可。
   
   $
     T(n) = cases(
       1 & "if" n = 1,
       2T(n /2) + n & "if" n >= 2
     )
   $
   
   == 代码插入
   === 伪代码插入
   插入伪代码的格式如下，用有序列表来实现缩进，用`*`包裹关键词实现加粗。伪代码格式的实现调用了 lovelace的库 。更多资料请#link("https://typst.app/universe/package/lovelace/")[点击这里]。
   
   #figure(
     kind: "algorithm",
     supplement: "Algorithm",
     pseudocode-list(booktabs: true, numbered-title: [Quick Sort])[
       + *Input:* Array $A$, low $p$, high $r$
       + *Output:* Sorted Array $A$
       + *if* $p < r$ *then*
         + $q =$ *Partition*($A, p, r$)
         + *QuickSort*($A, p, q-1$)
         + *QuickSort*($A, q+1, r$)
       + *end if*
       + *return*
     ],
   )<quick_sort>
   
   如果导入了参考文献，可以直接使用`@`来进行访问，例如 @clrs 这样，被引用到的文献会出现在参考文献的列表中。
   
   === 代码块和行内代码插入
   代码块的格式如下
   ```cpp
   #include<iostream>
   int main() {
     cout << "hello,world!";
   }
   ```
   
   ```python
   def helloWorld():
     print("hello,world!")
   
   helloWolrd()
   ```
   
   除此之外，还可以利用“ \` ”单引号包裹来实现行内代码的效果，例如`print()`
   ````

   更多关于Typst的使用教程，请访问[Typst官方文档](https://typst.app/docs/)。

---

#### 效果

![1](https://cdn.jsdelivr.net/gh/kkkkkkeng/pic-bed/img/20260116212628356.png)



![2](https://cdn.jsdelivr.net/gh/kkkkkkeng/pic-bed/img/20260116212731983.png)

![3](https://cdn.jsdelivr.net/gh/kkkkkkeng/pic-bed/img/20260116212816118.png)

![3](https://cdn.jsdelivr.net/gh/kkkkkkeng/pic-bed/img/20260116213256720.png)

---

#### 参数说明

 | **参数名**          | **类型** | **默认值**       | **说明**                                             |
  | ------------------- | -------- | ---------------- | ---------------------------------------------------- |
  | `type`              | string   | `"课程实验报告"` | 封面顶部的大标题                                     |
  | `course_name`       | array    | `none`           | 格式为 `("标签", "内容")`，如 `("课程名称", "OS")`   |
  | `title`             | array    | `none`           | 格式为 `("标签", "内容")`，如 `("实验题目", "Lab1")` |
  | `class_name`        | string   | `"CS2410"`       | 专业班级                                             |
  | `student_id`        | string   | `"U2024XXXXX"`   | 学号                                                 |
  | `name`              | string   | `"张三"`         | 学生姓名                                             |
  | `instructor`        | string   | `"李四"`         | 指导教师                                             |
  | `date`              | string   | *自动生成今日*   | 报告日期                                             |
  | `school`            | string   | `"计算机..."`    | 学院名称，显示在封面底部                             |
  | `header_text`       | string   | `"华中科技..."`  | 页眉中间的红字文本                                   |
  | `bibliography-file` | string   | `none`           | `.bib` 文件路径，传入即开启参考文献                  |
  | `appendix`          | content  | `none`           | 附录内容块，传入即开启附录模式                       |





