# 语音回拨DEMO 示例

<!-- toc -->

语音回拨，第三方开发者调用语音回拨接口，首先向第一个被叫方发起呼叫；在第一方接听后，向二方放发起呼叫；第二方接听后，双方通话。期间任何一方挂机，就结束语音回拨过程。

被叫的双方不能是同一个号码。

例子：呼叫号码1：188xxxxxxxx；号码2:189xxxxxxxx。

```java
	private static final String url = "";//接口API
    private static final String certId = "";//鉴权账号
    private static final String secretKey = "";//密钥
    private static final String appId = "";//应用标识
    /**
     * 语音回拨
     */
    @Test
    public void callBack(){
        SapiSdk sapiSdk = new SapiSdk(url,certId,secretKey);
        String from1 = null; // 第一方主叫号码 选填 如有绑定IVR号码，可填绑定号码,否则为空
        String to1 = "188xxxxxxxx"; // 第一方被叫号码 必填
        String from2 = null; // 第二方主叫号码 选填 如有绑定IVR号码，可填绑定号码,否则为空
        String to2 = "189xxxxxxxx"; // 第二方被叫号码 必填
        String ringTone = null; // 自定义回铃音 选填
        Integer ringToneMode = null; // 自定义回铃音播放模式 0：收到对端回铃后开始播放 1：拨号时即开始播放，收到对端回铃后停止播放 2：拨号时即开始播放，对端接听或者挂机后停止播放 选填
        Integer maxDialDuration = null; // 最大拨号等待时间（秒）
        Integer maxCallDuration = 50; // 最大接通时间（秒） 必填
        Boolean recording = null; // 是否录音 选填
        Integer recordMode = null; // 录音模式： 0: 双向接通后录音 1：开始呼叫第一方时启动录音 2: 开始呼叫第二方时启动录音 选填
        String userData = null; // 用户数据 选填
        try {
            String result = sapiSdk.duoCallback(appId,from1,to1,from2,to2,ringTone,ringToneMode,maxDialDuration,maxCallDuration,recording,recordMode,userData);
            System.out.println("接口返回数据："+result);
            //接口返回数据：{"code":"000000","msg":"请求成功","data":{"callId":"8a2d9fed5afa3b27015afa40e1290000","user_data":null}}
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```