# SPRING PLUS
### 개요
> Spring Boot 기반 프로젝트에서 코드 개선 과제를 수행한 결과입니다.</br>
> 총 9가지 미션을 통해 @Transactional, JWT, JPQL, 테스트 코드, AOP, Cascade, N+1,</br> QueryDSL, Spring Security에 대한 
> 이해와 개선 능력을 향상시켰습니다.
 
### 기술 스택

#### - Backend
- Java 17
- Spring Boot 3.x
- Spring Security
- Spring Data JPA
- QueryDSL
- JWT (io.jsonwebtoken)

#### - Database
- MySQL

#### - Test
- JUnit 5
- Spring MockMvc

#### - Build & Dependency
- Gradle

#### - Tools
- IntelliJ IDEA
- Git / GitHub
- Lombok


### 주요 개선 내용
#### 1.`@Transactional`의 이해
```
- 문제상황 
읽기 전용 트랜잭션으로 인해 insert시 오류 발생

- 개선
save 메서드를 다른 트랜잭션이 관리하도록 코드 작성
```
#### 2. JWT의 이해
```
- nickname 필드 entity 및 도메인에 추가
- JWT 생성 시 claim에 닉네임 추가
```
#### 3. JPA의 이해
```
- weather, modifiedAt 조건으로 할 일 검색 기능 추가
- 조건 유무에 따라 쿼리 나눠서 실행하도록 구현
```
#### 4. 컨트롤러 테스트의 이해
```
- 문제상황
예외 발생시 400 에러를 반환해야하는데 200에러 반환

- 개선
예외 발생 시 400에러를 반환할 수 있도록 코드 수정
```
#### 5. AOP의 이해
```
- 어노테이선 @Before로 수정 및 pointcut 설정 수정
```

#### 6. JPA cascade
```
- 할 일 생성 시 유저가 자동 등록 될 수 있도록 cascade 추가
```

#### 7. N+1
```
- comment 조회 시 JOIN으로 되어 N+1문제가 발생하던 코드를 FETCH JOIN으로 개선
```

#### 8. QueryDSL
```
- JPQL로 작성된 findByIdWithUser를 QueryDSL로 변경
- N+1 문제 해결을 위해 fetch join 메서드 사용
```

#### 9. Spring Security
```
- 기존 Filter와 Argument Resolver를 사용하던 코드들을 Spring Security로 변경
- 토큰 인증 방식을 유지하기 위해 JWT는 그대로 사용
```

### 프로젝트 구조 
```
.
├── main
│   ├── generated
│   ├── java
│   │   └── org
│   │       └── example
│   │           └── expert
│   │               ├── ExpertApplication.java
│   │               ├── aop
│   │               │   └── AdminAccessLoggingAspect.java
│   │               ├── client
│   │               │   ├── WeatherClient.java
│   │               │   └── dto
│   │               │       └── WeatherDto.java
│   │               ├── config
│   │               │   ├── AuthUserArgumentResolver.java
│   │               │   ├── GlobalExceptionHandler.java
│   │               │   ├── JwtFilter.java
│   │               │   ├── JwtUtil.java
│   │               │   ├── PasswordEncoder.java
│   │               │   ├── PersistenceConfig.java
│   │               │   ├── QueryDslConfig.java
│   │               │   ├── SecurityConfig.java
│   │               │   └── WebConfig.java
│   │               ├── domain
│   │               │   ├── auth
│   │               │   │   ├── controller
│   │               │   │   │   └── AuthController.java
│   │               │   │   ├── dto
│   │               │   │   │   ├── request
│   │               │   │   │   │   ├── SigninRequest.java
│   │               │   │   │   │   └── SignupRequest.java
│   │               │   │   │   └── response
│   │               │   │   │       ├── SigninResponse.java
│   │               │   │   │       └── SignupResponse.java
│   │               │   │   ├── exception
│   │               │   │   │   └── AuthException.java
│   │               │   │   └── service
│   │               │   │       └── AuthService.java
│   │               │   ├── comment
│   │               │   │   ├── controller
│   │               │   │   │   └── CommentController.java
│   │               │   │   ├── dto
│   │               │   │   │   ├── request
│   │               │   │   │   │   └── CommentSaveRequest.java
│   │               │   │   │   └── response
│   │               │   │   │       ├── CommentResponse.java
│   │               │   │   │       └── CommentSaveResponse.java
│   │               │   │   ├── entity
│   │               │   │   │   └── Comment.java
│   │               │   │   ├── repository
│   │               │   │   │   └── CommentRepository.java
│   │               │   │   └── service
│   │               │   │       └── CommentService.java
│   │               │   ├── common
│   │               │   │   ├── annotation
│   │               │   │   │   └── Auth.java
│   │               │   │   ├── dto
│   │               │   │   │   └── AuthUser.java
│   │               │   │   ├── entity
│   │               │   │   │   └── Timestamped.java
│   │               │   │   └── exception
│   │               │   │       ├── InvalidRequestException.java
│   │               │   │       └── ServerException.java
│   │               │   ├── manager
│   │               │   │   ├── controller
│   │               │   │   │   └── ManagerController.java
│   │               │   │   ├── dto
│   │               │   │   │   ├── request
│   │               │   │   │   │   └── ManagerSaveRequest.java
│   │               │   │   │   └── response
│   │               │   │   │       ├── ManagerResponse.java
│   │               │   │   │       └── ManagerSaveResponse.java
│   │               │   │   ├── entity
│   │               │   │   │   └── Manager.java
│   │               │   │   ├── repository
│   │               │   │   │   └── ManagerRepository.java
│   │               │   │   └── service
│   │               │   │       └── ManagerService.java
│   │               │   ├── todo
│   │               │   │   ├── controller
│   │               │   │   │   └── TodoController.java
│   │               │   │   ├── dto
│   │               │   │   │   ├── request
│   │               │   │   │   │   └── TodoSaveRequest.java
│   │               │   │   │   └── response
│   │               │   │   │       ├── TodoResponse.java
│   │               │   │   │       └── TodoSaveResponse.java
│   │               │   │   ├── entity
│   │               │   │   │   └── Todo.java
│   │               │   │   ├── repository
│   │               │   │   │   ├── TodoQueryRepository.java
│   │               │   │   │   ├── TodoQueryRepositoryImpl.java
│   │               │   │   │   └── TodoRepository.java
│   │               │   │   └── service
│   │               │   │       └── TodoService.java
│   │               │   └── user
│   │               │       ├── controller
│   │               │       │   ├── UserAdminController.java
│   │               │       │   └── UserController.java
│   │               │       ├── dto
│   │               │       │   ├── request
│   │               │       │   │   ├── UserChangePasswordRequest.java
│   │               │       │   │   └── UserRoleChangeRequest.java
│   │               │       │   └── response
│   │               │       │       ├── UserResponse.java
│   │               │       │       └── UserSaveResponse.java
│   │               │       ├── entity
│   │               │       │   └── User.java
│   │               │       ├── enums
│   │               │       │   └── UserRole.java
│   │               │       ├── repository
│   │               │       │   └── UserRepository.java
│   │               │       └── service
│   │               │           ├── UserAdminService.java
│   │               │           └── UserService.java
│   │               └── security
│   │                   ├── CustomUserDetailService.java
│   │                   └── CustomUserPrincipal.java
│   └── resources
│       └── application.properties
└── test
    └── java
        └── org
            └── example
                └── expert
                    ├── ExpertApplicationTests.java
                    └── domain
                        └── todo
                            └── controller
                                └── TodoControllerTest.java
```
### 트러블슈팅 및 느낀점
> 벨로그 넣어놓을 예정입니다 !
