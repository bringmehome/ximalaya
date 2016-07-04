##描述: ximalaya

* [initXmly](#initXmly)

* [getSearchedTracks](#getSearchedTracks)

* [getCategories](#getCategories)

* [getHotTracks](#getHotTracks)

* [getAlbumlist](#getAlbumlist)

* [getTracks](#getTracks)

* [错误码](#errcode)

##**概述**

本模块封装了喜马拉雅的声音获取的功能，声音最终返回的是mp3或者aac等格式的URL,你需要集成其他的模块比如"netAudio"来播放声音

>使用须知

1、使用此模块需要先在喜马拉雅平台完成注册，并得到对应的key，[传送门](http://open.ximalaya.com/doc/18)

2、得到了appkey，appsecret后，参考[接入演示](https://github.com/bringmehome/ximalaya)


#**initXmly**
<div id="initXmly"></div>

    初始化模块信息，打开页面require完成就应该去执行

    initXmly({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
  "code": 0,
  "message": "success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9001,
  "message": "already initialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    appsecret:"e1f6e1927fdab1ef1a8de1997557b6db"
};
ximalaya.initXmly(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getSearchedTracks**
<div id="getSearchedTracks"></div>

    通过关键字搜索声音

    getSearchedTracks({params}, function(ret, err))

##params

keyword：

- 类型：字符串
- 默认值：无
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

categoryid：

- 类型：字符串
- 默认值：无，
- 描述：分类ID，不填或者为0检索全库

page：

- 类型：number
- 默认值：无
- 描述：返回第几页，必须大于等于1，不填默认为1

pagesize：

- 类型：number
- 默认值：10
- 描述：返回的每页的条数

##callback(ret,err)

ret：

- 类型：JSON对象


参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
track_title | String | 声音名称
track_tags | String | 声音标签列表
track_intro | String | 声音简介
cover_url_small | String | 声音封面小图
cover_url_middle  |  String | 声音封面中图
cover_url_large | String | 声音封面大图
duration   | Int类型  | 声音时长，单位秒
play_count | Int | 播放数 
favorite_count | Int | 喜欢数 
comment_count |  Int  |评论数
download_count | Int |下载次数
play_url_32 | String | 播放地址32位
play_size_32   | Int | 32位声音文件大小
play_url_24_m4a | String | 声音m4a格式24位地址
play_size_24_m4a  |  Int |声音m4a格式24位大小
can_download  |  Bool   | 可否下载，true-可下载，false-不可下载
download_url  |  String | 声音下载地址
download_size | Int | 声音下载大小
order_num  | Int | 一条声音在一个专辑中的位置

```js
{
  "result": [
    {
      "track_title": "单面爱情",
      "track_tags": "故事,治愈,温暖,片刻,随笔",
      "track_intro": "用声音交换世界",
      "cover_url_small": "http://fdfs.xmcdn.com/group5/M04/E3/89/wKgDtVSOl6TxfG9NAAGO_vkIqwY278_web_meduim.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group5/M04/E3/89/wKgDtVSOl6TxfG9NAAGO_vkIqwY278_web_large.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group5/M04/E3/89/wKgDtVSOl6TxfG9NAAGO_vkIqwY278_mobile_large.jpg",
      "duration": 1035,
      "play_count": 1373,
      "favorite_count": 5,
      "comment_count": 3,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group5/M05/E2/A8/wKgDtlSOlovTwR05AD9VMnMC_vI747.mp3",
      "play_size_32": 4150578,
      "play_url_24_m4a": "http://audio.xmcdn.com/group7/M0A/51/C5/wKgDX1W1KVOx8QtpADDiOiLNwBA700.m4a",
      "play_size_24_m4a": "3203642",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group5/M05/E2/A8/wKgDtlSOln_h874vAEG4Tac1P3s358.aac",
      "download_size": 4307021,
      "order_num": 675
    }
  ]
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9002,
  "message": "uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
        keyword:"爱情",
    };
ximalaya.getSearchedTracks(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getSearchedTracks**
<div id="getSearchedTracks"></div>

    初始化模块信息，打开页面require完成就应该去执行

    getSearchedTracks({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
  "code": 0,
  "message": "success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9001,
  "message": "already initialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    appsecret:"e1f6e1927fdab1ef1a8de1997557b6db"
};
ximalaya.initXmly(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**initXmly**
<div id="initXmly"></div>

    初始化模块信息，打开页面require完成就应该去执行

    initXmly({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
  "code": 0,
  "message": "success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9001,
  "message": "already initialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    appsecret:"e1f6e1927fdab1ef1a8de1997557b6db"
};
ximalaya.initXmly(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**initXmly**
<div id="initXmly"></div>

    初始化模块信息，打开页面require完成就应该去执行

    initXmly({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
  "code": 0,
  "message": "success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9001,
  "message": "already initialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    appsecret:"e1f6e1927fdab1ef1a8de1997557b6db"
};
ximalaya.initXmly(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**initXmly**
<div id="initXmly"></div>

    初始化模块信息，打开页面require完成就应该去执行

    initXmly({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，[我的应用](http://open.ximalaya.com/apps)

##callback(ret,err)

ret：

- 类型：JSON对象

内部字段：

```js
{
  "code": 0,
  "message": "success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9001,
  "message": "already initialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    appsecret:"e1f6e1927fdab1ef1a8de1997557b6db"
};
ximalaya.initXmly(param, function(ret, err){
    if(ret)
        console.log(JSON.stringify(ret));
    else
        console.log(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本



<div id="9"></div>
#**错误码**

1. 0        请求成功

2. 90000    用户未登陆

3. 90001    参数为空

4. 其他，阿里返回的code和错误提示