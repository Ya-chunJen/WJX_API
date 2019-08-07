


## SSO创建和登录接口

### 接口介绍

使用该接口，可以通过单点登录（SSO）的方式创建子账户，创建成功之后可以通过此接口登录子账户。使用此接口创建的用户，属于主账户下属的子账户，权益同主账户同步。除创建和登录方式不同外，其他权益、设置同手动创建的子账户完全一致。



### 接口参数说明

请求方式：Get

接口链接：www.wjx.cn/zunxiang/login.aspx?appid=&subuser=&moblie=&email=&roleId=&ts=&sign=

| 参数名  | 参数说明                                                     | 是否必须 |
| ------- | ------------------------------------------------------------ | -------- |
| appid   | 开发ID，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| appkey  | 开发秘钥，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| subuser | 创建子账户的用户名，请使用绝对唯一性字段                     | 是       |
| moblie  | 创建子账户绑定的手机号码                                     | 否       |
| email   | 创建子账户绑定的邮箱                                         | 否       |
| roleId  | 创建子账户的角色，留空默认为“问卷管理员”                     | 否       |
| ts      | 时间戳，如“1562812073”表示2019/7/11 10:27:53，有效期30秒     | 是       |
| sign    | 加密签名算法 sigh=sha1(appid+appkey+subuser+moblie+email+roleId+ts) | 是       |



mobile，手机号码为可选字段，留空时子账户的手机号码为空；

email，邮箱可选字段，留空时子账户的邮箱为空；

roleId，子账户角色为可选字段，留空时子账户的角色默认为“问卷管理员”，可选参数角色对应关系分别为：1-系统管理员，2-问卷管理员，3-统计结果查看员，4-完整结果查看员。



### 子账户的创建/登录和删除

创建：第一次使用以上接口时，就是子账户的创建过程；

登录：子账户登录和创建使用相同的接口，其中手机号码、邮箱、角色三个字段，仅在首次创建时有效，在第二次登录时如果三个字段信息有更改，也不会将传递信息更新到问卷星系统；

删除：如需删除子账户，需要主账户登录后，在多用户管理页面手动删除。需要注意是：在您自己系统删除一个员工账户后，无法自动同步删除其在问卷星对应的子账户。





## 获取SSO子账户问卷列表接口

### 接口介绍

通过此接口，可以获取某一个子账户问卷管理员名下的问卷列表。

### 接口参数说明

请求方式：Get

接口链接：http://www.wjx.cn/zunxiang/getuserq.aspx?appid=&username=&ts=&folder=&sign=



| 参数名   | 参数说明                                                     | 是否必须 |
| -------- | ------------------------------------------------------------ | -------- |
| appid    | 开发ID，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| appkey   | 开发秘钥，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| folder   | 获取特定文件夹下的问卷，留空为全部用户问卷                   | 否       |
| ts       | 时间戳，如“1562812073”表示2019/7/11 10:27:53，有效期30秒     | 否       |
| username | 子账户的用户名                                               | 是       |
| sign     | 加密签名算法 sigh=sha1(appid+appkey+username+ts+folder)      | 是       |



### 获取到数据说明

此接口会有10分钟的缓存时间，新增的问卷可能需要10分钟以后才能获取。

数据格式：JSON

数据示例： [{"qid":"89767","name":"新考试","begindate":"2017-08-20 11:52:43","answercount":"5"},{"qid":"89819","name":"考试","begindate":"2017-08-18 21:21:35","answercount":"4"}]

qid：问卷ID

name：问卷标题

begindata：问卷的创建时间

answercount：当前问卷答卷数



## 获取SSO子账户答卷数据接口

### 接口介绍

通过此接口可以获取到部分答卷数据，包括：提交序号、参与者姓名、总分、提交时间、提交所用时间。需要注意的是，只有答卷总数少于20000才能使用此接口，而且此接口只能获取到部分数据而且全部答卷详情数据。如需获取全部答卷详情数据，可以参考：数据推送的API接口。

