<p align="center"><img src="http://okkzzhtds.bkt.clouddn.com/9887.png?imageView2/1/w/397/h/400/q/75|imageslim"/></p>

<p align="center">
  <a href="https://github.com/helpcode/Node-Crawler/"><img src="https://img.shields.io/travis/rust-lang/rust.svg" alt="rust"></a>
  <a href="https://cn.vuejs.org/"><img src="https://img.shields.io/badge/vue-2.8.2-blue.svg" alt="vuejs"></a>
  <a href="https://nodejs.org/en/download/"><img src="https://img.shields.io/badge/node.js-6.11.1-blue.svg" alt="nodejs"></a>
  <a href="https://webpack.github.io/"><img src="https://img.shields.io/badge/webpack-3.3.0-blue.svg" alt="webpack"></a>
  <a href="https://img.shields.io/packagist/l/doctrine/orm.svg"><img src="https://img.shields.io/packagist/l/doctrine/orm.svg" alt="orm"></a>

</p>


## 声明

这套API设计初衷只是为了继续学习更多的Node.js爬虫知识，为了所谓的动力所以将目标定为了某些不可描述的网站(男人都懂)。可供个人技术学习，但是请勿随意分享传播给其他人或者第三方。

同时请期待本人正在开发基于这套Node.js后端接口的 App，将同后端爬虫一到开源。

请勿传播，本人不承担任何的后果，如有意见请联系本人。

- QQ群：[540144097](http://shang.qq.com/wpa/qunwpa?idkey=1c684eb6c3d6b32ac50b0d179096ed64124b9db577add0319b7b1a96a0235656)
- 博客：[geekhelp.cn](http://geekhelp.cn/)

**觉得不错，请给本项目一个 start，感谢CCTV**


### 注意事项：

---

- 请求方式GET，URL地址栏传递参数即可！
- 根据第三方xo网站URL规则分析得出每页只展示24条数据，前端可以自增page字段获取更多页数据
- 需要注意当接口中传输的参数不在后端参数规则列表中时，后端默认返回首页数据
- 后端爬虫加载台湾的第三方网站解析数据存在2~3秒等待时间，前端做好loading
- 视频资源因为在美国第三方托管商那，所以播放视频需要Vpn翻墙(有的则不需要)。后期APP上线时本人会部署一台自己的VPN服务器，以供浏览视频使用。

### 实现功能：

---

- [x] 首页栏目 -- 完成
- [x] 推荐栏目 -- 完成
- [x] 最好栏目 -- 完成
- [x] 更多栏目 -- 完成
- [x] 最新栏目 -- 完成
- [x] 推荐标签 -- 完成
- [x] 获取下载地址 -- 完成
- [ ] 模拟登录后实现搜索抓取 -- 正在努力中！
- [ ] 搭建VPN服务器 -- 正在建设中！


### 数据格式

---

Node.js后端爬虫返回的数据格式如下，status 字段用于标志网络请求是否成功的返回码，前端可根据此字段的返回数值判断执行对应操作。result 字段为请求到的视频数据集合。


```javascript
{
  status: 200, // 200：请求成功 ，404：请求失败
  result: [
    {
        title: "标题",
        url: "播放地址(已集成第三方播放器)",
        img: "缩略图地址",
        time: "时长",
        hot: "关注度"
    },
    .....
  ]
 }
```  

## API接口

按照栏目分类共有以下接口，请遵循接口字段传递规范。

### 首页

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=1&state=index

**字段：**
- page：需要获取的第几页数据
- index：首页栏目


### 推荐

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=1&state=hot

**字段：**
- page：需要获取的第几页数据
- hot：推荐栏目


### 最好

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=1&state=best

**字段：**
- page：需要获取的第几页数据
- best：最好栏目


### 更多： 

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=1&state=more

**字段：**
- page：需要获取的第几页数据
- more：更多栏目


### 最新： 

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=1&state=created

**字段：**
- page：需要获取的第几页数据
- created：最新栏目


### 推荐标签：

---

**接口：** http://106.14.145.68:18080/api/v1.0/default?page=页数&state=tag&tagid=标签ID

**字段：**
- page：页数
- tag：表示为标签栏目
- tagid：标签栏目的具体ID，可参照下文默认标签传入ID


**默认提供标签：**

图片中`tag_id=xx`，其中`数字xx`就是接口需要传入的ID参数，本人太懒所以直接截图了！

**场景类(9条)：**

![场景类](http://okkzzhtds.bkt.clouddn.com/222.png)

---

**角色类(19条)：**

![角色类](http://okkzzhtds.bkt.clouddn.com/333333.png)

---

**国家类(10条):**

![国家类](http://okkzzhtds.bkt.clouddn.com/44444.png)

---

**部位类(8条):**

![部位类](http://okkzzhtds.bkt.clouddn.com/3334444.png)

---

**行为类(17条):**

![行为类](http://okkzzhtds.bkt.clouddn.com/xinwei.png)


### 如何获取视频下载地址？

---

打开任意接口，得到后端返回的数据，然后点击其实`url`字段的数值播放视频，谷歌浏览器`Ctrl + U`查看网页源码，在`script`脚本代码中找到如下代码：

```javascript
 clip: {
        sources: [
            	            	{ type: "application/x-mpegurl", src:"http://cdn.looklook.space/videos/1/154177/154177.240p.m3u8?v=1.1" }
            	        ]
    }

```
其`sources`数组中`src`字段数值`http://cdn.looklook.space/videos/1/154177/154177.240p.m3u8?v=1.1`即是视频`m3u8`地址！根据`m3u8`规范，我们可以复制地址到浏览器地址栏，将地址后缀`m3u8`改成`ts`。

例如：http://cdn.looklook.space/videos/1/154177/154177.240p.ts?v=1.1 ，回车即可实现视频下载，绕过网站会员直接下载视频。

## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2017-present, Bmy Code
