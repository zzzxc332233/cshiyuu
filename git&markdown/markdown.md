#Markdown实践
[toc]
##屁话
Markdown作为一款"轻量化的标记性语言"——也就是说它可以理解成一个html网页,其呈现什么样的排版完全取决于解释器的解释,但这样的好处是可以让我们更加方便快速地记录,将注意力集中到内容上面来.相对于什么LaTeX而言,MarkDown不用编译,也没有复杂的环境和屎山代码,非常轻松.

也许这个文档好像并没有什么必要,反正我其实也是从[官方说明文档](https://markdown.com.cn/)里CV过来的.不过为了学习体会一下还是打一篇文档.

## MarkDown基本语法
### 标题
<<<<<<< HEAD
要创建标题，在单词或短语前面添加井号 (#) .# 的数量代表了标题的级别.例如,添加三个 # 表示创建一个三级标题(如: `### My Header`).为了兼容考虑,请用一个空格在 # 和标题之间进行分隔.
=======
要创建标题，在单词或短语前面添加井号 (#) .# 的数量代表了标题的级别.例如,添加三个 # 表示创建一个三级标题,例如: 
```
### My Header
```

为了兼容考虑,请用一个空格在 # 和标题之间进行分隔.
>>>>>>> 511

还可以在文本下方添加任意数量的 == 号来标识一级标题,或者 -- 号来标识二级标题.例如

    Heading level 1         Heading level 2
    ===============         ---------------

<<<<<<< HEAD
=======
### 段落
在MarkDown里面,不用考虑缩进,因为考虑了也没用.因为在段首的四个空格或换行符都会被算作一个代码环境.效果如下:

    其实说是代码环境,倒是什么都能写,类似于LaTeX里面的\frame环境.

需要注意,为了兼容性,换行前最好在上一段的末尾加上空格.

### 强调
要加粗文本，请在单词或短语的前后各添加两个星号（**）.
`**114514**`$\implies$**114514**

要使用斜体，请在单词或短语的前后各添加一个星号（*）.
`*114514*`$\implies$*114514*

要加粗文本并使用斜体，请在单词或短语的前后各添加三个星号（***）.
`**114514**`$\implies$***114514***

其实使用下划线`_`替代星号一般也能得到同样的结果,不过在一些解释器中下划线强调的行为是未定义的,不建议用.

### 引用
要创建块引用，只需在段落前添加一个 `>` 符号。

    > Dorothy followed her through many of the beautiful rooms in her castle.
    >
    > The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

效果:
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

块引用可以嵌套

    > Dorothy followed her through many of the beautiful rooms in her castle.
    >
    >> ???
    >>>sb
    >
    > The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

效果:
 > Dorothy followed her through many of the beautiful rooms in her castle.
>
>> ???
>>>sb
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

### 列表
#### 有序列表
使用数字+英文句点来创建有序列表;列表可以相互嵌套.需要注意:句点前的数字并不会影响列表的计数器,只要是个数字就行.

    1. First item
    2. Second item
    3. Third item
        1. Indented item
        2. Indented item
        2. Indented item
    4. Fourth item

效果:
1. First item
 2. Second item
 3. Third item
     1. Indented item
     2. Indented item
     3. Indented item
 4. Fourth item

#### 无序列表
使用破折号 `-`, 星号 `*` 或加号 `*` 来创建有序列表;列表可以相互嵌套.

    - First item
    - Second item
    - Third item
        - Indented item
        - Indented item
    - Fourth item

效果:
- First item
- Second item
- Third item
    - Indented item
    - Indented item
- Fourth item

### 代码
行间代码只需要使用反引号`` ` ``括起来.例如`` `\textbf` ``$\implies$`textbf`.

如果代码中含有反引号,在两段使用多反引号括起来.例如``` `` `\im`` ```$\implies$`` `\im``.多反引号可以嵌套.

如前文所述,直接缩进就可以创建行间(或说段落)代码块.也可以用两个行首的`` ``` ``或者`~~~`创建行间代码块.在`` ``` ``的旁边写上语言种类可以实现语法高亮(取决于库实现).

    ```c
    #include <stdio.h>
    #include <stdlib.h>

    int main(void)
    {
        ...
    }
    ```

效果:
```c
    #include <stdio.h>
    #include <stdlib.h>

    int main(void)
    {
        ...
    }
```

### 分隔线
使用三个以上的星号`***`,破折号`---`或下划线`___`都能创建分割线.为了兼容性,分割线前后空行.分割线本行不能包含其它内容.

效果:
_________

### 链接
超链接Markdown语法代码：`[超链接显示名](超链接地址 "超链接title")`.其中`"超链接title"`是可选参数,是鼠标悬停在链接上时会出现的文字.

    这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。

效果: 这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。

支持文内引用,也可以使用一定的强调或代码样式:

    See the section on [`code`](#code).

See the section on [`code`](#链接).

使用尖括号可以很方便地把URL或者email地址变成可点击的链接。这个用法叫做*自动链接*

    <https://markdown.com.cn>
    <fake@example.com>

效果:
<https://markdown.com.cn>
<fake@example.com>

### 图片
插入图片Markdown语法代码：`![图片alt](图片链接 "图片title")`
相对路径绝对路径或者网址都可以(最好用个图床罢).

    ![时雨可爱捏]((https://i2.hdslb.com/bfs/face/94b72ad22b0f9c7d518e813b5eeb66bc788445f3.jpg@240w_240h_1c_1s.webp) "时雨神必捏")

效果:
![时雨可爱捏](https://i2.hdslb.com/bfs/face/94b72ad22b0f9c7d518e813b5eeb66bc788445f3.jpg@240w_240h_1c_1s.webp "时雨神必捏")

这样可以顺便让图片变成超链接:

    [![时雨可爱捏](https://i2.hdslb.com/bfs/face/94b72ad22b0f9c7d518e813b5eeb66bc788445f3.jpg@240w_240h_1c_1s.webp "时雨神必捏")](https://space.bilibili.com/16725323)

[![时雨可爱捏](https://i2.hdslb.com/bfs/face/94b72ad22b0f9c7d518e813b5eeb66bc788445f3.jpg@240w_240h_1c_1s.webp "时雨神必捏")](https://space.bilibili.com/16725323)

##拓展语法

