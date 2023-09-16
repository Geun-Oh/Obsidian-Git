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


## EFS 성능
- EFS Scale
	- 동시에 NFS 클라이언트 수천 개와 10GB 이상의 처리량 확보 가능
	- PB 규모의 NFS로 자동 확장 가능
- Performance mode (set at EFS creation time)
	- 범용 (default) - 지연시간에 민감한 경우 사용, 웹 서버나 CMS
	- Max I/O - 지연 시간은 있지만 처리량 최대화, 빅데이터나 미디어 작업 시
- Throughput mode (처리량 모드)
	- Bursting - 특정 시간에 처리량 증대 가능(버스트 모드)
	- Provisioned - 스토리지 크기와 무관하게 처리량 설정 가능 (1TB 스토리지에 1GiB 처리량도 가능)
	- Elastic - 처리량을 유연하게 가져가고 싶을 때, 예측이 어려울 때 사용


## EFS 스토리지 클래스

- Standard 
	- 기본적으로 자주 액세스하는 경우 사용하는 스토리지 클래스
- Infrequent access (EFS-IA)
	- 자주 사용하지 않는 파일들에 대한 적재
	- 파일 I/O 에 비용이 발생함
	- EFS-IA 사용 시 수명 주기 정책을 사용해야 한다.

>[!example] 
>수명 주기 정책 60일 설정 시, 만일 60일동안 액세스되지 않은 파일이 존재하는 경우 standard => IA로 자동으로 이동

- 가용성과 내구성
	- 다중 AZ 설정 가능
	- 개발용 One zone EFS 설정 가능 - 비용 90% 절감


> [!note] 
> 시험에는 언제 EFS를 사용해야하는지, 네트워크 파일 시스템에 어떤 옵션을 설정해야하는지에 대해 나온다.