Class JsSIP.UA  //UA类文档 是jsSIP的核心类

Instantiation //初始化

    一个UA需要和一个SIP账户关联,初始化时需要配置一些参数,这些参数可以写到一个JS对象中,详见 UA Configuration Parameters列表
    如果必须的参数缺少或者参数值不正常会抛出异常（CONFIGURATION_ERROR）
    
    var socket = new JsSIP.WebSocketInterface('wss://sip.example.com');
    var configuration = {
      sockets : [ socket ],
      uri     : 'sip:alice@example.com',
      ha1     : '350fe29ce3890bd85d105998b0a95cf7',
      realm   : 'sip.example.com'
    };

    var ua = new JsSIP.UA(configuration);

Instance Methods //实例方法

    start()
    
    连接到信令服务器并且恢复到之前的状态(如果之前停止的话),新的start的话,如果UA的注册参数值为true,会注册一个SIP域名
    
    stop()
    
    保存当前注册状态并且会在注销之后断开与信号服务器的连接。终止活动的会话
    
    register()
    
    注册UA,如果UA的注册参数值为true,会自动注册
    
    unregister(options=null)
    
    注销UA
    
    Parameters 参数：
        
        options :扩展的参数选项
        
        all:布尔类型,用来注销SIP用户所有的绑定,默认值false
        
        var options = {
          all: true
        };
        ua.unregister(options);
    
    registrator()
    
    有单独的页面介绍

    call(target, options=null) //发起请求
    
    发起一个多媒体呼叫
    
    Parameters 参数：
        
        target:呼叫地址,字符串类型,可以是目标用户名或者一个完整的SIP url或者是一个JsSIP.URI实例
        options：扩展参数配置对象，列表如下
        
            mediaConstraints:object类型,含video和audio2个可配置布尔参数,来标识着会话约束是视频 和/或 音频,默认值都为true.
            
            mediaStream:流类型，将流传送到其它终端
            
            pcConfig:object类型,RTCPeerConnection的RTCConfiguration(配置清单)
            
            rtcConstraints:object类型,RTCPeerConnection的约束
            
            rtcOfferConstraints:object类型,RTCPeerConnection约束的createOffer()方法
            
            rtcAnswerConstraints:object类型,RTCPeerConnection约束的createAnswer()方法(被用来下次接受请求或者用来更新SDP)
            
            eventHandlers:事件处理对象,可以在call过程各个事件定义响应操作及回调
            
            extraHeaders:字符串数组，扩展发送SIP请求的头
            
            anonymous:布尔类型，标志着call是否匿名,默认值是false
            
            sessionTimerExpires:时间(秒),设置默认的会话时间间隔(默认90,不能低于90)
            
        示例：
        
        // HTML5 <video> elements in which local and remote video will be shown H5标签显示本地和远程视频
        var views = {
          'selfView':   document.getElementById('my-video'),
          'remoteView': document.getElementById('peer-video')
        };

        // Register callbacks to desired call events //声明call的回调事件
        var eventHandlers = {
          'progress':   function(data){ /* Your code here */ },
          'failed':     function(data){ /* Your code here */ },
          'confirmed':  function(data){ /* Your code here */ },
          'ended':      function(data){ /* Your code here */ }
        };

        var options = {
          'eventHandlers': eventHandlers,
          'extraHeaders': [ 'X-Foo: foo', 'X-Bar: bar' ],
          'mediaConstraints': {'audio': true, 'video': true},
          'pcConfig': {
            'iceServers': [
              { 'urls': ['stun:a.example.com', 'stun:b.example.com'] },
              { 'urls': 'turn:example.com', 'username': 'foo', 'credential': ' 1234' }
            ]
          }
        };

        ua.call('sip:bob@example.com', options);

    sendMessage(target, body, options=null) //发送消息

    发送即时信息通过SIP方式
    
    Parameters 参数：
        
        target:呼叫地址,字符串类型,可以是目标用户名或者一个完整的SIP url或者是一个JsSIP.URI实例
        
        body:字符串,消息主体,消息内容
        
        options：扩展参数配置对象，列表如下
        
            contentType:字符串,消息主体的格式,默认 text/plain
            
            eventHandlers:事件处理对象 JsSIP.Message过程各个事件定义响应操作及回调   
            
            extraHeaders:字符串数组，扩展发送SIP消息请求的头
            
        示例：
        
        var text = 'Hello Bob!';

        var eventHandlers = {
          'succeeded': function(data){ /* Your code here */ },
          'failed':    function(data){ /* Your code here */ };
        };

        var options = {
          'eventHandlers': eventHandlers
        };

        ua.sendMessage('sip:bob@example.com', text, options);

    terminateSessions(options=null) //终止回话

    停止正在进行的会话
    
    Parameters 参数：
    
        options：扩展参数配置对象，详见JsSIP.RTCSession呼叫中止APL
        
    isRegistered() //是否注册

    如果UA已经注册,返回true,否则返回false
    
    isConnected() //是否连接

    如果传输已经见了连接返回true,否则返回false
    
    get(parameter) //获取参数值根据参数名
    
    获取运行时参数的值,一般可以获取到realm和ha1的值
    
    Parameters 参数：UA配置的参数名
    
    set(parameter, value) //设置参数值
    
    更新UA配置参数的值(运行时),一般来说只有display_name, password, realm 和 ha1 可以更新值
    更新成功会返回true
    
    parameter 参数：UA配置的参数名
    
    value:新值
    
