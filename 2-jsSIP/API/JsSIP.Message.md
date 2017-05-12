JsSIP.Message 类

    JsSIP.Message基于IM(Instant Messaging 即时通讯)

Instance Attributes //实例属性

    direction //指向
    
    字符串类型,表示消息的方向,远程端发出的值为'incoming',本地发出的值为'outgoing'
    
    local_identity //本地标识
    
    代表本地标识的JsSIP.NameAddrHeader实例,当指向是呼出时,它和消息发出源的头附加值一致
    
    当指向是呼入时,它和消息接受源的头附加值一致
    
    remote_identity //远程标识
    
    代表远程标识的JsSIP.NameAddrHeader实例,当指向是呼出时,它和消息接受源的头附加值一致
    
    当指向是呼入时,它和消息发出源的头附加值一致

Instance Methods //实例方法

    send(target,body,options=null) //发送方法
    
    通过WebSocket连接发送消息,本方法只能用于发出信息
    
    Parameters参数 
    
        target:消息的终端,字符串类型,值为消息的终端名或一个完整的SIP的URI
        
        body:消息内容,字符串类型,消息的主体
        
        options  参数对象,详情如下
        
            contentType:消息体的文档类型,默认是 text/plain
            
            eventHandlers:可以对每个消息事件注册的操作,可以为事件的结果定义事件操作
            
            extraHeaders:消息请求时的SIP头,字符串数组
        
    示例:
    
    var text = 'Hello Bob!';

    var eventHandlers = {
      'succeeded': function(e){ /* Your code here */ },
      'failed':    function(e){ /* Your code here */ };
    };

    var options = {
      'eventHandlers': eventHandlers
    };

    accept(options) //接受方法
    
    呼入消息的积极回应。表示发送着已经传送呼叫到终端,本方法只能用于呼入信息
    
    options  参数对象,详情如下
    
        extraHeaders:消息请求时的SIP头,字符串数组
        
        body:消息内容,字符串类型,SIP消息的主体
        
            (Note:这个参数设置的话,对应的extraHeaders中必须设置Content-Type字段)
        
    reject(options) //拒绝方法
    
    呼入消息的消极回应。表示发送着未成功传送呼叫到终端,回复码和原因表明拒绝情况.本方法只能用于呼入信息
    
    options  参数对象,详情如下
    
        extraHeaders:消息请求时的SIP头,字符串数组
        
        status_code:300~699,SIP回复的状态码
            
        reason_phrase:SIP回复的原因简介
        
        body:消息内容,字符串类型,SIP消息的主体
        
            (Note:这个参数设置的话,对应的extraHeaders中必须设置Content-Type字段)
    
Events //事件

    JsSIP.Message 类定义了一系列的事件,允许用户注册一系列回调操作在特定情况下执行。
    
    succeeded //成功事件
    
    当收到一个积极最终回复时发生(针对消息请求)
    
    事件data的参数:
    
        originator:'remote',远程端积极响应SIP消息
        
        response:JsSIP.IncomingResponse实例,(接受到的2XX系列回复)
        
    failed //失败事件
    
    当没有收到一个积极最终回复时发生(发送的信息已经被接收)
    
        originator:'remote'/'system',导致消息失败的地方
        
        response:JsSIP.IncomingResponse实例(当失败是远程端导致时,其他情况为null)
        
        cause:失败原因表实体(Failure and End Causes)的一个枚举纸
    
    

    
    
    
    
    
    
    
    
    
    