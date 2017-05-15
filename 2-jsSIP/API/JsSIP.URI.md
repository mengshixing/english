JsSIP.URI 类

    一个JsSIP.URI实例表示一个SIP的地址,提供了一个属性/方法清单来检索/设置URI的不同部分.
    
    它提供了一种方式来表示URI的完整形式(含头和参数)和AoR形式,URI允许复制,可以根据自身生成第二个URI
    
    Note:(URI //uniform resource indentifier是统一资源标识符,而 URL //uniform resource locator是统一资源定位符。)
    
Instantiation //实例化 

    JsSIP.URI(scheme="sip", user=null, host, port=null, parameters=null, headers=null)
    
    如果host值不合法的话,类初始化时会生成一个异常
    
        scheme: 字符串类型,uri的协议,默认'sip'
        
        user: 字符串类型,用户名
        
        host:字符串类型, 表示主机,可以是一个IP地址或者主机名
        
        parameters:字符串组成的参数对象,对于参数无值的情况,需赋值null
        
        headers:字符串或字符串数组组成的对象
        
    Example 示例:
    
    var parameters={    
        param_name:'param_value',
        valueless_param:null    
    }
    
    var headers={
        header_name:'header_value',
        multi:['multi_value1','multi_value2']
    }
    
    var uri = new JsSIP.URI('sip', 'alice', 'atlanta.com', 5060, parameters, headers)
    
    // Returns "sip:alice@atlanta.com" 返回Aor形式uri
    uri.toAor() 
    
    // Returns "sip:alice@atlanta.com:5060;param_name=param_value;
    // valueless_param?Header-Name=header_value&Multi-Header=multi_header_value1&Multi-Header=multi_header_value2"
    // 返回完整形式的uri
    uri.toString() 

Instance Attributes //实例属性
    
    scheme //协议/方案
    
    配置/获取 uri的协议
    
    Example 示例:
    
    uri.scheme = 'sip';
    uri.scheme // Returns 'sip'

    uri.scheme = 'sIP';
    uri.scheme // Returns 'sip' 转变小写？
    
    user //用户
    
    配置/获取 uri的用户
    
    Example 示例:
    
    uri.user = 'alice';
    uri.user // Returns 'alice'

    uri.user = 'Alice';
    uri.user // Returns 'Alice' 大小写敏感？

    uri.user = 'j@s0n'
    uri.toAor() // Returns 'sip:j%40s0n@atlanta.com' 返回Aor形式uri
    
    host // 主机
    
    配置/获取 uri的主机
    
    Example 示例:
    
    uri.host = 'atlanta.com';
    uri.host // Returns 'atlanta.com'

    uri.host = 'AtLATta.cOm';
    uri.host // Returns 'atlanta.com' 转变小写？
        
    port //端口
    
    配置/获取 uri的端口
    
    Example 示例:
    
    uri.port = 5060;
    uri.port // Returns 5060

    uri.port = '5060';
    uri.port // Returns 5060 字符串默认转成数字
    
Instance Methods //实例方法
    
    setParam(key, value=null) //设置参数
    
    创建/更新 对应的参数名/值
    
    Parameters参数 
    
        key:参数名,字符串类型
        
        value:参数值,字符串类型
    
    Example 示例:
    
        uri.setParam('param_name', 'param_value');
        
    getParam(key) //获取参数值
    
    根据key获取参数值,参数不存在的话返回undefined
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    uri.getParam('param_name'); // Returns 'param_value'
    
    hasParam(key) 
    
    验证uri参数是否存在,存在返回true,否则返回false
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    uri.hasParam('param_name'); // Returns true
    
    deleteParam(key) //删除指定参数
    
    根据key删除uri对应参数
    
    Parameters参数 
    
        key:参数名,字符串类型
    
    Example 示例:
    
    uri.deleteParam('param_name');
    
    clearParams() //清空参数
    
    清空uri所有参数
    
    setHeader(key, value) //设置报头
    
    创建/更新 报头下的参数名和值 
    
    Parameters参数 
    
        key:报头参数名,字符串类型
        
        value:报头参数值,字符串类型或数组类型
    
    Example 示例:
    
    uri.setHeader('header_name','header_value');
    uri.setHeader('header_name',['header_value1','header_value2']);
    
    getHeader(key) //获取参数值
    
    根据key获取报头参数值,返回一个数组.参数不存在的话返回undefined
    
    Parameters参数 
    
        key:报头参数名,字符串类型
            
    Example 示例:
    
    uri.setHeader('header_name',['header_value1','header_value2']);
    uri.getHeader('header_name'); // Returns ['header_value1','header_value2']返回数组

    uri.setHeader('header_name','header_value');
    uri.getHeader('header_name'); // Returns ['header_value']一个值也封装成数组
    
    hasHeader(key)//是否存在
    
    验证uri报头参数是否存在,存在返回true,否则返回false
    
    Parameters参数 
    
        key:报头参数名,字符串类型
            
    Example 示例:
    
    uri.setHeader('header_name','header_value');
    uri.hasHeader('header_name'); // Returns true
    
    deleteHeader(key) //删除指定参数
    
    根据key删除uri报头对应参数
    
    Parameters参数 
    
        key:报头参数名,字符串类型
            
    Example 示例:
    
    uri.delteHeader('header_name');
    
    clearHeaders() //清空参数
    
    清空uri报头所有参数
    
    Example 示例:
    
    uri.clearHeaders();
    
    clone()//克隆/复制
    
    返回一个复制的URI的JsSIP.URI实例
    
    cloned_uri = uri.clone();
    cloned_uri === uri // Returns false
    
    toString()//转换成字符串形式
    
    返回字符串形式uri。字符串不能出现未转义的字符像RFC 3261的BNF语法规定的那样
    
    uri.toString(); // Returns "sip:alice@atlanta.com:5060?header_name=header_value1&header_name=header_value2"
    
    toAor() //转换成Aor形式
    
    返回字符串，表示Aor形式uri。字符串不能出现未转义的字符像RFC 3261的BNF语法规定的那样
    
    uri.toAor(); // Returns "sip:alice@atlanta.com"

    uri.user = 'j%40s0n'
    uri.toAor(): // Returns "sip:j%40s0n@atlanta.com"
    
Module Functions  //模块方法

    parse(uri) //解析uri
    
    按SIP URI的语法规则解析给出的字符串,解析成功的话返回一个 JsSIP.URI 实例,否则返回undefined
    
    Parameters参数 

        uri:字符串,表示一个SIP URI.

    Example 示例:

    var uri = JsSIP.URI.parse('sip:alice@atlanta.com');

    
    
    
    