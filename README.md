## 严肃的声明

这套API设计初衷只是为了继续学习更多的Node.js爬虫知识，为了所谓的动力所以将目标定为了某些不可描述的网站(男人都懂)。可供个人技术学习，但是请勿随意分享传播给其他人或者第三方。

同时请期待本人正在开发基于这套Node.js后端接口的 App，将同后端爬虫一到开源。

请勿传播，本人不承担任何的后果，如有意见请联系本人。

- QQ：2271608011
- 博客：geekhelp.cn

**觉得不错，请给本项目一个 start，感谢CCTV**


## API接口


**注意：**
- 请求方式GET，URL地址栏传递参数即可！
- 根据第三方xo网站URL规则分析得出每页只展示24条数据，前端可以自增page字段获取更多页数据
- 需要注意当接口中传输的参数不在后端参数规则列表中时，后端默认返回首页数据
- 后端爬虫加载台湾的第三方网站解析数据存在2~3秒等待时间，前端做好loading
- 后端服务器IP：106.14.145.68，端口：18080，请求地址：http://106.14.145.68:18080 ，请自行拼接完整的接口地址
- 视频资源因为在美国第三方托管商那，所以播放需要Vpn翻墙。后期APP上线时本人会部署一台自己的Linux VPN服务器，以供各位浏览视频使用。


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

### 首页

---

**接口：** /api/v1.0/default?page=1&state=index

**字段：**
- page：需要获取的第几页数据
- index：首页栏目


### 推荐

---

**接口：** /api/v1.0/default?page=1&state=hot

**字段：**
- page：需要获取的第几页数据
- hot：推荐栏目


### 最好

---

**接口：** /api/v1.0/default?page=1&state=best

**字段：**
- page：需要获取的第几页数据
- best：最好栏目


### 更多： 

---

**接口：** /api/v1.0/default?page=1&state=more

**字段：**
- page：需要获取的第几页数据
- more：更多栏目


### 最新： 

---

**接口：** /api/v1.0/default?page=1&state=created

**字段：**
- page：需要获取的第几页数据
- created：最新栏目


### 推荐标签：

---

**接口：** /api/v1.0/default?page=页数&state=tag&tagid=标签ID

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

The code is available under the [MIT license](https://opensource.org/licenses/MIT).