### 接口参数说明

请求方式：Get

接口链接：http://www.wjx.cn/zunxiang/getjoinlist.aspx?appid=&activity=&ts=&sign=&pageindex=&pagesize=

| 参数名    | 参数说明                                                     | 是否必须 |
| --------- | ------------------------------------------------------------ | -------- |
| appid     | 开发ID，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| appkey    | 开发秘钥，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| activity  | 问卷ID，指定需要获取哪一份问卷的答卷数据                     | 是       |
| ts        | 时间戳，如“1562812073”表示2019/7/11 10:27:53，有效期30秒     | 否       |
| sign      | 加密签名算法 sigh=sha1(appid + appkey + activity + ts)       | 是       |
| pageindex | 页码序号                                                     | 否       |
| pagesize  | 指定每页数据条数，默认每页为10条数据，且最多不超过1000条数据 | 否       |



### 获取到数据说明

数据格式：JSON

数据示例：

[{"parterjoiner":"test2","totalvalue":"15","index":"3","timetaken":"8","submittime":"2017-08-20 14:25:39"},{"parterjoiner":"test3","totalvalue":"15","index":"4","timetaken":"141","submittime":"2017-08-20 14:38:55"}]

parterjoiner：参与者姓名

totalvalue：当前答卷得分

index：当前答卷序号

timetaken：当前答卷作答所用的时间，单位：秒

submittime：当前答卷的提示时间



## SSO子账户参与者端接口

### 接口介绍

使用该接口，做为问卷或考试填写参与者的登录之后，可看到一个完善的填写参与者的用户体系，查看到自己需要作答哪些问卷、已经完成了哪些问卷、积分排行等等信息。

### 接口参数说明

请求方式：get

加密链接参数如下：http://www.wjx.cn/zunxiang/qlist.aspx?appid=&username=&joiner=&realname=&dept=&extf=&ts=&sign=

| 参数名   | 参数说明                                                     | 是否必须 |
| -------- | ------------------------------------------------------------ | -------- |
| appid    | 开发ID，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| appkey   | 开发秘钥，需联系尊享版客服生成，生成后可以在多用户管理页面查看 | 是       |
| username | 子账户的用户名，填写参与者登录后看的的是该用户创建的问卷     | 是       |
| joiner   | 填写参与者的用户ID，如工号、学号、手机号等唯一字段           | 是       |
| realname | 填写参与者的真实姓名，如张三                                 | 否       |
| dept     | 填写参与者的部门，会在答卷来源详情中体现                     | 否       |
| extf     | 填写参与者的其他附加信息，不能超过1000个字符                 | 否       |
| ts       | 时间戳，如“1562812073”表示2019/7/11 10:27:53，有效期30秒     | 是       |
| sign     | 加密签名算法 sigh=sha1(appid+appkey+username+joiner+realname+dept+extf+ts) | 是       |



### 访问其他页面

以上接口填写者参与者点击后访问的是用户体系的主页，还可以通过携带参数访问其他不同的页面，如：

1、待参与页面：http://www.wjx.cn/zunxiang/getqlist.aspx?appid=&username=&joiner=&realname=&dept=&extf=&ts=&sign=

2、已参与页面：http://www.wjx.cn/zunxiang/getqlistjoin.aspx?appid=&username=&joiner=&realname=&dept=&extf=&ts=&sign=

3、答卷详情页：http://www.wjx.cn/zunxiang/joinrelquery.aspx?appid=&username=&joiner=&activity=&joinid=&realname=&dept=&extf=&ts=&sign=

访问答卷详情页，需增加两个参数：activity（问卷ID）和joinid（答卷流水号，需使用数据推送接口获取），同时加密签名算法改变为：sign=sha1(appid+appkey+username+joiner+activity+joinid+realname+dept+extf+ts)

