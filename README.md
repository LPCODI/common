# Codi-AI Common

Codi-AI는 사용자가 보유한 옷을 기반으로 날씨, 일정(TPO), 신체 프로필과 취향을 반영해 코디를 추천하고 가상 착장 결과를 제공하는 AI 스타일링 서비스입니다.

이 저장소는 프론트엔드와 백엔드가 함께 참고하는 아키텍처, 데이터베이스, API, 협업 문서를 관리합니다. 실행 코드는 각 애플리케이션 저장소에서 관리합니다.

## 바로가기

- [Backend 저장소](https://github.com/LPCODI/backend)
- [배포 API](https://backend-s092.onrender.com)
- [Swagger UI](https://backend-s092.onrender.com/swagger-ui/index.html)
- [OpenAPI JSON](https://backend-s092.onrender.com/v3/api-docs)

## 공통 문서

| 문서 | 내용 |
| --- | --- |
| [시스템 아키텍처](docs/architecture.md) | 서비스 구성, 데이터 흐름, 외부 연동 |
| [PostgreSQL 데이터베이스](docs/database-postgresql.md) | Neon PostgreSQL 테이블과 관계 |
| [API 엔드포인트](docs/api-reference.md) | 프론트엔드에서 사용하는 34개 API 요약 |
| [협업 가이드](docs/collaboration-guide.md) | 브랜치, PR, 환경변수, 검증 규칙 |

## 기술 구성

| 영역 | 기술 | 역할 |
| --- | --- | --- |
| Backend | Java 21, Spring Boot 3.3 | REST API와 비즈니스 로직 |
| 인증 | Spring Security, JWT | Access/Refresh Token 인증 |
| Database | Neon PostgreSQL, MyBatis, Flyway | 관계형 데이터와 스키마 관리 |
| Storage | Firebase Storage | 의류, 마스크, 아바타, 착장 이미지 저장 |
| AI | OpenAI Images | 고품질 이미지 렌더링 |
| Weather | 기상청 단기예보 | 위치·시간 기반 날씨 정보 |
| Deploy | Docker, Render | 백엔드 빌드와 운영 배포 |

## 저장소 구성

| 저장소 | 역할 |
| --- | --- |
| `backend` | Spring Boot API, Neon, Firebase, OpenAI, 날씨 연동 |
| `front` | 사용자 화면과 API 연동 |
| `common` | 공통 설계 및 협업 문서 |
| `.github` | LPCODI 조직 공개 프로필 |

## 기본 원칙

- API 기본 경로는 `/api/v1`입니다.
- 인증 API를 제외한 요청은 `Authorization: Bearer <accessToken>`을 사용합니다.
- 사용자는 요청에 `userId`를 직접 보내지 않으며 서버가 JWT에서 식별합니다.
- 이미지 파일은 Firebase Storage에, 이미지 메타데이터와 서비스 데이터는 Neon PostgreSQL에 저장합니다.
- 비밀번호, API 키, DB 접속 문자열, Firebase 서비스 계정 파일은 Git에 올리지 않습니다.
