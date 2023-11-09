

- 기존에 생성해 둔 스냅샷을 이용해 새로운 데이터베이스로 복원할 수 있다.
- [[S3]]에서 MySQL RDS 데이터베이스 복원
	- 온프레미스 데이터베이스에서 백업을 생성
	- S3에 저장(object storage)
	- MySQL을 구동하는 새 RDS 인스턴스에 백업 파일을 복원

- S3에서 MySQL Aurora 데이터베이스 복원
	- Percona XtraBackup이라는 외부 툴을 사용하여 온프레미스 데이터베이스 백업을 생성
	- S3에 저장(object storage)
	- MySQL을 구동하는 새 Aurora 인스턴스에 백업 파일을 복원
