# 微信读书助手(爬虫) wereader

> 本项目基于[@arry-lee](https://github.com/arry-lee)的项目[wereader](https://github.com/arry-lee/wereader/issues/20)修改而来，并借鉴了[@shengqiangzhang](https://github.com/shengqiangzhang)的[一键导出微信读书的书籍和笔记]([https://github.com/shengqiangzhang/examples-of-web-crawlers/tree/master/12.%E4%B8%80%E9%94%AE%E5%AF%BC%E5%87%BA%E5%BE%AE%E4%BF%A1%E8%AF%BB%E4%B9%A6%E7%9A%84%E4%B9%A6%E7%B1%8D%E5%92%8C%E7%AC%94%E8%AE%B0](https://github.com/shengqiangzhang/examples-of-web-crawlers/tree/master/12.一键导出微信读书的书籍和笔记))中的GUI登录方法，感谢原作者、感谢开源。

## 主要功能

1. 获取某本书的全部标注(笔记)
2. 获取某本书指定章节的标注
3. 获取某本书你的个人想法
4. 获取某一本书的热门划线
5. 获取某本书的目录
6. 获取某本书的详情(书本信息)
7. 获取某本书你的最新标注
8. 获取书架上的书籍列表
9. 自定义标注效果、标题级别

针对上面所获取的大多数内容，使用时有两方面的操作选择：一是输出到控制台并复制到剪切板；二是追加到指定文件。


主要代码见`wereader.py`

## 如何运行

```python
# 跳转到当前目录
cd 目录名
# 安装依赖库
pip install -r requirement.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
# 开始运行
python main.py
```

如果运行出错，尝试先卸载依赖库：

```python
# 跳转到当前目录
cd 目录名
# 先卸载依赖库
pip uninstall -y -r requirement.txt
# 再重新安装依赖库
pip install -r requirement.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
# 开始运行
python main.py
```

## 操作介绍

输入命令

```
python main.py
```

运行程序之后。

程序会提示登录，登录成功后会输出书架并提示输入书本id(书名前面的那一串数字)：

![](login.gif)

![](login.png)

输入id后会列出操作指南：

![](guide.png)

这时候有两类操作可以选择：`print`选项的功能是输出内容到控制台并复制到剪切板；`push`选项的功能是将内容追加到文件末尾。

比如，现在想要将这本书的想法输出到控制台并复制到剪切板，只需要输入`print 2`再回车:

![](print.gif)

同样，如果想要将想法追加到文件，输入`push 2`即可：

![](push.gif)

至于“个人最新标注”，是用来随时输出新标注(而不让内容重复)的功能。

假设你和我一样，喜欢读一部分做一部分的笔记，那么这个功能对你比较有帮助。

`push 1`或`print 1`只能够输出书中的所有标注或某一章的标注，这使得你要么全部做好笔记后一次性导出标注，要么每读完一章后做一次笔记。

而`push 6`或`print 6`则能够让你随时导出最新标注好的内容（初次使用时将只是记录最新内容所在位置，相当于初始化）。这个选项中有两种寻找最新内容的方式，一种效果不佳可以尝试另一种。

## 标注效果

可以编辑源文件来设置标注效果。

打开`wereader.py`，找到下面的代码：

```python
level1 = '##'#(微信读书)一级标题
level2 = '###'#二级标题
level3 = '####'#三级标题
style1 = {'pre': "",   'suf': ""}#(微信读书)红色下划线
style2 = {'pre': "**",   'suf': "**"}#橙色背景色
style3 = {'pre': "",   'suf': ""}#蓝色波浪线
thought_style = {'pre': "```\n",   'suf': "\n```"}#想法前后缀
hotmarks_number = {'pre': "`",   'suf': "`  "}#热门标注标注人数前后缀
```

三个`level`变量分别代表三级标题，如果你想将改变导出内容的标题级别，可以在这里修改井号个数。

三个`style`变量代表微信读书中的三种标注(见注释)，可以在这里设置标注效果，`pre`代表前缀，`suf`代表后缀。

比如这里的设置表示：不给用红色下划线和蓝色波浪线标注的部分添加前缀和后缀、给橙色背景色标注的部分添加前后缀`**`，也就是给它加粗。如果你想要将红色下划线标注的部分设置为Markdown格式的下划线内容，只需要将`style1`设置为`style1 = {'pre': "<u>",   'suf': "</u>"}`，也就是给它添加Markdown中的下划线标签。

变量`thought_style`、`hotmarks_number`类似，分别用于设置想法和热门标注人数的前后缀。

## 补充

项目托管于[GitHub](https://github.com/liuhao326/pythontools/tree/master/wereader)

如果gif动画没有播放，可以先打包下载再打开Markdown。

欢迎PR和star，有什么问题也可以提 issue。