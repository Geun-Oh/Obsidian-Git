> [!info] Elastic File System

- [[EC2]] 관리형 스토리지
- 기존에 온프레미스 서비스에서 사용하는 NFS, NAS 등의 Storage Data를 클라우드로 옮겨 온 형태
- **간단하고 확장성이 좋으며 안정적인 클라우드 파일스토리지**
- PB 사이즈까지 지원

> [!note]
> 온프레미스 스토리지를 AWS로 이전하고 싶다? EFS를 생각해보기!

>[!tip] [AWS EFS 개념 및 구성 방법](https://practice.hooniworld.io/entry/AWS-EFS-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EA%B5%AC%EC%84%B1-%EB%B0%A9%EB%B2%95)



## Architecture 사용 예

![[Pasted image 20230915001703.png]]

- EFS 생성 시 VPC 안의 AZ Subnet에 Mount Targer 생성
- AZ의 Subnet 하나만 Mount Target이 생성
- AZ의 Subnet이 두 개일 경우 한 개만 Mount Target 생성 가능


## EFS 이점

- 간편성
	- 빠르고 쉽게 구성 가능
	- 복잡한 파일시스템을 배포 및 fetch 할 필요가 없음
	- 리눅스 인스턴스에서만 사용 가능(Window 안됨...)

- 자동확장
	- 파일이 추가 또는 제거됨에 따라 자동으로 확장 및 축소
	- 필요한 만큼 자동으로 스토리지 공간 확보


- 공유 파일 스토리지
	- 수천대 EC2 동시 Access 가능
	- On-premise 서버 Access 가능

- 원할한 통합
	- NFSv4 프로토콜을 통해 EFS 파일 시스템 탑재
	- Direct Connect & VPN를 통해 On-Premise 서버와 탑재

- 높은 가용성 및 내구성을 제공 하도록 설계

- 보안
	- POSIX 권한을 통해 파일시스템에 대한 엑세스 제어
	- IAM을 통해 엑세스 제어