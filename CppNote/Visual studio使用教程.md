# VS 使用种存在的 问题

## 1 添加插件

如果你也使用Visual Studio学习C++，那么这里给你推荐一些扩展，能帮助我们学习C++

一、首先要安装微软自己开发的扩展：Productivity Power Tools 2017/2019。这是一个扩展套装，其中包含12个扩展(截至2019年6月）。只要安装这一个扩展套装，也就安装了其中包含的12个扩展。这12个扩展是：

1. Align Assignments
2. Copy As Html
3. Double-Click Maximize
4. Fix Mixed Tabs
5. Match Margin
6. Middle Click Scroll
7. Peek Help
8. Power Commands for Visual Studio
9. Quick Launch Tasks
10. Solution Error Visualizer
11. Shrink Empty Lines
12. Time Stamp Margin

二、安装CodeMaid

CodeMaid能够帮助我们在保存代码的时候，清理代码中无用的空格和空行

三、Open In Explorer

该扩展在解决方案管理器中添加了一些类似文件资源管理器的功能。只要在解决方案管理器中单击鼠标右键，在弹出菜单中就能看到“在资源管理器中打开文件夹”、“拷贝文件”等功能

四、Trailing Whitespace Visualizer

该扩展能够显示行尾无用的空格。当然，如果安装了CodeMaid扩展的话，在保存代码时，CodeMaid会自动将行尾五用空格删除

五、Viasfora

该扩展可以使程序中的成对匹配的大中小括号以不同的颜色显示，便于我们将括号的左右半边匹配

六、Visual Studio IntelliCode

基于机器学习的代码编写辅助工具。目前功能还比较弱。感兴趣可以尝尝鲜

七、PowerMode

敲键盘写代码的时候，字符会出现烟花效果。本课程中相当一部分示例都有该效果。

八、Snippetica

代码片段工具。按下特定的字符或者字符组合，然后按TAB键，Snippetica就会将该扩展中存储的一些代码片段直接粘贴到你的编辑器中。

该工具能比较有效地提升编码的速度。你可以尝试输入 forr 然后按tab键，它会自动将基于范围的for循环的框架代码贴到你的编辑器中。

九、VSColorOutput

该扩展与Output enhancer扩展的功能类似，但是比Output enhancer好用，所以如果同时安装了Output enhancer扩展的话，将其禁用即可

十、Smooth Scroll

让代码编辑器窗口的滚动更平滑。

十一、Word Higlight With Margin

当你用鼠标选中某个单词/标识符后，该扩展可以将所有的单词/标识符同时加亮显示。

这是一个非常有用的扩展

![img](https://edu-image.nosdn.127.net/E0A714F53FFE7F43864B78E39DB8AC14.JPG?imageView&thumbnail=890x0&quality=100)

![img](https://edu-image.nosdn.127.net/951137B296671EDB2F4F8661F1FBC807.JPG?imageView&thumbnail=890x0&quality=100)

![img](https://edu-image.nosdn.127.net/7D78675AC2C77DEBC9C38B779A593C06.JPG?imageView&thumbnail=890x0&quality=100)

![img](https://edu-image.nosdn.127.net/0E19CF8AFA9C4B8800123763CE321A27.JPG?imageView&thumbnail=890x0&quality=100)

![img](https://edu-image.nosdn.127.net/B9587B77039FF1A17E8B64F5248E86C7.JPG?imageView&thumbnail=890x0&quality=100)

## 2 配置语言标准

项目

​	 -- 属性

​		 -- C/C++

​			--C++语言标准（C++14/17/20）

​			--命令行 （其他选项 /Zc:__cplusplus）

## 3 运行当前项目

默认是单启动项目，右击解决方案-- 通用属性--启动项目--当前选定项目



