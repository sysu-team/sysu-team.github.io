# 后端架构文档

## 技术选型

### 编程语言：[Golang With Go Module](https://golang.org/)

Golang with go module 需要 go 的版本在 1.11 / 1.12 

### 基本框架：[Iris](https://iris-go.com/)


- [中文文档](https://learnku.com/docs/iris-go/10)

- [官方教程](https://docs.iris-go.com/)


### 数据库：

Mongodb: (具体的数据库设计请查看数据库设计文档) [数据库设计文档](todo)

### 架构设计

MVC (Router -> Controller -> Services -> Model)



使用 Iris 实现的后台中，框架已经给我们提供了基本的Http服务器的功能，我们不需要接触到底层的连接管理等方面，只需要编写上层的业务逻辑就可以。

- Router: 又称为路由, 我们通过 `router`，把用户发过来的请求和我们编写的处理逻辑对应起来，也就是 `request` 和 `handler` 之间的关系，在本次的框架中，`iris` 对 `mvc` 提供了强大的支持，我们无需像之前一样，编写冗余的代码在 endpoint 上去注册 handler，只需要按照一定的格式给我们的 handler 命名，iris 能够通过反射机制，实现绑定。
 
- Controller：负责验证和转发从Router中传递过来的参数，并对请求做出应答。Controller实际与Request和Response接触，采用的是 `thin controller`的设计方式，把业务逻辑的处理都在了 `Service` 中，之所以把参数简单格式的检验放在 controller 层而不是 service，是出于对性能的考虑，在service 层上处理的话，还需要在从 service 把错误传回给 controller。

- Service: 使用 model 层提供的接口，处理项目本身的业务逻辑，controller 保证了传下来的参数的格式正确性，逻辑正确性的验证需要在 Service 层中检查，把复杂的业务逻辑封装成简单的 api 供 controller 层使用。

- Model: 负责数据操作，封装与数据库进行操作的逻辑成函数，提供给上层使用


### 错误处理

没有采用 golang 原来的错误处理（err,作为函数返回值)，有很多处理逻辑相似的错误处理，这样的话会有很多的冗余代码，所以直接采用的中间件 + panic 的机制，来吧底层的错误抛出到中间件中统一处理，具体可以看 lib/assert，以及 ErrorHandler 中间件。

### 测试工具

本次开发采用的是前后端分离的开发方式，在设计好api 之后，和对接之前都是在后端使用测试工具单独测试 API 功能。 

- [postman](https://www.getpostman.com/) : 测试后端 api的基本功能

## 目录结构

```
│  .gitignore
│  config.example.yaml // 项目配置文件  
│  go.mod              // go module 支持
│  go.sum              // go module 支持
│  main.go             // 项目入口 
│  README.md            
│                       
├─app                   
│  │  app.go           // 配置  
│  │                    
│  ├─configs            
│  │      config.go    // 整个项目的配置文件， 包括数据库连接，小程序 appID, secret 等  
│  │                    
│  ├─controllers       // contorller 层
│  │      controller.go
│  │      delegation.go     // 委托相关
│  │      questionnaire.go  // 问卷调查相关
│  │      user.go           // 用户相关
│  │
│  ├─models            // model 层
│  │      delegation.go 
│  │      model.go      // 初始化数据库连接等
│  │      model_test.go
│  │      questionnaire.go
│  │      user.go
│  │
│  ├─services       // service 层
│  │      delegation.go
│  │      service.go
│  │      questionnaire.go
│  └─     user.go       
│ 
├─docs             // 项目文档    
│  │  document.md       
│  │                    
│  └─assets            
└─lib              // 项目中用到的一些功能函数     
        assert.go       
        json.go
```
## 参考链接

- [Go 教程](https://go.wuhaolin.cn/)

- [Go 标准库](https://books.studygolang.com/The-Golang-Standard-Library-by-Example/)
