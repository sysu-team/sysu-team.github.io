# 框架目录设计与逻辑架构与 ECB 的关系

## 1. 逻辑架构

逻辑架构由三层模型（表示层、业务层、持久化层）构成

### 1.1 表示层

顾客端使用微信小程序作为表示层，提供发布订单子系统，接受订单子系统

### 1.2 业务层

服务器充当业务层的角色，为表示层的各个子系统提供相应的服务模块

### 1.3 持久化层

- MySQL提供数据的持久化服务

## 2. 逻辑框架

### 2.1 前端

前端代码框架：

```bash
|-UI
|   | weui.wxss
|   |-dist
|   |	action-sheet
|
|-miniprogram_npm
|   |-set-cookie-parser
|   |-weapp=cookie
|
|-pages
|
|   |-detail
|   |	detail.js
|   |	detail.json
|   |	detail.wxml
|   |	detail.wxss
|
|   |-index
|   |	index.js
|   |	index.json
|   |	index.wxml
|   |	index.wxss  
|
|   |-logs
|   |	logs.js
|   |	logs.json
|   |	logs.wxml
|   |	logs.wxss  
|
|   |-publish
|   |	publish.js
|   |	publish.json
|   |	publish.wxml
|   |	publish.wxss  
|
|   |-questiondetail
|   |	detail.js
|   |	detail.json
|   |	detail.wxml
|   |	detail.wxss
|
|   |-questionnaire
|   |	questionnaire.js
|   |	questionnaire.json
|   |	questionnaire.wxml
|   |	questionnaire.wxss
|
|   |-questionresult
|   |	result.js
|   |	result.json
|   |	result.wxml
|   |	result.wxss
|
|   |-signup
|   |	signup.js
|   |	signup.json
|   |	signup.wxml
|   |	signup.wxss
|
|   |-user
|   |	user.js
|   |	user.json
|   |	user.wxml
|   |	user.wxss
|
|-source
|   |-image
|   |   detail.jpg
|   |   ...
|
|-utils
|   util.js
|   README.md
|   app.js
|   app.json
|   app.wxss
|   package-lock.json
|   package.json
|   project.config.json
|   sitemap.json
```

### 2.2 后端

后端代码开发框架：

```bash
│  main.go
│  go.sum
│  go.mod
│  config.example.yaml
│  README.md
│  .gitgnore
│  
|  lib
│  │  assert.go
│  │  json.go
|
|  docs
│  |  document.md
│          
|  app
│  |  configs
│  │  |  config.go
│  │  │  
│  │  controllers  
│  │  │  contronler.go     
│  │  │  delegation.go
│  │  │  questionnaire.go
│  │  │  user.go
│  │  │ 
│  │  model   
│  │  │  delegation.go
│  │  │  questionnaire.go
│  │  │  user.go
|  |  |  model.go
|  |  |  model_test.go
|  |  |
|  |  service
|  |  |  delegation.go
|  |  |  questionnaire.go
|  |  |  user.go
│  |  |
|  |  utils
|  |  |  reset.go       
```

## 3. 与 ECB 的关系 

- Entity 对象
  - 代表系统数据，如：问卷、任务、用户
  - 在本系统中，其代表的是
    - 服务端中各model类定义的与mysql相关的实体，承载系统数据。
    - 服务器的数据库中存储的信息。

- Boundary 对象：

  - 代表与用户的接口，如：界面、网关、代理等；
  - 在本系统中，其代表是：
    - 小程序端的用户界面，

- Controller 对象：

  - 代表在 Boundary 与 Entity 中的衔接媒介，编排来自 Boundary 的命令的执行；
  - 在本系统中，其代表是：
    - 服务端中各controller类定义的内容，他们接收来自Boundary的命令并进行相应的编排

  