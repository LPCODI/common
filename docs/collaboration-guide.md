# Codi-AI 협업 가이드

## 저장소별 책임

- `front`: 화면, 상태 관리, API 호출, 사용자 입력 검증
- `backend`: 인증, 권한 검사, 비즈니스 로직, DB와 외부 서비스 연동
- `common`: 팀 전체가 공유하는 설계와 계약 문서
- `.github`: GitHub 조직 소개와 공통 커뮤니티 설정

공통 API 계약이 바뀌면 백엔드 구현과 Swagger를 먼저 갱신하고, 프론트엔드 담당자에게 요청·응답 변경 내용을 전달합니다.

## 브랜치와 Pull Request

1. 최신 `main`에서 작업 브랜치를 만듭니다.
2. 기능은 `feat/<name>`, 수정은 `fix/<name>`, 문서는 `docs/<name>` 형식을 권장합니다.
3. 한 PR에는 하나의 목적만 포함합니다.
4. 변경 파일, 변경 이유, 검증 결과를 PR 본문에 기록합니다.
5. 리뷰와 자동 검증이 끝난 뒤 `main`으로 병합합니다.

`main`에 직접 push하거나, 관련 없는 파일을 한 커밋에 함께 넣지 않습니다.

## 커밋 메시지

```text
feat: add wardrobe filter
fix: validate refresh token
docs: update API reference
test: cover Firebase upload flow
```

## API 변경 체크리스트

- HTTP 메서드와 경로가 Swagger에 등록됐는가?
- 필수값, 선택값, 허용 범위가 명확한가?
- 성공·오류 상태 코드가 프론트엔드 계약과 일치하는가?
- 인증 및 사용자 소유권 검사가 적용됐는가?
- DB 마이그레이션이 필요한 경우 Flyway 파일을 추가했는가?
- 기존 클라이언트에 영향을 주는 변경을 공유했는가?

## 비밀정보 관리

다음 값은 저장소에 커밋하지 않습니다.

- `.env`
- Neon 접속 문자열과 DB 비밀번호
- JWT Secret
- Firebase Admin SDK 서비스 계정 JSON
- OpenAI API Key
- 기상청 API Key

로컬에서는 `.env`, Render에서는 Environment Variables와 Secret Files를 사용합니다. 예제 파일에는 실제 값 대신 설명용 placeholder만 기록합니다.

## 검증 기준

백엔드 변경은 최소한 다음 명령을 통과해야 합니다.

```bash
cd Backend
./mvnw test
./mvnw package
```

배포 후에는 Swagger, 인증 차단, DB 연결을 확인하고 Firebase·OpenAI 등 비용이나 데이터 변경이 발생하는 테스트는 전용 테스트 계정으로 실행합니다.
