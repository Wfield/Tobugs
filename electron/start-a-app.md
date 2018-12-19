## 运行electron程序
- 在使用`npm`下载`electron`要安装在`devDependencies`下
- `package.json`中的`main`字段指定程序的启动文件。否则，即使在`scripts`字段中添加命令，如`electron index.js`也不会运行程序


## 对于electron的理解
- `main.js`文件的功能是使`electron`加载`html`页面, `html`文件中加载的`index.js`文件是问页面添加功能
- electron： 使用`chromium`来加载`html`文件，显示网页 *+* 使用`nodejs`运行`js`脚本

## electron中的进程 [参考链接](https://electronjs.org/docs/tutorial/application-architecture#%E4%B8%BB%E8%BF%9B%E7%A8%8B%E5%92%8C%E6%B8%B2%E6%9F%93%E5%99%A8%E8%BF%9B%E7%A8%8B)
- 两种进程类型：主进程和渲染进程
- 运行`package`中`main`脚本的进程是主进程,主进程创建`web`界面。一个`electron`应用只有一个主进程
- 每个`electron`中的`web`页面运行在它自己的**渲染进程**中

## electron中的remote
- `electron`通过`remote`模块暴露一些通常只能在主进程中获取到的`API`

## API

- 所有的`electron`的`api`都被指派给一种进程类型。许多`API`只能用于主进程，有些`API`只能被用于渲染进程，又有一些主进程和渲染进程中都可以使用
- 所有在`Node.js`中可以使用的`API`，在`electron`中（主进程和渲染进程）同样可以使用。并且可以使用外部模块（`npm`模块）

## APP
> 控制应用程序的事件生命周期
>> 进程：主进程

## `BrowserWindow`
> 创建和控制浏览器窗口
>> 进程：主进程
- `BrowserWindow`是一个`EventEmitter`
- 通过 ```new BrowserWindow(option)```创建一个实例
- 实例事件：
	+ close: 在**窗口**要关闭时触发
	+ closed: 窗口已经关闭时触发
	+ show：当窗口显示时触发
	+ hide：当窗口隐藏时触发
	+ ready-to-show：当页面已经渲染完成（但是还没有显示）时触发
	+ 
- ```BrowserWindow```类的静态方法
	+ getAllWindows(): 返回所有打开的窗口的数组
- 实例属性
	+ webContent：对象，所有与网页有关的事件和操作都将通过它完成**（webContent表示BrowserWindow的内容，即html显示的内容，和窗口是有区别的）**[参考链接](https://electronjs.org/docs/api/web-contents)
- 实例方法
	+ destory()：强制关闭**窗口**
	+ close()：尝试关闭窗口。与用户手动点击关闭窗口按钮效果相同
	+ show()
	+ hide()
	+ setEnable()
	+ loadURL(url,[option]): url可以是远程地址，也可以是本地```HTML```文件路径
	+ loadFile(filePath): filePath是```HTML``文件相对于应用跟目录的相对路径
	+ reload()

## webContent
> 渲染以及控制web页面
>>进程：主进程
