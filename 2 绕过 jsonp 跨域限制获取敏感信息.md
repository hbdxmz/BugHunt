

（1）登录站点 a 后，选择手机号码修改业务  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/6de4a73c-d64c-47c6-adf4-50429f39d2b2)

（2）之后进入信息审核页面，按 F12 进入浏览器开发者模式，选择“网络”  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/a837c46e-eefe-4dc2-84f3-8d16be1e88f6)

（3）刷新页面，查看请求，发现在三个回调函数调用中会返回用户的敏感信息（用户名，资金账号，手机号等）  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/630d74c7-e7eb-40e8-b451-63784e9f2a6b)


（4）可以看到，回调函数名都是采用了长的随机数命名，这样每次调用都是一次性的，下次调用又是新的随机函数名，再次访问该 jsonp 接口将不会返回数据，https://a.com/hall/biz/judge/login?callback=jQuery112406353168200498462_1596181627657&_=1596181627658  

（5）由于同源策略的限制，其他站点想要获取到该站点下的这些用户敏感数据就可以尝试使用 jsonp 进行跨域获取。  

（6）这里尝试将回调函数后面的随机数删掉再进行跨域获取原始回调函数调用包含蓝色标记的随机数：
https://a.com/hall/biz/judge/login?callback=jQuery112406353168200498462_1596181627657&_=1596181627658
将蓝色标记的随机数删掉，只保留”jQuery“：
https://a.com.cn/hall/biz/judge/login?callback=jQuery  

（7）jsonp 跨域主要是利用<script>标签可以进行跨域访问这一点，先创建一个html 文件，用<script>标签的 src 属性去调用上面站点中返回用户敏感数据的那三个回调函数，接着在接收函数中将获取到的数据在控制台打印出来：  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/3e24e524-35fa-4e6a-869f-ed96497932c5)

（8）登录状态下在浏览器打开该 html 页面，按 F12 查看控制台，发现成功在控制台中打印出了用户敏感数据，说明删掉随机数后可以正常调用jsonp 接口，算是随机数命名的简单绕过，最后诱骗已登陆系统的用户去访问该构造好的url去获取他的敏感信息（用户名，资金账号，手机号等）  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/8cf3b7b3-d46d-4063-a6ea-8f652d1c309f)

(9) 挖掘方法  
1、浏览器的 F12 打开开发者模式，点击 Network 窗口并勾选preservelog
2、然后在 Filter 中筛选 jsonp 的关键字，常见的关键字有Cb、callback、jsoncb、jsonpcb、jsonp、jQuery、jsoncallback、jsonpcallback、jsoncall、jsonpcall
