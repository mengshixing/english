FAQ //常见问题Frequently Asked Questions

What is JsSIP?  //JsSIP是什么

	JsSIP是一个客户端纯js库,用于在web环境下构建SIP终端
	
What can I do with JsSIP? //JsSIP能做什么

	你可以在web页创建SIP的ua.用于
		收/发多媒体电话
		收/发文本消息
		
Can I use JsSIP from any web browser? //在所有浏览器都能用JsSIP么

	详见杂项 Interoperability章节
	
What do I need to run a JsSIP environment? //运行JsSIP环境需要什么

	JsSIP是一个SIP的Websocket客户端,他需要一个能连接/交换消息的SIP Websocket服务器
	
Can I connect a JsSIP client directly to my existing SIP server?//我能直接连接SIP服务器么

	是的,它支持SIP over WebSocket详见杂项 Interoperability章节
	
What if my existing SIP server lacks SIP WebSocket Server capabilities?//我的服务器没有WebSocket功能怎么办

	你可以放服务器上一个OverSIP 的SIP Websocket代理
	
		你的SIP服务器/注册端必须能够执行路径机制
		
		如果不能(比如Asterisk就不支持路径),使用OverSIP 的OutboundMangling模块

Asterisk rejects REGISTER from JsSIP//Asterisk与注册的冲突

	Asterisk不像SIP注册机一样联络报头含有"xxxxx.invalid"域的URI.

	如果用Asterisk来做注册机的话,参考UA配置选项的 hack_ip_in_contact.
	

	