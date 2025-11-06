This checklist is designed for comprehensive review of codebases against AWS Well-Architected Framework principles and cloud-native best practices. Each item should be verified and marked as ✅ PASS, ❌ FAIL, or ⚠️ REVIEW NEEDED.
### Identity and Access Management (IAM)

- [ ] IAM roles follow principle of least privilege
- [ ] No hardcoded AWS credentials in code or configuration
- [ ] IAM policies use specific actions rather than wildcards (*)
- [ ] Cross-account access uses AssumeRole with proper conditions
- [ ] Service-linked roles used where appropriate
- [ ] IAM policy conditions restrict access by IP, MFA, or time when needed
- [ ] No long-lived access keys for applications (use IAM roles instead)
- [ ] Resource-based policies are properly scoped
- [ ] We use AWS Cognito for all authentication - auth bypass must defeat Cognito
- [ ] Secrets are in AWS Secrets Manager or k8s secrets, never in code

### Data Protection

- [ ] Encryption at rest enabled for all data stores (S3, RDS, DynamoDB, EBS)
- [ ] Encryption in transit using TLS 1.2+ for all communications
- [ ] AWS KMS used for key management with customer-managed keys when required
- [ ] S3 bucket encryption enabled by default
- [ ] Database connections use SSL/TLS
- [ ] Secrets stored in AWS Secrets Manager or Systems Manager Parameter Store
- [ ] Data classification implemented (public, internal, confidential, restricted)
- [ ] SQL injection is only valid if using raw queries (we use Prisma ORM everywhere)
- [ ] All internal services communicate over mTLS within the k8s cluster
- [ ] File uploads go directly to S3 with presigned URLs (no local file handling)
- [ ] All user input is considered untrusted and validated on the backend
- [ ] All webhooks use HMAC signature verification
- [ ] All Amazon S3 buckets must have encryption enabled, enforce SSL, and block public access.
- [ ] All Amazon DynamoDB Streams tables must have encryption enabled. 
- [ ] All Amazon SNS topics must have encryption enabled and enforce SSL. 
- [ ] All Amazon SNS queues must enforce SSL.

### Network Security

- [ ] Resources deployed in VPC with private subnets for internal components
- [ ] Security groups follow least privilege (specific ports/protocols)
- [ ] NACLs implemented as additional security layer where appropriate
- [ ] VPC Flow Logs enabled for network monitoring
- [ ] AWS WAF configured for web applications
- [ ] CloudFront used with proper security headers
- [ ] No resources exposed to 0.0.0.0/0 unless required and justified

### Application Security

- [ ] Input validation implemented for all user inputs
- [ ] Output encoding prevents XSS attacks
- [ ] SQL injection prevention (parameterized queries/ORM)
- [ ] CSRF protection implemented
- [ ] Authentication and session management properly implemented
- [ ] API rate limiting and throttling configured
- [ ] Security headers configured (HSTS, CSP, X-Frame-Options)
- [ ] All APIs require valid JWT tokens validated at the gateway level
- [ ] We allow verbose error messages in dev/staging (not production)
- [ ] Frontend validation is only for UX, not security
- [ ] We use CSP headers and strict Content-Type validation
- [ ] CORS is configured per-service based on actual needs

### Compliance

- [ ] 用AI生成的内容，必须在内容底部加上一句话表明正在使用人工智能来辅助生成的报告、建议、决策或推荐，此披露必须至少在每次会话开始时进行，披露内容必须清晰、易懂且显著，保存披露记录以供审计
- [ ] 向用户提供AI系统的能力和限制说明
