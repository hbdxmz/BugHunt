1、访问管理后台，该平台未提供账号，输入任意账号密码登录
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/859e6c0e-c77f-4953-8bb8-910862cb58f8)  

![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/ac469d65-b922-4a07-9e67-d492809c4c2c)

![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/89f8d2d2-e985-4bc0-b524-63a6ef7c3dee)  

![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/b6558fb7-6fd7-4654-b8ef-514ae3f3b55e)

![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/9e336f5a-c69e-4cd4-80d1-28be3ff9b4a5)  

这里后台代码应该只是校验了Authorization 是否不为null且没过期，满足条件就会调用sys/user/add接口 执行在数据库插入新增用户的代码，并未校验这个Authorization的用户身份
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/95cbb74f-bf7e-46ac-bae5-5d3c417adfc9)  

![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/bf01e00b-902e-4b8a-a5e5-188367c5bad1)





 


