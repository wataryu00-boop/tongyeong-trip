# 통영고 2026 수학여행 앱

## 개요
- 2026년 통영고 2학년 수학여행(5월 6~8일, 서울·용인·전주) 운영용 웹 앱
- 호스팅: GitHub Pages — main 브랜치에 푸시하면 1~2분 내 자동 배포
- 라이브 주소: https://wataryu00-boop.github.io/tongyeong-trip/
- 기술 스택: Vanilla HTML + CSS + JS (모놀리식 단일 HTML 파일), Firebase Realtime Database + Storage

## 배포
배포 절차 따로 없음. **`git push origin main` = 즉시 운영 반영.**
수정 후 푸시 전에 사용자에게 한 번 더 확인할 것.

## 파일 구조

### 학생/교사가 실제 쓰는 파일 (수정 시 영향 큼)
- `student.html` (≈6,600줄) — 학생용 앱. 로그인(학번+이름), 일정, 장소, 사진 업로드, 위치 공유
- `teacher.html` (≈9,700줄) — 교사용 상황판. 학생 위치 지도, SOS, 공지, 점호, 교사 쪽지
- `조편성_방배정_데이터.json` — 조 편성·방 배정·학생 마스터 데이터. `groups`/`rooms`/`student_updates` 세 키

### 설치·관리용 (학생·교사 사용 안 함, 운영 중 거의 안 건드림)
- `index.html` — GitHub Pages 메인 페이지(메뉴 허브). 학생은 직접 student.html로 접속하므로 없어도 작동.
- `admin.html`, `admin_bootstrap.html`, `group_names_sync.html`, `teacher2.html`, `kakao-test.html` — 설치 단계에서 썼던 파일들. 운영 중 수정 거의 없음.

## 코드 탐색 팁
- HTML 파일 한 개에 HTML+CSS+JS가 다 들어있는 모놀리식 구조
- 함수 찾을 때: `grep -n 'function 이름(' student.html` 또는 Read로 직접
- 탭 구조: `data-tab="..."`, `class="panel"`, `switchTab()` / `goTab()` 함수가 핵심
- Firebase 데이터 접근: `firebase.database().ref('...')` 패턴

## 주의사항
- **운영 중 수정 → 곧바로 학생·교사 화면에 반영됨**. 큰 수정 전 사용자 확인 필수
- `<title>`, `<h1>` 같은 메타데이터 변경은 신중히
- Firebase 설정값(apiKey 등) 코드에 하드코딩 — 공개 클라이언트 키이므로 보안 이슈 아님
- JSON 데이터는 fetch로 로드되는 것으로 보임 — 구조 변경 시 student/teacher 양쪽 코드 영향 검토

## 핸드폰 원격 제어 워크플로
사용자는 여행 기간 중 핸드폰 Claude 앱의 Remote Control로 이 세션에 접속.
- 사용자가 보고하는 버그는 라이브 사이트 기준
- 수정 → `git add` + `git commit` → `git push` → GitHub Pages 재배포 (1~2분)
- 푸시 전 항상 한 번 더 확인 (학생·교사가 보고 있음)
