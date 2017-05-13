JsSIP.Socket interface //JsSIP.Socket 接口

    Socket接口抽象了jsSIP提供的SIP发送/接受通信机制,JsSIP内部通信处理通过Socket接口协议
    
    它不附着内置的WebSocket作为一个通信socket.使用时必须遵循接口规定,来满足JsSIP的底层传输机制
    
    JsSIP暴露了一个内置的JsSIP.WebSocketInterface类在浏览器环境下执行本接口
    
    Node.js的可用工具可通过:jssip-node-websocket.
    
Instance Attributes //实例属性

    via_transport //传输通道
    
    字符串类型,表示呼出请求时,在通信头字段的传输使用的通道(ex:tcp)
    
    url //地址
    
    字符串类型,表示socket地址,用于调试目的
    
    sip_url /sip地址
    
    字符串类型,表示连接终端的sip地址。SIP路由头字段使用
    
Instance Methods //实例方法

    connect() //连接
    
    