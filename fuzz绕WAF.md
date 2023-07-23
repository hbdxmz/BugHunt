一个某大厂WAF，常规的注释等方法被拦截  
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/6cc2c5bf-fba7-44c2-a7bf-d96448abdf52)

绕过的技巧就是插入了一个"\\",通常select version\\()无法在数据库中执行，但是在这个应用中，插入"\\"能绕过WAF执行sql，用瞎几把测的方式有时候真能绕过waf
![image](https://github.com/hbdxmz/BugHuntLogger/assets/94107024/e5bd2292-8156-497e-ab53-7554611f3d09)
