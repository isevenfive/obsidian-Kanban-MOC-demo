# obsidian-Kanban-MOC-demo
看板MOC插件的演示库。

直接下载解压使用 obsidian 打开。

插件：[obsidian-Kanban-MOC](https://github.com/1657744680/obsidian-Kanban-MOC)

# 前言

本人菜鸡，对 JavaScript 的了解就只有最基础的知识，代码写的也很烂，大佬勿喷。
希望这个教程能方便大家了解 obsidian 插件的开发流程，我个人感觉有点编程基础的话，做个简单的插件还是挺容易上手的。

这个展示库有两个目的：

1. 记录一个初次的 obsidian 开发过程
2. 展示这个开发的插件的功能、使用方法

下面就两个目的进行叙述：

1. 先叙述 obsidian 插件的开发上手
2. 再简介我的这个插件的开发流程，代码及对应的功能
3. 最后展示我开发的插件的完整使用

# obsidian 插件开发上手

## 1、尝试下载插件示例并在obsidian中启用

1. 下载并解压[插件示例](https://github.com/obsidianmd/obsidian-sample-plugin)，并将其放在 obsidian 库（可以新建、复制一个库用来开发）的插件文件夹下
2. 自行下载 node.js，配置好开发环境
3. 进到插件示例文件夹下，使用 `npm i` 命令安装依赖（只用整一次）
4. 接下来要使用命令：`npm run dev` 会实时监测文件变化，将 `main.ts` 文件编译成 `main.js` 文件
5. 编译完成后这时就可以在 obsidian 中启用该插件了。

## 2、插件示例文件结构

先来看插件示例文件的结构：

![image-20211218013344807](attachments/image-20211218013344807.png)

标红的是几个重要的文件，需要开发者进行编辑的主要就是以下 3 个文件：

- main.ts
- manifest.json
- style.css

重中之重肯定就是 main.ts 文件了，接下来开始看 ts 文件

## 3、用 vscode 打开插件示例

我在main.ts中写了点儿注释（我也不知道对不对），已经上传到GitHub了，有兴趣的可以瞅瞅：[obsidian-plugin-sample-notes (github.com)](https://github.com/1657744680/obsidian-plugin-sample-notes)。下载后解压同样放在obsidian的插件文件夹下，然后 `npm run dev`。

这是 main.ts 的总体结构：

![image-20211218015329845](attachments/image-20211218015329845.png)

点开详细看，我在[obsidian-plugin-sample-notes (github.com)](https://github.com/1657744680/obsidian-plugin-sample-notes)里面写了些注释，例如：

![image-20211218020011563](attachments/image-20211218020011563.png)

看 main.ts 文件，自己改改参数，然后重新加载 obsidian 中的该插件，看在 obsidian 中会有什么变化。

看完之后就大致知道了如何创建一个命令等等（就是抄代码）

## 4、结合例程讲讲如何开发

假设现在我想开发个插件，我希望这个插件具有以下功能：

- 有一条命令，且当我调用这条命令时，它会同时弹出一条通知和一个面板
  - 通知：展示一句欢迎语
  - 面板：展示当前打开的文档的一些相关信息
- 还有一个设置面板，我可以在里面设置这条欢迎语。

好，现在开始开发。

# 参考链接

[（转载）Obsidian 开发相关（简单引导） - 开发讨论 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/148)
