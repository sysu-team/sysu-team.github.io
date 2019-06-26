# 代码规范

## 1. Golang 代码规范

### 1.1 命名规范

1. 文件
   - 小写+下划线
2. 包命名
   - package名和目录保持一致，需避免和标准库冲突
   - 避免import相对路径
3. 方法/接口
   - 采用驼峰命名法
   - 非对外方法，首字母需为小写
4. 变量
   - 采用驼峰命名法
5. 常量
6. - 大写+下划线

### 2.2 注释

- 可以通过 `/* …… */` 或者 `// ……`增加注释， `//`之后应该加一个空格
- 注释内容需要在文件/方法/变量上方

### 3.3 异常

- 需要对异常做判断处理
- 不要将error赋值给匿名变量`_`

### 4.4 其他

- 不允许逻辑中调用Panic，选择日志的log.Fatal

- 不要频繁的调用defer

- 尽早return，一旦有错误发生，马上返回

- if接受初始化语句，约定如下方式建立局部变量

  ```go
  if err := file.Chmod(0664); err != nil {
      return err
  }
  ```

- 方法的接收器的名称 一般采用strcut的第一个字母且为小写，而不是this，me或者self

  ```go
  type rpcClient struct {       
      once sync.Once
  }
  func (r *rpcClient) newCodec(contentType string) (codec.NewCodec, error) {       
      //
  }
  
  ```

- 对于bool类型的变量`var b bool`,直接使用它作为判断条件，而不是使用它和true/false进行比较

- byte/string slice相等性比较，使用Equal

- 当接受者是map, chan, func, 不要使用指针传递，因为它们本身就是引用类型

- 当接受者是slice，而函数内部不会对slice进行切片或者重新分配空间，不要使用指针传递

- 当函数内部需要修改接受者，必须使用指针传递

- 当接受者是一个结构体，并且包含了`sync.Mutex`或者类似的用于同步的成员。必须使用指针传递，避免成员拷贝

- 当接受者类型是一个结构体并且很庞大，或者是一个大数组，建议使用指针传递来提高性能，其他场景使用值传递即可

------

## 2. Javascript代码规范

### 2.1 变量名

变量名推荐使用驼峰法来命名(**camelCase**):

```javascript
var firstName = "John";
var lastName = "Doe";

var price = 19.90;
var tax = 0.20;

var fullPrice = price + (price * tax);
```

### 2.2 空格与运算符

通常运算符 ( = + - * / ) 前后需要添加空格:

```javascript
var x = y + z;
var values = ["Volvo", "Saab", "Fiat"];
```

### 2.3 对象规则

对象定义的规则:

- 将左花括号与类名放在同一行。
- 冒号与属性值间有个空格。
- 字符串使用双引号，数字不需要。
- 最后一个属性-值对后面不要添加逗号。
- 将右花括号独立放在一行，并以分号作为结束符号。

```js
var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```

------

## 3. 参考及转载

- [JavaScript 代码规范](https://www.runoob.com/js/js-conventions.html)
- [go语言编码规范](https://juejin.im/post/5c16f16c5188252dcb30ff42)



