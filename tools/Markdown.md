# Markdown学习笔记

[toc]

## 一、标题

ctrl + 1	一级标题（#加空格）

ctrl + 2	二级标题（##加空格）

ctrl + 3	三级标题（###加空格）

ctrl + 4	四级标题（####加空格）

ctrl + 5	五级标题（#####加空格）

ctrl + 6	六级标题（######加空格）

## 二、字体

ctrl + B 	字体加粗

ctrl + I 	字体倾斜

ctrl + U 	下划线

alt + shift + 5 	删除线

## 三、列表

### 1.无序列表：*、-、+加空格

### 2.有序列表：1.，2.，3.加空格

## 四、表格

### 1.创建表格：ctrl + T

### 2.创建表格语法

2.1分隔表头和其他行：

> ```markdown
> |  表头   | 表头  |
> |  ----  | ----  |
> | 单元格  | 单元格 |
> | 单元格  | 单元格 |
> ```

2.2设置对齐方式

2.2.1右对齐：-：

2.2.2左对齐：:-

2.2.3居中对齐：:-:

> ```markdown
> | 左对齐 | 右对齐 | 居中对齐 |
> | :-----| ----: | :----: |
> | 单元格 | 单元格 | 单元格 |
> | 单元格 | 单元格 | 单元格 |
> ```

## 五、图片

ctrl + shift + I 插入图片

## 六、链接

ctrl + K	插入链接

网址： \<网址>

## 七、代码

1.行内代码：用 \`` 	\``括起代码，代码会以主题中设置的样式出现在行内，但不会实现代码高亮。

2.代码块：输入\```后并输入语言名，换行，开始写代码，Typora 就会自动帮你实现代码高亮。Typora 原生支持许多编程语言代码块的语法高亮，基本日常常用的编程语言它都能很好地支持。 

## 八、HTML

```html
<!--换行-->
<br>
<!--居中-->
<center></center>
<!--上标下标-->
<sup></sup>
<sub></sub>
```

## 九、其他

ctrl + home/end 	返回typora顶部或底部

ctrl + L	 选中某句话

ctrl + D	 选中某个单词

大于号 + 空格 	引用文字

\***或者\---加回车 	水平分割线

\==高亮文字==	显示高亮文字

[toc]加回车	生成目录 

## 十、问题

## 1.github上传图片不显示问题：

打开：C:\Windows\System32\drivers\etc\hosts在文件末尾添加

GitHub raw & imag

199.232.28.133 raw.githubusercontent.com

## 2.markdown应用github上的图片：

复制图片的github地址：https://github.com/lxiopeng/image/blob/master/Git/gitjiegou.png
将blob改成raw：https://github.com/lxiopeng/image/raw/master/Git/gitjiegou.png

