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
    
    JsSIP在要用socket发送/接受数据时可调用本方法。
    
    当socket准备好的时候会调用onconnect事件操作,失败或不可用时会调用ondisconnect事件
    
    disconnect() //断开
    
    JsSIP在要当下不需要socket时可调用本方法.本方法之后的时间操作不会执行
    
    send(data) //发送数据
    
    JsSIP需要发送指定数据时可调用本方法
    
    Parameters参数 
    
        data:字符串类型,指要发送的数据

Events //事件
    
    onconnect() //连接
    
    在connnect()被调用之后,socket可以接发数据时发生,或者有断开请求时发生
    
    ondisconnect(error, code, reason) //断开
    
    在socket不能收发数据时发生
    
    Parameters参数 
    
        error:布尔类型,表明断开是否是有一个错误导致的
        
        code:数值型,socket断开码
        
        reason:字符串类型,socket中断原因
        
    ondata(data)//数据传输
    
    jsSIP要处理一个完整的SIP消息时发生
    
    Parameters参数 
    
        data:二进制字符串,表示数据
    
    
   