Events 

    每个事件操作的发生都会随着一个参数,此时发生该事件的类定义了一个data对象
    
    你可以查看每个时间对应的定义来获取它对应data的更多信息
    
    事件发生时,事件的句柄(发生事件的实例)的值可以用this(通过on()方法的监听着的对象/实例)
    
Example

    var ua = new JsSIP.UA( ... );

    ua.on('newRTCSession', function(data) {
      var originator = data.originator;
      var session = data.session;
      var request = data.request;

      // Stop the UA. Note that `this` is bound to the `ua` instance. this此时指ua
      this.stop();
    });
