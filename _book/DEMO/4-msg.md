# 发送短信示例

<!-- toc -->

第三方开发者，在使用消息发送接口时，需要先创建模板，之后再发送。

模板可以通过控制台手工添加，也可以通过API调用添加，模板只有经过审核通过才可以使用。

系统默认拥有供测试使用

模板编号：10001

模板内容：【壹耘】您的手机验证码为：#*#，请在#*#内进行验证。

## 新增模板

例子：通过接口新增模板

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 添加模板
     */
    @Test
    public void addTemplate(){
        MessageSapiSdk messageSapiSdk = new MessageSapiSdk(url,certId,secretKey);
        String name = "验证模板";//名称
        String type = "msg_sms";//msg_sms表示短信类型
        String content = "【XX信通】您的验证码是：#*#";//模板内容
        String remark = "备注使用场景";//备注使用场景
        try {
            String result = messageSapiSdk.addTemplate(appId,name,type,content,remark);
            System.out.println("接口返回数据："+result);
            //接口返回数据：{"code":"000000","msg":"请求成功","data":{"name":"验证模板","type":"msg_sms","tempId":"10001","content":"【XX信通】您的验证码是：#*#","status":0,"remark":"备注使用场景"}}
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```



## 消息发送接口

消息接口包含，单发接口，群发接口，查询发送记录接口。

例子1：给用户188xxxxxxxx发送模板编号为10001（模板内容：【XX信通】您的验证码是：#*#）,验证码为：123456

```java
 	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 短信单发
     */
	@Test
    public void send(){
        MessageSapiSdk messageSapiSdk = new MessageSapiSdk(url,certId,secretKey);
        String tempId = "10001";//模板ID
        String tempArgs = "123456";//模板参数，用英文分号分隔
        String mobile = "188xxxxxxxx";//目标手机号码
        try {
            String result = messageSapiSdk.sendSms(appId,mobile,tempId,tempArgs);
            System.out.println("接口返回数据："+result);
          //接口返回数据：{"code":"000000","msg":"请求成功","data":{"msgKey":"c71afe4b63034d9bb6e70f7785aa82e5"}}
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```

例子2：给5个用户发送模板编号为10001（模板内容：【壹耘】您的验证码是：#*#）,验证码为：123456

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 群发任务
     */
 	@Test
    public void addMassTask(){
        MessageSapiSdk messageSapiSdk = new MessageSapiSdk(url,certId,secretKey);
        String taskName = "群发任务1";//任务名称
        String tempId = "10001";//模板ID
        String tempArgs = "123456";//模板参数，用英文分号分隔
        String mobiles = "188xxxxxx1,188xxxxxx2,188xxxxxx3,188xxxxxx4,188xxxxxx5";//目标手机号码
        String sendTime = "";//发送时间格式（yyyy-MM-dd hh:mm:ss）
        try {
            String result = messageSapiSdk.addSmsMassTask(appId,taskName,tempId,mobiles,tempArgs,sendTime);
            System.out.println("接口返回数据："+result);
          	//接口返回数据：{"code":"000000","msg":"请求成功","data":{"msgKey":"6c69cc043a31ff08c6bc2771f4a4a0ab","state":0,"invalidMobiles":[]}}
          //其中invalidMobiles是失败的号码集合
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

```

例子3：查询刚刚发送的记录

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识 	
	/**
     * 查询发送记录
     */
 	@Test
    public void log(){
        MessageSapiSdk messageSapiSdk = new MessageSapiSdk(url,certId,secretKey);
        String msgKey = "";//任务标识
        Integer pageNo = null;//第几页
        Integer pageSize = null;//每页记录数
        try {
            String  result = messageSapiSdk.getSmsSendResult(appId, msgKey,pageNo,pageSize);
            System.out.println("接口返回数据："+result);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```

