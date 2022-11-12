# 项目说明

把mPaaS的扫码组件包装为UTS插件。

# 已知问题

- UTS 插件的 API 接口不支持入口参数为 optional？

如果入口参数定义为 optional，那么调用时提供了这个参数还好，不提供的话就会报错：
```
Error: targetMethod error::java.lang.IllegalArgumentException: Callable expects 1 arguments, but 0 were provided.
```

- 结构类型的入口参数里面属性的数据类型问题：

	- 数组类型，貌似不支持。

	- 对于 boolean 类型，如果调用时没有提供的话，取到的缺省值是 true。

	- 对于 boolean optional 类型，调用时如果提供对应的值还好，如果不提供的话，程序调用没有任何反应，
	  也看不到报错信息。

- 回调函数不支持返回值？

从前端 js 侧调用 UTS 插件 API 的时候传入一个 callback 函数，从 UTS 侧调用这个 callback 的时候无法获取其返回值，
得到的返回值总是一个 `kotlin.Unit`。

- 如何给回调函数传入一个 null 值？

- UTS 如何调用具有可变参数的原生接口？

比如原生接口的函数签名是：
```
public ScanRequest setRecognizeType(ScanRequest.RecognizeType... recognizeTypes)
```
如果像下面这样调用，会导致接口调用没有反应（也看不到任何报错信息）：
```
let types = [ScanRequest.RecognizeType.QR_CODE]
scanRequest.setRecognizeType(types)
```

# 参考资料

[DCloud](https://www.dcloud.io)
| [uni-app 官网](https://uniapp.dcloud.net.cn/)

[UTS 原生插件](https://uniapp.dcloud.net.cn/plugin/uts-plugin.html)
| [UTS 语法](https://uniapp.dcloud.net.cn/tutorial/syntax-uts.html)
| [Hello UTS](https://gitcode.net/dcloud/hello-uts/-/tree/dev)

[支付宝扫码组件](https://help.aliyun.com/document_detail/52599.html)

[Android Studio 接入 mPaaS 开发](https://help.aliyun.com/document_detail/164890.htm)

[可下载 mPaaS 程序包的仓库](https://mvn.cloud.alipay.com/nexus/content/repositories/open/)
