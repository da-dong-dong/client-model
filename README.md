# 下载器
一个使用vue作为前端页面，通过electron集成方式的下载器
![erp-cloud-download text](https://github.com/da-dong-dong/erp-cloud-download/blob/master/MD_imgs/1.png)
``` javascript 
// background.js

}
```
##### 安装方式
yarn install
##### 运行方式
yarn run electron:serve
##### 打包方式
yarn run electron:build
## 必备知识
node.js  vue.js  electron 
### 1，background.js 主程序
##### 1，注册本地协议
``` javascript 
// background.js
// 本地文件协议
protocol.interceptFileProtocol('file',(request, callback) => {
        const url = request.url.substr(6)
        log.debug(`本地文件协议:${this.pathStr}/${url}`)
        callback({ path: path.normalize(`${this.pathStr}/${url}`) })
        //本地文件协议:D:\lyfz\aaa\erp-cloud-download\dist_electro//lyfz-erp-cloud-download/loading/index.html
        // callback(fs.createReadStream(path.normalize(`${__dirname}/${url}`)))
    },
    error => {
        console.log(error)
    },
)
}
```

##### 2，注册全局快捷键
``` javascript 
// background.js
// 注册打开调试快捷键
globalShortcut.register('ctrl+d+b+n', () => {
    this.win.webContents.openDevTools();
})
```

##### 3，是否启动多个线程
``` javascript 
// background.js
//判断关闭多个线程
const gotTheLock = app.requestSingleInstanceLock()
if (!gotTheLock) {
    app.quit()
}else{
    // 你的程序
}
```

##### 4，托盘
``` javascript 
// background.js
//实例化托盘
appTray = new Tray(iconPath);

//图标的上下文菜单
const contextMenu = Menu.buildFromTemplate(trayMenuTemplate);

//设置此图标的上下文菜单
appTray.setContextMenu(contextMenu);

//我们这里模拟桌面程序点击通知区图标实现打开关闭应用的功能
appTray.on('click', ()=>{ 
    this.win.isVisible() ? this.win.hide() : this.win.show()
    this.win.isVisible() ?this.win.setSkipTaskbar(false):this.win.setSkipTaskbar(true);
})
```

##### 5，创建窗口
``` javascript 
this.win = new BrowserWindow({
      minWidth: 516,
      minHeight: 384,
      width: 1024,
      height: 768,
      fullscreen: false,
      frame: false,//无边框窗口
      show: false, // 先隐藏
      webPreferences: {
        // Use pluginOptions.nodeIntegration, leave this alone
        // See nklayman.github.io/vue-cli-plugin-electron-builder/guide/security.html#node-integration for more info
        nodeIntegration: true,
        nodeIntegrationInWorker: true,
        webSecurity: false
      },
    })
```

#### 6，热更新
``` javascript 
import AppUpdate from './update.js';
// 调用自动更新
const feedUrl = "服务器地址";
const appupdate = new AppUpdate(this.win, feedUrl);
```

#### 7，fileRow 
1，文件查询
2，文件写入
3，托盘事件
4，监听回调事件

#### 8，并发下载
1，bagpipe模块
2，http模块请求数据
3，节流传递给渲染进程

### 目录结构
home.js 
项目时间不够充分，前端没有优化，没有进行模块化组件拆分，功能都可以正常使用




### 打包设置


a、需要提前下载一下文件：

   版本号  [electron-v15.3.5-win32-x64.zip](https://registry.npmmirror.com/binary.html?path=electron/v15.3.5/)

   版本号  [winCodeSign-2.6.0.7z](https://registry.npmmirror.com/binary.html?path=electron-builder-binaries/winCodeSign-2.6.0/)

   版本号  [nsis-resources-3.4.1](https://cdn.npmmirror.com/binaries/electron-builder-binaries/nsis-resources-3.4.1/nsis-resources-3.4.1.7z)

b、将上述下载好的文件分别添加到对应的文件夹下

C:\Users\Administrator\AppData\Local\electron-builder\Cache\electron
C:\Users\Administrator\AppData\Local\electron-builder\Cache\winCodeSign
C:\Users\Administrator\AppData\Local\electron-builder\Cache\nsis



### 下载 electron-v9.4.4-win32-ia32.zip
https://npm.taobao.org/mirrors/electron/9.4.4/electron-v9.4.4-win32-ia32.zip
解压放到 C:\Users\Admin\AppData\Local\electron-builder\Cache 目录下

### 下载 winCodeSign
https://npm.taobao.org/mirrors/electron-builder-binaries/winCodeSign-2.6.0/
解压放到C:\Users\Admin\AppData\Local\electron-builder\Cache\winCodeSign\winCodeSign-2.6.0目录下（没有的话，自己创建winCodeSign-2.6.0）
 
### 下载/nsis-3.0.4.1
⨯ Get "https://github.com/electron-userland/electron-builder-binaries/releases/download/nsis-3.0.4.1/nsis-3.0.4.1.7z": dial tcp 52.74.223.119:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.

https://npm.taobao.org/mirrors/electron-builder-binaries/nsis-3.0.4.1/
解压放到C:\Users\Admin\AppData\Local\electron-builder\Cache\nsis\nsis-3.0.4.1 目录下（没有的话，自己创建nsis-3.0.4.1）
