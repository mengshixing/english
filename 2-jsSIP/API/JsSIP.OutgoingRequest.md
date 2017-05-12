JsSIP.OutgoingRequest类 

    JsSIP.OutgoingRequest实例,保持发送SIP请求

Instance Attributes //实例属性
    
    method //方法
    
    SIP请求的方法名,字符串类型
    
    ruri // 地址
    
    JsSIP.URI实例,表示请求目标的url
    
    cseq //发送包的编号号码
    
    表示CSeq,数字类型(CSeq消息头用于标识事务先后顺序,一个响应消息有与其对应的请求消息相同的CSeq值)
    
    call_id //呼叫ID