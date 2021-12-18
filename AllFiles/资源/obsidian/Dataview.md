
[Dataview官方文档](https://blacksmithgu.github.io/obsidian-dataview/)

DataviewJs 使用还是挺方便的，这里的[[选中文档相关资源项目-模板]]和[[未引用文档-模板]]就是用 DataviewJS 实现的。

原理就不说了。

# 小窍门

如果在多个地方需要设置相同的 dataviewjs 代码，当代码出现问题时修改代码是个要命的问题，所以推荐把 dataviewjs 代码写在一个模板文件里，然后使用 `![[模板]]` 来引用模板，这样的话代码需要修改时非常方便。这里的[[选中文档相关资源项目-模板]]和[[未引用文档-模板]]就是引用的模板。
![[Pasted image 20211218005238.png]]

# 问题

有时候 Dataview 的刷新会出问题，像下面这样明明 Dataview 已经被 obsidian 引用了，但是DataviewJs 模板“未引用文档”还是显示该文件未被引用。
![[Pasted image 20211218005654.png]]
这时候可以尝试重启 obsidian，重启后可以看到显示正常了：
![[Pasted image 20211218005832.png]]