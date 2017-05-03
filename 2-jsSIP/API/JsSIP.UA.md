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
    

    