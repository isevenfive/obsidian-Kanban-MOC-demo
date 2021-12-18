# obsidian-Kanban-MOC-demo（编辑中）
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
2. 再结合例程讲讲插件的开发流程，代码及对应的功能
3. 最后展示我开发的插件的完整使用

# 一、obsidian 插件开发上手

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

看完之后就大致明白如何创建一个命令等等（就是抄代码）

## 4、hot-reload 插件辅助开发

**现在总结下开发流程**：

1. 在插件文件夹下 npm i（仅需设置一次）
2. 然后 npm run dev，这会实时监测 ts 文件变化并将其编译成 js文件
3. 编辑 main.ts 文件
4. 保存更改，最后去obsidian重新加载开发中的第三方插件，然后就可以看到更改

第 4 步手动重载插件比较麻烦，所以可以用 [hot-reload](https://github.com/pjeby/hot-reload) 这款 obsidian 插件来实现自动重新加载发生变化的插件。
当装上这款插件后，开发流程就变成了下面这样：

1. 在插件文件夹下 npm i（仅需设置一次）
2. 手动安装 [hot-reload](https://github.com/pjeby/hot-reload) 插件并启用（仅需设置一次）
3. 然后 git init（仅需设置一次）（需要安装 git），只有这样 hot-reload 才会重载该插件。
4. 然后 npm run dev，这会实时监测 ts 文件变化并将其编译成 js文件
5. 编辑 main.ts 文件
6. 保存更改，最后去obsidian就可以看到更改

现在就可以不用手动重载开发的插件了。

# 二、结合例程讲讲如何开发插件

## 先定一个小目标😉（功能需求）

假设现在我想开发个简单的插件，名字就叫：demo-simple-plugin
我希望这个插件具有以下功能：

1. 有一条**命令**，且当我调用这条命令时，它会同时弹出一条通知和一个面板
   1. **通知**：展示一句**欢迎语**
   2. **面板**：展示**当前打开的文档的一些相关信息**
2. 还有一个**设置面板**，我可以在里面**自定义通知的欢迎语**。

好，现在开始开发。 

## 1、下载、解压官方插件示例

假设已经安装 hot-reload 插件了，然后在下载的官方插件示例中 npm i、git init、npm run dev

我把这个插件文件夹更名为插件名：demo-simple-plugin

接下来用 vscode 打开这个插件文件夹

![image-20211218105648333](attachments/image-20211218105648333.png)

## 2、编辑插件信息：manifest.json

obsidian 会识别这个文件作为插件信息（很简单就不多说了）

![image-20211218110843695](attachments/image-20211218110843695.png)

然后在obsidian中找到启用该插件：

![image-20211218111026620](attachments/image-20211218111026620.png)

## 3、⚠️重点：编辑 main.ts 文件

使用 vscode 打开 main.ts 文件。

前面提到了 main.ts 的大致结构：
![image-20211218015329845](attachments/image-20211218015329845.png)

### 设置变量：MyPluginSettings

根据功能需求可知，欢迎语需要能够自定义，所以欢迎语肯定是要保存的。

根据上图，我们很容易能够看到应该在哪里设置变量：
![image-20211218111330450](attachments/image-20211218111330450.png)

将欢迎语设置为变量：welcomeStr，并赋默认值："欢迎来到 obsidian"
也就是下面这样：
![image-20211218111511560](attachments/image-20211218111511560.png)

❓那么这个变量怎么被调用加载呢？
详见：[加载设置 loadSettings](#加载设置 loadSettings)

❓又是怎样修改个变量的值呢？
详见：[保存设置 saveSettings](#保存设置 saveSettings)

### 编写插件设置面板：PluginSettingTab

注意：这里只是编写插件设置面板，除此之外还需要在 [插件启用 onload](#⚠️插件启用 onload) 中把该面板添加到设置里去

先看下原来的设置页面：
可以看到这个设置页面的内容有一个h2标题、一个设置项。
![image-20211218112053158](attachments/image-20211218112053158.png)

我们要把原来的mySetting改成我们刚刚设好的 welcomeStr，如下图所示：
![image-20211218121117757](attachments/image-20211218121117757.png)

### 插件：Plugin

插件程序的大致结构如下图：我们主要编程的位置是 **async onload()**，其它 3 个了解即可。![image-20211218112853269](attachments/image-20211218112853269.png)

#### ⚠️插件启用 onload()

这里就是主要编程的地方了，你将在这里进行命令、侧边按钮、底部状态栏、设置面板、事件监听等等的添加。

下面我们要在这里添加：

- 一条命令：弹出通知、面板
- 一个设置面板：刚才我们已经编写过插件设置面板了，在这里要做的是把编辑好的面板添加到插件中去

##### 添加一条命令并令其发出通知

先让它发出通知，通知内容为我们设置的欢迎语：welcomeStr。
copy 官方的示例代码自己改下：
![image-20211218122342173](attachments/image-20211218122342173.png)

保存去 obsidian 点击 Ctrl+P 调查命令，可以看到已经有我们刚才改动的新命令了：
![image-20211218122533105](attachments/image-20211218122533105.png)

点击命令会看到obsidian右上角出现通知，通知内容为我们设置的默认值：
![image-20211218122638613](attachments/image-20211218122638613.png)

##### 为该命令添加弹出面板



#### 插件禁用 onunload()

> 你可以在这里设置一些动作，当插件被禁用时会执行

#### 加载设置 loadSettings()

❓设置变量怎么被加载的呢？

回到刚才的设置变量，右键 DEFAULT_SETTINGS，查看谁引用了它
![image-20211218112504593](attachments/image-20211218112504593.png)

页面会跳到加载设置 loadSettings()：
可以看到加载设置里除了 DEFAULT_SETTINGS 外，还有个 loadData() 的值，它们被赋值给 this.settings。
其中的 loadData() 加载的是保存设置时生成的 data.json 文件。
![image-20211218112653866](attachments/image-20211218112653866.png)

❓设置变量又是什么时候被加载呢？即什么时候调用的这个 loadSettings()？

同样右键转到引用：
可以看到在插件被加载的时候会调用加载设置。![image-20211218115011157](attachments/image-20211218115011157.png)

#### 保存设置 saveSettings()

可以看到是把 this.settings 保存到生成的 data.json。
![image-20211218120647167](attachments/image-20211218120647167.png)

❓那么什么时候保存设置呢？即什么时候会调用 saveSettings() 呢？
同样跳转到引用：可以看到设置面板中的设置项的文本发生变化（onChange）时会调用 savaSettings() 来保存设置。
（当然你也可以根据自己的程序来调用保存设置）![image-20211218114210610](attachments/image-20211218114210610.png)



# 参考链接

[（转载）Obsidian 开发相关（简单引导） - 开发讨论 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/148)
