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
    
    Parameters 
        
        options :扩展的参数选项
        all:布尔类型,用来注销SIP用户所有的绑定,默认值false
        
        var options = {
          all: true
        };
        ua.unregister(options);
    
    registrator()
    
    有单独的页面介绍

call(target, options=null) //发起请求