---
title: Serverless framework
date: 2019-02-04
categories: [ serverless ]
tags: [ serverless, aws, lambda ]
---

## Installation
**Install serverless globally**
```bash
npm install serverless -g
```

**Signin to your Serverless account**
```bash
serverless login
```

**Create a serverless function**
```bash
serverless create --template hello-world
```

**Deploy to cloud provider**
```bash
serverless deploy
```

**Serverless config credential**
```bash
serverless config credentials --provider aws --key 액세스키ID --secret 비밀액세스키
```
> [AWS IAM 설정 참조 링크](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/getting-started_create-admin-group.html)


Create serverless-project for nodejs
sls create -t aws-nodejs -p hello-serverless

Local function test
serverless invoke local --function hello