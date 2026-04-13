# 3-1반 열정 ON! UI

GitHub Pages에서 열리는 정적 채팅방입니다.
메시지 조회는 모두 가능하지만, 메시지 작성/수정/삭제는 관리자 비밀번호를 통과한 경우에만 가능합니다.
관리자 권한이 없으면 하단 입력창은 화면에 보이지 않습니다.
관리자 인증 팝업은 상단의 `3-1반 열정 ON!` 제목을 5번 눌렀을 때만 열립니다.

## 파일

- `index.html`
- `styles.css`
- `app.js`
- `config.js`
- `supabase.sql`

## 현재 구조

- 읽기: `messages` 테이블을 공개 조회
- 쓰기: `chat_admin_send_message()` RPC 함수만 허용
- 수정: `chat_admin_update_message()` RPC 함수만 허용
- 삭제: `chat_admin_delete_message()` RPC 함수만 허용
- 비밀번호 검증: `chat_admin_login()` RPC 함수에서 처리
- 관리자 작성 메타데이터: 이름과 시간을 직접 입력
- 이미지 업로드: `Supabase Storage` 버킷 `class-chat-images`에 저장
- 레거시 이미지: 예전 `image_data_url` 메시지는 계속 읽기 가능
- 직접 insert/update/delete: 비허용

## 해야 할 일

1. 현재 `supabase.sql`에는 관리자 비밀번호 `Rooming`이 반영되어 있습니다.
2. 이 `supabase.sql` 전체를 Supabase `SQL Editor`에서 다시 실행합니다.
3. `config.js` 값이 현재 프로젝트 URL / publishable key와 맞는지 확인합니다.
4. GitHub Pages에 배포합니다.

`supabase.sql`을 다시 실행하면 아래가 같이 적용됩니다.

- `messages` 테이블에 `image_url`, `image_path` 컬럼 추가
- Storage 버킷 `class-chat-images` 생성
- Storage 공개 읽기 / anon 업로드 / 수정 / 삭제 정책 생성

## 관리자 모드 사용법

1. 페이지 접속
2. 김동현은 신이야
3. 비밀번호 입력
4. 인증 성공 시 김동현은 신이야

수정을 누르면 해당 메시지 내용과 이미지가 아래 입력칸으로 내려오고, `수정 중` 상태에서 저장할 수 있습니다.
상단 오른쪽 버튼은 바로 새로고침입니다.
페이지를 새로고침하면 관리자 모드는 다시 잠깁니다.
비밀번호는 브라우저 localStorage에 저장하지 않고, 현재 열린 페이지 메모리에만 유지합니다.

## 이미지 관련 주의

- 새 이미지는 DB 문자열이 아니라 `Supabase Storage` URL로 저장됩니다.
- 그래서 모바일에서 올린 사진을 다른 기기에서도 같은 URL로 볼 수 있습니다.
- 업로드 전에 브라우저에서 JPEG로 압축합니다.
- 텍스트 없이 이미지만 보내는 것도 가능합니다.
- 아주 큰 원본 이미지는 거절될 수 있으니, 그 경우 더 작은 이미지를 선택하면 됩니다.
- 예전 방식의 `image_data_url` 메시지는 읽을 수 있고, 관리자 수정 저장 시 Storage 방식으로 자동 전환됩니다.

## 주의

- 김동현은 신입니다

