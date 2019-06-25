# 1、设计
{:.no_toc}

* 目录
{: toc}

## 1.1前端


### 1.1.1前端技术选择


前端候选技术：mpVue、wepy与微信小程序

三种技术优缺点比较：
* mpVue
  * 优势：
    * 支持 npm 包，支持 css 预处理器
    * 可以直接使用 vuex 做应用状态管理
  * 劣势：
    * 开发者需要熟悉 vue ，目前版本（v1.0.5）不支持 slot 
    * 框架发布时间比较短，里面存在很多对小程序原生的替换，容易出现你想写的功能vue里找不到和你写的小程序功能在vue里不是这样写，增加解决问题的时间
* wepy
  * 优势：
    * 支持 slot 组件内容分发插槽，支持 npm 包，支持 css 预处理器
    * 可以将 Redux or Mobx 引入到项目中
  * 劣势：
    * 云信暂不支持wepy开发
    * 开发者需要熟悉 vue 和 wepy 两种语法
    * 产品市场
* 微信小程序：
   * 优点：
     * 使用者角度：简单方便，不用额外安装app 、安全
     * 开发者角度：节省成本和降低了门槛难度
     * 微信本身的用户基础带来的流量优势、宣传更方便（转发分享）扫描二维码即可
     * 速度快、不占内存
   * 劣势：
     * 小程序文件限制、不适用于大型的小程序开发
     * 用户流失较快
     
