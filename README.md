# awsDeployDemo

## 1. GitHub Secrets 설정
> 먼저 GitHub Secrets에 다음 값들을 설정해야 합니다:
> - `AWS_ACCESS_KEY_ID`
> - `AWS_SECRET_ACCESS_KEY`
> - `AWS_REGION`
> - `AWS_ACCOUNT_ID`


## 2. AWS IAM에서 필요한 권한 설정:

- ECR 관련 권한
- App Runner 관련 권한

다음과 같은 IAM 정책이 필요합니다:

```json
{
"Version": "2012-10-17",
"Statement": [
{
"Effect": "Allow",
"Action": [
"ecr:BatchCheckLayerAvailability",
"ecr:CompleteLayerUpload",
"ecr:GetAuthorizationToken",
"ecr:InitiateLayerUpload",
"ecr:PutImage",
"ecr:UploadLayerPart",
"apprunner:CreateService",
"apprunner:UpdateService",
"apprunner:DescribeService",
"apprunner:ListServices"
],
"Resource": "*"
}
]
}
```

## 3. App Runner 서비스 역할 생성 및 ARN을 GitHub Secrets에 추가:
방금 추가한 `APPRUNNER_SERVICE_ROLE_ARN` 시크릿 추가


# 4. 결과 확인

이제 master 브랜치에 푸시하면:

1. GitHub Actions가 트리거됨
2. Docker 이미지 빌드
3. ECR에 이미지 푸시
4. App Runner 서비스 자동 업데이트