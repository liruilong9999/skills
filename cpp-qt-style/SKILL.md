---
name: cpp-qt-style
description: enforce Qt C++ coding style, UTF-8 encoding rules, Chinese documentation, cross-platform consistency, and strict control-flow safety rules
---

# C++ Qt Coding Style Rules

## Goal

统一代码风格、编码规范、日志规范与控制流安全规则，确保跨平台一致性（Windows/Linux）

---

## 注释规范

- 必须使用 Doxygen 风格
- 必须使用中文
- 所有 public 接口必须有注释

---

## 编码规范

- 所有源码必须使用 UTF-8（推荐无 BOM）
- 禁止 GBK / ANSI
- 必须保证编译器按 UTF-8 解析源码

MSVC：
- /utf-8 或 #pragma execution_character_set("utf-8")

GCC / Clang：
- -finput-charset=UTF-8

---

## QString 使用规则

- 默认使用 QStringLiteral（性能最优）
- 若编译环境不保证 UTF-8，可使用 QString
- 同一模块必须统一策略
- 禁止混用

---

## 日志规范

- 所有日志必须使用中文
- 必须包含模块标识（英文）
- 允许保留必要英文术语（关键字 / 错误码 / 协议字段）

格式：
[Module] 中文描述

- 禁止无上下文日志
- 禁止 silent fail

---

## 命名规范

- 成员变量：m_ 前缀
- 指针成员：m_p 前缀
- 函数：小驼峰，动词开头
- 类名：大驼峰

---

## Qt 规则

- 必须使用新 connect 语法
- QObject 使用父子内存管理
- 禁止子线程操作 UI

---

## 控制流与条件规范（新增强制规则）

### 指针判空

- 禁止使用隐式布尔判断
- 必须使用显式 nullptr 比较

---

### if / for 结构

- if / for / while 必须使用大括号
- 即使单行语句也必须使用 {}

---

### 逻辑表达式

- 多条件逻辑必须显式使用括号明确优先级
- 禁止依赖默认运算符优先级

---

### 常量比较规则

- 常量必须写在左侧进行比较

---

## 禁止项

- 禁止依赖系统默认编码
- 禁止魔法数字
- 禁止旧 connect
- 禁止无日志错误处理
- 禁止裸指针无生命周期管理
- 禁止隐式条件判断指针
- 禁止无大括号控制流
- 禁止未显式优先级的逻辑表达式

---

## 健壮性

- 所有输入必须校验
- 所有错误必须输出日志（中文日志，关键字和专业术语等可保留英文）

---

## 返回值规范

- true = 成功
- false = 失败
- 禁止反语义

---

## 设计原则

- 单一职责
- 函数 ≤ 80 行
- 使用 early return

---

## Enforcement

- 必须遵守所有规则
- 不符合规范代码必须重构
- 编码问题优先检查：源码 → 编译器 → Qt中，不要举例