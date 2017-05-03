Getting Started // 入门

    jsSIP的用户代理UA(User Agent)是jsSIP的核心,它关联着SIP客户端与SIP账号,UA在JsSIP.UAl类中定义。
    
    可以同时创建多个UA(在一个web应用程序中有多个不同的SIP账户时会显得很有用)
    
Creating a JsSIP User Agent //创建一个UA

    User Agent Configuration  //UA配置
    
        jsSIP需要一个配置列表用于自身的初始化,有一些必须的参数也有可选的,可以参考配置参数清单.(详见API)
        
        var socket = new JsSIP.WebSocketInterface('wss://sip.myhost.com');
        var configuration = {
          sockets  : [ socket ],
          uri      : 'sip:alice@example.com',
          password : 'superpassword'
        };
    
    User Agent instance //UA实例化
    
        var coolPhone = new JsSIP.UA(configuration);
    
User Agent events definition //UA定义事件
    
    详见API的UA事件清单
    
    WebSocket connection events //websocket连接事件
        
        coolPhone.on('connected', function(e){ /* Your code here */ });

        coolPhone.on('disconnected', function(e){ /* Your code here */ });

    New incoming or outgoing call event //新的呼入呼出呼叫事件

        coolPhone.on('newRTCSession', function(e){ /* Your code here */ });
    
    New incoming or outgoing IM message event //新的呼入呼出IM信息事件

        coolPhone.on('newMessage', function(e){ /* Your code here */ });
        
    SIP registration events //SIP注册事件

        coolPhone.on('registered', function(e){ /* Your code here */ }); //SIP注册
        coolPhone.on('unregistered', function(e){ /* Your code here */ }); //SIP注销
        coolPhone.on('registrationFailed', function(e){ /* Your code here */ }); //SIP注册失败

Starting the User Agent //UA开始
    
    详见JsSIP.UA.start()API.
    coolPhone.start();
    
Making outbound calls //呼叫外面Sever的信号
    
    详见JsSIP.UA.call()API. 示例：
    
    // Create our JsSIP instance and run it: 创建实例,运行

    var socket = new JsSIP.WebSocketInterface('wss://sip.myhost.com');
    var configuration = {
      sockets  : [ socket ],
      uri      : 'sip:alice@example.com',
      password : 'superpassword'
    };

    var ua = new JsSIP.UA(configuration);

    ua.start(); //

    // Register callbacks to desired call events //声明回调函数
    var eventHandlers = {
      'progress': function(e) {
        console.log('call is in progress');
      },
      'failed': function(e) {
        console.log('call failed with cause: '+ e.data.cause);
      },
      'ended': function(e) {
        console.log('call ended with cause: '+ e.data.cause);
      },
      'confirmed': function(e) {
        console.log('call confirmed');
      }
    };
    //声明选项
    var options = {
      'eventHandlers'    : eventHandlers,
      'mediaConstraints' : { 'audio': true, 'video': true }
    };

    var session = ua.call('sip:bob@example.com', options); //开始会话呼叫
    
Instant messaging //即使通信

    详见JsSIP.UA.sendMessage()API. 2种通信方法示例：
    
    Example 1

    var text = 'Hello Bob!';

    coolPhone.sendMessage('sip:bob@example.com', text);
    
    Example 2

    var text = 'Hello Bob!';

    // Register callbacks to desired message events 声明发送消息成功或者失败的回调函数
    var eventHandlers = {
      'succeeded': function(e){ /* Your code here */ },
      'failed':    function(e){ /* Your code here */ }
    };

    var options = {
      'eventHandlers': eventHandlers
    };

    coolPhone.sendMessage('sip:bob@example.com', text, options);