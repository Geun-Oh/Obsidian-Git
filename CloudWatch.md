
>[!info] AWS 리소스에 대한 지표 모니터링 시스템


## CloudWatch Metrics

- CloudWatch는 모든 AWS 서비스에 대한 지표(Metric)를 제공
	- CPU 사용률, networking, bucket size...

- 지표는 네임스페이스에 속하기 때문에 각기 다른 네임스페이스에 저장
	- 서비스 당 네임스페이스는 하나!

- 지표의 속성으로 측정 기준이 있다.
	- instance id, environment,,,

- 지표 당 최대 측정 기준은 10개
- 지표가 많아지면 CloudWatch 대시보드에 추가해 모든 지표를 한 번에 볼 수 있다.
- 사용자 지정 지표도 가능
	- 메모리 사용량 추출 등등..

## CloudWatch Metric System


- CloudWatch 외부로 스트리밍 가능
- 근 실시간 전송(near RT) + 매우 낮은 레이턴시
- firehose, 원하는 곳(서드파티도 가능!)
- 지표 또한 네임스페이스 등으로 필터링 가능
	- 필터링 지표의 서브셋만 firehose로 전송 가능
- ![[스크린샷 2023-10-02 오후 11.18.24.png]]


## CloudWatch Logs

- 로그 그룹: 로그들을 로그 그룹으로 그룹화 => 로그 그룹의 이름으로는 애플리케이션을 나타냄
- 로그 스트림: 로그 그룹에는 로그 스트림이 있고, 애플리케이션 내 인스턴스나 다양한 로그 파일명 또는 컨테이너를 나타낸다.
- 로그 만료 기한도 정할 수 있다.
- S3, Kinesis Data Streams, Firehose, AWS Lambda, Elastic Search 등으로 보낼 수 있다.

