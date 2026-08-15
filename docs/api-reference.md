# Codi-AI API 엔드포인트

운영 Base URL은 `https://backend-s092.onrender.com`이며 모든 서비스 API는 `/api/v1`을 사용합니다.

Swagger UI에서 요청 스키마와 실제 응답 예시를 확인할 수 있습니다.

- Swagger: <https://backend-s092.onrender.com/swagger-ui/index.html>
- OpenAPI JSON: <https://backend-s092.onrender.com/v3/api-docs>

## 인증

| Method | Path | 역할 |
| --- | --- | --- |
| POST | `/api/v1/auth/signup` | 회원가입 |
| POST | `/api/v1/auth/login` | Access/Refresh Token 발급 |
| POST | `/api/v1/auth/refresh` | 토큰 갱신 |
| POST | `/api/v1/auth/logout` | Refresh Token 폐기 |

로그인 후 인증이 필요한 API에는 다음 헤더를 전송합니다.

```http
Authorization: Bearer ACCESS_TOKEN
```

## 사용자·신체 프로필·아바타

| Method | Path | 역할 |
| --- | --- | --- |
| GET | `/api/v1/users/me` | 내 계정 조회 |
| PUT | `/api/v1/users/me` | 내 계정 수정 |
| DELETE | `/api/v1/users/me` | 회원 탈퇴 |
| GET | `/api/v1/body-profile` | 신체 프로필 조회 |
| PUT | `/api/v1/body-profile` | 신체 프로필 저장·수정 |
| DELETE | `/api/v1/body-profile` | 신체 프로필 삭제 |
| POST | `/api/v1/avatar/generate` | 기본 설정으로 아바타 생성 |
| GET | `/api/v1/avatar` | 현재 아바타 조회 |
| PUT | `/api/v1/avatar` | 설정을 반영해 아바타 재생성 |
| DELETE | `/api/v1/avatar` | 아바타 삭제 |

## 옷장

| Method | Path | 역할 |
| --- | --- | --- |
| GET | `/api/v1/wardrobe` | 옷장 목록과 필터 조회 |
| POST | `/api/v1/wardrobe` | `multipart/form-data` 의류 등록 |
| GET | `/api/v1/wardrobe/{itemId}` | 의류 한 건 조회 |
| PUT | `/api/v1/wardrobe/{itemId}` | 의류 속성 수정 |
| DELETE | `/api/v1/wardrobe/{itemId}` | 의류와 이미지 삭제 |
| POST | `/api/v1/wardrobe/{itemId}/reanalyze` | 의류 이미지 재분석 |

## 일정·날씨·추천

| Method | Path | 역할 |
| --- | --- | --- |
| POST | `/api/v1/tpo/parse` | 자연어 일정을 TPO로 구조화 |
| GET | `/api/v1/weather/forecast` | 위·경도와 시각 기준 날씨 조회 |
| POST | `/api/v1/recommendations` | 옷장 기반 추천 생성 |
| GET | `/api/v1/recommendations/{id}` | 추천 결과 조회 |
| POST | `/api/v1/recommendations/{id}/regenerate` | 추천 다시 생성 |

## 즐겨찾기·피드백

| Method | Path | 역할 |
| --- | --- | --- |
| GET | `/api/v1/favorites` | 즐겨찾기 목록 조회 |
| POST | `/api/v1/favorites` | 추천 착장 저장 |
| DELETE | `/api/v1/favorites/{favoriteId}` | 즐겨찾기 삭제 |
| POST | `/api/v1/recommendations/{id}/feedback` | 추천 결과 평가 |
| POST | `/api/v1/outfits/feedback` | 직접 선택한 코디 평가 |

## 가상 착장

| Method | Path | 역할 |
| --- | --- | --- |
| POST | `/api/v1/try-on/preview` | 빠른 2D 착장 생성 |
| POST | `/api/v1/try-on/render` | 고품질 비동기 렌더 요청 |
| GET | `/api/v1/try-on/{resultId}` | 렌더 상태와 결과 조회 |
| DELETE | `/api/v1/try-on/{resultId}` | 착장 결과 삭제 |

총 23개 경로, 34개 API 작업입니다. 요청·응답 필드의 최종 기준은 배포 서버의 OpenAPI 문서입니다.
