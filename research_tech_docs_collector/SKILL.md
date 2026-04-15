---
name: research_tech_docs_collector
description: enforce full-dimension technical research workflow, structured Chinese Markdown output, mandatory save path /docs/调研/{technology_name}_资料收集.md, knowledge-graph style documentation, Codex-compatible rules
---

# 技术资料调研 Skill 规则

## Goal

统一技术调研流程、文档结构、输出路径与中文撰写规范，确保对指定技术（如 NISQA、深度学习模型、框架、系统组件等）进行全维度信息调研、结构化整理与对比分析，输出标准、可直接归档的中文技术调研文档。

---

## 输入参数

- `technology_name`：string（必填）—— 技术名称，例如 `NISQA`、`PyTorch`、`Kafka`
- `focus_area`：string（可选）—— 重点关注领域，例如 `训练原理`、`使用`、`部署`、`对比`
- `depth`：enum（必填）—— 调研深度，可选值：`shallow`、`normal`、`deep`

---

## 输出文档规范

- 必须生成完整的 Markdown 文档
- 全部正文使用中文（香港地区优先使用繁体中文）
- 文档标题使用中文
- 结构必须严格按照下方「调研工作流」的 11 个章节组织
- 每个章节必须有实质性内容，不得留空
- 必须包含真实可访问的 URL（优先 GitHub + arXiv + 官方文档）
- 禁止编造论文、版本信息或不存在的链接

---

## 文档保存路径（强制）

- 必须保存到以下路径：
	`/docs/调研/{technology_name}_资料收集.md`
- 文件名严格格式：`{technology_name}_资料收集.md`（technology_name 保持原始写法，不加空格或下划线替换）

---

```markdown
## 调研工作流（必须严格遵循）

### 1. 技术总体介绍
- 技术是什么（定义）
- 解决什么问题
- 所属领域（ML / backend / infra 等）
- 核心思想一句话总结

### 2. 技术发展历史
- 起源论文 / 初始版本
- 时间线（年份 + 关键变化）
- 重要版本演进
- 社区或公司推动情况

### 3. 版本信息整理
- major version 列表
- 每个版本主要变化点
- 是否仍维护
- 当前主流版本

### 4. 核心原理（模型/算法适用）
- 模型结构（如 transformer / CNN / MOS predictor）
- 输入输出
- loss function（如适用）
- 训练方式（supervised / self-supervised）

### 5. 功能能力分析
- 支持的能力列表
- 典型使用场景
- 优势
- 局限性

### 6. 使用方法指南
- 安装方式（pip / git clone / build）
- 基本使用代码（Python/C++ 示例）
- 推理流程
- 常用 API 说明

### 7. 环境配置要求
- 支持操作系统（Linux / Windows / WSL）
- Python / CUDA / 主要依赖
- requirements.txt 说明
- 常见安装问题及解决办法

### 8. 实际使用示例
- 最小可运行 Demo
- 输入输出示例
- 结果解读

### 9. 横向对比分析
- 同类技术对比（例如 NISQA vs DNSMOS）
- 精度 / 速度 / 使用成本
- 适用场景差异

### 10. 参考资料（严格格式化）
- 官方论文（标题 + URL）
- GitHub 仓库
- 官方文档
- 博客 / 技术解析
- 视频资源（如有）

### 11. 风险与限制
- 适用边界
- 数据偏差问题
- 模型/技术局限
- 工程落地风险

---

## 规则

- 必须严格按照以上 11 个章节输出 Markdown
- 每个章节必须有实质内容，不得留空或写“暂无”
- 所有正文必须使用中文（专有名词、代码、链接可保留英文）
- 必须包含真实可访问的 URL
- 优先来源：GitHub、arXiv、官方文档
- 输出文档必须可直接用于团队知识库归档

---

## 禁止项

- 禁止只输出简介或部分章节，必须覆盖全部 11 个章节
- 禁止正文使用英文（除必要专有名词、代码块、链接外）
- 禁止编造论文、链接或技术信息
- 禁止输出路径错误（必须严格保存至 `/docs/调研/` 目录）
- 禁止省略任何必填章节

---

## 可选扩展功能

- `add_docker_support`：增加 Docker 部署章节
- `add_api_service_design`：增加 API 服务设计章节
- `add_model_architecture_diagram`：增加模型架构图描述
- `add_cli_usage`：增加命令行使用示例

---

## Enforcement

- 必须严格遵守所有规则
- 不符合规范的输出必须重新生成
- 优先检查顺序：输入参数 → 11 个工作流章节 → 输出路径 → 中文规范 → 真实链接有效性
```
