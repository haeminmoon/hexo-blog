---
title: AWS-CLI installation
date: 2019-02-06
categories: [ aws ]
tags: [ aws, aws-cli, mac ]
---

MAC의 OSX 환경에서 aws-cli 설치 방법과 초기 Credential 설정 방법에 대해 정리한 글 입니다.

<!-- more -->

## Pre-installation

Python이 기본적으로 설치되어 있어야 합니다. (Mac에는 기본적으로 Python이 설치 되어 있다.)
```bash
python --version
```
> python 버전 확인 및 설치 유무 확인

## Installation

기본적으로 aws-cli를 설치하는 방법은 다양한 방법들이 존재하나, 해당 포스트에서는 Bundle을 이용한 설치를 진행해보고자 한다.

1. **Step1** : aws-cli bundle 설치
```bash
curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
```
2. **Step2** : aws-cli bundle 압축 해제
```bash
unzip awscli-bundle.zip
```
3. **Step3** : 관리자 권한으로 aws-cli 설치 프로그램 실행
```bash
sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
```

## Configuration
다음 명령어를 실행 후, IAM에서 발급 받은 정보룰 입력하면 된다.
```bash
aws configure
# AWS Access Key ID [None]: Input your access key id
# AWS Secret Access Key [None]: Input your secret access key
# Default region name [None]: ap-northeast-2
# Default output format [None]: json
```
> [AWS IAM 설정 참조 링크](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/getting-started_create-admin-group.html)

모든 설정이 끝난난 후, '.aws' 경로에 'configure, credential'이 생성된 것을 확인 할 수 있다.
> 설정 변경시, 설정 Command를 실행하는 방법과 직접 파일을 편집하는 방법 모두 가능하다.
