# Readme

[toc]

## 项目介绍

- 实现了一个静态测试选择工具，借助WALA框架能够根据代码变更自动选取出受变更影响的测试（Impacted Tests）。
- 为了实现可扩展性以及高内聚低耦合，采用了面向接口编程的思想以及抽象工厂的设计模式。

## 鲁棒性考虑

进行了一些输入错误处理

- 处理了输入的项目或者变更信息路径不存在、输入粒度不是m/c的情况。
- 在StaticTestCaseChose类中定义了**checkArgsValid**方法在最开始检测参数是否有效

## 代码布局

### StaticTestCaseChose

- **项目入口**，通过调用各子类来实现项目功能。
- 分为**3步**，初始化代码依赖图、将代码依赖图转成Dot文件、读取变更信息并选择测试用例。

### DependencyGraph

- 一个**抽象类**，是**自定义的依赖图结构**，用来存储测试用例选择所需的信息。

- 依赖图中存储的是节点及**直接调用**该节点的节点的映射关系。

- 测试用例选择时所需的**间接依赖**关系则通过调用**getCallers**方法得出
- 有ClassDependencyGraph和MethodDependencyGraph两个子类。

### TestChoose

- **接口**，根据变更信息以及代码间依赖关系来进行测试用例选择
- 有**两个**实现，ClassTestChoose以及MethodTestChoose

### Utils

- 自定义的工具类
- 有**6个函数**，被其它类所使用，具体见代码注释。