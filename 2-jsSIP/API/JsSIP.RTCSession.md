Class JsSIP.RTCSession

    JsSIP.RTCSession类 是个webRTC多媒体通信(音/视频),可以由本机或者远程用户发起.
    它内部有一个RTCPeerConnection实例,可以connection通过属性得到
    
Instance Attributes //实例属性

    connection
    
    是RTCPeerConnection实例连接到会话的基础,可以用它来设置webRTC相关的事件(推流,添加信道等)
    需要说明的是,呼出时RTCPeerConnection在调用 ua.call()之后设置,呼入时在session.answer()后设置
    
    direction //方向
    
    字符串用户,表明会话开始用户,值为'incoming'(远程用户发起的会话)或'outgoing'(本地用户发起的会话)
    
    local_identity //本地标识
    
    