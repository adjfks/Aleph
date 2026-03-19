---
date created: Thursday, March 19th 2026, 11:23:30 pm
date modified: Friday, March 20th 2026, 1:22:54 am
tags:
  - AI
  - ClaudeCode
---

## 是什么
CLAUDE.md是专门写给claude code读取的onboarding文档（项目上手指南）


存放位置
1. 全局级别：~/.claude/CLAUDE.md。

2. 项目根目录：./CLAUDE.md。

3. 子目录：./src/api/CLAUDE.md。适合 monorepo 场景。比如前端目录有自己的规范，后端目录有自己的规范，可以各自维护。

4. 本地私有：CLAUDE.local.md。个人偏好，加到 .gitignore 里，不提交。

这四个层级是可以叠加的。Claude 会按顺序全部读取，从全局到具体。


## 为什么

它有几个作用：

1. 提供持久化上下文和记忆：claude code是无状态的，每次启动会读取claude.md
2. 规范化agent行为
3. 节省token：减少agent盲目探索代码的行为

写好CLAUDE.md是一件收益大于投入的事情，要做一个[[Harness Engineer]]

## 怎么做

1. 内容精简化
agent能可靠遵循的指令大概是150~200条，而claude code本身系统提示词就占了50条，因此一般claude.md行数控制在200行以内。
写claude.md的时候可以问自己：删除这一行，agent会犯错吗，如果不会就删除掉

2. 框架
what - why - how
what: 介绍项目是什么，技术栈，目录结构和对应作用等
why: 某个模块或架构这么设计的原因
how: 一些流程化的东西，比如启动命令`npm run dev`，测试命令`npm run test`，环境变量等信息。

3. 指令要具体，正向，可验证
比如不要说“编写整洁的代码”，而要说“使用Zustand，不要使用redux”等。
"不要X，要Y"原则
提供预期输出和检查清单

4. 渐进式披露
在claude.md中使用“@”导入语法`当修改api时：@src/api.md`
使用`.claude/rules/*`
```
your-project/
├── .claude/
│   ├── CLAUDE.md           # Main project instructions
│   └── rules/
│       ├── code-style.md   # Code style guidelines
│       ├── testing.md      # Testing conventions
│       └── security.md     # Security requirements
```
在md文件中可以使用YAML frontformatter
```
---
paths:
  - "src/api/**/*.ts"
---

# API Development Rules

- All API endpoints must include input validation
- Use the standard error response format
- Include OpenAPI documentation comments
```

5. 建立自我完善循环
更新 CLAUDE.md，这样你下次就不会再犯这个错误了

6. 软硬结合
软性要求使用claude.md
硬性要求使用claude hook，比如在每次修改完文件后，使用eslint格式化

7. 自定义压缩策略
```
## 压缩策略  
  
压缩对话的时候，务必保留：  
  
- 所有修改过的文件列表  
- 测试命令和测试结果  
- 当前的实现计划和进度
```


## 如何让非claude code编程工具也遵循CLAUDE.md

答案是：使用AGENTS.md

AGENTS.md 是由 Linux 基金会旗下 Agentic AI Foundation 维护的通用指令文件标准.

- Claude Code → `CLAUDE.md`
    
- Cursor → `.cursor/rules`
    
- GitHub Copilot → `.github/copilot-instructions.md`
    
- Open Code → `OPENCODE.md`
    
- Gemini CLI → `GEMINI.md`
```
Include:  
@./AGENTS.md
```

