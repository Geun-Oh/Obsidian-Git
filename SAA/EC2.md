
> Elastic Compute Cloud

- Infrastructure as a Service
- 하나의 서비스가 아니고 많은 것을 포함하고 있다.
	- [[EC2]]: Virtual Machines
	- [[EBS]]: Storing data on Virtual Device
	- [[ELB]]: Distributing load across machines
	- [[ASG]]: Scaling the services using an auto-scaling group

- EC2를 재부팅했을 때 퍼블릭 IP는 변경될 수 있지만, 내부 IP는 변경되지 않는다.


## EC2 sizing & configuration options

- OS: Linux, windows, Mac OS
- CPU
- RAM
- Storage Space
	- Network-attached: EBS & [[EFS]]
	- Hardware: EC2 Instance Store => 블록 수준의 임시 스토리지
- Network card
	- speed, Public IP address
- Firewall rules: [[Security Group]]
- Bootstrap script: EC2 User Data
	- configure at first launch


## EC2 Hibernate

> [!meno] EC2 인스턴스의 절전모드!

- 인 메모리(RAM)의 데이터가 보존된다.
	- 즉, 인스턴스의 재부팅이 매우 빠르다!
	- 절전에 들어가기 직전의 RAM의 상태가 루트 경로의 EBS 볼륨에 저장된다. 따라서 EBS 암호화와 RAM의 상태를 저장하기 위한 충분한 공간이 있어야 한다.
	- 최대 60일까지 절전 가능

- 사용 사례
	- 오래 실행되는 프로세스를 갖고 있고 중지하지 않을 때
	- RAM 상태를 저장하고 싶을 때
	- 빠르게 재부팅을 하고 싶을 때
	- 서비스 초기화에 시간이 많이 걸려, 인스턴스 중지에 대한 비용이 크게 들어갈 때
