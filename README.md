# WechatSign

用于微信支付签名第三方应用的
1、前期的准备：把App安装到手机，然后去微信平台下载签名工具：https://open.weixin.qq.com/zh_CN/htmledition/res/dev/download/sdk/Gen_Signature_Android.apk，安转到手机上。打开签名工具：输入你App的包名。然后去微信开放平台的管理中心修改应用签名。这样就不用担心签名的问题了。

2、我们需要的资源其实有以下几样，在开始前，就这些转备好吧
1）微信支付的APPID（还是在微信开放平台查看）

2）微信支付依赖包 ：libammsdk.jar（Demo中复制）
3）一个Activity类 >>> WXPayEntryActivity.java（Demo中复制，注意放的位置：必须在wxapi包下，就是这么霸道）

3、这里开始就可以写代码了：
1）提交订单信息给后台获取加签后的订单信息：这里就是调用服务器接口，看一下你需要传给服务器什么收据了。比如我的项目中需要传给服务器一下的参数：
//票务id
mMap.put("TicketId",ticketId);
//场次id
mMap.put("SeasonId",seasonId);
//主题id
mMap.put("TeamId",teamId);
//当前日期
mMap.put("BookingTime",date);
//女士订票人数
mMap.put("FemalePlayerCount",personTotalNv);
//男士订票人数
mMap.put("MalePlayerCount",personTotalNan);
//支付类型：1：微信
mMap.put("PayType",1)等
这样添加请求参数发起网络访问。然后后去一般会给你还回一个是否提交订单成功的Flag，如果提交订单成功，这样就可以获取到加签后的订单信息（有可能项目根据是否提交订单成功，如果成功还要发起一次网络访问获取加签后的订单信息）

2）Gson解析获取到的加签订单。如果用的是Retrofit那就是直接获得到实体类（我的定义成WXOrderEntity），直接到第三步。

3）调用微信SDK

