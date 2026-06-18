# Web — 커뮤니티 게시판

React · Spring Boot · MySQL 기반 풀스택 웹 애플리케이션 실습 저장소입니다.  
회사별 게시판, 댓글, 파일 첨부, 회원 인증 기능을 포함합니다.

---

## 기술 스택

### Backend
![Java](https://img.shields.io/badge/Java_17-007396?style=flat&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.4-6DB33F?style=flat&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security_6-6DB33F?style=flat&logo=springsecurity&logoColor=white)
![JPA](https://img.shields.io/badge/JPA/Hibernate-59666C?style=flat&logo=hibernate&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-005F0F?style=flat&logo=thymeleaf&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white)

### Frontend
![React](https://img.shields.io/badge/React_19-61DAFB?style=flat&logo=react&logoColor=black)
![React Router](https://img.shields.io/badge/React_Router_7-CA4245?style=flat&logo=reactrouter&logoColor=white)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=flat&logo=axios&logoColor=white)

### Infra
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

---

## 프로젝트 구조

```
SK-PROJECT1/
├── backend/                        # Spring Boot 백엔드
│   └── src/main/
│       ├── java/org/example/demo_sc/
│       │   ├── config/             # Spring Security 설정 (AppSecurityConfig)
│       │   ├── controller/         # REST API 컨트롤러
│       │   │   ├── CompanyApiController  # 회사 목록·게시글 API
│       │   │   ├── PostController        # 게시글 CRUD + 댓글 + 첨부파일
│       │   │   ├── UserController        # 회원 가입·조회
│       │   │   ├── HomeController        # 메인 페이지
│       │   │   └── MyPageController      # 마이페이지
│       │   ├── dto/                # 데이터 전송 객체 (PostDto, UserDto …)
│       │   ├── entity/             # JPA 엔티티 (User, Post, Comment, Company, Mentor, Attachment)
│       │   ├── exception/          # 전역 예외 처리 (GlobalExceptionHandler)
│       │   ├── repository/         # Spring Data JPA 레포지토리
│       │   ├── service/            # 비즈니스 로직 (PostService, UserService, FileService …)
│       │   └── util/               # 인증 유틸 (AuthUtil)
│       └── resources/
│           ├── application.yml     # DB·Security·파일 업로드 설정
│           ├── db/                 # schema.sql, ERD 다이어그램
│           └── templates/          # Thymeleaf 템플릿 (board, post, login, mypage …)
│
├── frontend/                       # React 프론트엔드 (SPA)
│   └── src/
│       ├── App.js                  # 라우팅 설정 (React Router DOM)
│       └── components/
│           ├── Header.js           # 공통 헤더 (로그인 상태 표시)
│           ├── MainBoard.js        # 메인 — 회사별 최신 게시글 목록
│           ├── Company.js          # 특정 회사 게시판 (전체 게시글)
│           ├── Article.js          # 게시글 상세 보기
│           ├── WritePage.js        # 게시글 작성
│           ├── Profile.js          # 마이페이지
│           ├── Signin.js           # 로그인
│           └── Signup.js           # 회원 가입
│
└── demo/                           # React CRA 초기 템플릿 (참고용)
```

---

## 실행 방법

### 1. MySQL 실행 (Docker)

```bash
docker run -d -p 3306:3306 --name mysql \
  --env MYSQL_ROOT_PASSWORD=1234 \
  --env MYSQL_DATABASE=NEW9 \
  mysql
```

> `backend/src/main/resources/db/schema.sql`을 실행해 테이블을 생성하세요.

### 2. 백엔드 실행

```bash
# IntelliJ → File > Open → backend 폴더 선택
# build.gradle 인식 후 의존성 다운로드 대기
# DemoScApplication.java 실행
# http://localhost:8080 접속
```

> `application.yml`에서 DB 접속 정보(username, password, url)와 `file.dir` 경로를 환경에 맞게 수정하세요.

### 3. 프론트엔드 실행

```bash
cd frontend
npm install
npm start
# http://localhost:3000 접속
```

> 백엔드가 먼저 실행 중이어야 API 통신이 정상 동작합니다.

---

## 학습 내용

| 영역 | 주요 학습 내용 |
|------|---------------|
| **Spring Security** | 세션 기반 로그인·로그아웃, 커스텀 `UserDetailService`, 경로별 인가 정책, Thymeleaf Security 연동 |
| **JPA / Hibernate** | 엔티티 설계, 연관관계 매핑 (`@ManyToOne`, `@OneToMany`), JPQL·파생 쿼리, `ddl-auto: update` |
| **REST API** | `@RestController` + `@CrossOrigin`, DTO 변환, `ResponseEntity`, 전역 예외 처리 (`@ControllerAdvice`) |
| **파일 업로드** | `MultipartFile`, 서버 로컬 저장(`FileService`), Attachment 엔티티 연동 |
| **Thymeleaf** | 서버사이드 렌더링, `th:each·th:if·th:text`, Spring Security 통합 (`sec:authorize`) |
| **MySQL** | DDL 스키마 설계, 외래키·CASCADE, Docker 컨테이너로 로컬 DB 구동 |
| **React (SPA)** | 컴포넌트 분리, `useState·useEffect`, React Router DOM v7 보호 라우트 |
| **Axios / Fetch** | REST API 호출, 비동기 상태 관리, 상대·절대 URL 처리 |
| **CORS** | `@CrossOrigin` 설정, 프론트(3000)↔백엔드(8080) 통신 허용 |

---

## 개발 환경

- **JDK 17** 이상 — [다운로드](https://download.oracle.com/java/17/archive/jdk-17.0.12_windows-x64_bin.exe)
- **Node.js 18** 이상 — [다운로드](https://nodejs.org/)
- **IntelliJ IDEA** Ultimate (추천) / Community
- **Docker** — MySQL 컨테이너 실행

```bash
docker run -d -p 3306:3306 --name mysql \
  --env MYSQL_ROOT_PASSWORD=1234 \
  --env MYSQL_DATABASE=NEW9 \
  mysql
```

- **DB 클라이언트** — HeidiSQL / MySQL Workbench / IntelliJ 내장 DB 탭
