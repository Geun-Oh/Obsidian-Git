
> [!info] AWS 계정 전반에 관한 감사를 진행하는 CCTV

- AWS 게정의 거버넌스, 감사 및 규정 준수를 돕는다
- 기본적으로 활성화
- 콘솔, SDK, CLI, 기타 AWS 서비스에서 발생한 AWS 계정 내의 모든 이벤트 및 API 호출기록 확인 가능 => 계정 관련 모든 로그 기록
- CloudTrail의 로그를 CloudWatch Logs나 S3로 옮길 수 있다.
- 전체 또는 단일 리전에 적용되는 트레일을 설정해 모든 리전에 걸친 이벤트 기록을 한 곳으로 모을 수 있다. => S3 버킷에 저장 가능
- 누군가가 AWS 에서 무언가 삭제했을 대 확인 가능
	- API호출이 남아 있다.


## CloudTrail Diagram

- 모든 이벤트를 90일 이상 보존하려면 S3 나 CloudWatch Logs로 보내면 된다.