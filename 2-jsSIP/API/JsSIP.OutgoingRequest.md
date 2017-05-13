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
    
    Call-ID头的值,字符串类型
    
    from //发起
    
    JsSIP.NameAddrHeader,指发起者头的值
    
    to //目标
    
    JsSIP.NameAddrHeader,指目标头的值
    
    body //主体
    
    字符串类型,请求的主体部分
    
Instance Methods //实例方法

    setHeader(name, value) //设置头
    
    给指定的头赋值
    
    Parameters参数 
    
        name:头的名字
        
        value:头的值,字符串类型或字符串数组类型
        
    getHeader(name) //获取头
    
    根据名字获取特点头的初值,返回头的值(字符串类型),如果名字不存在,返回null
    
    Parameters参数 
    
        name:头的名字
        
    getHeaders(name)    //获取头
    
    根据名字获取特点头的值,返回头的值(字符串数组类型),包含本名字对应所有的值
    
    Parameters参数 
    
        name:头的名字
    
    hasHeader(name) //是否存在
    
    验证头名字是否存在,存在返回true,否则返回false
    
        name:头的名字
    
    toString() //转化为字符串
    
    SIP 请求生成字符串
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    