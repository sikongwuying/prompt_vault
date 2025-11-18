# Kiro 开发规范与项目模板

这是一个专为 Kiro AI 开发助手设计的规范和模板集合，包含了多种 AWS 技术栈的开发规则、安全标准和项目规格。

## 📁 项目结构

### Rules（开发规范）
- **security_rule.md** - AWS Well-Architected 安全框架检查清单
- **tech_rule_amplify.md** - Vue 3.0 + Amplify 技术栈规范
- **tech_rule_lambda_function.md** - Lambda 无服务器应用开发规范
- **tech_rule_static_html.md** - 静态网站开发规范

### Specs（项目规格）
- **合规新闻日报.md** - 安全合规新闻自动推送系统需求
- **frontend-requirement-en.md** - Streamlit 天气助手前端需求

## 🚀 使用方法

### 1. Agent Steering 配置
将 `rules/` 目录下的规范文件添加到 Kiro 的 Agent Steering 中，约束 AI 开发的技术规范和安全标准。

### 2. Spec 驱动开发
使用 `specs/` 目录下的规格文件让 AI 规划开发需求和任务分解。

### 3. 技术栈选择
根据项目需求选择对应的技术规范：
- **Web 应用**: Amplify + Vue 3.0
- **智能代理**: Bedrock AgentCore + Strands
- **无服务器**: Lambda + Python
- **静态网站**: HTML + Tailwind CSS

