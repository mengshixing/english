chrome.storage  中文文档

chrome.storage  //谷歌浏览器存储
    描述: 使用chrome.storage API 来存储,检索,跟踪用户数据改变
    支持: chrome 20以上版本
    权限: "storage"   //ps:在manifest.json文件中声明 "permissions": [ "http://*/*", "https://*/*", "storage" ]
    内容脚本: 完全支持

ps: Content Scripts是在Web页面内运行的javascript脚本。通过使用标准的DOM，它们可以获取浏览器所访问页面的详细信息，并可以修改这些信息。
    下面是content scipt可以做的一些事情范例:
    从页面中找到没有写成超链接形式的url，并将它们转成超链接
    放大页面字体使文字更清晰
    找到并处理DOM中的microformat

chrome.storage综述
    本API实现了扩展程序所需的存储特性优化,可以和localStorage API一样用来存储,但是有以下几点不同之处:
    
    用户数据可以通过storage.sync自动同步
    引入的扩展脚本可以直接存取用户数据不需要后台页面
    用户的扩展程序在隐身模式下也可以使用
    大量的读写操作会异步执行，因此快于阻塞,串行的localStorage API.
    用户数据可以以对象格式存储(the localStorage API存储的是字符串)
    管理员配置的扩展程序配置可以通过storage.managed模式读取

Manifest //配置清单

	你必须在扩展程序的配置(manifest.json)中声明"storage"权限,才能使用storage API.示例:
	{
        "name": "My extension",
        ...
        "permissions": [
          "storage"
        ],
        ...
	}