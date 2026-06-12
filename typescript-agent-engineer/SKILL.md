---
name: typescript-agent-engineer
description: 用于 AI Agent、MCP、Workflow、LLM Runtime 等 TypeScript 项目的工程规范。当用户需要些前端代码时触发该skill
---

# 总体原则

强调：

* strict TypeScript
* schema-first
* streaming-first
* 明确边界
* production-ready

禁止：

* any
* 弱类型
* demo 风格代码
* 隐式 schema
* 巨型模块

---

# runtime

默认：

```txt
Node.js LTS
Bun
ESM
TypeScript 5.5+
```

---

# typescript rules

必须启用：

```json
{
  "strict": true,
  "noImplicitAny": true,
  "strictNullChecks": true,
  "exactOptionalPropertyTypes": true,
  "noUncheckedIndexedAccess": true
}
```

禁止关闭 strict。

---

## no any

禁止：

```ts
const value: any
```

允许：

```ts
unknown
```

并显式解析。

---

## explicit types

公共函数必须声明：

* 参数类型
* 返回值类型

禁止大型结构隐式推导。

---

# architecture rules

目录结构允许自由设计，但必须：

* 按职责拆分
* 避免循环依赖
* 避免共享可变状态
* 避免 God Object

禁止：

```txt
utils.ts
helpers.ts
common.ts
```

---

# naming rules

文件：

```txt
kebab-case
```

类型：

```txt
PascalCase
```

函数：

```txt
camelCase
```

常量：

```txt
UPPER_SNAKE_CASE
```

---

# schema rules

以下内容必须做 schema validation：

* API 输入
* Tool 参数
* 配置
* 环境变量
* LLM 输出

统一使用：

```txt
zod
```

禁止直接信任：

```ts
req.body
tool input
model output
```

---

# async rules

所有 IO 使用：

```txt
async/await
```

禁止：

```txt
callback hell
```

---

## abort signal

以下操作必须支持：

* fetch
* stream
* websocket
* long task

统一使用：

```txt
AbortSignal
```

---

# stream rules

LLM streaming 必须使用：

```ts
AsyncIterable<AgentChunk>
```

禁止：

```txt
裸字符串流
callback stream
```

---

# chunk rules

```ts
type AgentChunk =
  | {
      type: "text"
      content: string
    }
  | {
      type: "tool-call"
      toolName: string
      arguments: unknown
    }
  | {
      type: "tool-result"
      toolName: string
      result: unknown
    }
```

---

# tool rules

Tool 必须包含：

* schema
* 类型
* 错误处理
* 超时控制

禁止修改全局状态。

禁止：

```ts
return "success"
```

必须：

```ts
return {
  success: true,
  data
}
```

---

# agent rules

禁止 Agent 直接：

* 操作数据库
* 操作文件
* 调用 infra

必须通过明确的 service/repository 边界。

---

# prompt rules

Prompt 必须：

* 模板化
* 版本化

禁止：

```ts
const prompt = "..."
```

---

# logging rules

统一：

```txt
pino
```

禁止：

```ts
console.log
```

---

# error rules

禁止：

```ts
catch {}
```

错误必须分类，例如：

```txt
ValidationError
ToolError
NetworkError
AgentError
WorkflowError
```

禁止向用户暴露：

* stack
* token
* sql
* internal path

---

# ai generation rules

AI 生成代码时必须包含：

* 类型
* schema
* async
* 错误处理

禁止：

* any
* 巨型函数
* 巨型类
* 魔法字符串
* 动态字段

---

# preferred libraries

validation:

```txt
zod
```

logging:

```txt
pino
```

web:

```txt
Hono
Fastify
```

orm:

```txt
Drizzle
Prisma
```

ai sdk:

```txt
OpenAI SDK
Vercel AI SDK
```

---

# code generation

生成代码默认要求：

```txt
production-ready
```

禁止：

```txt
demo-only
toy example
```
