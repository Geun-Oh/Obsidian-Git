
>Identity and Access Management

- IAM에서는 사용자를 생성하고 그룹에 배치한다.
	- **따라서 글로벌 서비스!**
	- 계정을 만들 때 생성되는 루트 계정도 여기에 포함된다.
		- 단, 그 이후로 사용하거나 공유해서는 안된다. => 보안 문제
		- 그 대신 다른 사용자를 생성해야 한다.

## IAM Users

- 조직 내 사람을 나타내는데, 그룹으로  묶일 수 있다.
- 한 사용자가 여러 그룹에 속할 수 있다.

## IAM Groups

- 그룹은 오직 사용자만 가질 수 있다.
- 그룹이 그룹을 포함할 수 없다.

## IAM: Permissions

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "FirstStatement",
      "Effect": "Allow",
      "Action": ["iam:ChangePassword"],
      "Resource": "*"
    },
    {
      "Sid": "SecondStatement",
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    },
    {
      "Sid": "ThirdStatement",
      "Effect": "Allow",
      "Action": [
        "s3:List*",
        "s3:Get*"
      ],
      "Resource": [
        "arn:aws:s3:::confidential-data",
        "arn:aws:s3:::confidential-data/*"
      ],
      "Condition": {"Bool": {"aws:MultiFactorAuthPresent": "true"}}
    }
  ]
}
```

- 사용자나 그룹은 JSON 문서를 수정할 수 있다.
	- 이를 정책(Policies) 이라고 한다.
- 정책은 특정 사용자, 혹은 특정 그룹이 어떤 작업에 어떤 권한을 가지고 있는지 명시해둔 것이다.

- AWS는 최소 권한의 원칙을 적용한다.
	- 권한을 모두 주지 않고 최소한만 준다.
	- 