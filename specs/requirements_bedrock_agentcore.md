https://catalog.us-east-1.prod.workshops.aws/workshops/41e422c0-0580-4443-9dc9-0bb5f2e36bc5/en-US/lab-3-aidlc-implement/lab-3-1-strands-and-runtime

生成一个安全智能代理，用于根据代码生成一个最小权限的IAM策略。
```markdown
Develop a simple Strands Agent and deploy it to AgentCore Runtime. Strands Agent uses a "model-driven" approach that fully leverages AI models' planning, reasoning, tool calling, and self-reflection capabilities. You only need to define prompts and tool lists in the code to build an AI Agent.

Please use the strands MCP and aws-document MCP to see how to develop a Strands Agent and deploy it to Amazon Bedrock AgentCore Runtime. After researching, complete the following tasks:

Develop a cybersecurity strands agent focused on IAM policy generation by using Python , the user can submit a code by API to this IAM strands agent, then analyze this code to  generate a least-privilege IAM policy. Create a `iam_agent.py` file to implement this IAM strands agent. Keep the code simple - no need for extensive testing or error handling.

After creating the IAM strands agent, continue using this IAM strands agent to deploy it on Amazon Bedrock's AgentCore Runtime, naming it `security_agent_iam`.

Deployment steps to AgentCore: `agentcore configure` which will automatically create the required IAM Role and ECR, then after configure, proceed with `agentcore launch` to launch it on AgentCore Runtime, and finally `agentcore invoke` (please refer to aws-document MCP for details).

After creating this IAM agent and successfully deploy it on AgentCore Runtime, create an API Doc `security_agent_iam.md` to store information needed for future frontend development, including AgentCore ARN / IAM Role / ECR Repository URI, etc.

Rules must follow:
a) Use Python for development and deploy in us-east-1
b) Always keep the code and process simple. No extensive testing needed, but ensure weather-agent.py can execute correctly and can correctly invoke the strands agent on agentcore runtime
c) If additional files are created for testing during the process, delete unnecessary files after task completion
d) When there's something you're not sure about, you need to use MCP tools to research strands agent or AgentCore development methods again.
e) Strictly follow the specs
f) Development needs to based on the official documentations and examples
g) Before executing each task, always confirm using the `workshop-profile` as the AWS configure profile
h) Must execute and complete this project in the `uv` Python virtual environment `.venv`
i) Use following model:

"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-sonnet-4-20250514-v1:0","modelId": "anthropic.claude-sonnet-4-20250514-v1:0";
"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-sonnet-4-5-20250929-v1:0","modelId": "anthropic.claude-sonnet-4-5-20250929-v1:0";
"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0","modelId": "anthropic.claude-3-5-sonnet-20240620-v1:0";
"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-sonnet-20241022-v2:0","modelId": "anthropic.claude-3-5-sonnet-20241022-v2:0";
"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-7-sonnet-20250219-v1:0","modelId": "anthropic.claude-3-7-sonnet-20250219-v1:0";
"modelArn": "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-haiku-20241022-v1:0", "modelId": "anthropic.claude-3-5-haiku-20241022-v1:0";
```