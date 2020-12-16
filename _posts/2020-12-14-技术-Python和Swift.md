---
layout: post
title: 技术 Swift 计算器的设计逻辑
---

# 技术 Swift 计算器的设计逻辑

教授iOS 开发的Stanford Paul Hegarty老师，大约在2017年的课程中讲过用swift写计算器app的例子，后来，特别是在iOS开发从MVC框架，转到MVVM框架上来的时候，他已经不再使用这个例子。

但我个人认为，计算器的设计逻辑，对于理解swift语言，是一个很好的入门例子，它比较简单(虽然从完整app的角度，其实一点都不简单)，能比较快地写出demo。

下面的内容里面，如果有不准确的地方，一定是我个人的理解。这个文章会持续更新和修改。

### 首先来看一下大的框架定义：

```swift
struct Cal {
	// 定义一个内部的参与计算的变量，这个变量从外部无法访问，只能从内部设定
	private var accmulator: Double? 
	
	// 计算引擎函数
	func perform(_ symbol: String) {
	
	}
	
	// 赋值函数，它负责把外部值赋给内部变量，因为内部变量可变，所以它是mutating
	mutating func setOperand(_ operand: Double) {
		accumulator = operand
	}
	
	// 结果取值接口，它对外暴露，并且通过 get 设定为当前结果只读模式
	var result: Double {
		get {
		    return accumulator!
		}
	}
}

```

上面是一个经典的数据处理引擎的设计模式。


待续写
post status: in progress

tag: 编程 python swift