下面用几张图片简单概括三者的区别
![](https://github.com/uml163/UML/blob/master/report/documents/pictures/zfr-1.png?raw=true)

![](https://github.com/uml163/UML/blob/master/report/documents/pictures/zfr-2.png?raw=true)

我们的选择：

基于前面三种候选的比较，我们最终对客户端以及商家端进行了选型。
* 客户端

为便于顾客使用和轻量级开发、我们选择微信小程序作为客户端。
* 商家端

商家端对于产品的便利性需求并不是很高，而对产品功能、产品的稳定性有着较高的需求，因此我们选用WEb端作为商家端。

### 1.1.2 框架选择


* 客户端：

微信小程序：不使用额外的框架、使用微信提供的小程序框架（WXML+WXSS+JS+JSON）进行开发。没有额外引入框架出现的潜在错误情况。
* 商家端：
  * JQuery + Bootstrap：使用bootstra框架提供的样式和组件快速的完成一个网站的前端页面，只需要引用一些定义好样式和组件（通过定义好的class来引用相应的样式和组件），就可以完成一个非常漂亮网页。
  * Angular：文档例子非常少, 验证功能错误信息显示比较薄弱，需要写很多模板标签
  * Vue：MVVM模式，组件化开发，通过setter与getter以及VDOM提供了较好的性能
  * React：React是目标是UI组件，通常可以和其它框架组合使用，目前并不适合单独做一个完整的框架

基于开发难度与前景、我们选用JQuery + Bootstrap进行单页面应用开发

### 1.1.3后端技术选择

后端候选技术：java+ jesery、GO、Python + Flask等等

后端技术优缺点比较：
* java+ jesery
  * 优势：
    * Java SE 规范，这让 Java 即能像 C/C++ 一样贴近操作系统，又自由处理网络相关、IO 相关的内容，功能很强大。
    * Java EE 规范，完善的规范使得 Java 后端发展有了很好的规范基础。统一的环境、规范让框架和业务代码有了交互的标准。
   * 劣势：
     * 开发效率相对较低。
     * 虽然上手开发相对容易，但真正理解框架底层的运行原理相对较难，需要大量的学习和经验。
* GO
  * 优势：
    * Golang 的设计理念很明确，就是将动态类型语言的编程容易度和静态类型语言的安全效率结合起来。
    * 部署简单，Go 编译生成的可执行文件无需担心包和库的依赖关系。     * 并发性能好，即使是单个Go应用也能有效利用多个 CPU 核心。良好的语言设计，且自带完善的工具链。
  * 劣势：
    * import 的包不支持自定义版本，项目容易因为包的升级而不可用。
    * 垃圾回收机制仍存在一些问题。缺乏比较完善的框架。
* Python + Flask
  * 优势：
    * 学习简单，能快速进行开发构建 Web 应用。
    * 拥有丰富的标准库和第三方库。
    * 在WEB方面有多种成熟的框架。
  * 劣势：
    * 作为解释型语言，运行速度较慢，且无法有效利用多线程。
    
从团队技术栈来看、团队中了解程序开发的基本上只有架构师、架构师比较熟悉的开发语言为python。

从选型技术层来看，选型语言需要考虑可用框架、开发工具、设计模式、开发模式等方面。

从业务需求来看，由于个人申请的微信小程序不能获取paykey，所以我们的程序将不会进行市场投放，高可用的、轻量级是程序所需的。

基于以上三个因素的考量、最终我们选用Python + Flask最为后端编程语言。

## 1.2架构设计

### 1.2.1系统基本架构

* 小程序与商家端作为前端与用户交互
* 前端通过 API 与后端沟通
* Nginx 捕获 HTTPS 请求并进行均衡负载，反向代理到任一服务器实例
Flask服务器由多个实例，处理请求
* 使用 MySQL 作为数据库

## 1.3模块划分

### 1.3.1顾客端

* 小程序
按照设计初稿的页面进行划分，划分成了，主页、购物车、我的详情页
* 按照不同页面的程序功能划分，主页设置了轮转播放、下拉刷新、点击进入详情等等功能
* 图标基本使用本地在线图片，对于buttonbar等不能使用在线图标的，我们选择将我们想要的图片上传至我们的服务器，通过服务器引入图标。
* 组件树如下图所示：

```
.
├── app.js
├── app.json
├── app.wxss
├── components
│   ├── cart
│   │   ├── bar.js
│   │   ├── bar.json
│   │   ├── bar.wxml
│   │   ├── bar.wxss
│   │   ├── count-picker.js
│   │   ├── count-picker.json
│   │   ├── count-picker.wxml
│   │   ├── count-picker.wxss
│   │   ├── list.js
│   │   ├── list.json
│   │   ├── list.wxml
│   │   ├── list.wxss
│   │   ├── modal
│   │   │   ├── select-customer-count.js
│   │   │   ├── select-customer-count.json
│   │   │   ├── select-customer-count.wxml
│   │   │   └── select-customer-count.wxss
│   │   ├── specification.js
│   │   ├── specification.json
│   │   ├── specification.wxml
│   │   ├── specification.wxss
│   │   ├── submit-order-bar.js
│   │   ├── submit-order-bar.json
│   │   ├── submit-order-bar.wxml
│   │   └── submit-order-bar.wxss
│   ├── food
│   │   ├── category-list.js
│   │   ├── category-list.json
│   │   ├── category-list.wxml
│   │   ├── category-list.wxss
│   │   ├── menu-list-item.js
│   │   ├── menu-list-item.json
│   │   ├── menu-list-item.wxml
│   │   ├── menu-list-item.wxss
│   │   ├── menu-list.js
│   │   ├── menu-list.json
│   │   ├── menu-list.wxml
│   │   ├── menu-list.wxss
│   │   ├── search-box.js
│   │   ├── search-box.json
│   │   ├── search-box.wxml
│   │   └── search-box.wxss
│   └── iview
├── config.js
├── config.server.default.js
├── config.server.js
├── pages
│   ├── food
│   │   ├── cart.js
│   │   ├── cart.json
│   │   ├── cart.wxml
│   │   ├── cart.wxss
│   │   ├── detail.js
│   │   ├── detail.json
│   │   ├── detail.wxml
│   │   ├── detail.wxss
│   │   ├── menu.js
│   │   ├── menu.json
│   │   ├── menu.wxml
│   │   ├── menu.wxss
│   │   ├── search.js
│   │   ├── search.json
│   │   ├── search.wxml
│   │   └── search.wxss
│   ├── index
│   │   ├── index.js
│   │   ├── index.json
│   │   ├── index.wxml
│   │   └── index.wxss
│   ├── order
│   │   ├── comment.js
│   │   ├── comment.json
│   │   ├── comment.wxml
│   │   ├── comment.wxss
│   │   ├── detail.js
│   │   ├── detail.json
│   │   ├── detail.wxml
│   │   ├── detail.wxss
│   │   ├── index.js
│   │   ├── index.json
│   │   ├── index.wxml
│   │   └── index.wxss
│   └── queue
│       ├── index.js
│       ├── index.json
│       ├── index.wxml
│       └── index.wxss
├── project.config.json
├── service
│   ├── auth.js
│   ├── cart.js
│   ├── category.js
│   ├── customer.js
│   ├── desk.js
│   ├── food.js
│   ├── order.js
│   └── util.js
└── utils
    └── util.js
```
### 1.3.2后端

* 路由注入

```
#路由注入
route_account = Blueprint( 'account_page',__name__ )
#路由
@route_account.route( "/index" )
def index():
    pass
@route_account.route( "/info" )
def info():
    pass
```

* 获取用户openid
```
 @staticmethod
    def getWeChatOpenId( code ):
        url = "https://api.weixin.qq.com/sns/jscode2session?appid={0}&secret={1}&js_code={2}&grant_type=authorization_code" \
            .format(app.config['MINA_APP']['appid'], app.config['MINA_APP']['appkey'], code)
        r = requests.get(url)
        res = json.loads(r.text)
        openid = None
        if 'openid' in res:
            openid = res['openid']
        return openid
```
* 数据库防止并发库存问题，坐下selector、update

```
#为了防止并发库存出问题了，我们坐下selectfor update,
tmp_food_list = db.session.query( Food ).filter( Food.id.in_( food_ids ) )\.with_for_update().all()
```
* 错误反馈与日志管理

```
def error_404( e ):
    LogService.addErrorLog( str( e ) )
    return ops_render( 'error/error.html',{ 'status':404,'msg':'很抱歉！您访问的页面不存在' } )

class LogService():
    @staticmethod
    def addAccessLog():
        AccessLog = AppAccessLog()
      ...
        db.session.add( AccessLog )
        db.session.commit( )
        return True

    @staticmethod
    def addErrorLog( content ):
        if 'favicon.ico' in request.url:
            return
        ErrorLog = AppErrorLog()
       ...
        db.session.add(ErrorLog)
        db.session.commit()
        return True
```
# 2编码风格

[代码规范](8.1-coding_standard.md)

**可读性注释与说明** 

```
    @staticmethod
    #MD5方法生成授权码
    def geneAuthCode(user_info = None ):
        m = hashlib.md5()
        str = "%s-%s-%s-%s" % (user_info.uid, user_info.login_name, user_info.login_pwd, user_info.login_salt)
        m.update(str.encode("utf-8"))
        return m.hexdigest()

    # 登陆密码MD5加密
    @staticmethod
    def genePwd( pwd,salt):
        m = hashlib.md5()
        str = "%s-%s" % ( base64.encodebytes( pwd.encode("utf-8") ) , salt)
        m.update(str.encode("utf-8"))
        return m.hexdigest()
```
