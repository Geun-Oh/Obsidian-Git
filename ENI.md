
> [!info] Elastic Network Interfaces

>[!info] 
>ENI는 인스턴스가 AWS 서비스, 다른 인스턴스, 온프레미스 서버, 인터넷 등 다른 네트워크 리소스와 통신할 수 있도록 하며, Secure Shell(SSH) 또는 Remote Desktop Protocol(RDP) 등을 이용해 인스턴스에서 실행중인 OS와도 통신할 수 있도록 한다.


- 탄력적 네트워크 인터페이스
- [[VPC]]의 논리적 구성 요소, [[EC2]]가 네트워크에 액세스 할 수 있도록 해준다.

>[!example] 
>AZ내부에 하나의 인스턴스가 있다고 가정
>해당 EC2는 Eth0(예시)이라는 ENI를 통해 연결

## Primary Private IP Address & Secondary Private IP Address

- 각 인스턴스는 서브넷으로 지정한 범위 내의 기본 프라이빗 IP 주소를 지니며, 이는 인스턴스의 기본 ENI와 연결된다. 이 주소는 변경 혹은 삭제가 불가하지만, 기본 ENI