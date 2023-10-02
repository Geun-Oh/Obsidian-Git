
## CloudWatch Container Insights

- 컨테이너로부터 지표와 로그를 수집, 집계, 요약하는 서비스
- ECS, EKS 컨테이너에서 사용 가능 or Fargate
- 지표를 수집해 세분화된 대시보드 생성 가능
- 컨테이너화된 버전의 CloudWatch를 실행할 에이전트를 사용해야 컨테이너를 찾을 수 있다.

## Lambda Insights

- Lambda 에서 실행하는 서버리스 애플리케이션을 위한 모니터링과 트러블슈팅 솔루션
- CPU, 메모리 디스크, 네트워크같은 시스템 지표를 수집, 집계 가능
- Lambda 계층으로 제공된다 => 람다 함수 옆에서 실행해 대시보드를 생성해 성능을 모니터링
	- 세부모니터링 필요 시 사용


## Contributor Insights

- CloudWatch Logs를 통해 컨트리뷰터 데이터를 표시하는 <font color="#f79646">시계열 데이터를 생성</font>하고 로그를 분석하는 서비스
- 상위 컨트리뷰터에 대한 지표 확인과 총 기고자 수 및 사용량에 대한 지표 확인