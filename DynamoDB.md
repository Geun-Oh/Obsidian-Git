
> [!summary] DynamoDB Summary
> 
> - AWS 자체 기술, 관리형 서버러스 NoSQL 데이터베이스, 밀리세컨드 응답 시간
> - On-demand 용량 모드: 용량 프로비저닝을 하지 않아도 자동 확장이 된다. 워크로드 예측이 어려운 경우 사용하면 좋다.
> - Key-Value 저장을 위해 ElastiCache를 사용 가능
> - TTL 기능이 있어 웹사이트 세션 데이터 저장에 좋다.
> - 가용성이 높다. 기본으로 다수의 AZ에 걸쳐 있다.
> - 읽기와 쓰기 분리가 잘 되어 있고, DynamoDB 테이블 외에도 트랜잭션이 가능하다.
> - DAX - 마이크로 초 단위의 읽기 레이턴시를 얻을 수 있다.
>  - 보안, 인증, 승인 등 모든 것이 IAM을 통해 이루어지고, DynamoDB 이외에 이벤트 처리 능력도 가질 수 있다.
>  - 이벤트 제어: DynamoDB Streams를 활성화해서 데이터베이스에서 일어나는 모든 변경사항을 스트리밍할 수 있고, DynamoDB Streams에서 람다를 호출할 수 있도록 통합이 가능.
>  - 이외에도 DynamoDB Streams 외에 Kinesis Data Stream을 통해 Kinesis Data Firehose기능을 활용하는 등의 통합도 가능하다.
>  - 글로벌테이블 기능: active-active 설정
>  - PITR 기능 활성화 시 35일 내 자동 백업 가능, 혹은 백업 장기간 보관 시 On-demand 백업 설정 가능
>  - 읽기 용량을 사용하지 않고 S3에 데이터를 백업하거나, 쓰기 용량을 사용하지 않고 S3에서 데이터를 불러올 수 있다.
>    
>    - use case: 서버리스 애플리케이션 개발(100s KB 내의 작은 문서), 분산 서버리스 캐시