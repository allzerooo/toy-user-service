# 1. Code
## 1.1 @EnableDiscoveryClient
- Discovery Client 역할을 하는 애플리케이션으로 기동하겠다고 명시적으로 나타냄 
- 의존성에 eureka client가 추가되어 있으면 @EnableDiscoveryClient 애너테이션을 추가하지 않아도 Eureka 클라이언트 역할로 Eureka 서버에 등록이 된다.
- 등록이 자동으로 되게 해주는 설정
  - eureka.client.service-url.defaultZone: 해당 URL에 서비스를 등록하고, 자신의 위치 정보를 전달.
  - eureka.client.fetch-registry
  - eureka.client.register-with-eureka

# 2. Eureka 대시보드
- eureka server를 실행하고, eureka client(현재 프로젝트)를 실행하면 대시보드에 user-service가 등록된걸 확인할 수 있다

# 3. 분산 상황 설정
## 3.1 IntelliJ
Run Configuration -> Edit Configurations -> Spring Boot 서비스 선택 -> Copy Configuration -> Name 변경 -> Modify Options -> Add VM options -> VM option 입력 : -Dserver.port=60001
## 3.2 Terminal
### 3.2.1 Gradle
### 3.2.2 Java
```bash
java -jar build/libs/user-service-0.0.1-SNAPSHOT.jar --server.port=60001
```
** 60000 포트와 60001 포트에 서비스를 실행하면 Eureka 대시보드에 2개의 user-service가 등록된 것을 확인할 수 있다

# 4. Load Balancer
## 4.1 Scale Out
클라이언트의 네트워크 트래픽이 증가하면 User Service 개수를 늘린다(확장성).
## 4.2 부하 분산 처리
이때 클라이언트가 어떤 User Service를 사용할 지 결정하는 것이 아니라, User Service들 앞단에서 어떤 User Service를 사용할 지 핸들링할 수 있는 Load Balancer라는 것을 둔다.

