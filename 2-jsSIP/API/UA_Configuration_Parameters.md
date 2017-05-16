UA Configuration Parameters

	JsSIP.UA需要一个配置对象,包括可选/必选的参数对象
	
	var socket = new JsSIP.WebSocketInterface(ws://sip-ws.example.com);

	var configuration = {
		sockets  : [ socket ],
		uri      : 'sip:alice@example.com',
		password : 'superpassword'
	};

	var ua = new JsSIP.UA(configuration);
	
	参数列表如下
	
Mandatory parameters //必选参数

	uri
	
	SIP的uri关联用户代理(UA),这是一个提供者提供的SIP地址
	
	uri: "sip:alice@example.com"
	
	sockets
	
	JsSIP.Socket实例的集合,本参数有以下几种不同的表示方式
	
	单一的JsSIP.Socket实例	
	JsSIP.Socket实例数组
	一个数组对象,定义带权重的JsSIP.Socket实例,权重大的Sockets优先级高于低的
	
	sockets: socket

	sockets: [
	  socket1,
	  socket2,
	]

	sockets: [
	  {socket: socket1, weight: 10},
	  {socket: socket2, weight: 1}
	]

Optional parameters //可选参数

	authorization_user //认证用户
	
	字符串类型,用户名,生成认证证书时使用,未定义的话使用uri参数列表里面的那个名字
	
		authorization_user: "alice123"
	
	connection_recovery_max_interval //重连最大时间间隔
	
	WebSocket试图重连的最大时间间隔,单位秒,默认30
	
		connection_recovery_max_interval: 60
		
	connection_recovery_min_interval //重连最小时间间隔
	
	WebSocket试图重连的最小时间间隔,单位秒,默认2
	
		connection_recovery_min_interval: 4
		
	contact_uri //联系标识(通信录,电话本)
	
	字符串类型,表示用于Contact头字段的联系地址.给出的URI主机被用于传递头的地址参数
	
	display_name //显示名
	
	呼叫/发送IM信息时显示的呼叫部分的名字标识,它不能含有双引号,即使多字节的也不行(因为JsSIP会用""包含它的值)
	
		display_name: "Alice ¶€ĸøĸø"
		
	instance_id //实例ID
	
	字符串类型,表示一个UUID URI,被作为一个UA实例的实例ID当使用GRUU时
	
	Note: UUID (universally unique identifier通用唯一识别码)GRUU(Globally Routable UA URI全局路由用户代理用户资源标识)
	
		instance_id: "uuid:8f1fa16a-1165-4a96-8341-785b1ef24f12"

		instance_id: "8f1fa16a-1165-4a96-8341-785b1ef24f12"

	no_answer_timeout //置拒绝未接时长
	
	如果没有回应的话,呼入通话在该时长之后被拒接.默认60
	
		no_answer_timeout: 120
	
	session_timers //会话定时器
	
	会话定时器是否支持,默认值true
	
		session_timers: false
	
	password //密码
	
	SIP认证的密码.
	
	SIP密码原文件,明文。JsSIP在初次认证成功之后会在内存中删除该密码,替代的会存储 ha1和realm合成的
		
		password: "1234"
	
	realm //域
	
	SIP认证的域,字符串类型
	
	只在SIP密码明文未提供时有用,同时需要提供ha1
	
		realm: "mydomain.com"
		
	星号用户可以使用星号(*)作为域
	
	ha1 //哈希
	
	SIP 认证HA1的哈希,字符串类型,用于认证摘要
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	