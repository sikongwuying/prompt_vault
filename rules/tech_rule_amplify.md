# Vue 3.0 + Amplify Technology Stack

## AWS鉴权校验机制

- **Custom Cognito User Pool** - 使用自定义Cognito用户池，不使用Amplify Auth模块

- **AWS IAM Role** - 本地环境使用AWS SSO的临时凭据，部署在AWS计算服务上则使用IAM Role绑定进行授权。不使用任何的IAM User AKSK

- **Cognito JWT Token** - 前端使用Cognito JWT token进行API调用鉴权

- 注意，授权使用S3存储桶的权限时，定义具体的资源要用Arn：Resource: !Sub '${Bucket.Arn}/*'

  

## Frontend Framework

- **Vue 3.0** - 使用Composition API和TypeScript

- **Amplify Hosting** - 无需构建过程，直接部署

- **Vite** - 开发服务器和构建工具

- **TypeScript** - 类型安全的JavaScript开发

- **Tailwind CSS** - 实用优先的CSS框架

- **Vue Router** - 单页应用路由管理

- **Pinia** - Vue 3状态管理

  

## Backend Framework

- **AWS Amplify Data** - 自动创建和管理DynamoDB表，无需手动创建

- **AWS AppSync** - GraphQL API，通过Amplify Data模块自动生成

- **AWS Lambda** - Serverless compute with Python 3.12+（如需自定义业务逻辑）

- **监控和日志**：集成CloudWatch和CloudTrail，cloudtrail已经有了，不需要重复创建

  

## Amplify Configuration

```typescript

// amplify/data/resource.ts

import { type ClientSchema, a, defineData } from '@aws-amplify/backend';

  

const schema = a.schema({

// 定义数据模型，Amplify会自动创建DynamoDB表

User: a

.model({

id: a.id(),

email: a.string().required(),

name: a.string(),

createdAt: a.datetime(),

})

.authorization(allow => [allow.authenticated()]),

});

  

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({

schema,

authorizationModes: {

defaultAuthorizationMode: 'userPool',

userPoolConfig: {

userPoolId: 'your-custom-cognito-user-pool-id'

}

}

});

```

  

## Cognito Integration

```typescript

// src/auth/cognito.ts

import { CognitoUserPool, CognitoUser, AuthenticationDetails } from 'amazon-cognito-identity-js';

  

const poolData = {

UserPoolId: 'your-user-pool-id',

ClientId: 'your-client-id'

};

  

export const userPool = new CognitoUserPool(poolData);

  

// 登录函数

export const signIn = (username: string, password: string): Promise<any> => {

return new Promise((resolve, reject) => {

const authenticationDetails = new AuthenticationDetails({

Username: username,

Password: password

});

const cognitoUser = new CognitoUser({

Username: username,

Pool: userPool

});

cognitoUser.authenticateUser(authenticationDetails, {

onSuccess: resolve,

onFailure: reject

});

});

};

```

  

## Deployment

- **Amplify Hosting** - 自动化CI/CD部署

- **Environment separation** - 通过Amplify环境管理prod/dev分离

- **Automated rollback** - Amplify自动回滚失败的部署

- **Custom Domain** - 支持自定义域名配置

  

## Development Workflow

```bash

# 安装依赖

npm install

  

# 本地开发

npm run dev

  

# Amplify初始化

npx ampx sandbox

  

# 部署到Amplify

git push origin main # 自动触发部署

  

# 查看Amplify状态

npx ampx sandbox --list

```

  

## File Structure Conventions

```

src/

├── components/ # Vue组件

├── views/ # 页面组件

├── stores/ # Pinia状态管理

├── auth/ # Cognito认证逻辑

├── api/ # API调用封装

├── types/ # TypeScript类型定义

└── utils/ # 工具函数

  

amplify/

├── data/ # 数据模型定义

├── auth/ # 认证配置（如果使用）

└── storage/ # 存储配置（如果需要）

```

  

## Browser Support

- **Modern Browsers** - Chrome 90+, Firefox 88+, Safari 14+, Edge 90+

- **Mobile Browsers** - iOS Safari 14+, Chrome Mobile 90+

- **Progressive Web App** - 支持PWA特性

- **Responsive Design** - 移动优先的响应式设计

  

## 期望交付物

  

1. Vue 3.0应用程序源代码

2. Amplify配置文件和数据模型

3. 自定义Cognito集成代码

4. 部署和配置文档

5. 安全配置说明

6. 测试和验证脚本

  

## 更新要求

  

每次修复错误以后都需要更新部署和配置文档，保持配置和配置文档与实际情况一致。特别注意Amplify Data模型变更和Cognito配置的同步更新。