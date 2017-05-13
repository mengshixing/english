JsSIP.IncomingMessage 类

    JsSIP.IncomingMessage实例,接受的SIP请求/回复
    
Instance Attributes //实例属性

    method //方法
    
    SIP呼入消息的方法名,字符串类型
    
    from //发起
    
    JsSIP.NameAddrHeader,指SIP呼入消息发起者头的值
    
    to //目标
    
    JsSIP.NameAddrHeader,指SIP呼入消息目标头的值
    
    body //主体
    
    字符串类型,SIP消息的主体部分,没有的话返回null
    
Instance Methods //实例方法

    countHeader(name) //获取头的数目
    
    根据名字获取头的数量,数值型,返回指定头值的数量
    
    Parameters参数 
    
        name:头的名字
    
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
    
    Parameters参数 
    
        name:头的名字
        
    parseHeader(name, idx) //解析头
    
    在指定的位置(索引点)解析特定的头,返回解析后的对象,头不存在或者解析失败返回undefined
    
    Parameters参数 
    
        name:头的名字
        
        idx:要解析的头的索引(数值型),默认0(第一个头)
        
    toString() //转化为字符串
    
    SIP 请求生成字符串
    