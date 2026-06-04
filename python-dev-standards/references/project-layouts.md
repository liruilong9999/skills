# Python 项目目录骨架参考

## 1. 通用服务/CLI 混合骨架

```text
project-root/
├─ pyproject.toml
├─ README.md
├─ .gitignore
├─ src/
│  └─ my_project/
│     ├─ __init__.py
│     ├─ entrypoints/
│     │  ├─ cli.py
│     │  ├─ api.py
│     │  └─ worker.py
│     ├─ application/
│     │  ├─ services/
│     │  ├─ use_cases/
│     │  └─ dto/
│     ├─ domain/
│     │  ├─ models/
│     │  ├─ rules/
│     │  └─ ports/
│     ├─ infrastructure/
│     │  ├─ config/
│     │  ├─ persistence/
│     │  ├─ clients/
│     │  └─ repositories/
│     └─ shared/
│        ├─ logging.py
│        ├─ exceptions.py
│        └─ utils/
├─ tests/
│  ├─ unit/
│  ├─ integration/
│  └─ e2e/
├─ scripts/
│  ├─ dev/
│  ├─ maintenance/
│  └─ release/
├─ docs/
│  ├─ architecture/
│  ├─ api/
│  └─ decisions/
├─ config/
│  ├─ settings.example.toml
│  └─ logging.yaml
└─ examples/
```

适合：

- 既有 CLI 又有服务接口
- 有一定模块复杂度
- 需要长期维护

## 2. 通用库项目骨架

```text
project-root/
├─ pyproject.toml
├─ README.md
├─ src/
│  └─ my_library/
│     ├─ __init__.py
│     ├─ api.py
│     ├─ models.py
│     ├─ exceptions.py
│     ├─ adapters/
│     └─ internal/
├─ tests/
│  ├─ unit/
│  └─ integration/
├─ docs/
│  └─ usage/
└─ examples/
```

适合：

- 对外暴露 Python API
- 没有复杂运行时入口
- 重点是稳定库接口

## 3. CLI 工具项目骨架

```text
project-root/
├─ pyproject.toml
├─ README.md
├─ src/
│  └─ my_cli/
│     ├─ __init__.py
│     ├─ main.py
│     ├─ commands/
│     ├─ services/
│     ├─ formatters/
│     └─ shared/
├─ tests/
│  ├─ unit/
│  └─ integration/
├─ scripts/
└─ docs/
```

适合：

- 以命令行为唯一入口
- 命令集比较清晰
- 不需要复杂 Web 服务层

## 4. 最小可维护骨架

```text
project-root/
├─ pyproject.toml
├─ README.md
├─ src/
│  └─ my_project/
│     ├─ __init__.py
│     ├─ main.py
│     ├─ core.py
│     └─ config.py
├─ tests/
│  └─ test_core.py
└─ scripts/
```

适合：

- 小型项目
- 原型快速起步
- 后续可能演进成更完整结构

## 5. 分层选型建议

### 5.1 小项目

- 可以简化为 `entrypoints + core + config + tests`
- 不要过早细分十几个目录

### 5.2 中型项目

- 建议使用 `entrypoints + application + domain + infrastructure + shared`
- 这是通用默认方案

### 5.3 大项目

- 在保持层次清晰的基础上，再按子域拆包
- 先按边界拆，再按技术细节拆

## 6. 常见反模式

- 所有代码堆在一个 `utils.py`
- 入口层直接写数据库和网络细节
- 测试目录完全不映射源码结构
- 脚本目录变成第二套业务实现
- 配置值在多个文件里直接 `os.getenv`
- 领域层直接依赖 Web 框架对象
