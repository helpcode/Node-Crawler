## API接口

**注意：**
- 根据第三方xo网站URL规则分析得出每页只展示24条数据，前端可以自增page字段获取更多页数据
- 请求方式POST，请勿使用GET拼接URL地址栏参数，否则直接报错URL不存在
- 需要注意当接口中传输的参数不在后端参数规则列表中时，后端默认返回首页数据
- 后端爬虫加载台湾的第三方网站解析数据存在2~3秒等待时间，前端做好loading


### 首页

**接口：** /api/v1.0/default?page=1&state=index

**字段：**
- page：需要获取的第几页数据
- index：首页栏目


### 推荐

**接口：** /api/v1.0/default?page=1&state=hot

**字段：**
- page：需要获取的第几页数据
- hot：推荐栏目


### 最好

**接口：** /api/v1.0/default?page=1&state=best

**字段：**
- page：需要获取的第几页数据
- best：最好栏目


### 更多： 

**接口：** /api/v1.0/default?page=1&state=more

**字段：**
- page：需要获取的第几页数据
- more：更多栏目


### 最新： 

**接口：** /api/v1.0/default?page=1&state=created

**字段：**
- page：需要获取的第几页数据
- created：最新栏目


### 推荐标签：

**接口：** /api/v1.0/default?page=页数&state=tag&tagid=标签ID

**字段：**
- page：页数
- tag：表示为标签栏目
- tagid：标签栏目的具体ID，可参照下文默认标签传入ID


#### 默认提供标签：

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
