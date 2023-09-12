
>Identity and Access Management

- IAM에서는 사용자를 생성하고 그룹에 배치한다.
	- <font color="#de7802">따라서 글로벌 서비스!</font>
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

- AWS는 <font color="#de7802">최소 권한의 원칙</font>을 적용한다.
	- 권한을 모두 주지 않고 최소한만 준다.


## IAM Policies

- 정책을 그룹에 적용하면 그룹에 속한 모든 사용자에게 해당 정책이 적용된다.
	- 사용자가 여러 그룹에 속하면 여러 정책이 적용된다.
- 그룹 단위가 아니라 사용자에게 정책을 추가하는 것도 가능하다.
	- 이때 <font color="#de7802">인라인 정책</font>을 사용한다.

```json
{
  "Version": "2012-10-17",
  "Id": "Policy1547641195782",
  "Statement": [
    {
      "Sid": "Stmt1547641192882",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": ["arn:aws:s3:::redwood-170306/*"]
    }
  ]
}
```

- Version: 정책 언어 버전. 항상 "2012-10-17"
- ID: 정책을 식별하는 식별자 (선택사항)
- Statement: 정책은 여러 개의 Statement를 가지며 필수다.
	- Sid: Statement식별자 (선택사항)
	- Effect: Allow or Deny
	- Principal: 해당 정책을 어떤 계정/유저/역할에 적용할지 목록
	- Action: Allow / Deny 되는 액션 목록
	- Resource: Action이 적용되는 리소스 목록
	- Condition: 해당 정책을 언제 적용할지 (선택사항)


## IAM: Roles for Services

- AWS 서비스가 특정 권한을 필요로하는 경우가 있다.
	- IAM Role을 사용해서 서비스에게 특정 권한을 줄 수 있다.
	- AWS에게 잠깐 동안 Credentials를 받고 특정 작업을 수행할 수 있다.
- IAM Role은 User와 비슷하지만 실제 사람이 아니라 AWS 서비스를 위한 것
	- ex) EC2 가 S3에 접근하고 싶다면 IAM Role 부여
- Common
	- EC2 Instance Roles
	- Lambda Function Roles
	- Roles for CloudFormation

## IAM Security Tools

- IAM Credentials Report (account-level)
    - IAM 자격 증명 보고서
    - 계정에 있는 사용자와 다양한 Credentials의 상태를 확인할 수 있다
- IAM Access Advisor (user-level)
    - 사용자에게 부여된 서비스 권한과 해당 서비스에 마지막으로 액세스한 시간을 볼 수 있다
    - 이를 활용해 어떤 권한이 사용되는지 볼 수 있다
        - 이에 따라 사용자의 권한을 줄여 최소 권한의 원칙을 지킬 수 있다

## IAM: Password Policy

- 강력한 패스워드를 쓰면 더 안전하다
- AWS에서는 패스워드 정책을 설정할 수 있다
    - AWS IAM → Access management → Account settings에서 설정 가능
    - 최소 길이
    - 특정 유형의 글자 포함
    - 패스워드 변경을 허용하거나 금지하거나
    - 일정 기간이 지나면 비밀번호 만료시켜 새로운 비밀번호 설정하게 요구
    - 패스워드 재사용 방지
      
## Multi Factor Authentication - MFA

- 사용자는 리소스를 생성하거나, 삭제할 수 있는 권한이 있다
- 루트 계정과 IAM 사용자를 보호해야 한다
- MFA = 비밀번호 + 각자의 보안 장치
- MFA의 장점
    - 패스워드가 유출되어도 계정은 탈취당하지 않는다
- IAM → Security credentials

### MFA devices options in AWS

- Virtual MFA device
    - Google Authenticator(phone only)
    - Authy (multi-device)
    - 한 기기에서 여러 개의 계정 등록 가능
- Universal 2nd Factor (U2F) Security Key
    - 실제 물리 장치
    - 한 기기에서 여러 개의 계정 등록 가능
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)

## IAM Guidelines & Best Practices

- 계정을 설정할 때 제외하고는 루트 계정을 사용하지 말아라
- 한 명의 실제 사람 = 한 개의 AWS 사용자
    - 계정 공유하지 말아라
- 사용자를 그룹에 포함시켜 권한 관리를 할 수 있다
- 강력한 패스워드 정책을 사용해라
- MFA 사용을 강제해라
- AWS 서비스에게 권한을 주기 위해 IAM Roles을 사용할 수 있다
- 프로그램에서 접근하기 위해서는 액세스 키가 필요하다
- IAM Credentials Report와 IAM Access Advisor을 통해 권한을 감시할 수 있다
- IAM 사용자와 액세스 키를 공유하지 말아라

## IAM Summary

- Users : 실제 물리적 사용자와 대응되는 사용자. 콘솔 비밀번호를 가짐
- Groups : 사용자를 그룹으로 묶을 수 있다. 오직 사용자만 포함
- Policies : 사용자, 또는 그룹에 대한 권한을 설명하는 JSON 문서
- Roles : AWS 서비스를 위한 사용자
- Security : MFA + 패스워드 정책
- AWS CLI : command-line에서 AWS 서비스 관리
- AWS SDK : 프로그래밍 언어에서 AWS 서비스 관리
- Access Keys : CLI나 SDK에서 AWS 서비스 접근에 필요한 키
- Audit : IAM Credential Reports & IAM Access Advisor