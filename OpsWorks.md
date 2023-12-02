> [!info] Chef라는 오픈소스 서비스를 기반으로 한다.
> Chef의 클라우드 버전
> 3-tier application 구성에 매우 좋다


- custom cheif recipe에서 Setup, Deploy, Undeploy, Shutdown은 Instance specific인데, Configure만 그렇지 않아 하나의 Instance에서의 이벤트를 타 인스턴스에 적용할 수 있음을 기억해야 한다.
- Setup에 Deploy과정이 포함되어 있다.