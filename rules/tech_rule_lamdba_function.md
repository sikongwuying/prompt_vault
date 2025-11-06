# Technology Stack

## AWS鉴权校验机制
- AWS  IAM Role - 本地环境使用AWS SSO的临时凭据，部署在AWS计算服务上则使用IAM Role绑定进行授权。不使用任何的IAM User AKSK
- 注意，授权使用S3存储桶的权限时，定义具体的资源要用Arn：Resource: !Sub '${Bucket.Arn}/*'

## Frontend Framework
- **Static HTML/CSS/JavaScript** - No build process required
- **Inline CSS** - Email client compatibility via embedded styles
- **Responsive HTML Email** - Mobile-first design with media queries

## Backend Framework
- **AWS Lambda** - Serverless compute with Python 3.12+
- **Amazon DynamoDB** - NoSQL database for lamdba functions，创建Dynamo数据库时如果使用KMS进行加密，When specifying a KMSMasterKeyId, you must also specify SSEType as KMS.
- **Amazon SES** - HTML email service
- **Amazon EventBridge** - Scheduled triggers
- **使用Python代码：** 使用独立的虚拟环境部署python的依赖包，并且在README的指引中描述清楚如何部署，如何使用。使用pip3安装依赖包。
- **监控和日志**：集成CloudWatch和CloudTrail, 如果CloudTrail已经有一个，不需要重新创建了。

## Deployment
- **AWS CloudFormation** - Infrastructure as Code deployment
	- Lambda函数先用内联占位符代码创建
	- CloudFormation部署成功后上传实际代码
	- 使用update-function-code更新Lambda函数
- **No build commands** - Direct Python code deployment to Lambda
- **Environment separation** - Prod/dev stacks with parameter overrides
- **Automated rollback** - CloudFormation stack rollback on failure
- **部署文档**：初次创建提供详细的部署和配置说明。每次更新代码都需要更新文档。

## Browser Support
- **Email Clients** - Outlook, Gmail, Apple Mail, Thunderbird
- **Mobile Email** - iOS Mail, Android Gmail, Outlook Mobile
- **Responsive design** - Adaptive layout for different screen sizes
- **Progressive enhancement** - Plain text fallback for unsupported clients

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

### 期望交付物

1. CloudFormation基础设施模板
2. 应用程序源代码
3. 部署和配置文档
4. 安全配置说明
5. 测试和验证脚本

## 更新要求

每次修复错误以后都需要更新部署和配置文档，保持配置和配置文档与实际情况一致。