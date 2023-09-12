
- [[EC2 Instance Store]]는 임시 스토리지로 사용된다.
- [[EC2 Instance Store]] 볼륨에 저장된 데이터는 인스턴스 중지, 종료 또는 하드웨어 장애 시 삭제된다.
- [[EBS]]는 위의 경우에도 데이터를 보존하고, [[EBS]] 스냅샷을 활용해 볼륨 백업이 가능하다.
- 의도치 않은 변경 혹은 손실 방지를 위해 스냅샷 생성 주기를 짧게 가져가자.

>[!tip] [인스턴스 스토어와 EBS의 차이점은 무엇인가요?](https://repost.aws/ko/knowledge-center/instance-store-vs-ebs)

