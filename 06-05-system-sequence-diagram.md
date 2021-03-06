# System Sequence Diagram （功能模型）

根据我们的[用例分析](<https://github.com/sysu-team/sysu-team.github.io/blob/master/06-02-use-cases.md>)

## 基本功能

1. **用户注册**

   用户在允许微信授权登录之后，如果没有已注册账号，可以点击进入注册界面进行注册。通过输入学号和设置的密码进行账号注册。当学号已被注册时，用户可以联系客服处理或自己找回密码。

2. **用户登录**

   用户在允许微信授权登录之后，如果拥有已注册账号，可以输入学号和密码进行登录。系统确认账号和密码无误后，即可进入系统进行相关委托操作。如账号和密码有误，系统会弹出提示。

3. **浏览委托**

   用户可以在任一时刻在委托广场查看当前已发布的委托。同时对感兴趣的委托可以点击查看详情，了解委托的委托类型、委托地点、委托具体描述、委托报酬、委托截止时间等详细信息。

4. **接受委托**

   接受委托的用户，首先可以查看该委托的详情决定是否接受委托；当点击接受委托按钮时，前端会向后端请求该用户的信誉分情况，以确认用户是否有资格接受该委托；确认符合资格后，将为用户添加此委托，并建立新的交易。

5. **发布委托**

   发布委托的用户发布委托时，首先前端向后端请求该用户的信誉分情况，确认该用户是否有资格发布委托；确认用户资格后，显示填写委托的界面；用户填写完毕后，前端对填写的内容进行格式审查，无误后由用户进行确认；确认完成后自动进行账户积分的预冻结，若账户积分不足系统会进行相应的提示；预冻结完积分之后，系统会分配一个委托id，并向全网进行发布。

6. **交易确认**

   交易确认过程中，当接受委托的用户完成委托后，前端将提醒后端更改交易的状态，并提醒发布委托者交易状态的变更；发布委托者在一定的时间需要对完成的委托进行审核，并确认委托；发布委托者确认委托后，前端请求后端进行交易状态变更并进行系统转账；转账成功后，前端通知接受委托者和发布委托者该交易已经完成。其中若接受委托者长时间未确定，委托过期后将会对接受委托者进行惩罚；若发布委托者长时间未确定，则委托到期后，将自动进行确认操作并完成转账。

7. **发布者取消已发布委托**

   发布委托者有权在任一时刻对自己之前已发布的委托进行取消。当发布委托者对自己已发布的委托进行取消时，后台根据该委托是否已经被接受来对取消者进行处理。如果该委托未被接受，则返回预冻结积分到发布委托者账户上；若该委托已被接受，则返回部分预冻结积分到委托发布者的账户上，其余部分返回到接受委托者账户上作为补偿。同时双方关于该委托达成的初步交易取消。

8. **接受者取消已接受委托**

   接受者在接受委托后，有权在委托到期前对已接受的委托进行取消操作。当接受委托者对已接受委托发起取消操作时，系统将对该取消委托的用户进行一定积分扣除的惩罚，并将该部分积分作为补偿转至发布委托者的账户上。同时解除接受委托者与该委托的缔结关系，并修改该委托的状态，在全网继续进行公布。

## 系统顺序图

**1.用户注册**

![](imgs/06-05/用户注册.jpg)

**2.用户登录**

![](imgs/06-05/用户登录.jpg)

**3.浏览委托**

![](imgs/06-05/浏览委托.jpg)

**4.接受委托**

![](imgs/06-05/接受委托.jpg)

**5.发布委托**

![](imgs/06-05/发布委托.jpg)

**6.交易确认**

![](imgs/06-05/交易确认.jpg)

**7.发布者取消已发布委托**

![](imgs/06-05/发布者取消已发布委托.jpg)

**8.接受者取消已接受委托**

![](imgs/06-05/接受者取消已接受委托.jpg)