/*
Title: ximalaya
Description: ximalaya
*/

<p style="color: #ccc; margin-bottom: 30px;">来自于：开发者</p>

<ul id="tab" class="clearfix">
  <li class="active"><a href="#method-content">Method</a></li>
  <li><a href="#method-content2">参数列表</a></li>
</ul>
   
<div id="method-content">

<div class="outline">

[initXmly](#initXmly)

[getCategories](#getCategories)

[getSearchedTracks](#getSearchedTracks)

[getTags](#getTags)

[getHotTracks](#getHotTracks)

[getAlbumlist](#getAlbumlist)

[getTracks](#getTracks)

[getProvinces](#getProvinces)

[getRadios](#getRadios)

[XmPlayerInit](#XmPlayerInit)

[XmPlayerPlay](#XmPlayerPlay)

[XmPlayerPause](#XmPlayerPause)

[XmPlayerStop](#XmPlayerStop)
</div>



##**概述**

本模块封装了喜马拉雅的声音获取的功能，声音最终返回的是mp3或者aac等格式的URL,你需要集成其他的模块来播放声音,比如"netAudio"；而电台播放的部分你可以使用自带的播放器播放

1、使用此模块需要先在喜马拉雅平台完成注册，并得到对应的key，<a href="http://open.ximalaya.com/doc/18" target="_blank">喜马拉雅开放平台</a>

2、得到了appkey，appsecret后，参考<a href="https://github.com/bringmehome/ximalaya" target="_blank">GitHub接入教程</a>


#**initXmly**
<div id="initXmly"></div>

    初始化模块信息，打开页面require完成就应该去执行

    initXmly({params}, function(ret, err))

##params

appsecret：

- 类型：字符串
- 默认值：无，如果你使用的是github里提供的测试模块这里的appsecret可以传(e1f6e1927fdab1ef1a8de1997557b6db)
- 描述：喜马拉雅开发平台申请我的应用时候得到的appsecret，<a href="http://open.ximalaya.com/apps" target="_blank">喜马拉雅我的应用</a>

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
  "message": "Already initialized"
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


##可用性

    Android系统

    可提供的1.0.0及更高版本

#**getCategories**
<div id="getCategories"></div>

    获取喜马拉雅的内容分类

    getCategories(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象
- 说明：categories [内容分类](#category)

```js
{
  "categories": [
    {
      "order_num": 1,
      "category_name": "资讯",
      "cover_url_small": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnBP5BhAAAGSmFXT7I057.png",
      "cover_url_middle": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnjLKBmAAAGSmFXT7I174.png",
      "cover_url_large": "http://fdfs.xmcdn.com/group16/M05/17/DD/wKgDbFVxNDnjLKBmAAAGSmFXT7I174.png"
    },
    {
      "order_num": 2,
      "category_name": "音乐",
      "cover_url_small": "http://fdfs.xmcdn.com/group12/M08/17/A2/wKgDW1VxM-3hix-3AAAGGBNsGas721.png",
      "cover_url_middle": "http://fdfs.xmcdn.com/group12/M08/17/A0/wKgDXFVxM-LyPrvZAAAGGBNsGas270.png",
      "cover_url_large": "http://fdfs.xmcdn.com/group12/M08/17/A0/wKgDXFVxM-LyPrvZAAAGGBNsGas270.png"
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
  "message": "Uninitialized"
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



##可用性

    Android系统

    可提供的1.0.0及更高版本

#**getSearchedTracks**
<div id="getSearchedTracks"></div>

    通过关键字搜索声音

    getSearchedTracks({params}, function(ret, err))

##params

keyword：

- 类型：字符串
- 默认值：无
- 描述：搜索关键词

categoryid：

- 类型：数字
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
total_count | 数字 | 声音总个数
total_page | 数字 | 声音总页数
tracks | JSON | [声音列表](#track)

```js
{
  "total_count": 475,
  "total_page": 159,
  "tracks": [
    {
      "id": 15044519,
      "kind": "track",
      "track_title": "2012年8月16日“1063会客厅”--晓琳的爱情",
      "track_tags": "爱情",
      "track_intro": "2012年8月16日“1063会客厅”--晓琳的爱情",
      "cover_url_small": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRnBkShsAAMuxLWEITo931_web_meduim.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRnBkShsAAMuxLWEITo931_web_large.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRnBkShsAAMuxLWEITo931_mobile_large.jpg",
      "announcer": {
        "id": 45892933,
        "vcategory_id": 0,
        "nickname": "真我风采网络电台",
        "avatar_url": "http://fdfs.xmcdn.com/group10/M03/34/39/wKgDaVb92VvwPqQ7AAEYxcnPdRo044_web_large.jpg",
        "follower_count": 0,
        "following_count": 0,
        "released_album_count": 0,
        "released_track_count": 0,
        "is_verified": true
      },
      "duration": 1779,
      "play_count": 49,
      "favorite_count": 0,
      "comment_count": 0,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group11/M08/61/EA/wKgDbVci1cjC2NYuAGyXxW6Re9Q985.mp3",
      "play_size_32": 7116741,
      "play_url_64": "http://fdfs.xmcdn.com/group13/M02/57/46/wKgDXVci1WOSF4g9ANkvXLkuurs474.mp3",
      "play_size_64": 14233436,
      "play_url_24_m4a": "http://audio.xmcdn.com/group13/M02/57/28/wKgDXlci1WeyTmH5AFPN_WnH5c0527.m4a",
      "play_size_24_m4a": "5492221",
      "play_url_64_m4a": "http://audio.xmcdn.com/group13/M02/57/28/wKgDXlci1W3BMfXsANuNJ5RDsr4084.m4a",
      "play_size_64_m4a": "14388519",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group13/M02/57/28/wKgDXlci1V_Qx-oxAHCvStWeZXE745.aac",
      "download_size": 7384906,
      "order_num": 0,
      "subordinated_album": {
        "id": 4078979,
        "album_title": "媒体报道",
        "cover_url_small": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRXjWXMWAAMuxLWEITo094_mobile_small.jpg",
        "cover_url_middle": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRXjWXMWAAMuxLWEITo094_mobile_meduim.jpg",
        "cover_url_large": "http://fdfs.xmcdn.com/group8/M03/45/4F/wKgDYVcPbRXjWXMWAAMuxLWEITo094_mobile_large.jpg"
      },
      "source": 2,
      "updated_at": 1467848133000,
      "created_at": 1461901027000
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    keyword:"大海",
    categoryid:1,
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



##可用性

    Android系统

    可提供的1.0.0及更高版本


#**getTags**
<div id="getTags"></div>

    获取专辑标签或者声音标签

    getTags({param}, function(ret, err))

##params

categoryid：

- 类型：数字
- 默认值：无
- 描述：分类ID，指定分类，为0时表示热门分类

type：

- 类型：数字
- 默认值：无，
- 描述：指定查询的是专辑标签还是声音标签，0-专辑标签，1-声音标签

##callback(ret,err)

ret：

- 类型：JSON对象

参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
tag_name | 字符串 | 标签名

```js
{
  "tags": [
    {
      "tag_name": "热血体育"
    },
    {
      "tag_name": "科技之声"
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    categoryid: 1,
    type: 0
};
ximalaya.getTags(param, function(ret, err) {
    if (ret)
        alert("getTags", JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```



##可用性

    Android系统

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

tagname：

- 类型：字符串
- 默认值：无
- 描述：分类下对应声音标签，不填则为热门分类

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
total_count | 数字 | 声音总个数
total_page | 数字 | 声音总页数
tracks | JSON | [声音列表](#track)

```js
{
  "total_count": 396,
  "total_page": 132,
  "tracks": [
    {
      "id": 17567064,
      "kind": "track",
      "track_title": "夏日酷热，听清凉的Bossa Nova（上）~优品音乐104",
      "track_tags": "爵士",
      "track_intro": "玫瑰色的七四七 - 彭靖惠 蓝旗袍 - 范晓萱 南屏晚钟 - 蔡淳佳 梦里人 - 陈百强 三个人的晚餐 - 王若琳 明天你是否依然爱我 - 潘越云",
      "cover_url_small": "http://fdfs.xmcdn.com/group4/M05/A5/7F/wKgDtFd0akzzjYI0AAFCS2M5dWU382_web_meduim.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group4/M05/A5/7F/wKgDtFd0akzzjYI0AAFCS2M5dWU382_web_large.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group4/M05/A5/7F/wKgDtFd0akzzjYI0AAFCS2M5dWU382_mobile_large.jpg",
      "announcer": {
        "id": 7327678,
        "vcategory_id": 0,
        "nickname": "叶子的音乐纪念册",
        "avatar_url": "http://fdfs.xmcdn.com/group3/M0A/32/07/wKgDsVMTC2yjFJhMAAIzUhpL4Aw998_web_large.jpg",
        "follower_count": 0,
        "following_count": 0,
        "released_album_count": 0,
        "released_track_count": 0,
        "is_verified": true
      },
      "duration": 1647,
      "play_count": 10050,
      "favorite_count": 19,
      "comment_count": 3,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group13/M03/9E/C7/wKgDXldvo0nDoozzAGSNGpgF97Q640.mp3",
      "play_size_32": 6589722,
      "play_url_64": "http://fdfs.xmcdn.com/group13/M03/9E/E1/wKgDXVdvo1Xi1xlmAMkZ6omVxGg077.mp3",
      "play_size_64": 13179370,
      "play_url_24_m4a": "http://audio.xmcdn.com/group13/M03/9E/E1/wKgDXVdvo0ODKmPcAE3QNFI7tNU018.m4a",
      "play_size_24_m4a": "5099572",
      "play_url_64_m4a": "http://audio.xmcdn.com/group13/M06/9E/C7/wKgDXldvo1nQCRb2AMuBat1FXF8306.m4a",
      "play_size_64_m4a": "13336938",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group9/M05/9E/53/wKgDYldvozjTyLTiAGhWw8uY6DU027.aac",
      "download_size": 6837955,
      "order_num": 3,
      "subordinated_album": {
        "id": 2650009,
        "album_title": "音乐优品",
        "cover_url_small": "http://fdfs.xmcdn.com/group7/M07/8A/EB/wKgDWldWrWfyrAyDAAJLp6xUS-k951_mobile_small.jpg",
        "cover_url_middle": "http://fdfs.xmcdn.com/group7/M07/8A/EB/wKgDWldWrWfyrAyDAAJLp6xUS-k951_mobile_meduim.jpg",
        "cover_url_large": "http://fdfs.xmcdn.com/group7/M07/8A/EB/wKgDWldWrWfyrAyDAAJLp6xUS-k951_mobile_large.jpg"
      },
      "source": 1,
      "updated_at": 1467849575000,
      "created_at": 1466934452000
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    categoryid: 2,
    tagname: "爵士",
    page:1,
    pagesize:3
};
ximalaya.getHotTracks(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本


#**getAlbumlist**
<div id="getAlbumlist"></div>

    根据分类和标签获取某个分类某个标签下的专辑列表(最火/最新/最多播放)

    getAlbumlist({params}, function(ret, err))

##params

categoryid：

- 类型：数字
- 默认值：无
- 描述：分类ID，指定分类，为0时表示热门分类

tagname：

- 类型：字符串
- 默认值：无
- 描述：分类下对应声音标签，不填则为热门分类

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
total_count | 数字 | 专辑总个数
total_page | 数字 | 专辑总页数
albums | JSON | [专辑列表](#album)

```js
{
  "total_count": 885,
  "total_page": 89,
  "albums": [
    {
      "id": 259608,
      "album_title": "音乐大明星",
      "album_tags": "华语,流行,大明星,音乐大明星,音乐",
      "album_intro": "最棒的音乐，最大牌的明星，音乐大明星！ ！！",
      "cover_url_small": "http://fdfs.xmcdn.com/group11/M09/A0/E1/wKgDbVdkvXPj7tlcAASejY-0bwM580_mobile_small.jpg",
      "cover_url_middle": "http://fdfs.xmcdn.com/group11/M09/A0/E1/wKgDbVdkvXPj7tlcAASejY-0bwM580_mobile_meduim.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group11/M09/A0/E1/wKgDbVdkvXPj7tlcAASejY-0bwM580_mobile_large.jpg",
      "announer": {
        "id": 10454766,
        "vcategory_id": 0,
        "nickname": "音乐大明星",
        "avatar_url": "http://fdfs.xmcdn.com/group5/M05/69/5B/wKgDtlRZf7-zuwtRAA1dzBlF_vE351_web_large.jpg",
        "follower_count": 0,
        "following_count": 0,
        "released_album_count": 0,
        "released_track_count": 0,
        "is_verified": true
      },
      "play_count": 33333725,
      "favorite_count": 0,
      "include_track_count": 189,
      "track_id": {
        "track_id": 18024973,
        "track_title": "SNH48做DJ，微信公众号FunRadio。萌妹子青春逼人，夏天纳凉必备！-2016034",
        "duration": 752,
        "created_at": 1467881426000,
        "updated_at": 1467798106000
      },
      "is_finished": 0,
      "can_download": true,
      "updated_at": 1467881426000,
      "created_at": 1402299017000
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var param = {
    categoryid: 2,
    tagname: "流行",
    calcdimension: 3,
    page: 1,
    pagesieze: 8
};
ximalaya.getAlbumlist(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

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
total_count | 数字 | 声音总个数
total_page | 数字 | 声音总页数
tracks | JSON | [声音列表](#track)

```js
{
  "total_count": 726,
  "total_page": 363,
  "tracks": [
    {
      "id": 17727441,
      "kind": "track",
      "track_title": "【国际风云】土耳其政策转变导致其与IS反目成仇",
      "track_tags": "",
      "track_intro": "",
      "cover_url_small": "http://fdfs.xmcdn.com/group10/M00/9D/6C/wKgDZ1d0foLw3dMTAAOvpIJHvI8367_web_meduim.png",
      "cover_url_middle": "http://fdfs.xmcdn.com/group10/M00/9D/6C/wKgDZ1d0foLw3dMTAAOvpIJHvI8367_web_large.png",
      "cover_url_large": "http://fdfs.xmcdn.com/group10/M00/9D/6C/wKgDZ1d0foLw3dMTAAOvpIJHvI8367_mobile_large.png",
      "announcer": {
        "id": 36193304,
        "vcategory_id": 0,
        "nickname": "头条滚出来",
        "avatar_url": "http://fdfs.xmcdn.com/group10/M07/CB/31/wKgDaVZxIG7y6MciAADXlSjVU68904_web_large.jpg",
        "follower_count": 0,
        "following_count": 0,
        "released_album_count": 0,
        "released_track_count": 0,
        "is_verified": true
      },
      "duration": 89,
      "play_count": 5640,
      "favorite_count": 0,
      "comment_count": 0,
      "download_count": 0,
      "play_url_32": "http://fdfs.xmcdn.com/group8/M02/A1/8C/wKgDYVd0Vu7RNhCaAAV72IgN3Zg333.mp3",
      "play_size_32": 359384,
      "play_url_64": "http://fdfs.xmcdn.com/group8/M08/A1/BF/wKgDYFd0Vu7Dr_IJAAr3G7nAmYQ948.mp3",
      "play_size_64": 718619,
      "play_url_24_m4a": "http://audio.xmcdn.com/group8/M02/A1/8C/wKgDYVd0Vu6QMHhRAAQ_3JcFizg903.m4a",
      "play_size_24_m4a": "278492",
      "play_url_64_m4a": "http://audio.xmcdn.com/group8/M08/A1/BF/wKgDYFd0Vu7jh39fAAsZoprR7eE932.m4a",
      "play_size_64_m4a": "727458",
      "can_download": true,
      "download_url": "http://download.xmcdn.com/group8/M02/A1/8C/wKgDYVd0Vu7hZFs_AAV91aDQ71A294.aac",
      "download_size": 359893,
      "order_num": 2,
      "subordinated_album": {
        "id": 3985798,
        "album_title": "头条滚出来2016年7月专辑",
        "cover_url_small": "http://fdfs.xmcdn.com/group15/M06/34/66/wKgDaFb9rQ2zsGgKAABHpjuAWcs136_mobile_small.jpg",
        "cover_url_middle": "http://fdfs.xmcdn.com/group15/M06/34/66/wKgDaFb9rQ2zsGgKAABHpjuAWcs136_mobile_meduim.jpg",
        "cover_url_large": "http://fdfs.xmcdn.com/group15/M06/34/66/wKgDaFb9rQ2zsGgKAABHpjuAWcs136_mobile_large.jpg"
      },
      "source": 2,
      "updated_at": 1467854459000,
      "created_at": 1467242253000
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
    albumid: 3985798,
    sort: "desc",
    page: 2,
    pagesize: 2
};
ximalaya.getTracks(param, function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本

#**getProvinces**
<div id="getProvinces"></div>

    获取直播省市列表

    getProvinces(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象

- 说明：provinces | JSON | [直播省市列表](#Province)

```js
{
  "provinces": [
    {
      "id": 1,
      "province_code": 110000,
      "province_name": "北京",
      "created_at": 1468208401425
    },
    {
      "id": 2,
      "province_code": 120000,
      "province_name": "天津",
      "created_at": 1468208401425
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
ximalaya.getProvinces(function(ret, err) {
    if (ret)
        alert(JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本

#**getRadios**
<div id="getRadios"></div>

    获取直播省市列表

    getRadios({params}, function(ret, err))
##params

radiotype：

- 类型：数字
- 默认值：无
- 描述：电台类型：1-国家台，2-省市台，3-网络台

provincecode：

- 类型：数字
- 默认值：无
- 描述：省份代码，radio_type为2时不能为空

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
total_count | 数字 | 专辑总个数
total_page | 数字 | 专辑总页数
radios | JSON | [直播电台列表](#radio)

```js
{
  "total_count": 21,
  "total_page": 11,
  "radios": [
    {
      "id": 55,
      "radio_name": "上海Love Radio",
      "radio_desc": "",
      "program_name": "音乐爱当家",
      "schedule_id": 66241,
      "start_time": 0,
      "end_time": 0,
      "support_bitrates": [
        24,
        64
      ],
      "rate24_aac_url": "http://live.xmcdn.com/live/55/24.m3u8",
      "rate24_ts_url": "http://live.xmcdn.com/live/55/24.m3u8?transcode=ts",
      "rate64_aac_url": "http://live.xmcdn.com/live/55/64.m3u8",
      "rate64_ts_url": "http://live.xmcdn.com/live/55/64.m3u8?transcode=ts",
      "radio_play_count": 377110,
      "cover_url_small": "http://fdfs.xmcdn.com/group6/M07/84/C3/wKgDhFT_ojPTjAwDAAB4jvN3ySk144_mobile_small.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group6/M07/84/C3/wKgDhFT_ojPTjAwDAAB4jvN3ySk144_mobile_large.jpg",
      "updated_at": 0
    },
    {
      "id": 59,
      "radio_name": "上海交通广播电台",
      "radio_desc": "",
      "program_name": "1057大家帮",
      "schedule_id": 140852,
      "start_time": 0,
      "end_time": 0,
      "support_bitrates": [
        24,
        64
      ],
      "rate24_aac_url": "http://live.xmcdn.com/live/59/24.m3u8",
      "rate24_ts_url": "http://live.xmcdn.com/live/59/24.m3u8?transcode=ts",
      "rate64_aac_url": "http://live.xmcdn.com/live/59/64.m3u8",
      "rate64_ts_url": "http://live.xmcdn.com/live/59/64.m3u8?transcode=ts",
      "radio_play_count": 272782,
      "cover_url_small": "http://fdfs.xmcdn.com/group6/M05/88/B6/wKgDg1T_ovnBV-ZGAACMhbWr3WA680_mobile_small.jpg",
      "cover_url_large": "http://fdfs.xmcdn.com/group6/M05/88/B6/wKgDg1T_ovnBV-ZGAACMhbWr3WA680_mobile_large.jpg",
      "updated_at": 0
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
  "message": "Uninitialized"
}
```

##示例代码

```js
var param = {
  radiotype:2,
  provincecode:310000,
  page: 2,
  pagesize: 2
};
ximalaya.getRadios(param, function(ret, err){
  if(ret)
    alert(JSON.stringify(ret));
  else
    alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本

#**XmPlayerInit**
<div id="XmPlayerInit"></div>

    初始化播放器

    XmPlayerInit(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象

```js
{
  "code":0,
  "message":"success"
}
```

err：

- 类型：JSON对象

内部字段：

```js
{
  "code": 9002,
  "message": "Uninitialized"
}
```

##示例代码

```js
ximalaya.XmPlayerInit(function(ret, err){
  if(ret)
    alert(JSON.stringify(ret));
  else
    alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本

#**XmPlayerPlay**
<div id="XmPlayerPlay"></div>

    使用播放器播放音乐电台(且只能播放电台的声音)

    XmPlayerPlay({params}, function(ret, err))

##params

index：

- 类型：数字
- 默认值：无
- 描述：getRadios方法会获取一个电台列表，比如上面的[getRadios](#getRadios)方法获取了两个电台(上海Love Radio、上海交通广播电台)，想播放第一个，那么index值传0， 想播放第二个index值传1

##callback(ret,err)

ret：

- 类型：JSON对象

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
  "code": 9002,
  "message": "Uninitialized"
}

{
  "code": 9002,
  "message": "Player uninitialized"
}

{
  "code": 9004,
  "message": "Radio list is empty"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
var param = {
  index:0
};
ximalaya.XmPlayerPlay(param, function(ret, err){
  if(ret)
    alert(JSON.stringify(ret));
  else
    alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本    

#**XmPlayerPause**
<div id="XmPlayerPause"></div>

    暂停播放

    XmPlayerPause(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象

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
  "code": 9002,
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
ximalaya.XmPlayerPause(function(ret, err) {
    if (ret)
        alert("Pause", JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本   
     
#**XmPlayerStop**
<div id="XmPlayerStop"></div>

    停止播放

    XmPlayerStop(function(ret, err))

##callback(ret,err)

ret：

- 类型：JSON对象

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
  "code": 9002,
  "message": "Uninitialized"
}
```

##示例代码

```js
var ximalaya = api.require('ximalaya');
ximalaya.XmPlayerStop(function(ret, err) {
    if (ret)
        alert("Stop", JSON.stringify(ret));
    else
        alert(JSON.stringify(err));
});
```


##可用性

    Android系统

    可提供的1.0.0及更高版本


</div>



<div id="method-content2">
<div class="outline">
[track](#track)

[announcer](#announcer)

[album](#album)

[SubordinatedAlbum](#SubordinatedAlbum)

[Category](#Category)

[Province](#Province)

[radio](#radio)

[错误码](#errcode)
</div>

<div id="track"></div>
#**track参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
total_count | 数字 | 声音总个数
total_page | 数字 | 声音总页数
tracks | json | 声音列表
||
id | 数字 | 声音ID
track_title | 字符串 | 声音名称
track_tags | 字符串 | 声音标签列表
track_intro | 字符串 | 声音简介
cover_url_small | 字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
announcer | JSON | [专辑所属主播信息](#announcer)
duration   | 数字  | 声音时长，单位秒
play_count | 数字 | 播放数 
favorite_count | 数字 | 喜欢数 
comment_count |  数字  |评论数
download_count | 数字 |下载次数
play_url_32 | 字符串 | 播放地址32位
play_size_32   | 数字 | 32位声音文件大小
play_url_64 | 字符串 | 播放地址64位
play_size_64   | 数字 | 64位声音文件大小
play_url_24_m4a | 字符串 | 声音m4a格式24位地址
play_size_24_m4a  |  数字 |声音m4a格式24位大小
play_url_64_m4a | 字符串 | 声音m4a格式64位地址
play_size_64_m4a  |  数字 |声音m4a格式64位大小
can_download  |  Bool   | 可否下载，true-可下载，false-不可下载
download_url  |  数字 | 声音下载地址
download_size | 数字 | 声音下载大小
order_num  | 数字 | 一条声音在一个专辑中的位置
subordinated_album  | JSON | [声音所属专辑信息](#SubordinatedAlbum)
source  | 数字 | 声音来源，1-用户原创，2-用户转采
updated_at  | 数字 | 声音更新时间，Unix毫秒数时间戳
created_at  | 数字 | 声音创建时间，Unix毫秒数时间戳

<div id="announcer"></div>
#**announcer参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | 主播用户ID
vcategory_id | 数字 | 主播分类ID
nickname | 字符串 | 主播用户昵称
avatar_url | 字符串 | 主播头像
is_verified | Boolean | 主播是否加V

<div id="SubordinatedAlbum"></div>
#**subordinated_album参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | ID
album_title | 字符串 | 专辑名称
cover_url_small | 字符串 | 专辑封面小，无则返回空字符串””
cover_url_middle | 字符串 | 专辑封面中，无则返回空字符串””
cover_url_large | 字符串 | 专辑封面大，无则返回空字符串””

<div id="Category"></div>
#**Category参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
order_num | 数字 | 排序值，值越小排序越在前
category_name | 字符串 | 分类名
cover_url_small | 字符串 | 分类封面小图
cover_url_middle | 字符串 | 分类封面中图
cover_url_large | 字符串 | 分类封面大图

<div id="album"></div>
#**album参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | ID
album_title | 字符串 | 专辑名称
album_tags | 字符串 | 专辑标签列表
album_intro | 字符串 | 专辑简介
cover_url_small  |  字符串 | 声音封面小图
cover_url_middle  |  字符串 | 声音封面中图
cover_url_large | 字符串 | 声音封面大图
announcer | JSON | [专辑所属主播信息](#announcer)
play_count | 字符串 | 专辑播放次数
favorite_count | 字符串 | 专辑喜欢数
include_track_count | 字符串 | 专辑包含声音数
track_id | JSON | [专辑中最新上传的一条声音信息](#track)
can_download | Bool | 能否下载，true-可下载，false-不可下载
updated_at  | 数字 | 声音更新时间，Unix毫秒数时间戳
created_at  | 数字 | 声音创建时间，Unix毫秒数时间戳

<div id="Province"></div>
#**Province参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | 省市ID
province_code | 数字 | 省市代码，比如110000
province_name | 字符串 | 省市名称，比如”北京”、”河北”
created_at | 数字 | 创建时间，Unix毫秒数时间戳

<div id="radio"></div>
#**radio参数说明**
参数名 | 类型 | 描述
:-----------  | :-------------:| -----------:
id | 数字 | 声音ID
radio_name | 数字 | 电台名称
radio_desc | 字符串 | 电台简介
program_name | 字符串 | 正在直播的节目名称
schedule_id | 数字 | 正在直播的节目时间表ID
start_time | 数字 | 节目开始时间，比如”09:00”
end_time | 数字 | 节目结束时间，比如”10:00”
support_bitrates | Array | 支持的码率列表，如[24,64]
rate24_aac_url | 字符串 | 24码率aac格式播放地址
rate24_ts_url | 字符串 | 24码率ts格式播放地址
rate64_aac_url | 字符串 | 64码率aac格式播放地址
rate64_ts_url | 字符串 | 64码率ts格式播放地址
radio_play_count | 数字 | 电台累计收听次数
cover_url_small | 字符串 | 电台封面小图
cover_url_large | 字符串 | 电台封面大图
updated_at | 数字 | 声音更新时间，Unix毫秒数时间戳

<div id="errcode"></div>
#**错误码**

code | 描述
:-----------  | :-------------:
0 | 请求成功
9400 | 参数错误
9001 | 已经初始化了
9002 | 未初始化
9003 | JSON组装异常
9004 | 播放器列表为空