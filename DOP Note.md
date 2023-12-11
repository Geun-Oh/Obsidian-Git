<aside>
💡 AWS Certification - DevOps Professional 시험을 준비하며 배운 내용들을 archive
</aside>

## CloudWatch

### CloudWatch Log Insights Query vs CloudWatch Logs Metric Filter

Metric filter는 시계열 형식으로 Metric data를 생성한다. 이를 통해 ITSM에 통합되는 경보를 생성하거나, Lambda 를 실행하거나, 이상 탐지 모델 등을 생성하는 등의 추가 작업이 용이하다.

반면 Insights Query에서 자동적으로 위와 같은 작업들을 호출하기는 어렵다.

### CloudWatch Subscription Filter

- CloudWatch Subscription Filter ⇒ 로그 이벤트를 다른 서비스로 전송할 때 사용된다.

## Lambda

### 예약된 동시성 VS 프로비저닝된 동시성

- 예약된 동시성: 특정 Lambda 함수의 동시 실행 가능 수를 지정해(최대 1000) 트래픽 증가에 대비할 수 있다. 물론 병렬처리가 아님에 주의하자
    
- 프로비저닝된 동시성: cold-start를 막아주는 기능이다!
    

## AWS Control Tower

- Control Tower Landing Zone에는 IAM 적용이 어렵다.

## SDLC

- CodeCommit Push Event ⇒ EventBridge ⇒ CodePipeline
- aws stop deployment ⇒ 롤백 안 된다!

## CloudFormation

- CF 스택 삭제를 할 때, S3의 경우 내부 객체가 잔존하면 버킷을 지울 수 없다. 따라서 CF 스택 삭제가 감지되면, Lambda-backed custom resource를 사용해 S3 내부 객체를 모두 삭제하는 과정이 선행되어야 한다. 이때 presigned-url을 통해 작업에 대한 결과 여부를 CF측애 알려주는 과정이 포함된다.
    
- CF는 교차리전 작업 수행이 가능하다.
    

[Add a cross-Region action in CodePipeline - AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/actions-create-cross-region.html#actions-create-cross-region-cfn)

## S3

- S3 이벤트 알림을 보낼 수 있는 곳은 Lambda, SQS, SNS 이다.
    
- S3 교차리전 복제(CRR)의 경우, 복제 원본 쪽 역할에서 직접 복제를 대상에 하는 방식. 대상은 버킷 정책을 허용해두기만 한다. 이 경우 암호화가 필요하다면 복호화용 키를 공유하는 것도 필요하다(주로 KMS).
    

## Organization Unit

- SCP 는 루트 계정 or OU에 적용하면 해당 그룹 전체에 공통 적용된다.
- 개별 리소스에서 허용한 정책이라도, OU 단위에서 막아버리면 막힌다.

## Other Configuration Stacks

- AWS-RunPatchBaseline: 해당 패치 기준선을 정의하고 기준선에 대한 규정 준수를 보장할 수 있다.