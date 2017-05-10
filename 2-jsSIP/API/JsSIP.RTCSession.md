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
    
    refer(target, options=null) //引用 访问
    
    通过将目标作为引用的源,发出一个引用方法.
    
    一个REFER方法会自动生成一个引用状态的订阅,
    
    通过 JsSIP.RTCSession.ReferSubscriber的一系列事件收到NOTIFY(通知)请求
    
    Parameters 参数：
        
        target：引用的源,字符串表示目标用户名或者一个完整的SIP地址,或者一个JsSIP.URI实例
        
        options  参数对象,详情如下
        
            extraHeaders:字符串数组,SIP引用请求时扩展的头参数
             
            eventHandlers：JsSIP.RTCSession.ReferSubscriber注册的事件操作
            
            replaces：可选的JsSIP.RTCSession实例,用户通话中替换引用目标,这是一个用户和引用源之间的即使通信
    
    resetLocalMedia() //重置本地媒体
    
    重置本地媒体流通过音视频的信道(除非远程用户正在保持通信)
    
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
        
    sending //发送事件
    
    在最初的邀请发送之前发生(对呼出情况来说),它能使用户在此时进行SIP请求或他的SDP的mangle(过滤机制)
        
        事件data的参数(呼出会话时):
    
        request:JsSIP.OutgoingRequest实例,表示呼出的SIP请求消息
    
    progress //进展事件
    
    对会话邀请收到或者生成一个1XX的SIP回复时发生
    
    事件发生在SDP处理之前,如果需要的话可以对它进行微调,甚至可以通过移出Data对象中的回复参数(response)体来终止它
    
    事件data的参数(呼入会话时):
    
        originator:'local'
    
    事件data的参数(呼出会话时):
    
        originator:'remote'
        
        response:接受1XX系列 SIP回复的JsSIP.IncomingResponse实例
    
    accepted //接收事件
    
    当呼叫被接受时发生((2XX received/sent(接受/发送))
        
    事件data的参数(呼入会话时):
    
        originator:'local'
    
    事件data的参数(呼出会话时):
    
        originator:'remote'
        
        response:接受2XX系列 SIP回复的JsSIP.IncomingResponse实例   
    
    confirmed //确认事件
        
    当呼叫被确认时发生((ACK(即确认字符，在数据通信中，接收站发给发送站的一种传输类控制字符,
    
    表示发来的数据已确认接收无误。) received/sent(接受/发送))   
        
    事件data的参数(呼入会话时):
    
        originator:'local'
    
    事件data的参数(呼出会话时):
    
        originator:'remote'
        
        response:接受2XX系列 SIP回复的JsSIP.IncomingResponse实例   

    ended //结束事件
    
    当已建立的连接结束时发生
    
    事件data的参数:
    
        originator:'local'/'remote'/'system' (本地/远程/系统字符串),终止会话的发起着
        
        message:JsSIP.IncomingRequest或者JsSIP.IncomingResponse实例,originator为远程时,呼叫终止时
        
        生成.其他情况下,为null
        
        cause:Failure and End Causes(失败/结束原因)的值
    
    failed //失败事件
    
        当会话未能建立时发生
        
        事件data的参数:
    
        originator:'local'/'remote'/'system' (本地/远程/系统字符串),会话失败的发起着
        
        message:JsSIP.IncomingRequest或者JsSIP.IncomingResponse实例,originator为远程时,会话失败时
        
        生成.其他情况下,为null
        
        cause:Failure and End Causes(失败/结束原因)的值
        
    newDTMF //新的多频信号事件
    
    当有呼入/呼出的信号时发生
    
    事件data的参数(呼入信号时):
    
    originator: 'remote'字符串,信号由远程端发起
    dtmf: JsSIP.RTCSession.DTMF  信号实例
    request: JsSIP.IncomingResponse(呼入回复) 收到请求信息的实例
    
    事件data的参数(呼出信号时):
    
    originator: 'local'字符串,信号由本地用户发起
    dtmf: JsSIP.RTCSession.DTMF  信号实例
    request: JsSIP.OutgoingResponse(呼出回复) 收到呼出请求的实例  
    
    newInfo //新信息的事件
    
    当有呼入/呼出的SIP INFO消息时发生
        
    事件data的参数(呼入INFO信息时):
    
    originator: 'remote'字符串,INFO信息由远程端生成
    info: JsSIP.RTCSession.Info   信息实例
    request: JsSIP.IncomingResponse(呼入回复) 收到请求信息的实例
    
    事件data的参数(呼出INFO信息时):
    
    originator: 'local'字符串,INFO信息 由本地用户生成
    info: JsSIP.RTCSession.Info   信息实例
    request: JsSIP.OutgoingResponse(呼出回复) 收到呼出信息请求的实例    
        
    hold //暂停事件

    当本地或远程端暂停时发生
    
    事件data的参数(呼出INFO信息时):
    
        originator:'local'本地暂停远程的流,'remote'远程端暂停本地推的流
        
    unhold //继续/取消暂停
    
    当本地或远程端结束暂停时发生
        
    事件data的参数(呼出INFO信息时):
    
        originator:'local'本地继续远程的流,'remote'远程端继续本地推的流    
            
    muted // 静音事件     
    
	当本地静音时发生
            
    事件data的参数：
	
		audio:布尔类型,是否音频静音
		
		video:布尔类型,是否视频静音
	
	unmuted //取消静音事件
	
	当本地取消静音时发生
            
    事件data的参数：
	
		audio:布尔类型,是否音频取消静音
		
		video:布尔类型,是否视频取消静音
	
	reinvite //再次邀请/重连事件
	
	当收到会话重连请求时发生
	
	事件data的参数：
	
		request:接受重连请求的JsSIP.IncomingRequest实例
		
		callback:初值是undefined,如果用户配置了一个函数的话,会在重连进行时执行
		
		reject():拒绝重连请求的方法。拒绝时执行,默认403回复码
		
		事件data.reject()的参数：
		
		options：扩展参数配置对象，列表如下
		
			extraHeaders: 字符串数组,扩展发送SIP MESSAGE请求的头
			
			status_code:300~699,SIP回复的状态码
            
            reason_phrase:SIP回复的原因简介
            
    update //更新事件

	收到会话更新请求时发生
     
	事件data的参数：
	
		request:接受UPDATE 请求的JsSIP.IncomingRequest实例
		
		callback:初值是undefined,如果用户配置了一个函数的话,会在UPDATE 进行时执行
		
		reject():拒绝重连请求的方法。拒绝时执行,默认403回复码
		
		事件data.reject()的参数：
		
		options：扩展参数配置对象，列表如下
		
			extraHeaders: 字符串数组,扩展发送SIP MESSAGE请求的头
			
			status_code:300~699,SIP回复的状态码
            
            reason_phrase:SIP回复的原因简介
			
	refer  //引用 访问事件
		
	当收到会话的引用时发生
	
	如果引用被授权通过,一个新的呼出会话会立即产生,呼出的目标是引用头的值
	
	通知机制(NOTIFY)用于通知通信端发送引用的引用状态(RFC 3515定义)
	
	NOTE: 呼入请求指向的JsSIP.URI属性 是可以访问的引用源
	
	事件data的参数：
	
		request:接受REFER 请求的JsSIP.IncomingRequest实例
		
		accept(): 准许同意的方法,当引用被接收时发生,本方法生成一个指向引用源 URL的呼出请求
	
		事件data.reject()的参数：
		
			newRTCSession(session)：回调方法, JsSIP.UA针对新的呼出会话生成newRTCSession事件时执行,
			
			如果此方法未定义,之前的事件会被提交
			
			options:
			
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
            
            
            
            
            
            
            
            
            
            