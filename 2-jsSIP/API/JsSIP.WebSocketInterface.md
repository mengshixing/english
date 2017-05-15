JsSIP.WebSocketInterface 

    JsSIP为浏览器环境内置的JsSIP.Socket接口
    
    socket可以自定义属性设置如果有必要的话
    
Instantiation //实例化 

    准备一个字符串参数表示WebSocket服务器地址
    
Attribute setters //属性配置

    via_transport(value)
    
    字符串类型,标志着呼出请求的头的传输方式的值
    
    Example //示例
    
    var socket = new JsSIP.WebSocketInterface('ws://sip-ws.example.com');
    
    socket.via_transport='tcp';
    
    configuration.sockets=[socket];
    
    var ua = new UA(configuration);