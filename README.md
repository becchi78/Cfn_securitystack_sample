# Cfn_sample_securitystack

Cfn のネステッドスタックとクロススタック参照のサンプル（security）

## 準備

templates/にある security-group.yaml と iam-role.yaml、iam-policy はあらかじめ S3 の cfn-nested-sample に置いておく。

```bash
aws s3 cp ./templates/security-group.yaml s3://cfn-nested-sample/security/
aws s3 cp ./templates/iam-role.yaml s3://cfn-nested-sample/security/
aws s3 cp ./templates/iam-policy.yaml s3://cfn-nested-sample/security/
aws s3 cp ./templates/ec2keypair.yaml s3://cfn-nested-sample/security/
```

## デプロイ

```bash
aws cloudformation create-stack \
  --stack-name SecurityStack \
  --template-body file://root-template.yaml \
  --parameters file://param/parameters.json \
  --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND
```

## 削除

```bash
aws cloudformation delete-stack --stack-name SecurityStack
```

## Output

| キー                | 説明                          | エクスポート名                    |
| ------------------- | ----------------------------- | --------------------------------- |
| Ec2KeyPairName      | The Ec2 Key Pair Name         | SecurityStack-Ec2KeyPairName      |
| IAMPolicyArn        | The ARN of the managed policy | SecurityStack-IAMPolicyArn        |
| IAMRoleArn          | The ARN of the IAM role       | SecurityStack-IAMRoleArn          |
| IAMRoleName         | The Name of the IAM role      | SecurityStack-RoleName            |
| InstanceProfileName | The Name of the InstanceProfile name      | SecurityStack-InstanceProfileName |
| SecurityGroupId     | The ID of the security group  | SecurityStack-SecurityGroupId     |
