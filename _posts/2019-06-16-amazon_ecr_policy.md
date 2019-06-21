---
layout:     post
title:      "Amazon ECR 접근 권한 부여"
subtitle:   "connecting Amazon ECR from external"
date:       2019-06-15
author:     "CiEL"
tags:
    - amazon
    - ecr
---

## 사용 예시

A Org 에서 B Org 에 있는 ECR 을 접근하여 pull, push 하고 싶을때  
B Org 에 아래 정책을 참고하여 적용한다.

```
ECR Repository policy
---------------------------------
{
 "Version": "2008-10-17",
 "Statement": [
   {
     "Sid": "new statement",
     "Effect": "Allow",
     "Principal": {
       "AWS": "arn:aws:iam::<accountdev_id>:root"
     },
     "Action": [
       "ecr:BatchCheckLayerAvailability",
       "ecr:BatchGetImage",
       "ecr:CompleteLayerUpload",
       "ecr:DescribeImages",
       "ecr:DescribeRepositories",
       "ecr:GetDownloadUrlForLayer",
       "ecr:GetLifecyclePolicy",
       "ecr:GetLifecyclePolicyPreview",
       "ecr:GetRepositoryPolicy",
       "ecr:InitiateLayerUpload",
       "ecr:ListImages",
       "ecr:PutImage",
       "ecr:PutLifecyclePolicy",
       "ecr:SetRepositoryPolicy",
       "ecr:StartLifecyclePolicyPreview",
       "ecr:UploadLayerPart"
     ]
   }
 ]
}
```