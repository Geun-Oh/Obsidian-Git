
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


## CloudWatch Logs Metric Filter & Insights

- CloudWatch Logs에서 필터 표현식을 쓸 수 있다.
	- 로그 내 특정 IP를 찾을 수 있거나 로그 중 'ERROR' 메세지가 들어있는 로그를 찾을 수 있다.

- Metric Filter를 통해 출현 빈도를 계산해 지표를 만들 수 있다.
	- CloudWatch 알람 트리거로도 사용 가능

- CloudWatch Logs Insights => 로그를 쿼리하고 대시보드로 추가 가능
	- 빠른 검색과 효율적인 분석 가능


## S3 Export

- Export까지 최대 12시간
- Non-real time 이므로 로그를 스트림하고 싶다면 Log Subscriptions를 사용해야 한다.


## CloudWatch Logs Subscriptions

- CloudWatch 위에 적용해 로그를 목적지로 보내는 필터
- S3 내보내기보다 훨씬 빠르다.![[스크린샷 2023-10-02 오후 11.23.36.png]]


## CloudWatch Logs Aggregation Multi-Account & Multi Region


- 모든 로그를 한 곳에 모을 수 있다.![[스크린샷 2023-10-02 오후 11.24.32.png]]


## CloudWatch Logs for EC2

- EC2에서 CloudWatch로는 로그 옮기기가 불가함
- 에이전트라는 작은 프로그램을 실행해 원하는 로그 파일을 EC2 내부에서 푸시해야한다.
- EC2 인스턴스에 IAM Role을 추가해야한다.
- 온프레미스에서도 적용 가능!


## CloudWatch Logs Agent & Unified Agent

- 두 서비스 모두 온프레미스와 같이 가상 서버를 위함

### Logs Agent

- CloudWatch Log 로만 로그를 보낼 수 있다.

### Unified Agent

- 프로세스나 RAM 과 같이 컴퓨팅 자원과 관련된 지표도 수집 가능
- SSM Parameter Store를 통해 쉽게 구성 가능
	- 모든 통함 에이전트를 모아 중앙 집중식 환경 구성을 할 수 있다.


## Unified Agent - Metrics

인스턴스나 리눅스 서버를 만들면 지표 정보를 직접적으로 가져올 수 있다.

하드웨어 소프트웨어 지표 모두 수집 가능

- CPU → (active, guest, idle, system, user, steal)
- Disk metrics → (free, used, total), 디스크 I/O (writes, reads, bytes, iops)
- RAM → (free, inactive, used, total, cached)
- 넷 상태(Netstat) → (number of TCP and UDP connections, net packets, bytes)
- 프로세스 → (total, dead, bloqued, idle, running, sleep)
- 스와프 공간 → (Swap Space) (free, used, used %)


## CloudWatch Alarms

- 지표에서 알람 트리거
- 다양한 옵션을 추가해 복잡한 정의가 가능
- 알람 상태
	- OK => 트리거되지 않은 안정 상태
	- INSUFFICIENT_DATA => 상태를 결정할 데이터가 부족
	- ALARM => 임계를 넘는 상태
- Period => 경보가 지표를 살펴보는 기간
	- 짧게 설정하거나 길게 설정 가능
	- 고해상도 사용자 지정 지표에도 적용 가능 => 10초, 30초, 60의 배수,,,


## CloudWatch Alarm Targets

- EC2 인스턴스들의 동작 => 멈춤, 종료, 재부팅, 복구 등
- EC2 오토 스케일링 => 스케일 아웃, 인
- SNS => 람다를 통해 위반 시 알림 작업 수행



## 알아두면 좋은 정보

- CloudWatch Logs 지표 필터를 기반으로 알람 생성 가능
- CloudWatch Logs 는 경보에 연결된 필터를 가질 수 있다.
- 필터에 특정 단어가 지나치게 많이 생기면 알람을 방생시키도록 설정이 가능하다.
- set-alarm-state를 통해 경보알림테스트 가능
