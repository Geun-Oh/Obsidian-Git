
> [!info] Elastic Network Interfaces

>[!info] 
>ENI는 인스턴스가 AWS 서비스, 다른 인스턴스, 온프레미스 서버, 인터넷 등 다른 네트워크 리소스와 통신할 수 있도록 하며, Secure Shell(SSH) 또는 Remote Desktop Protocol(RDP) 등을 이용해 인스턴스에서 실행중인 OS와도 통신할 수 있도록 한다.

>[!memo]
>[[EC2]]를 연결하는 IP를 직접 만들어서 입혀주는 느낌인데, EC2를 중지-시작했을 때 IP가 바뀌는 이슈나, 특정 인스턴스에 장애가 발생해 이를 동일한 역할을 하는 다른 인스턴스로 서비스를 잠시 옮겨두어야하는 경우, 직접 만들어둔 ENI를 사용하 IP주소를 변경하지 않고 가리키는 [[EC2]]만 제어해줌으로써 에러 발생 상황에서도 사용자들에게 서비스를 제공할 수 있다.



- 탄력적 네트워크 인터페이스
- [[VPC]]의 논리적 구성 요소, [[EC2]]가 네트워크에 액세스 할 수 있도록 해준다.
- [[Availability Zone]]에 바인딩되어, 하나의 ENI는 해당 ENI가 있는 특정 AZ 내부의 요소들에만 연결 가능하다.

>[!example] 
>AZ내부에 하나의 인스턴스가 있다고 가정
>해당 EC2는 Eth0(예시)이라는 ENI를 통해 연결

## Primary Private IP Address & Secondary Private IP Address

- 각 인스턴스는 서브넷으로 지정한 범위 내의 기본 프라이빗 IP 주소를 지니며, 이는 인스턴스의 기본 ENI와 연결된다. 이 주소는 변경 혹은 삭제가 불가하지만, 기본 ENI에 보조 프라이빗 주소를 할당해 사용 가능하다. 이 또한 하나의 서브넷 범위 내에 존재해야 한다.


## ENI 부착하기

- ENI는 인스턴스와 독립적으로 존재할 수 있고, ENI를 생성한 뒤 인스턴스에 부착 가능하다.