Events //事件
   
    JsSIP.UA类定义了一系列的事件,用户可以在事件中书写回调操作
   
    connecting //各种连接进行时,事件触发
    
    事件data的参数:
    
    socket:正在连接的JsSIP.Socket 实例
    attempts: 数值,传输链接时长
    
    connected //配置完成后,发起连接时,事件触发
    
    事件data的参数:
    
    socket:正在连接的JsSIP.Socket 实例
    
    disconnect //连接传输请求或者自动重连请求失败时的事件
    
    事件data的参数:
    
    socket:正在连接的JsSIP.Socket 实例
    error: 布尔类型，标志着socket连接失败是否是发生一个错误
    code:连接状态码
    reason:连接失败原因
    
    registered //注册成功时触发
    
    事件data的参数:
    
    response:   JsSIP.IncomingResponse(呼入回复)收到2.X响应码的实例
    
    unregistered //注销
    
    2种情况下会发生:1,发送注销请求(UA.unregister()),2,已注册的重复检测注册状态失败
    
    事件data的参数:
    
    response:   JsSIP.IncomingResponse(呼入回复),收到注册请求后SIP发出的回复的实例
    cause:  SIP注销请求恢复可能为null,或者参照(Failure and End Causes) API
    
    registrationFailed //注册失败
    
    事件data的参数:
    
    response:   JsSIP.IncomingResponse(呼入回复),收到SIP发出的失败的实例,可能是SIP收到null等导致的
    cause:  SIP注销请求恢复可能为null,或者参照(Failure and End Causes) API
    
    newRTCSession //新的会话 
    
    呼入/呼出 会话/呼叫时发生
    
    事件data的参数(呼入会话时):
    
    originator: 'remote'字符串,会话由远程端发起
    session: JsSIP.RTCSession  会话实例
    request: JsSIP.IncomingResponse(呼入回复) 收到会话邀请的实例
    
    事件data的参数(呼出会话时):
    
    originator: 'local'字符串,会话由本地用户发起
    session: JsSIP.RTCSession  会话实例
    request: JsSIP.OutgoingResponse(呼出回复) 收到呼出请求的实例
    
    newMessage //新消息
    
    发出/收到 消息时发生
    
    事件data的参数(收消息时):
    
    originator: 'remote'字符串,消息由远程端发出
    session: JsSIP.Message  会话实例
    request: JsSIP.IncomingResponse(呼入回复) 收到会话邀请的实例
    
    事件data的参数(发消息时):
    
    originator: 'local'字符串,消息由本地用户发出
    session: JsSIP.Message  会话实例
    request: JsSIP.OutgoingResponse(呼出回复) 收到呼出请求的实例
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

    