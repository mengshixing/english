Class JsSIP.Registrator //注册器类

    本类管理UA注册过程
    
Instance Methods //实例方法

    setExtraHeaders(extraHeaders)
    
    在注册/注销时候可以添加自定义的头,它们任何时候都可被覆盖
    
    Parameters 参数:
    
    extraHeaders:字符串数组,所有的SIP请求会附加扩展的参数,设置为null可以移除设置的参数
    
    ua.registrator.setExtraHeaders([
      'X-Foo: bar'
    ]);
        
    setExtraContactParams(extraContactParams)　
    
    在注册/注销时候可以添加自定义的接口参数,它们任何时候都可被覆盖
    
    Parameters 参数:
    
    extraContactParams:对象类型,以键值队来书写,key表示参数名,value表示参数值.
    设置为null可以移除设置的参数
    
    ua.registrator.setExtraContactParams([
        x-vendor: 'FooBar',
        verified: true
    ]);

    // =>  ;x-vendor=FooBar;x-verified