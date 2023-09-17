
## [[ALB]]

- ALB 는 L7 단의 로드 밸런서를 지원
- ALB는 http/https 프로토콜의 헤더를 확인해 적절한 패킷으로 전송
- ALB는 IP주소 + 포트 번호 + 패킷 내용을 보고 스위칭
- ALB는 IP주소가 변동되기 때문에 Client에서 Access할 [[ELB]]의 DNB Name을 이용해야한다.
- L7단을 지원하므로 SSL 적용이 가능

## [[NLB]]

- NLB는 L4단의 로드 밸런서를 지원
- NLB는 TCP/IP 프로토콜의 헤더를 확인해 적절한 패킷으로 전송
- NLB는 IP + 포트 번호를 보고 스위칭
- NLB는 할당한 Elastic IP를 고정 IP로 사용할 수 있으며, DNS Name과 IP주소 모두 사용 가능
- NLB는 SSL 적용이 인프라 단에서 불가하므로 애플리케이션 게층에서 따로 적용해주어야함.