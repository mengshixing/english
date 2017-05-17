jssip-node-websocket

    是基于nodejs的websocket模块的JsSIP.Socket接口.
    
    本模块保证的JsSIP可以在nodejs运行下使用websocket，把这部分代码从JsSIP模块分离出去的目的在于
    
    防止nodejs的websocket模块在浏览器环境下编译
    
Documentation and examples //文档&示例

Installation //初始化 

    npm install jssip-node-websocket --save
    
Requirements //环境

    jssip >= v2.0.0
    Node.js>= v4.0.0
    
Usage //用法

    const JsSIP = require('jssip');
    const NodeWebSocket = require('jssip-node-websocket');

    let socket = new NodeWebSocket('wss://foo.example.com');

    let ua = new JsSIP.UA(
    {
        uri          : 'sip:alice@example.com',
        password     : 'xxxxxxxx',
        display_name : 'Alice',
        sockets      : [ socket ]
    });

API
    
    本模块提供了一个符合JsSIP.Socket接口规范的NodeWebSocket类
    
    var socket = new NodeWebSocket(url, [options])
    
    url (String): The WebSocket URL//
    
    options (Object):包含origin, headers, requestOptions,clientConfig等字段,和websocket.W3CWebSocket
    
    的构造函数参数对应的格式意义是一致的
    
FAQ 

    如何绕过TLS证书/认证(Transport Layer Security 传输层安全协议)
    
    var socket = new Socket('wss://foo.example.com',
    {
        origin: 'https://www.example.com',
        requestOptions :
        {
          agent : new https.Agent({ rejectUnauthorized: false })
        }
    });
  
  