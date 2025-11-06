# Technology Stack

## AWS鉴权校验机制
- OAuth2 with Cognito
- 使用Agentcore Identity和Agentcore gateway实现权限管理
## Frontend Framework
- 无，系统为AI智能体，不需要前端

## Backend Framework
- **AWS Bedrock AgentCore**: Managed agent runtime environment
- **AWS Lambda** - Serverless compute with Python 3.12+
- **Amazon Cognito**: Authentication and authorization
- **Strands Agents**: Agent framework with MCP integration
- **Amazon EventBridge** - Scheduled triggers
- **使用Python代码：** 使用独立的虚拟环境部署python的依赖包，并且在README的指引中描述清楚如何部署，如何使用。使用pip3安装依赖包。
- **FastAPI**: Modern API framework for Python
- **CloudWatch**: Monitoring and observability
- Direct API access： AgentCore Gateway configuration exposing insurance API as MCP tools
- Amazon Neptune: will store your knowledge graph, ensuring that the data is up-to-date and accessible.
- **Amazon S3：** 在将数据加载到 Neptune Analytics 图表之前，Amazon S3 存储桶将保存原始和处理过的数据。
- **LlamaIndex：** LlamaIndex 是一个简单、灵活的第三方开源数据框架，用于将自定义数据源连接到大型语言模型 (LLM)。我们将使用 LlamaIndex 为我们的 GraphRAG 应用程序生成向量和知识图谱嵌入。更多信息，请访问 LlamaIndex [网站](https://www.llamaindex.ai/)
- **Streamlit：** Streamlit 是一个开源 Python 框架，面向数据科学家和 AI/ML 工程师，只需几行代码即可交付交互式数据应用程序。更多信息，请访问 Streamlit [网站](https://streamlit.io/)

## Deployment
**AWS CloudFormation** - Infrastructure as Code deployment
	- Lambda函数要用独立的文件，不需要写在CloudFormation模板里
	- CloudFormation部署成功后上传实际代码
	- 使用update-function-code更新Lambda函数
- **部署文档**：初次创建提供详细的部署和配置说明。每次更新代码都需要更新文档。


## Development Workflow
```bash
# No build process - direct file editing
# Deploy infrastructure:
./deploy.sh

# Test functionality:
aws lambda invoke --function-name <replace-real-function-name> --payload '{}' response.json

# Monitor logs:
aws logs tail /aws/lambda/replace-real-function-name --follow
```

## File Structure Conventions
- All Python files use relative imports for cross-references
- Infrastructure templates in `/infrastructure/` directory
- Lambda source code in `/src/` directory
- Management scripts in `/scripts/` directory
- Documentation in `/docs/` directory
- Each service module has its own subdirectory with dedicated resources

### 期望交付物

1. CloudFormation基础设施模板
2. 应用程序源代码
3. 部署和配置文档
4. 安全配置说明
5. 测试和验证脚本

## 更新要求

每次修复错误以后都需要更新部署和配置文档，保持配置和配置文档与实际情况一致。