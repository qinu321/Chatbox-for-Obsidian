# Chatbox — Chat Styles CSS snippet for Obsidian

[English](./README_EN.md)

仅用CSS snippet就能让你的Obsidian展现对话流样式！
这就是Chatbox，一款专为Obsidian而写的CSS！


## 样式展示

一共有7种样式可选，全都使用超简单代码，可以随意自由切换，支持深浅色。
由于本身就是在Obsidian原生callout的代码上进行扩展的，所以可以在对话气泡框里支持各种markdown语法（比如添加图片、设置斜体、粗体、代码框等等）。
仅用css实现，样式十分持久，至少作者放置它两年了也没啥bug，几乎不会失效。

注：基础、bbs、pop的粗体和斜体的颜色为你自己的Obsidian的设置色。且所有的颜色都可以在安装了“[Style Settings](https://github.com/community-archive/obsidian-style-settings)”插件后自由调节！


### 基础+首行为右

![](./Image/Snipaste_2026-09-10_11-44-34.jpg)
![](./Image/Snipaste_2026-09-10_11-48-18.jpg)

### 基础+首行为左

![](./Image/Snipaste_2026-09-10_11-44-48.jpg)
![](./Image/Snipaste_2026-09-10_11-48-29.jpg)

### bbs

![](./Image/Snipaste_2026-09-10_11-44-55.jpg)
![](./Image/Snipaste_2026-09-10_11-48-38.jpg)

### pop

![](./Image/Snipaste_2026-09-10_11-45-05.jpg)
![](./Image/Snipaste_2026-09-10_11-48-47.jpg)

### wechat

![](./Image/Snipaste_2026-09-10_11-45-15.jpg)
![](./Image/Snipaste_2026-09-10_11-48-59.jpg)

### qqchat

![](./Image/Snipaste_2026-09-10_11-45-24.jpg)
![](./Image/Snipaste_2026-09-10_11-49-09.jpg)

### 邻舍

[邻舍是啥哦](https://github.com/icecranberry/galgame-with-comfyUI)

![](./Image/Snipaste_2026-09-10_11-45-33.jpg)
![](./Image/Snipaste_2026-09-10_11-49-18.jpg)

### Baker

对、就是模仿终末地里的Baker

![](./Image/Snipaste_2026-09-10_11-45-43.jpg)
![](./Image/Snipaste_2026-09-10_11-49-26.jpg)

### 基础+无名字+无头像+无标题

搭配组合一些超简单代码，你甚至能实现这样的样式！

![](./Image/Snipaste_2026-09-10_11-50-18.jpg)


## 安装方法

下载releases里的zip包，解压后：
1. 把Css文件夹里的`chatbox.css`和`chatbox-inputbox.css`复制粘贴到你的Obsidian的`CSS 样式代码片段` 文件夹内（可以点设置-外观-CSS  样式代码片段，点击那个文件夹按钮）
一般就是你库的`.obsidian\snippets`
然后在设置-外观-CSS  样式代码片段里把`chatbox`和`chatbox-inputbox`启用。

2. 把`Chat Generator`整个文件夹放入库的根目录，在Obsidian里查看样本笔记的样式是否有生效


## 强烈推荐安装的插件

[Dataview](https://github.com/blacksmithgu/obsidian-dataview)
[Style Settings](https://github.com/community-archive/obsidian-style-settings)

装完dataview后，需要启用`enable JavaScript queries`选项
让它支持dataviewjs代码，这样对话生成器就能正常使用了。

Style Settings里则有着Chatbox的超丰富设置细节！
你可以按照喜好设置对话框大小，气泡颜色，背景颜色，文本粗体和斜体颜色，且几乎每种样式都能单独设置


## 对话生成器（Chat Generator）

能在Obsidian里直接运行的小程序，可以帮助你无需记住任何代码就能生成Chatbox用的对话流文本格式。
功能十分简单直白，想要什么样式自己选就行，添加角色头像的方法在[01-对话角色表-中文](./Chat%20Generator/02%20Material/Character/01-%E5%AF%B9%E8%AF%9D%E8%A7%92%E8%89%B2%E8%A1%A8-%E4%B8%AD%E6%96%87.md)里有详细说明，可以去看看。

点击头像就会出现角色对话框，输入文字按回车就会生成ta的对话
![](./Image/Snipaste_2026-09-10_12-37-26.jpg)

点开编辑框，你甚至能直接拖动排序、更改反向位置、切换角色（点击角色头像就能替换角色）等等
![](./Image/Snipaste_2026-09-10_12-38-49.jpg)

点开代码框，可以直接粘贴已有的对话代码，方便用生成器修改
![](./Image/Snipaste_2026-09-10_12-39-04.jpg)

你甚至可以在代码框里直接写角色的对话（不需要名字）
比如
```markdown
一个标题
测试一下
好哦
懒得想对话了
真懒啊作者
```
然后勾上`作为对话输入`后按输入按钮
代码框就会直接变成
```markdown
> [!chatbox]+ 一个标题
> - 测试一下
> - 好哦
> - 懒得想对话了
> - 真懒啊作者
```
接着用编辑框添加角色和改变方向就行

搞完对话之后，点击预览上方的最后一个按钮，就能在设定的文件夹里生成笔记
默认模板里有能被生成器直接替换的变量，修改模板时可以照着使用。

![](./Image/Snipaste_2026-09-10_08-47-21.jpg)

只想复制则可以去最后的代码预览框那里，有Obsidian原生的复制按钮。


## 可以删除的部分

01 Chat Notes下的所有样本笔记
02 Material/Character下的对话角色表（建议直接修改而不是删除）
02 Material/Icon下的全部头像（都是我家OC，不用的话可以全部删除）
02 Material/Template/Chat Template.md（可以改成你自用的模板，因为有替换变量所以更建议直接修改而不是删除）

如果你修改了对话生成器的文件夹位置，那么上述这些文件夹也能被删除。


## 代码介绍

你其实完全不需要记这些！不过可以稍微了解一下

```markdown
> [!chatbox|wechat]+ 对话标题
> - ![face](http://头像图片链接.jpg) *名字A* 一段对话
> + ![face](支持本地图片) *名字B* 一段对话
> - ![[本地图片也能这么写|face]] *名字A* 一段对话？……一段对话？*（斜体样式）*
> + ![[xxx.png|face]] *名字B* 一段对话……一段对话 **粗体样式**!!!
> 
> 旁白对话
> - ![face](http://头像图片链接.jpg) *名字A* 一段对话
> 会接在A上面的对话气泡框里
> - A的对话但只有气泡没有名字和头像
> + ![face](支持本地图片) *名字B* 一段对话
> 
> 想要显示成旁白必须空出一行
> 
```

需要注意的是'-'和'+'只是表示这两个对话框的方向会不同，但完全不固定位置，开头是左还是右只看有没有加swap。

```markdown
> [!chatbox|wechat-swap]+ 对话标题
> - ![face](http://头像图片链接.jpg) *名字A* 一段对话
> + ![face](支持本地图片) *名字B* 一段对话
> - ![[本地图片也能这么写|face]] *名字A* 一段对话？……一段对话？*（斜体样式）*
> + ![[xxx.png|face]] *名字B* 一段对话……一段对话 **粗体样式**!!!
```


样式值有7种，每次只能用1种：普通（什么都不加）、bbs、pop、wechat、qqchat、linshe、baker。

```markdown
> [!chatbox|bbs]
```

属性值有9种，可以任意复数叠加：notitle、fix、short、frame、noname、noface、long、point、htmltag

```markdown
> [!chatbox|notitle-fix-short-frame-noname-noface-long-point-htmltag]
```

swap的水很深，推荐用生成器自动生成，你手写如果带旁白的话，会有一些规则来确保对话框方向正确。
因为旁白其实也占用一行方向，且相当于跟上面的对话是不同方向的，此时如果想接不同方向的对话，则必须让旁白变成偶数行，我常用的方法是加个不会显示的`> \n> <span></span>`来调节行数。

比如下面这种实际显示时，A和B其实都在左边

```markdown
> [!chatbox]+ 对话标题
> - ![face](http://头像图片链接.jpg) *名字A* 一段对话
> 
> 旁白对话
> + ![face](支持本地图片) *名字B* 一段对话
```

只有改成这样才会正确显示成两边

```markdown
> [!chatbox]+ 对话标题
> - ![face](http://头像图片链接.jpg) *名字A* 一段对话
> 
> 旁白对话
> 
> <span></span>
> + ![face](支持本地图片) *名字B* 一段对话
```

当然你其实**实际完全不需要记这些**！使用**对话生成器**，轻松就能自动生成chatbox的代码！