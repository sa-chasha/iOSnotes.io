# iOSnotes.io
iOS开发的学习笔记（tips，翻译）。
# SwiftUI

## WWDC19

### SwiftUI简介：数据驱动而不是事件驱动

- 陈述性语法
- 组合式UI
- 如何自动保持状态
- 可中断动画
- 自动支持

### SwiftUI基础知识

- Views and Modifiers，自定义视图：小视图构建大视图

	- Views：永远拆分成小结构

		- container view

			- 比如：堆栈

		- $:passing a binding

			- 允许一个视图编辑另一个视图的状态的托管参考

				- 传递一个被绑定的参数

		- @State

			- 数据依赖关系

		- 视图是如何遵循View协议的？

			- 函数

		- 添加和删除View的时候，if很好用
		- 重复代码段用forEach

	- Modifiers

		- 从一个视图创建新视图的方法：外侧包里侧
		- 动画

- Adaptive controls：自动适应上下文

	- Form&Section
	- Button
	- Toggle
	- Picker
	- disabled
	- accentColor
	- contextMenu
	- environment preview
	- gesture

- Navigating the screens

	- NavigationView
	- NavigationLink？
	- NavigationButton(destination:)
	- NavigationBarItems
	- NavigationBarTitle
	- Tabbar
	- SplitView

### Data Flow Though SwiftUI

- 二原则

	- 在视图层级中，读取的每一条数据都有source of truth
	- 每次在视图读取数据，都在为视图创建依赖

### 整合SwiftUI

- 整合数据模型和SwiftUI

	- BindableObject

		- Key value publisher
		- Delegate

	- $data

		- 直接重写数据模型的权限

- Drag and Drop

	- onDrop

- Pasteboard

	- onPaste

- Focus
- Commands

### Building Custom Views in SwiftUI：利用SwiftUI构建自定视图

- layout basics

	- 布局过程

		- 根据视图提供推荐尺寸

			- 根视图会提供整个safearea

		- 子视图选择自己的尺寸

			- 视图有尺寸调整行为，要决定何时与如何调整

		- 父视图决定子视图位置
		- SwiftUI会圆角化边缘

	- Frame不是一个约束，而是一个View，因此子视图会选择自己的尺寸（导致图片不适应尺寸）
	- HStack and VStack

		- change the childview's layoutPriority

			- 默认：0
			- 1:次优先级

	- SwiftUI的默认布局符合apple human interface building原则
	- Alignments

		- AlignmentGuide

- Graphics in SwiftUI

	- Drawing-views
	- Drawing Model
	- Gradients
	- Sample  Control

		- custom shape

	- ZStack
	- Custom Animation

		- 定义结束状态

			- ViewModifier

### SwiftUI的辅助功能

### Combine（重要！）

- Combine简介

	- A unified, declarative API for processing values over time：会根据时间处理这些值的统一声明式API。

		- Publishers

			- 声明部分：描述值和错误是如何产生的，但并不是这些值的源头。

				- 是一个结构

		- Operators

			- 从上游获取值，向下游发送值

				- upsteam
				- subscribe

		- Subscribers

			- 随着时间接收Publisher的值

				- 执行并改变状态，因此使用引用状态：是一个类

		- Declarative Operator API

			- 如何选择
			- .compactMap

				- 坏值不取用

			- .prefix

				- 三次

		- Combing publisher

			- Zip

				- 将几个上游转为一个元组

					- network request

			- Combine Latest

				- when/or

			- decoder

				- json

- Combine Practice 
*之后可以重看一下！

	- Publisher：发送

		- publisher重要的部分是它的输出和错误类型
		- map function：将通知转换成需要的形式，作用于publisher并返回一个新的publisher操作符
		- tryMap：可以将错误抛出
		- decode：处理Json数据
		- Error handling Operators

			- 错误恢复

		- Flat map

			- return a new publisher

		- Schedule Operators

	- Subscriber：接收

		- AnyCancellable
		- Sink
		- Subjects
		- 三规则

			- subscriber receive a singe subscription, follow by zero or more values, possibly be terminated by a single completion, indicates the complete or fail. 

				- 结束是可选的

		- SwiftUI BindableObject

	- Design for composition

		- @Published
		- CombineLatest
		- eraseToAnyPublisher
		- debounce
		- remove duplicates

### SwiftUI Lab

### 联网改进

### [现代SwiftAPI设计](https://www.swift.org/documentation/api-design-guidelines/)

- more in property wrapper

	- Property Wrapper related talks
	- 当你添加属性包装器的时候，你就在打包这个属性，并在它读写时添加一些额外操作。

### Core Location新功能

- 

	- 授权将由弹窗开始

		- create a CLLocationManager
		- LocationManager.requestAuthorization()

	- 永久授权

		- 授权不一致的情况

			- 最开始就申请永久授权
			- inUse，在之后的某一时刻升级

		- tvOS does not support Always, watchOS does not have Always. MacOS不需要请求授权

	- 使用期间授权

- 子主题 2

## 定义：基于Swift的API

## WWDC20

### Formatter API：让数据人性化
（内置本地化，尽可能多用）

- 测量：measurement formats
- 时间：DateFormat

	- 时间
	- 时间段
	- Check out Date Field Symbol Table if needed

- Names：PersonNameCompoentsFromatter

	- 首字母头像
	- 内置功能

- 列表：ListFormatter
- 数字：NumberFormatter
- 字符串：Stringsdict

### 创建位置感知的企业app（有代码）

- Caffe macs app基于位置的体验

	- （重要）存储用户选择：UserDefaults
	- 准确定位

		- Core Location

			- When in use
			- Always

		- iBeacon（暂时用不到）：需要在店铺里设置iBeacon通信模块

	- 数据本地化

### 位置的新功能

- 一个app需要了解我的哪些信息才能提供功能？
- 增加了精确定位的许可

	- 高精度

		- 区域功能需要高精度。在低精度定位的设备上不会触发提醒。
		- 低精度授权可以升级为高精度

	- 低精度

		- 大概每小时重新计算四次

- Key: check out when needed
- ActivityType
- App chlips

	- app的轻量级子应用

- WidgetKit

