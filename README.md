# WsNet
android WebService的网络请求库

https://raw.githubusercontent.com/zdmisif/WsNet/master

添加对应的maven库地址
```
maven {  
   url "https://raw.githubusercontent.com/zdmisif/WsNet/master"  
} 
```

添加对应的库
```
dependencies{  
        compile 'com.sandu.develop:wsnet:0.0.1'  
}  
```
## 三方库使用的简单说明

### 1.创建Wsnet对象，初始化Webservice的服务名和接入点（用网上查询IP所属地的Webservice作为例子）
```
Wsnet wsnet = new Wsnet();
wsnet.init("http://WebXml.com.cn/", "http://www.webxml.com.cn/WebServices/IpAddressSearchWebService.asmx");
```
### 2.生成一个定义方法的接口类
```
public interface WsApi {

    @WsMethodName("getCountryCityByIp")
    WsCall getCountryCityByIp(@WsParam("theIpAddress") String theIpAddress);

}
```
WsMethodName 对应声明对应的方法
WsParam 对应方法的参数
WsFileParam 上传图片的参数，传的是图片数据类型为byte[]
类似Retrofit的用法

### 3.创建接口对应的一个实体类,调用对应的方法即可
```
WsApi wsApi = wsnet.create(WsApi.class);
wsApi.getCountryCityByIp("119.132.20.130").execute(new WsCallBack() {
            @Override
            public void onSuccess(String result) {
                //返回的结果数据
            }

            @Override
            public void onFaile(String error) {
                //调用的错误，返回错误信息
            }
        });
```

### PS：目前对返回的数据，都是返回一个字符串，具体返回的数据格式，需要在得到对应的结果数据再进行转换。



