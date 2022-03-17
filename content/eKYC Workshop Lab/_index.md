---
title: "AWS eKYC Workshop"
chapter: false
weight: 10
tags:
  - eKYC Workshop
---

![](/images/eKYC/Architecture.png)

eKYC Workshop 将完全基于 Serverless，完成 ID Verification 和 Identity Verification 两项工作，主要包括以下几部分：

 **1. ID Verification 和 Identity Verification 过程均通过 Step Function 实现工作流编排**

 **2. 用户上传 ID document (照片或复印件) 到 S3，通过 SQS 触发 Lambda，然后执行 ID Verification Step Functions 工作流**
    
   2.1. 利用 Rekognition DetectFace API 检测证件照中是否包含人脸
   2.2. 利用 Textract AnalyzeID API 提取证件信息，并将 OCR 结果存储到 DynamoDB

 **3. 用户上传自拍照到 S3，通过 SQS 触发 Lambda，然后执行 Identity Verification Step Functions 工作流**
    
   3.1. 利用 Rekognition DetectFace API 检测自拍照中是否包含人脸

   3.2. 利用 Rekognition DetectFace API 检测自拍照中是否包含多张人脸

   3.3. 利用 Rekogntion SearchFace API 检测当前自拍照的人脸是否与Rekognition中的现存人脸冲突，避免用户重复注册或照片伪造
    
   3.4. 如果人脸没有冲突，则利用 Rekognition IndexFace API，将当前用户的人脸存储到 Rekognition 中，用于后续用户注册时的人脸搜索

   3.5. 利用 Rekognition CompareFace API 检测自拍照和证件照中的人脸是否一致

**4. 上述所有工作流的状态信息，比如ID 和 Identity Verification 的检测状态(Pass/Fail)，以及失败原因,均保存在 DynamoDB 中**

DynamoDB table 字段如下： 
![](/images/eKYC/DDB.png)

{{% notice info %}}
实验环境默认位于 ap-northeast-1 东京区域，也可以选择其他区域，完成全部实验，大约需要 2 小时。
{{% /notice  %}}


