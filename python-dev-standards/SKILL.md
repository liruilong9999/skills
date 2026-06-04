---
name: python-dev-standards
description: Define or review general Python development standards for non-business-specific projects. Use when Codex needs to create a new Python project structure, standardize an existing repository, choose common layering, organize packages, tests, configuration, scripts, and delivery conventions, or review whether a Python codebase follows maintainable engineering practices.
---

# Python 开发规范

## 核心目标

为通用 Python 项目提供稳定、可维护、可测试的开发规范。  
这个 skill 不绑定具体业务框架，重点约束目录结构、分层、配置、测试、脚本、质量门槛和交付方式。

## 适用范围

适用于以下场景：

- 新建通用 Python 项目
- 重构已有 Python 仓库的目录结构
- 为团队补统一开发规范
- 审查仓库是否缺少分层、测试、配置或脚本约定
- 落地 CLI、服务、库、任务型工具等通用 Python 工程

## 使用流程

### 1. 先判断项目类型

先判断当前项目更接近哪一类：

- 纯库项目
- CLI 工具项目
- Web 服务项目
- 任务/脚本驱动项目
- 混合型项目

再按需参考 [references/project-layouts.md](references/project-layouts.md) 选目录骨架。

### 2. 固定顶层目录职责

默认顶层目录职责如下：

- `src/`：正式业务代码
- `tests/`：测试代码
- `scripts/`：一次性或维护型脚本
- `docs/`：设计、约定、接口与说明文档
- `configs/` 或 `config/`：非代码配置模板
- `examples/`：示例调用或演示代码
- `tools/`：开发辅助脚本或本地工具

不要把运行时代码、测试、脚本、临时文件混在一起。

### 3. 固定 `src/` 分层

通用情况下，优先使用以下分层思想：

- `entrypoints`：入口层，例如 CLI、HTTP、worker
- `application`：用例编排层
- `domain`：核心领域模型与规则
- `infrastructure`：外部依赖适配层
- `shared`：跨模块共用但不含业务语义的工具

如果项目规模较小，可以合并层，但不要把全部逻辑塞进单个 `utils.py` 或巨型入口文件。

### 4. 配置规范

默认规则：

- 区分“代码默认值”和“运行环境配置”
- 敏感信息只从环境变量或本地未跟踪配置读取
- 配置加载集中管理，不散落在模块顶层
- 配置对象要有明确结构，不要全仓库直接读环境变量

如果项目需要多环境，至少区分：

- `dev`
- `test`
- `prod`

### 5. 测试规范

默认测试层次：

- 单元测试：覆盖核心规则、纯函数、边界条件
- 集成测试：覆盖模块协作、数据库/网络/文件系统适配
- 端到端测试：只给关键主流程

基本要求：

- 新增功能优先补测试
- 修 bug 必须补回归测试
- 测试目录结构尽量映射 `src/` 结构
- Mock(模拟对象) 只隔离边界，不模拟核心逻辑本身

### 6. 脚本与工具链规范

优先区分三类脚本：

- 开发脚本：格式化、检查、测试、本地运行
- 维护脚本：数据修复、迁移、导出导入
- 发布脚本：构建、打包、发布

脚本不要承担隐藏业务逻辑。  
重复使用的逻辑要沉淀回 `src/`，脚本只做参数组装和调用。

### 7. 编码规范

默认约束：

- 一个文件只承载相对内聚的一组职责
- 明确公开 API 和内部实现边界
- 避免跨层直接调用
- 避免循环依赖
- 类型注解优先覆盖边界、核心模型和公共函数
- 异常处理在边界层统一转换，不在底层随意吞错

命名建议：

- 包和模块：小写下划线
- 类：大驼峰
- 函数和变量：小写下划线
- 常量：全大写下划线

### 8. 依赖管理规范

默认原则：

- 区分运行时依赖与开发依赖
- 优先删除不用的依赖，而不是继续堆积
- 对外部框架的使用收敛在边界层
- 不让框架对象深度渗透到整个领域层

### 9. 文档与交付规范

至少维护这些内容：

- 项目启动方式
- 目录结构说明
- 配置项说明
- 测试运行方式
- 关键模块职责

当项目发生结构性变化时，优先同步文档，不要让代码结构和文档长期脱节。

## 默认目录骨架

按需参考 [references/project-layouts.md](references/project-layouts.md) 中的模板。  
如果用户没有指定框架或业务风格，优先使用“通用服务/CLI 混合骨架”。

## 什么时候不要强行套规范

以下情况不要机械套完整骨架：

- 一次性小脚本
- 临时数据处理任务
- 极小型实验项目
- 用户明确要求最小化结构

这时只保留最小必要规范：

- 明确入口
- 配置不要硬编码密钥
- 至少有基础测试或验证方式
- 文件职责清晰

## 审查清单

用这个 skill 做审查时，优先检查：

- 顶层目录是否混乱
- `src/` 是否缺少边界分层
- 配置读取是否散乱
- 测试是否能映射主功能
- 脚本是否承载过多业务逻辑
- 依赖是否过度耦合
- 文档是否能指导启动、测试和交付

## 完成定义

一个符合本 skill 的通用 Python 项目，至少应满足：

- 有清晰顶层目录结构
- 有稳定入口层
- 有明确配置加载方式
- 有可运行测试
- 有基础文档
- 模块职责和依赖方向清晰

## 参考资料

- 目录骨架与分层示例：见 [references/project-layouts.md](references/project-layouts.md)
