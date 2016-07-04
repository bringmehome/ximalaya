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
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
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

- 类型：数字
- 默认值：1
- 描述：返回第几页，必须大于等于1，不填默认为1

pagesize：

- 类型：数字
- 默认值：10
- 描述：返回的每页的条数

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
track_title | 字符串 | 声音名称
track_tags | 字符串 | 声音标签列表
track_intro | 字符串 | 声音简介
cover_url_small | 字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
duration   | 数字  | 声音时长，单位秒
play_count | 数字 | 播放数 
favorite_count | 数字 | 喜欢数 
comment_count |  数字  |评论数
download_count | 数字 |下载次数
play_url_32 | 字符串 | 播放地址32位
play_size_32   | 数字 | 32位声音文件大小
play_url_24_m4a | 字符串 | 声音m4a格式24位地址
play_size_24_m4a  |  数字 |声音m4a格式24位大小
can_download  |  Bool   | 可否下载，true-可下载，false-不可下载
download_url  |  数字 | 声音下载地址
download_size | 数字 | 声音下载大小
order_num  | 数字 | 一条声音在一个专辑中的位置

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
    page:1,
    pagesize:2
};
ximalaya.getSearchedTracks(param, function(ret, err){
  if(ret)
    alert(JSON.stringify(ret));
  else
    alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getCategories**
<div id="getCategories"></div>

    获取喜马拉雅的内容分类

    getCategories(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
order_num | 数字 | 排序值，值越小排序越在前
category_name | 字符串 | 分类名
cover_url_small | 字符串 | 分类封面小图
cover_url_middle | 字符串 | 分类封面中图
cover_url_large | 字符串 | 分类封面大图

```js
{
  "result": [
    {
      "order_num": 1,
      "category_name": "资讯",
      "cover_url_small": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnBP5BhAAAGSmFXT7I057.png",
      "cover_url_middle": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnjLKBmAAAGSmFXT7I174.png",
      "cover_url_large": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnjLKBmAAAGSmFXT7I174.png"
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
ximalaya.getCategories(function(ret, err){
  if(ret)
    alert(JSON.stringify(ret));
  else
    alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getHotTracks**
<div id="getHotTracks"></div>

    根据分类和标签获取热门声音列表

    getHotTracks({params}, function(ret, err))

##params

categoryid：

- 类型：字符串
- 默认值：无
- 描述：分类ID，指定分类

page：

- 类型：数字
- 默认值：1
- 描述：返回第几页，必须大于等于1，不填默认为1

pagesize：

- 类型：数字
- 默认值：10
- 描述：返回的每页的条数

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
track_title | 字符串 | 声音名称
track_tags | 字符串 | 声音标签列表
track_intro | 字符串 | 声音简介
cover_url_small | 字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
duration   | 数字  | 声音时长，单位秒
play_count | 数字 | 播放数 
favorite_count | 数字 | 喜欢数 
comment_count |  数字  |评论数
download_count | 数字 |下载次数
play_url_32 | 字符串 | 播放地址32位
play_size_32   | 数字 | 32位声音文件大小
play_url_24_m4a | 字符串 | 声音m4a格式24位地址
play_size_24_m4a  |  数字 |声音m4a格式24位大小
can_download  |  Bool   | 可否下载，true-可下载，false-不可下载
download_url  |  数字 | 声音下载地址
download_size | 数字 | 声音下载大小
order_num  | 数字 | 一条声音在一个专辑中的位置

```js
{
  "result": [
    {
      "id": 0,
      "kind": "track",
      "track_title": "日本小孩子为什么没人想当老板？",
      "track_tags": "",
      "track_intro": "",
      "cover_url_small": "http://fdfs.xmcdn.com/group6/M07/AE/95/wKgDg1dzg5yzi7tOAACL4yEqAYg563_web_meduim.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group6/M07/AE/95/wKgDg1dzg5yzi7tOAACL4yEqAYg563_web_large.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group6/M07/AE/95/wKgDg1dzg5yzi7tOAACL4yEqAYg563_mobile_large.jpg",
      "duration": 720,
      "play_count": 243096,
      "favorite_count": 649,
      "comment_count": 401,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group8/M0B/A1/2A/wKgDYFdziISj_o6YACv05VJsKB8557.mp3",
      "play_size_32": 2880741,
      "play_url_24_m4a": "http://audio.xmcdn.com/group7/M01/A1/B7/wKgDWldzhoiA1TMdACIHfGiWyxA508.m4a",
      "play_size_24_m4a": "2230140",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group6/M07/AA/86/wKgDhFdzg6WQpGL_AC2cjZTaqhg590.aac",
      "download_size": 2989197,
      "order_num": 0
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
    categoryid: "1",
    page: 1,
    pagesize: 2
};
ximalaya.getHotTracks(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getAlbumlist**
<div id="getAlbumlist"></div>

    根据分类和标签获取某个分类某个标签下的专辑列表(最火/最新/最多播放)

    getAlbumlist({params}, function(ret, err))

##params

categoryid：

- 类型：字符串
- 默认值：无
- 描述：分类ID，指定分类，为0时表示热门分类

calcdimension：

- 类型：数字
- 默认值：无
- 描述：计算维度，现支持最火（1），最新（2），经典或播放最多（3）

page：

- 类型：数字
- 默认值：1
- 描述：返回第几页，必须大于等于1，不填默认为1

pagesize：

- 类型：数字
- 默认值：10
- 描述：返回的每页的条数

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | ID
album_title | 字符串 | 专辑名称
album_tags | 字符串 | 专辑标签列表
album_intro | 字符串 | 专辑简介
cover_url_small  |  字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
play_count | 字符串 | 专辑播放次数
favorite_count | 字符串 | 专辑喜欢数
include_track_count | 字符串 | 专辑包含声音数
can_download | Bool | 能否下载，true-可下载，false-不可下载

```js
{
  "result": [
    {
      "id": 392497,
      "album_title": "老赵说天下-话题脱口秀",
      "album_tags": "",
      "album_intro": "《老赵说天下》新潮时讯 脱口秀 一天一个话题 互动QQ群1149391",
      "cover_url_small": "http://fdfs.xmcdn.com/group16/M02/5E/A7/wKgDbFcrI_fBGDk5AAG3wAjciBU628_mobile_small.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group16/M02/5E/A7/wKgDbFcrI_fBGDk5AAG3wAjciBU628_mobile_meduim.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group16/M02/5E/A7/wKgDbFcrI_fBGDk5AAG3wAjciBU628_mobile_large.jpg",
      "play_count": 5390495,
      "favorite_count": 0,
      "include_track_count": 226,
      "can_download": true
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
var param = {
    categoryid: "1",
    calcdimension: "1",
    page: 2,
    pagesize: 5
};
ximalaya.getAlbumlist(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本


#**getTracks**
<div id="getTracks"></div>

    专辑浏览，根据专辑ID获取专辑下的声音列表

    getTracks({params}, function(ret, err))

##params

albumid：

- 类型：数字
- 默认值：无
- 描述：专辑ID

sort：

- 类型：字符串
- 默认值：无
- 描述：asc-正序或desc-倒序，默认为asc-正序

page：

- 类型：数字
- 默认值：1
- 描述：返回第几页，必须大于等于1，不填默认为1

pagesize：

- 类型：数字
- 默认值：10
- 描述：返回的每页的条数

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
track_title | 字符串 | 声音名称
track_tags | 字符串 | 声音标签列表
track_intro | 字符串 | 声音简介
cover_url_small | 字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
duration   | 数字  | 声音时长，单位秒
play_count | 数字 | 播放数 
favorite_count | 数字 | 喜欢数 
comment_count |  数字  |评论数
download_count | 数字 |下载次数
play_url_32 | 字符串 | 播放地址32位
play_size_32   | 数字 | 32位声音文件大小
play_url_24_m4a | 字符串 | 声音m4a格式24位地址
play_size_24_m4a  |  数字 |声音m4a格式24位大小
can_download  |  Bool   | 可否下载，true-可下载，false-不可下载
download_url  |  数字 | 声音下载地址
download_size | 数字 | 声音下载大小
order_num  | 数字 | 一条声音在一个专辑中的位置

```js
{
  "result": [
    {
      "id": 0,
      "kind": "track",
      "track_title": "【财经火眼】商务部：富士进口相纸反倾销新税率今起征",
      "track_tags": "",
      "track_intro": "",
      "cover_url_small": "http://fdfs.xmcdn.com/group13/M06/A2/83/wKgDXld0fkPyM4VjAACP7yfFdQs951_web_meduim.png",
      "cover_url_middle": "http://fdfs.xmcdn.com/group13/M06/A2/83/wKgDXld0fkPyM4VjAACP7yfFdQs951_web_large.png",
      "cover_url_large": "http://fdfs.xmcdn.com/group13/M06/A2/83/wKgDXld0fkPyM4VjAACP7yfFdQs951_mobile_large.png",
      "duration": 96,
      "play_count": 5109,
      "favorite_count": 1,
      "comment_count": 0,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group5/M0A/94/8E/wKgDtld0WGPCRHE3AAXf2BQyNw0067.mp3",
      "play_size_32": 384984,
      "play_url_24_m4a": "http://audio.xmcdn.com/group5/M00/95/F0/wKgDtVd0WGTyVTg1AASMsnbNtUY458.m4a",
      "play_size_24_m4a": "298162",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group5/M00/95/F0/wKgDtVd0WGPizeF8AAXiA0ib02g916.aac",
      "download_size": 385539,
      "order_num": 3
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
    albumid: 3985798,
    sort: "desc",
    page: 2,
    pagesize: 3           
};
ximalaya.getTracks(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```

##补充说明

    无

##可用性

    Android系统, iOS系統

    可提供的1.0.0及更高版本

<div id="errcode"></div>
#**错误码**

code | 描述
:-----------  | :-------------:
0 | 请求成功
9400 | 参数错误
9001 | 已经初始化了
9002 | 未初始化
9003 | JSON组装异常
