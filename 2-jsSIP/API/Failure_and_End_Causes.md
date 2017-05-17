Failure and End Causes
    
    JsSIP提供了以个原因集合,来使用户弄清导致请求/会话失败的原因。所有的原因在JsSIP.C.causes命名空间
    
    下定义,因此所有含有cause字段参数的事件可以在这里比对结果(原因明细)
    
    Example //示例
    
    var target = 'sip:bob@example.com';
    var eventHandlers = {
        'failed': function(data) {
            if (data.cause === JsSIP.C.causes.BUSY) {
              coolPhone.sendMessage(target, 'Please, call me later!');
            }
        }
    }
    //JsSIP.C.causes.BUSY是SIP Error之一
    coolPhone.call(target, useAudio, useVideo, eventHandlers, views);
    
Common Causes //公共原因

    Constant//常量          Value//值                    Description//描述

    CONNECTION_ERROR        'Connection Error'          WebSocket发生连接错误
    
    REQUEST_TIMEOUT         'Request Timeout'           无回复,客户端事务超时
    
    SIP_FAILURE_CODE        'SIP Failure Code'          SIP消极回复,不属于下面"SIP Error Causes"表中的原因
    
    INTERNAL_ERROR          'Internal Error'            意外错误,内部错误
    
SIP Error Causes //SIP错误

    一些SIP回复状态码及原因
    
    Constant//常量               Value//值                                       SIP Status Codes//状态码

    BUSY                        'Busy'  //忙                                     486,600
    
    REJECTED                    'Rejected'  //拒绝                               403,603
    
    REDIRECTED                  'Redirected'    //重定向                         300,301,302,305,380
    
    UNAVAILABLE                 'Unavailable'   //不可用                         480,410,408,430
    
    NOT_FOUND                   'Not Found'     //不存在                         404,604
    
    ADDRESS_INCOMPLETE          'Address Incomplete'    //地址不全               484
    
    INCOMPATIBLE_SDP            'Incompatible SDP'  //SDP不兼容/不可用           488,606 
    
    MISSING_SDP                 'Received a request/response that should have SDP body but did not'//缺少SDP主体
    
    AUTHENTICATION_ERROR        'Authentication Error'    //认证失败             401,407
    
 RTCSession Causes //会话原因

    下列原因适用于音视频会话
    
    Constant//常量             Value//值             Description//描述

    BYE                        'Terminated'          RTC的会话被本地/远程用户正常终止
    
    CANCELED                   'Canceled'            RTC的会话被本地/远程用户取消
    
    NO_ANSWER                  'No Answer'           呼入电话未在配置时间内(no_answer_timeout)接听/回应
    
    EXPIRES                    'Expires'             呼入电话包含一个过期头,本地用户未在头设置时间内回复
    
    NO_ACK                     'No ACK'              呼入请求回复了2XX系列码,但是没收到"确认收到"
    
    DIALOG_ERROR               'Dialog Error'        一个内部通话请求收到了SIP 408/481的错
    
    USER_DENIED_MEDIA_ACCESS   'User Denied Media Access'       本地用户拒绝媒体接入当提示音/视频设备时
    
    BAD_MEDIA_DESCRIPTION      'Bad Media Description'          收到的SDP是错的
    
    RTP_TIMEOUT                'RTP Timeout'         RTP丢包导致会话终止
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    