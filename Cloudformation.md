
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

스택 세트 혹은 변경 세트 작동 중에 특정한 참조값을 SSM Parameter Store 혹은 Secrets Manager에서 가져올 수 있다.

## 사용 예시

DB 인스턴스 접근 패스워드를 Secrets Manager에서 가져오는 경우



- SSM, SSM-Secure, Secrets manager 등에서 다 가져올 수 있다.
- 최대 60개까지 설정할 수 있다. 
- Amazon Linux 2 AMI와 같이 퍼블릭 SSM parameter는 가져오지 못한다.


# 스택 세트

동일한 하나의 작업 / 템플릿을 다중 계정 및 리전에 배포할 수 있도록 한다.

관리자가 스택 세트를 생성하고, 타깃 계정들은 스택 인스턴스에 대한 CRUD를 수행한다.

여러 계정과 리전에 걸쳐 통일된 스택을 배포할 수 있다. 하나의 OU에서 스택 설정을 다룰 때 용이하다.

## 스택 세트 작동 방식

### Create StackSet

템플릿을 제공하고 + 타깃 계정에 해당 템플릿을 배포한다.

### Update StackSet

스택 세트 업데이트는 모든 스택에 영향을 준다.(선택적으로 특정 스택만 업데이트할 수 있다)

### Delete Stack

타겟 계정 / 리전에 대해 특정 리소스를 지울 수 있다.
스택 세트에서 특정 스택을 지운다 => 해당 스택은 스택 세트와 독립적으로 구성
모든 스택을 삭제 => 스택 세트 삭제에 대한 준비 과정

### Delete StackSet

스택 세트 내부의 모든 스택 인스턴스를 삭제


## 스택 세트 배포 옵션

1. 배포 순서 지정
	1. 스택이 배포되는 리전의 순서를 지정할 수 있다.
	2. 한 번의 리전 당 몇 번의 작업이 수행되는지 지정 가능.
2. 동시 업데이트하는 계정 수 지정
	1. 동시 업데이트하는 계정의 수 or 비율을 지정해서 한 번에 업데이트되는 정도를 조정할 수 있다.
3. 실패 허용
	1. 특정 리전/계정에 대한 스택 세트 적용이 실패하는 경우, 어느 정도까지 허용할지를 숫자로 지정해준다.
4. 리전 동시성
	1. 여러 리전에 병렬로 배포할 것인지 명시.
5. 스택 유지
	1. 스택 세트를 삭제할 때 삭제되지 않고 남기고자 하는 스택 리소스를 지정 가능.