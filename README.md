# 喜马拉雅 For APICloud的接入教程

* [创建自定义模块](#testver)

* [测试模块](#finalver)

<div id="testver"></div>
#**准备工作**

1、下载自定义模块，[传送门](https://github.com/bringmehome/ximalaya/blob/master/%E8%87%AA%E5%AE%9A%E4%B9%89%E6%A8%A1%E5%9D%97/ximalayakey.zip)

2、因为调用喜马拉雅接口，需要先初始化，而初始化的时候喜马拉雅会做身份校验这时候需要传人appkey，appsecret, Android客户端包名，于是需要完成以下几步

>1、创建应用获取appkey, appsecret, Android客户端包名, [创建应用](http://open.ximalaya.com/apps)

其中Android客户端包名获取，见下图，android的签名见包名上面

![](./img/packagename.png)

>2、解压刚刚下载的自定义模块ximalayakey.zip

>3、编辑AndroidManifest.xml文件，修改其中的app_key和pack_id的value

![](./img/manifest.png)

>4、压缩文件夹为zip格式，替换之前测试用的自定义模块

![](./img/package.png)

<div id="finalver"></div>
#**测试模块**

1、将此作为自定义模块上传到APICloud的对应项目，并使用，同时引用聚合API里的ximalaya模块

2、下载测试demo，[传送门](https://github.com/bringmehome/ximalaya/blob/master/%E6%B5%8B%E8%AF%95Demo/widget.zip)

3、解压后将其中的文件复制到自己的测试项目中，运行看看效果，是不是这个样子

![](./img/xmlyapp.png)

如果还有其他问题请邮件(bringmehome@vip.qq.com)
(完)