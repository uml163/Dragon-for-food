# 软件需求规格说明书 SRS

## 1.引言

### 1.1 编写目的

为了保证项目团队按时完成项目目标，便于项目团队成员更好地了解项目情况，使项目工作开展的各个过程合理有序，也便于用户与开发成员进行沟通交流，因此将以文档形式描述项目的各项功能需求、性能需求，阐述项目背景及范围等总体结构和功能结构。此文档也是后续软件开发的依据。

### 1.2 背景

随着智能手机的普及，生活中越来越多事情可以通过互联网与智能手机变得更加方便。微信作为一个即时通讯软件，在很多人的工作，学习，日常生活中扮演着举足轻重的角色。2016年微信正式推出小程序的内测版本，随后掀起了小程序便捷开发与使用的热潮。

微信小程序能得到大力推广，主要归功于微信小程序无需下载安装的便捷使用，联系扫码点餐，成就了“互联网+餐饮”潮流的产物，从而可以有效地为餐厅节省人力成本，提高顾客点餐用餐效率，节省顾客时间，提高餐厅翻台率。 

### 1.3 参考资料

- 微信小程序开发及使用的市场调查
  - [2017-2018年微信小程序市场发展研究报告](http://co-image.qichacha.com/upload/chacha/att/20180130/1517306145864730.pdf)
  - [2018年微信小程序报告](https://36kr.com/p/5116573.html)

- GB856T——88，软件设计文档国家标准—软件需求说明书

## 2.任务概述

### 2.1 目标

我们的目标是打造一个快速、简单、便捷的扫码点餐系统，同时为商户提供一定规模的售卖管理功能。为食客提供一个舒适的点餐体验，同时降低商户在用餐高峰期的服务压力。 

我们的期望打造的产品有以下优点：

- 简单易懂——即使没有使用过之前其他点餐系统，都能够迅速学会使用该点餐软件。
- 购物车轻松增减——增加购物抽屉，可对已选的菜品进行随意增减。
- 餐厅桌子随意加——商家能根据餐桌号自行生成二维码。

### 2.2 功能需求

#### 2.2.1 用例图

##### 顾客用例：

![](https://github.com/ChickenDinner8/SDP-document/blob/master/Assets/SRS/customer-usecase.png?raw=true)

##### 商家用例：

![](https://github.com/ChickenDinner8/SDP-document/blob/master/Assets/SRS/merchant-usecase.png?raw=true)

#### 2.2.2 活动图

##### UC1 顾客扫码就坐

概要：顾客进入某餐厅，在餐桌前坐下，用手机扫描餐桌上的二维码，服务器返回二维码对应的餐厅、餐桌信息，顾客确认自己所在的餐厅和餐桌后，开始点餐。

活动图：

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/Nick/activity1.png?raw=true)

##### UC2 顾客点餐

概要：服务器向顾客返回当前餐厅的菜单，顾客浏览菜单并选择需要的菜品及其数量。 

活动图：

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/Nick/activity2.png?raw=true)

##### UC3 商家编辑菜品

概要：商家在打开网页，登录在编辑菜品信息处修改菜品，并确认操作。服务器接收到相关信息后修改数据库内容。 

活动图：

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/Nick/activity3.png?raw=true)

#### 2.2.3 领域模型

领域模型如下：

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/DomainModel/domain%20model.png?raw=true)

#### 2.2.4 状态模型

状态模型如下：

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/StateModel/state-model.png?raw=true)

#### 2.2.5 功能模型

##### SSD1 顾客编辑菜单 

用户进入菜单页面进行增减菜品

![](https://raw.githubusercontent.com/ChickenDinner8/ChickenDinner8.github.io/master/public/img/Rayman/SSD1.png)

##### SSD2 商家查看餐厅菜单 

用户进入订单页面进行订单取消

![](https://github.com/ChickenDinner8/ChickenDinner8.github.io/blob/master/public/img/Yang/Eat%E7%82%B9%E7%82%B9%E7%B3%BB%E7%BB%9F%E9%A1%BA%E5%BA%8F%E5%9B%BE.png?raw=true)

### 2.3 用户特点

本点餐系统的最终用户为使用微信，以及熟悉微信支付功能的用户。

本商家管理系统最终用户为能够熟练使用浏览器打开网页的用户。

### 2.4 假定和约束

#### 2.4.1 时间约束

本系统需要在第18周结束前（2019.06.25 23:59）完成开发，并且通过在线测试。

#### 2.4.2 实现约束

客户端：使用微信小程序，省去用户安装APP的时间。

## 3. 需求规定

### 3.1 功能规定

#### 3.1.1客户端功能规定

- 顾客可以在小程序菜单页面浏览各种菜品，并根据需要选择添加的数量；
- 顾客可以在小程序购物车抽屉中快速增减菜品；
- 顾客可以在小程序商家页面浏览评论；
- 顾客可以在提交订单前编辑备注告诉厨房相关信息；


### 3.2 性能规定

#### 3.2.1 精度

菜品价格精度为小数点后两位。

#### 3.2.2 时间特性要求

由于服务器使用了外网的服务器，相应时间尽量控制在10秒内。

#### 3.2.3 灵活性

客户端能运行在支持微信小程序版本的微信上操作。

### 3.3 故障处理要求
当客户端出现崩溃，能保证数据库中数据完整性。

## 4. 运行环境

### 4.1 设备

顾客点餐系统需运行在智能手机上；

### 4.2 支持软件

顾客点餐系统需要运行在更新了5.3版本及以上的微信上；
