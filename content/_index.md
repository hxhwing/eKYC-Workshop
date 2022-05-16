---
title: "AWS eKYC Workshop"
chapter: false
weight: 1
---

# AWS eKYC Workshop

## What is eKYC

eKYC (Know Your Customer) 是一个用于验证客户身份的电子流程，作为风控环节一个基础部分，已经是国际社会中所有金融活动中必不可少的环节，主要用于预防反洗钱、身份盗窃、金融诈骗等犯罪行为。

通用的 eKYC 流程主要包含两个部分：
 1. **证件验证 (ID Verification)**: 验证用户的身份证件是否真实有效，是否存在证件伪造

   要求用户上传政府机构颁发的证件照，例如身份证，护照，驾照等，验证证件的真实性和有效性，并从证件中提取用户信息，包括证件照片，证件ID等，具体分为以下几个部分：
   
   - 证件照真伪验证
   - 证件信息提取
   - 证件验证
 
{{% notice info %}}
对于证件验真，AWS不提供此类服务，可选择第三方服务商。
{{% /notice  %}}

 2. **人脸验证 (Identity Verification)**： 确保进行注册和交易行为的用户与上传的证件信息一致，主要基于人脸识别，活体检测等验证用户身份

   通常对用户人脸进行活体检测 (Liveness Detection)，或要求上传自拍照进行人脸识别，并与证件照进行比对，确保人证一致，具体分为以下几个部分：

   - 活体检测
   - 人脸识别
   - 人脸搜索
   - 人脸比对

 3. **其他验证**： 额外的身份验证手段，比如要求用户上传的水电等生活账单，信用卡账单等，验证用户身份真实存在，且居住和生活在某个国家和地区

## eKYC Workshop

本 eKYC Workshop 主要是借助 AWS AI Services，在客户对其最终用户进行 eKYC 的流程中提供支持。

![](/images/eKYC/AtAGlance.png)

主要包括：
 1. 利用 Rekognition 服务对人脸进行活体检测 
{{% notice info %}}
目前 Rekognition 活体检测功能在 Private Preview 阶段，预计在2022.3Q 正式发布，本次 Workshop 目前暂不支持。待正式发布后，将加入活体检测部分
{{% /notice  %}}
 2. 利用 Rekognition 服务对 ID 证件照和自拍照中的人脸进行识别，处理，审核，比对等工作
 3. 利用 Textract 服务对 ID 证件进行 OCR 内容提取
 4. 利用 AWS Step Functions 工作流， SQS 消息队列， Lambda 等无服务器产品，编排和构建 eKYC 的工作流程。

