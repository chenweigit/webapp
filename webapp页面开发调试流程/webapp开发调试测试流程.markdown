# webapp开发调试测试流程

标签（空格分隔）： webapp
-------------------------


现在我们开发模式是这个样子：

> 先把本地的网页上传到远程服务器（因为好多设备都要去访问一个固定的地址），然后将网址输入到各个测试机的测试浏览器里面手动打开(或者使用浏览器插件等，生成二维码扫一下）。然后手机开始下载页面，需要等待下载。观看效果进行测试，每个测试机都要操作一遍。测试其他网页的时候，每个测试机重新输入网址、刷新。如果代码有修改，需要重新上传服务器进行刷新。

我希望是这个样子
> 在我的前面有两显示器，一边是IDE写代码，一边是浏览器我正在开放的应用，此时桌上还有调试机，一般调试机越多表明你们公司越豪（牢骚一句而已不要在意）。现在我写了一段代码，CTRL+S后，接着你的手机和另一个显示器里的应用，就变成了更新后的效果。想象一下，PC和所有的手机、平板都同步变化，是不是像在看美国大片。其实就是在开放中少按F5刷新而已，但是效率提高了啊。

今天给大家介绍一个工具叫 [browsersync][1]
    
## 环境安装

### 1、安装node.js
browsersync是基于nodejs 的所以首先安装nodejs。这里是node官方网站 [请猛撮我][2]  安装自己系统相应的安装包。

### 2、安装 BrowserSync
  
     windows 安装指令: npm install -g browser-sync               /*我是注释 -g 是指安装到全局环境中 */ 
     mac安装指令: sudo npm install -g browser-sync 
     
-------------------------------
 如果无法使用 npm 安装 browsersync别担心，船到桥头直然直，有可能是大天朝的网络问题大家都懂得，那么可以使用 [淘宝 NPM 镜像][3] 使用简单说明：
使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:
    
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    cnpm install -g browser-sync
    
![browser安装成功][4]
这样就能正确的安装，如果还有问题，请再三检测代码或者问别人家的孩子吧。

## 如何使用

来举一个完整的栗子（前提是环境已经搭建好）：

- 第一步进入你项目的根目录：
   
        C:\Users\Administrator>cd D:\workspace\advert\我的项目                 
        
        C:\Users\Administrator>d:                                               
        
        D:\workspace\advert\我的项目>

- 第二步启动BrowserSync

        D:\workspace\advert\我的项目>browser-sync start --server  --files "**"
    下面是反馈结果：
    
        [BS] Access URLs:
         ------------------------------------
               Local: http://localhost:3000
            External: http://10.10.12.77:3000
         ------------------------------------
                  UI: http://localhost:3001
         UI External: http://10.10.12.77:3001
         ------------------------------------
 简单解释一下
    - browser-sync start --server 是启动他内置的一个服务器，  --files "**" 是指监听这个根目录下所有文件的变化。   
    - Local: http://localhost:3000 是本地浏览器访问的地址
    - External: http://10.10.12.77:3000 外部网络访问的地址，把手机连入到PC 同一个局域网里，首先在PC 上打开这个地址，使用插件（我这使用的是chrome 草料二维码）将网址生成二维码，手机扫描打开
    - UI: http://localhost:3001，它是BrowserSync提供的一个简易控制面板。BrowserSync最常用的几个配置选项，都可以在这个面板里调整。具体的使用说明就不在这里详解。温馨提示在面板里你还会发现远程调试工具 weinre
    - UI External: http://10.10.12.77:3001 雷同，远程控制面板谁去打开谁明白。
    
当然他会自动打开http://localhost:3000 这个地址。现在你可以尝试在你的编辑器里写代码，你会发现PC 和移动终端都会同步你所有的变化，再也不用去按F5了，当然如果你想详细了解BrowserSync参数请移步到他的[官网][5]。就这样完了？对就这么简单，如果我是要处理less，coffeescript，同时图片、CSS、script 文件压缩，版本控制,甚至是 .jsp 、.php 页面等怎么办？不用担心，到你项目的发布目录去执行 命令 browser-sync start --server  --files "**"。流程看下面这个图（这里我加了百度的FIS,如果没有用其他的服务器发布，你就把IDE工作空间当作为服务器空间）：
![这是图片][6]


  [1]: http://www.browsersync.io/
  [2]: https://nodejs.org/
  [3]: http://npm.taobao.org/
  [4]: http://showimg.oss-cn-shenzhen.aliyuncs.com/browsersyncinstall.png
  [5]: http://www.browsersync.io/
  [6]: http://showimg.oss-cn-shenzhen.aliyuncs.com/imgs/lct.png
