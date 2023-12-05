
# 스택 정책

Cloudformation 스택에서 특정 설정을 업데이트하는 등의 작업이 필요한 경우가 존재. 이 경우 수정 가능한 스택과 그렇지 않은 스택에 대한 정의가 있어야 하는데, 이를 위해 스택 정책을 설정한다.

스택 정책을 사용하여 수정이 가능한 정책과 그렇지 않은 정책을 명시해줄 수 있다.


## 중첩 스택

자주 사용되는 스택으를 따로 중첩 스택으로 설정하여 다른 cloudformation stackset에 적용할 수 있다.

VPC, IAM 등 여러 템플릿에 걸쳐 자주 사용되는 설정들을 따로 빼둔 뒤 import해오는 방식으로 사용한다.

# 서비스 역할

기본적으로 생성된 Cloudformation 템플릿은 해당 템플릿을 생성한 유저의 iam role을 따라간다. 

다만 여기서 해당 유저가 Cloudformation에게 실행 권한을 부여하려면, `iam:PassRole` 권한이 존재해야한다.

## 사용 사례

- 작업 수행에 필요한 최소한의 권한만 부여하고자 하는 경우


# SSM Parameter

Systems Manager Parameter Store: 다양한 설정 및 환경 변수등을 저장하는 곳
CF는 언제나 parameter store에서 최신 값을 가져온다.

## 사용 예시

최신 AMI ID 를 가져오는 경우

=> 리전 별 최신 AMI ID가 다르므로, 각 리전에서의 AMI ID를 따로 알 필요가 있다.
이는 parameter store에 기ㅣ본적으로 저장되어 있으므로, CF는 기본적으로 SSM Parameter store에서 EC2 AMI ID를 가져와서 사용하게 된다.


# 동적 참조

런타임에 직접적으로 SSM Parameter Store 혹은 Secrets Manager 내부의 값을 가져오는 것!
