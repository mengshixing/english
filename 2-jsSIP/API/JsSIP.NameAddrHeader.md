JsSIP.NameAddrHeader 类

    一个JsSIP.NameAddrHeader类的实例,由一个符合RFC 3261 BMF规定的地址名(name-addr)或地址明细(addr-spec)组成
    
    name-addr(地址名)值的格式是"display name <URI>".
    
    Example 示例:
    
        From: "Alice" <sip:alice@atlanta.com>
        
    addr-spec(地址细则)的形式是"URI"
    
    Example 示例:
    
        From: sip:alice@atlanta.com

Instantiation //初始化 

    JsSIP.NameAddrHeader(uri, display_name=null, parameters=null)
    
    初始化时缺少uri参数会抛异常
    
    Parameters参数 
    
        uri:JsSIP.URI实例
        
        display_name:显示名
        
        parameters:字符串组成的参数对象,对于参数无值的情况,需赋值null
    
    Example 示例:
    
    var parameters = {
        'parameter_1': 'value_1',
        'parameter_2': null
    }
    var header = new JsSIP.NameAddrHeader(uri, 'Mrs. Alice', parameters)

    header.toString() // Returns '"Mrs. Alice" <sip:alice@atlanta.com>;parameter_1=value_1;parameter_2'
    
Instance Attributes //实例属性

    display_name //显示名字
    
    设置/获取报头显示的名字
    
    Example 示例:
    
    header.display_name = 'Mrs. Alice';
    
    uri //资源地址
    
    从JsSIP.URI实例的获取组成name-addr(地址名)

Instance Methods //实例方法
    
    setParam(key, value=null) //设置参数
    
    创建/更新 对应的参数名/值
    
    Parameters参数 
    
        key:参数名,字符串类型
        
        value:参数值,字符串类型
    
    Example 示例:
    
    header.setParam('param_name', 'param_value');
        
    getParam(key) //获取参数值
    
    根据key获取参数值,参数不存在的话返回undefined
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    header.getParam('param_name'); // Returns 'param_value'
    
    hasParam(key) //是否存在
    
    验证参数是否存在,存在返回true,否则返回false
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    header.hasParam('param_name'); // Returns true
    
    deleteParam(key) //删除指定参数
    
    根据key删除对应参数
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    header.deleteParam('param_name');
    
    clearParams() //清空参数
    
    清空所有参数    
    
    clone()//克隆/复制
    
    返回一个复制的报头的JsSIP.NameAddrHeader实例
    
    cloned_header = header.clone();
    cloned_header === header // Returns false
    
    toString()//转换成字符串形式
    
    返回字符串形式header。字符串不能出现未转义的字符像RFC 3261的BNF语法规定的那样
    
    header.toString(); // Returns '"Mrs. Alice" <sip:alice@atlanta.com:5060>;param_name=param_value'
        
Module Functions  //模块方法

    parse(nameAddrHeader) //解析uri
    
    按地址报头的语法规则解析给出的字符串,解析成功的话返回一个JsSIP.NameAddrHeader 实例,否则返回undefined
    
    Parameters参数 

        nameAddrHeader:字符串,表示一个地址名.

    Example 示例:

    var uri = JsSIP.URI.parse('sip:alice@atlanta.com');
    
    var name_addr_hdr = JsSIP.NameAddrHeader.parse('"Mrs. Alice" <sip:alice@atlanta.com:5060>;param_name=param_value');
    
    
    