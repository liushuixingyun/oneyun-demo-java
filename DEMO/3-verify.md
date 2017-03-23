# 语音验证码DEMO 示例

<!-- toc -->

语音验证码，第三方开发者调用语音验证码接口，首先向被叫方发起呼叫； 在接听后，播放提示语音和验证码内容。

例子：呼叫号码188xxxxxxxx播放验证码123456

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 语音验证码
     */
    @Test
    public void verifyCall(){
        SapiSdk sapiSdk = new SapiSdk(url,certId,secretKey);
        String from = null;//主叫号码，只能填租用的号码，不填平台会自动选择一个可用的 选填
        String to = "188xxxxxxxx";//被叫号码 必填
        Integer maxDialDuration = null;//最大拨号等待时间（秒），默认50秒 选填
        Integer repeat = null;//重复播放次数，默认1，表示播放两次。注意，0表示播放一次，不重复 选填
        String[] files = null;//验证码提示音文件 文件名为开发者用户中心的放音文件名 选填
        String verifyCode = "123456";//要播放的验证码内容，只能是十进制数字，1到12个字符 选填
        //参数 files 与 verifyCode 不得同时为空。 两者都被赋值的情况下，首先播放 files 指定的文件，然后才播放 verifyCode 中的内容。
        String userData = null;//用户数据,最大128个字符 选填
        try {
            String result = sapiSdk.verifyCall(appId,from,to,maxDialDuration,repeat,files,verifyCode,userData);
            System.out.println("接口返回数据："+result);
            //接口返回数据：{"code":"000000","msg":"请求成功","data":{"callId":"8a2d9fed5afa3b27015afa4952c70003"}}
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```