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