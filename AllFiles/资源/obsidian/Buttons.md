主要是使用这个插件来调用我的看板MOC插件的命令：
```
	```button  
	name 新建项目
	type command  
	action 看板MOC: 创建新项目
	```
```

以下两个文档里就是资源、项目的操作指令按键：

这个插件只有 inline button 可以在 Kanban 里渲染，但是点击没用……

# 带id button，下列内容勿删！！
> 用于 inline button

```button
name 新建资源
type command
action 看板MOC: 创建新资源
color blue
```
^button-newRes

```button
name 新建项目
type command
action 看板MOC: 创建新项目
color blue
```
^button-newPrj

```button  
name 更新索引
type command  
action 看板MOC: 更新索引
```
^button-updateMOC