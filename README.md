# :rocket: 

此项目来自https://github.com/anabioticsoul/BJTU-thesis-template

2024-0602-经过管利聪修改，增加了一些功能，修改了一些bug。

### 北京交通大学研究生论文模板

学校的官方模板过于陈旧，且与word版本有较大差距。

本模板基于 [北交官方模板](https://gs.bjtu.edu.cn/cms/item/477.html) 修订，编译无报错，下载即用。相较于原版，本模板优化了对研究生类别的支持，优化了学校log的分辨率（使用的是学校官方提供的latex模板文件）


本模板支持以下特性：
- 模板支持种类
1. 学术型硕士研究生 (AcMaster)
2. 专业型硕士研究生 (EnMaster)
3. 学术型博士研究生 (Doctor)
- 单双面论文模板

#### 使用前
##### 必须修改
请在main.tex中修改如下参数

```latex
\documentclass[AcMaster]{BJTU-thesis}      %%%    选择模板为学硕
```

##### 单面论文和双面论文
1. 请在main.tex中加入`twoside`参数来启用双面论文模板

```latex
\documentclass[AcMaster,twoside]{BJTU-thesis} 
```

2. 在`BJTU-thesis.cls`文件中将单面打印换成双面打印

##### 中文字体粗体问题
Overleaf和TeXstudio加载的库不同，使用TeXstudio加粗文字时，需要加入`\songti`。（只用\textbf对中文加粗无效）
```latex
\songti\textbf{粗体}
```

#### 编译前
请选择`XeLaTeX`作为编译器进行编译，Overleaf和TeX live都可以使用

#### 致谢
鸣谢[bigworldsmall](https://github.com/bigworldsmall) 




### 在以上基础上进行修改记录------管利聪

使用者只需要看一下内容，无需进行修改了。

```latex
- SimSun.ttf 字体安装，已放入项目中

- GBT7714-2005NLang.bst 
    2045行
    % "In " booktitle * %修改为
      "//" booktitle *

    2232行
    %  format.collection.editors "editor" output.warn  % 不警告empty editor
    editor empty$
    { skip$ }
    { format.collection.editors "editor" output.warn }
    if$ 

    2171行
    %  format.pages "pages" output.warn  %不警告empty pages
    pages empty$
      { skip$ }
      { format.pages "pages" output.warn }
    if$

    2242行
    %  format.pages "pages"          output.warn    %不警告empty pages
    pages empty$
      { skip$ }
      { format.pages "pages" output.warn }
    if$

```

```latex
- BJTU-thesis.cls 
  138行
  \begin{tabular}{lp{5mm}l} 调整间距

  38行:~ 改为：
  %定义使用者需要填写的标签
  \def\BJTU@label@schoolNumber{学校代码：}
  \def\BJTU@label@classification{密级：}
  \def\BJTU@label@author{作者姓名：}
  \def\BJTU@label@studentNumber{学~~~~~~号：}
  \def\BJTU@label@advisor{导师姓名：}
  \def\BJTU@label@advisorTitle{职~~~~~~称：}
  \def\BJTU@label@engineeringMasterField{专业学位类别：}
  \def\BJTU@label@degreeLevel{学位级别：}
  \def\BJTU@label@degreeType{学位类别：}
  \def\BJTU@label@major{学科专业：}
  \def\BJTU@label@researchArea{研究方向：}


- BJTU-thesis.cls 
  425行 注释掉这个旧的包
  % \RequirePackage{subfigure}  
  431行加入subcaption 使图子标题字体大小与正文一致
  \RequirePackage{subcaption}

  说明：https://blog.csdn.net/yzy_1996/article/details/117574086
  subfigure配合subfigure使用太老了，舍弃，subfig配合subfloat使用2015年，现在最新的是sub­cap­tion配合\subcaptionbox或者subfigure使用


- BJTU-thesis.cls
  实现 致谢 在左侧大纲出现，而不在目录出现。
  160行将
    \renewenvironment{thanks}{
      \chapter*{致谢}\thispagestyle{myStyle}
    }{} 改为

    \renewenvironment{thanks}{
      % 添加 PDF 书签
      \pdfbookmark[0]{致谢}{sec:acknowledgement}
      \chapter*{致谢}\thispagestyle{myStyle}
    }{} 


- BJTU-thesis.cls
  159行添加如下
    %重新定义答辩委员会名单环境
    \newenvironment{committee}{
      \chapter*{答辩委员会名单}\thispagestyle{myStyle}
    }{}


- BJTU-thesis.cls
  90行-103注释掉，自己增加makeAuthorization.tex，内容拷贝BJTU-thesis.cls文件中的授权页内容

```


### 写作注意事项

- ppt画图使用宋体和新罗马12号字体，编译完相当于5号字体
- 表格使用\fontsize{10pt}{12pt}\selectfont 相当于5号字体，第一个是10是字体大小，第二个12是行距，使用时默认将\tablestyle{6.0pt}{1}第二个行距设为1，所以只用12来调整行距
- origin画图使用宋体和新罗马，单图使用20号字体，使用0.7/linewidth，双图和四图使用31字体，设置0.5/linewidth