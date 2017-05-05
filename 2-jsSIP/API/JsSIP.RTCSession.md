Class JsSIP.RTCSession

    JsSIP.RTCSession类 是个webRTC多媒体通信(音/视频),可以由本机或者远程用户发起.
    它内部有一个RTCPeerConnection实例,可以connection通过属性得到
    
Instance Attributes //实例属性

    connection //连接
    
    是RTCPeerConnection实例连接到会话的基础,可以用它来设置webRTC相关的事件(推流,添加信道等)
    需要说明的是,呼出时RTCPeerConnection在调用 ua.call()之后设置,呼入时在session.answer()后设置
    
    direction //方向
    
    字符串用户,表明会话开始用户,值为'incoming'(远程用户发起的会话)或'outgoing'(本地用户发起的会话)
    
    local_identity //本地标识
    
    本地标识的JsSIP.NameAddrHeader实例,当指向呼出时,指邀请者头部的值,反之亦然
    
    remote_identity //远程地址头标识
    
    远程标识的JsSIP.NameAddrHeader实例,当指向呼出时,指受邀请者头部的值,反之亦然
    
    start_time //开始时间
    
    Data类型,会话开始的时间,当accepted事件发生时初始化出值
    
    end_time //结束时间
    
    Data类型,会话结束的时间,当ended事件发生时的时间
    
    data //数据
    
    应用程序存储的与会话相关的自定义信息。object类型
    
    data //数据
    
    可以自定义会话空的object,开发者可以自定义键值对
    
Instance Methods //实例方法

    isInProgress()
    
    返回true如果正在会话进行中,(不是创建和结束状态)
    
    isEstablished() 
    
    返回true如果会话已经创建
    
    isEnded()
    
    返回true如果会话已经结束
    
    isReadyToReOffer()
    
    返回true如果会话可以进行 SDP重连((hold(), unhold() or renegotiate()等方法// 持续,断开,重连)
    
    answer(options)
    
    回复外来会话,本方法只能用于本地被呼叫的情况
    
        Parameters参数 
        
        options  参数对象,详情如下
        
            extraHeaders:字符串数组，SIP回复200(OK)时的头
            
            mediaConstraints: object类型,含video和audio2个可配置参数,来标识着会话约束是视频 和/或 音频,
            
            默认值由收到的SDP请求决定
            
            mediaStream:流类型，将流传送到其它终端
            
            pcConfig:object类型,RTCPeerConnection的RTCConfiguration(配置清单)
            
            rtcConstraints:object类型,RTCPeerConnection的约束
            
            rtcAnswerConstraints:object类型,RTCPeerConnection约束的createAnswer()方法
            
            rtcOfferConstraints:object类型,RTCPeerConnection约束的createOffer()方法(被用来下次接受请求(没有SDP准许的))
            
            sessionTimerExpires:时间(秒),设置默认的会话时间间隔(默认90,不能低于90)
    
    terminate(options) //终止会话
    
    终止当前会话无论发起着是谁,无论当前状态是什么。
    
    根据当前会话状态情况,本方法可能会发一个不同的请求。
    
    对呼入会话请求来说,如果用户还没有回复请求,此时会发一个 non-2xx的最终回复,包括一个特定的状态码和原因字段,默认480 Unavailvable
    
    对呼出情况来说,如果原始的会话申请请求还未发送的话,将不再发送该请求。如果该请求已经发出,但尚未收到最终回复
    
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            