# 一、固定要求

## 涉及文档时，遵循以下要求：

- markdown中写中文，除非指定英文
- markdown中绘制流程图等，图中也写中文
- 如果专业术语需要英文，首次出现带上括号和中文解释，如：xxx(叉叉叉） 
- 禁止使用rm -rf 或者类似的批量删除，只能单个依次删除

## C++/Qt

- 如果是C++/Qt代码，默认使用Qt5
- 如果代码框架已经有cmake，默认沿用当前风格
- 如果代码中cmake已经使用了Qt路径或者Qt环境变量，默认使用该部分
- C++/Qt倾向于模块化编程，分库和插件，库不处理业务，只提供能力，插件处理业务

## 编码时遵循

- 项目的AGENTS.md需要明确当前项目是干什么的，代码结构等
- 修改代码前需要进行影响域分析
- 需要识别代码的承重墙，在项目的AGENTS.md标注高风险区域
- 编写代码前，建立变更预算，明确边界，允许修改哪些，禁止修改哪些，禁止顺手重构
- 编译通过后，建立三层测试兜底：1.当前功能的测试、2.关联功能的回测、3.业务闭环测试
- 禁止自己开发、自己审查

# 二、其它要求

- 每次回答问题前叫一句"老大"，调用工具前叫一次"老大"
- 如果仓库有codegraph，修改完代码后，执行一次`codegraph sync`

<!-- CODEGRAPH_START -->

## CodeGraph

In repositories indexed by CodeGraph (a `.codegraph/` directory exists at the repo root), reach for it BEFORE grep/find or reading files when you need to understand or locate code:

- **MCP tool** (when available): `codegraph_explore` answers most code questions in one call — the relevant symbols' verbatim source plus the call paths between them, including dynamic-dispatch hops grep can't follow. Name a file or symbol in the query to read its current line-numbered source. If it's listed but deferred, load it by name via tool search.
- **Shell** (always works): `codegraph explore "<symbol names or question>"` prints the same output.

If there is no `.codegraph/` directory, skip CodeGraph entirely — indexing is the user's decision.
<!-- CODEGRAPH_END -->
