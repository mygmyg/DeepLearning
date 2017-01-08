# Markdown语法学习

##标题
  在 Markdown 中，如果一段文字被定义为标题，只要在这段文字前加 # 号即可。总共有六级标题，建议在#号后面加一个空格

## 列表
在 Markdown 下，列表的显示只需要在文字前加上 - 或 * 即可变为无序列表，有序列表则直接在文字前加 1. 2. 3. 符号要和文字之间加上一个字符的空格。

#### 无序列表
* 1
* 2
* 3

#### 有序列表
1. Ordered list item
2. Ordered list item
3. Ordered list item

## 引用

如果你需要引用一小段别处的句子，那么就要用引用的格式。只需要在文本前加入 > 这种尖括号（大于号）即可.
> 这里是引用

## 图片与链接

插入链接与插入图片的语法很像，区别在一个 !号
插入图片的地址需要图床，这里推荐 CloudApp 的服务，生成URL地址即可。
#### 插入邮箱
An email <example@example.com> link.
#### 插入链接
[Baidu](https://www.baidu.com/)
#### 插入图片
![Mou icon](http://25.io/mou/Mou_128.png)

An inline image ![Smaller icon](http://25.io/smaller/favicon.ico "Title here"), title is optional.

A ![Resize icon][2] reference style image.

[2]: http://resizesafari.com/favicon.ico "Title"

## 粗体与斜体
Markdown 的粗体和斜体也非常简单，用两个 * 包含一段文本就是粗体的语法，用一个 * 包含一段文本就是斜体的语法。

例如 **粗体** or __粗体__ （cmd+B） 
例如 *斜体* or _斜体_ (cmd+I)

**Sometimes I want a lot of text to be bold.Like, seriously, a _LOT_ of text**

## 表格
A simple table looks like this:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

If you wish, you can add a leading and tailing pipe to each line of the table:

| First Header | Second Header | Third Header |
| ------------ | ------------- | ------------ |
| Content Cell | Content Cell  | Content Cell |
| Content Cell | Content Cell  | Content Cell |

Specify alignment for each column by adding colons to separator lines:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right

##代码框
如果你是个程序猿，需要在文章里优雅的引用代码框，在 Markdown 下实现也非常简单，只需要用两个 ` 把中间的代码包裹起来，如 `code：
`hello word`:

	void main(){
		;
	}

使用 tab 键即可缩进。
## 分割线
分割线的语法只需要另起一行，连续输入三个星号 *** 即可

## Footnotes
That's some text with a footnote.[^1]

[^1]: And that's the footnote.

***
## 小结

到这里，Markdown 的基本语法在日常的使用中基本就没什么大问题了，只要多加练习，配合好用的工具，写起东西来肯定会行云流水。更多的语法规则，其实 Mou 的 Help 文档例子很好，当你第一次使用 *Mou* 时，就会显示该文档，其次，你也可在撰写过程中，使用<!----> CMD+R 快捷键来快速打开文档，以随时查阅和学习语法。**写中文文档时，需要注意语法符号是英文的。**
***
 [认识与入门Markdown](http://sspai.com/25137)
 
 [为什么我们要学习 Markdown 的三个理由](https://news.cnblogs.com/n/139649/)