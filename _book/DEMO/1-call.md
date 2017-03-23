# 语音通知DEMO 示例

<!-- toc -->

 语音通知，第三方开发者调用语音通知接口，平台向被叫方发起呼叫；在被叫方接通后，播放指定语音。

例子：呼叫188xxxxxxxx号码，接通后，播报123456789。

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 语音通知
     */
    @Test
    public void notifyCall(){
        SapiSdk sapiSdk = new SapiSdk(url,certId,secretKey);
        String from = null;//主叫号码，只能填租用的号码，不填平台会自动选择一个可用的 选填
        String to = "188xxxxxxxx";//被叫号码 必填
        Integer maxDialDuration = null;//最大拨号等待时间
        Integer repeat = null;//重复播放次数，默认1，表示播放两次。注意，0表示播放一次，不重复 选填
        String[] files = null;//放音文件列表，需要先上传放音文件
        String[][] playContent = {{"123456789","1"}};//这里表示 播放数字123456789
        String userData = "";
        try {
            String result = sapiSdk.notifyCall(appId,from,to,maxDialDuration,repeat,files,playContent,userData);
            System.out.println("接口返回数据："+result);
            //接口返回数据：{"code":"000000","msg":"请求成功","data":{"callId":"8a2a294c5afa26f7015afa32d54f0000","user_data":""}}
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
