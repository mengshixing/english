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
    
    对呼入会话请求来说,如果用户还没有回复请求,此时会发一个 non-2xx的最终回复,包括一个特定的状态码和原因字段,    
    默认480 Unavailvable,对呼出情况来说,如果原始的会话申请请求还未发送的话,将不再发送该请求。如果该请求已经发出,    
    但尚未收到最终回复,根据是否收到临时回复,有以下情况,如果收到了会发送一个取消请求。如果没有,根据RFC 3261暂不
    发送取消请求,如果之后收到临时回复的话会立即发送取消请求。
    
    无论是呼入呼出,如果已经收到最终回复,会发送一个bye的请求
        
        Parameters参数 
        
        options  参数对象,详情如下
            
            extraHeaders:字符串数组,SIP消息请求时扩展的头参数
            
            status_code:300~699,SIP回复的状态码
            
            reason_phrase:SIP回复的原因简介
            
            body: SIP的消息体.(如果设置了本参数的话,需要在extraHeader参数中设置一个对应的Content-Type)
            
        NOTE:当发生取消请求时,status_code值可以取200-699,按照 RFC3326说明,status_code和 reason_phrase 会组成
        一个回复的头,取消的请求不带 extraHeaders和 body参数
        
    sendDTMF(tone, options=null) //发送多频
    
    使用SIP的info方法发送一个或多个多频信号
    
        tone:数字组成的字符串,由一个或多个可用DTMF信号组成
        
        options  参数对象,详情如下
            
            duration(持续时间):表示信号传递时间,单位是毫秒,正整数,默认值100
            
            interToneGap:表示2个信号传递时间间隔,单位是毫秒,正整数,默认值500
            
            extraHeaders:字符串数组,SIP每个INFO请求的头

    示例1：
        
        call.sendDTMF(1);
        call.sendDTMF(4);
    
    示例2：
    
        var tones = '1234#';
        var extraHeaders = [ 'X-Foo: foo', 'X-Bar: bar' ];
        var options = {
          'duration': 160,
          'interToneGap': 1200,
          'extraHeaders': extraHeaders
        };
        call.sendDTMF(tones, options);
    
    sendInfo(contentType, body=null, options=null)//发送信息
    
    发送一个SIP信息的消息
    
    contentType：SIP信息头的类型值
    
    body:SIP信息内容
    
    options  参数对象,详情如下
        
        extraHeaders：字符串数组,INFO请求的头参数
        
    hold(options=null, done=null) //保持(暂停)
    
    通过重复邀请或者更新SIP请求来暂停呼叫(通话),当不能重定义时返回false
    
    done：函数类型,当重定义成功时使用
    
    options  参数对象,详情如下
    
        useUpdate：布尔类型,发送UPDATE(更新)指令替换re-INVETE(重新邀请)
        
        extraHeaders:字符串数组,SIP消息请求时扩展的头参数
        
    unhold(options=null, done=null)//恢复
    
    通过重复邀请或者更新SIP请求来恢复呼叫(通话),当不能重定义时返回false
    
    done：函数类型,当重定义成功时使用
    
    options  参数对象,详情如下
    
        useUpdate：布尔类型,发送UPDATE(更新)指令替换re-INVETE(重新邀请)
        
        extraHeaders:字符串数组,SIP消息请求时扩展的头参数
    
    renegotiate(options=null, done=null)//重新协商  
    
    发起一个SDP重连,可以修改本地连接到底层RTCPeerConnection的流(通过连接属性)
    
    done：函数类型,当重定义成功时使用
    
    options  参数对象,详情如下
    
        useUpdate：布尔类型,发送UPDATE(更新)指令替换re-INVETE(重新邀请)
        
        extraHeaders:字符串数组,SIP消息请求时扩展的头参数
        
        rtcOfferConstraints:object类型,RTCPeerConnection约束的createOffer()方法
        
    isOnHold() //暂停
    
    返回一个对象包含'local','remote'字段和它们的值(布尔),标志着本地和远程的是否保持同步
    
    示例：
    
        rtcsession.isOnHold();
        
        {
          'local': true,    // User has put the other peer on hold 
          'remote': false   // Peer hasn't put user on hold
        }
    
    mute(options=null) //静音
    
    静音本地的音/视频
        
        audio:布尔,决定本地音频是否必须静音
        
        video:布尔,决定本地视频是否必须静音
        
    unmute(options=null) //取消静音
    
    取消静音本地的音/视频
    
        audio:布尔,决定本地音频是否取消静音
            
        video:布尔,决定本地视频是否取消静音
    
    isMuted() //静音设置
    
    返回一个对象包含'audio','video'字段和它们的值(布尔),标志着音/视频是否静音
    
    示例：
    
        rtcsession.isMuted();
        
        {
          'audio': true,   // Local audio is muted
          'video': false   // Local audio is not muted
        }
    
    
Events //事件

    JsSIP.RTCSession类定义了一系列的事件,允许用户注册一系列回调操作在特定情况下执行。
    
    peerconnection //预备连接事件
    
    对一个呼出请求,当内部的RTCPeerConnection(连接)被创建,而SDP准许尚未生成时发生该事件发生,或者呼入请求未生成
    SDP许可事法师。   
    应用可以在此时改变peerconnection连接,例如通过在它上面添加一个RTCDataChannel(RTC数据通道)
    
    事件data的参数:
    
        peerconnection: RTCPeerConnection的实例.
        
    示例
    var datachannel;
    session.on('peerconnection', function(data) {
      datachannel = data.peerconnection.createDataChannel('chat');
    });
    
    connecting //连接事件
    
    发生在当本地媒体流添加到RTCSession(会话)后,在中间件收到最初的会话请求之前或者传递"200 OK"回复之前
    
    事件data的参数(呼入会话时):
    
        request:JsSIP.IncomingRequest实例,表示呼入的SIP请求消息
    
    事件data的参数(呼出会话时):
    
        request:JsSIP.OutgoingRequest实例,表示呼出的SIP请求消息
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            
            