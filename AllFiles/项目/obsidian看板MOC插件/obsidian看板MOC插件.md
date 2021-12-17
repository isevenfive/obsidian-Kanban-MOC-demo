---

kanban-plugin: basic

---

## 🗃️信息

- [ ] [obsidian-Kanban-MOC: 自用插件 github](https://github.com/1657744680/obsidian-Kanban-MOC)
- [ ] [（转载）Obsidian 开发相关（简单引导） - 开发讨论 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/148)
- [ ] 记录第一次的[[obsidian]]插件开发
- [ ] ![[选中文档相关资源项目-模板]]
- [ ] ![[未引用文档-模板]]


## ⭕待做

- [ ] bug：手机端更新索引失效！<br>估计是文件写入write失效


## 🟢进行中



## ✔️已完成

**完成**
- [x] 添加功能：输入显示候选框
- [x] 开发完成后只需要保留以下 3 个文件：<br>- `main.js` 文件：主程序文件<br>- `manifest.json` 文件：插件信息<br>- `styles.css` 文件
- [x] 看板MOC插件开发……
- [x] 开发主要就是编辑 ts 文件。<br>看懂例程中的 ts 文件：<br>- **插件主程序**<br>	- **onload()**<br>- **插件创建一个命令**<br>- 插件创建侧边栏按钮<br>- 插件创建底部状态栏<br>- 插件全局事件监听<br>- 插件创建一个面板<br>- **插件设置面板**<br>- ……<br><br>上面几个加粗的比较重要。<br>对官方例程做点注释：[1657744680/obsidian-plugin (github.com)](https://github.com/1657744680/obsidian-plugin)
- [x] 用 VScode 开发
- [x] 下载并开启重载插件工具（开发的时候会监测文件变化并自动重新加载）：[hot-reload: Automatically reload Obsidian plugins in development when their files are changed (github.com)](https://github.com/pjeby/hot-reload)<br>需要在要开发的插件目录下：<br>`git init`
- [x] 下载并按介绍运行obsidian插件示例程序： [obsidian-sample-plugin](https://github.com/obsidianmd/obsidian-sample-plugin)<br>- `npm i`（第一次）<br>- `npm run dev`（每次开发时）




%% kanban:settings
```
{"kanban-plugin":"basic","show-add-list":false,"show-archive-all":false,"show-view-as-markdown":false,"show-board-settings":false}
```
%%