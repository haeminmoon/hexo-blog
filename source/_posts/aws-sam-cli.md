---
title: AWS-SAM-CLI installation
date: 2019-02-06
categories: [ aws ]
tags: [ aws, sam, serverless ]
---

AWS Lambda의 Serverless framework인 SAM-CLI 설치 방법에 대해 정리한 글 입니다. (OSX)

<!-- more -->

## Pre-installation

1. aws-cli 설치 - [aws-cli 설치 링크](/2019/02/06/aws-cli/)
2. Docker 설치 - [Docker for Mac 설치 링크](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
3. Homebrew 설치 - [Homebrew 설치 링크](https://brew.sh/)

## Installation

Homebrew를 사용하여 sam-cli를 설치하는 방법에 대해 알아보고자 한다.

1. Upgrade homebrew latest version 
```bash
brew upgrade
brew update
```
2. brew tap 추가
```bash
brew tap aws/tap
```
3. aws-sam-cli를 설치
```bash
brew install aws-sam-cli
```
4. 설치 유무 확인
```bash
# 설치가 정상적으로 완료되었다면 해당 경로에 sam dir이 존재
/usr/local/bin/sam
# 설치 확인 Command
sam --version
```

이상으로 AWS Lambda의 SAM(Serverless Application Model)의 기본 sam-cli 설치 방법에 대해 알아 보았다.