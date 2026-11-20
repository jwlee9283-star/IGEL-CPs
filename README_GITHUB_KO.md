# Our Ever After – V28 GitHub Pages 패키지

이 폴더는 V28의 **6페이지 청첩장**을 GitHub Pages에 올리고, 사진과 문구를 직접 바꾸기 쉽게 정리한 버전입니다.

## 1) 폴더 구성

```text
our-ever-after-v28-github-ready/
├── index.html                 # 청첩장 본문과 디자인/인터랙션
├── .nojekyll                  # 정적 파일 배포용 설정 파일
├── README_GITHUB_KO.md        # GitHub 가입·배포·수정 가이드
└── assets/
    ├── couple-cover.jpg       # 표지 + 2페이지 아치 사진 + 갤러리 1번
    ├── paper-tone.png         # 종이/배경 질감
    ├── swipe-guide.png        # 첫 접속 시 좌우 넘김 안내
    ├── couple-proposal.jpg    # 갤러리 2번 + 마지막 Thank You 사진
    └── gallery-03-preview.jpg# 갤러리 3번 교체용 미리보기
```

**중요:** `index.html`과 `assets` 폴더는 반드시 같은 최상위 폴더 안에 있어야 합니다. GitHub 저장소에는 이 폴더 안의 파일들을 그대로 올립니다. ZIP 파일 자체를 저장소에 올리는 방식이 아닙니다.

## 2) 자주 바꾸는 정보

`index.html`을 VS Code 또는 메모장으로 열고 `const INVITATION = {`를 검색합니다.

- `groom`: 신랑 이름
- `bride`: 신부 이름
- `dateTime`: 예식 날짜와 시간. 예: `2027-02-27T17:00:00+09:00`
- `venue`: 예식장 이름
- `venuePhoto`: 5페이지 예식장 사진 주소 또는 `assets/venue.jpg`
- `address`: 예식장 주소
- `groomParents`, `brideParents`: 양가 부모님 표기
- `contacts`: 연락처 목록
- `transport`: 대중교통 안내
- `parking`: 주차 안내
- `accounts`: 축의금 계좌 목록
- `mapUrl`: 지도 링크

날짜는 한국 표준시(+09:00)를 포함한 형식으로 입력합니다. D-day는 이 날짜를 기준으로 한국 시간(Asia/Seoul)으로 자동 계산됩니다.

## 3) 사진 교체 방법 – 가장 쉬운 방법

1. `assets` 폴더에서 교체할 사진 파일을 찾습니다.
2. 새 사진을 기존 파일과 **완전히 같은 파일명**으로 저장합니다.
3. 기존 파일을 덮어씁니다.
4. GitHub에 수정된 사진 파일을 다시 업로드합니다.

파일별 사용 위치:

| 파일명 | 사용 위치 |
|---|---|
| `couple-cover.jpg` | 1페이지 표지, 2페이지 아치형 사진 배경, 갤러리 첫 번째 사진 |
| `couple-proposal.jpg` | 갤러리 두 번째 사진, 6페이지 Thank You 배경 |
| `gallery-03-preview.jpg` | 4페이지 갤러리 세 번째 미리보기 사진 |
| `venue.jpg` (새로 추가 가능) | 5페이지 예식장 사진. 아래 설명 참고 |
| `paper-tone.png` | 종이/배경 질감 이미지이므로 교체하지 않는 것을 권장 |
| `swipe-guide.png` | 첫 접속 시 표시되는 좌우 넘김 안내 이미지 |

새 사진은 JPG 또는 PNG를 권장합니다. 휴대폰 사진 원본이 너무 크면 가로/세로 긴 변을 약 1600~2200px 정도로 줄이고, JPG 품질 80~90 정도로 저장하면 로딩이 빨라집니다.

## 4) 갤러리에 사진 4~13번 추가하기

1. 새 사진을 `assets` 폴더에 넣습니다. 예: `gallery-04.jpg`
2. `index.html`에서 `const GALLERY_PHOTOS = [`를 검색합니다.
3. 배열 마지막 객체 뒤에 쉼표를 붙이고 새 객체를 추가합니다.

예시:

```js
  { src: 'assets/gallery-03-preview.jpg', alt: '바닷가 여행 사진', caption: 'A little escape', placeholder: true },
  { src: 'assets/gallery-04.jpg', alt: '함께 여행한 사진', caption: 'Our journey' }
```

- `src`: 파일 경로
- `alt`: 사진을 설명하는 문장
- `caption`: 갤러리 아래에 보일 짧은 문구
- `placeholder: true`: 미리보기 사진에 붙는 PREVIEW 표시. 실제 사진이면 이 항목을 삭제합니다.

이 패키지는 기본 3장에 더해 최대 10장의 추가 사진 자리를 보여줍니다. 실제 사진 객체를 추가할수록 빈 자리는 자동으로 줄어듭니다.

## 5) 5페이지 예식장 사진을 내 사진으로 바꾸기

1. 예식장 사진을 `assets/venue.jpg`라는 이름으로 저장합니다.
2. `INVITATION` 안의 `venuePhoto` 값을 다음처럼 바꿉니다.

```js
venuePhoto: 'assets/venue.jpg',
```

사진 파일과 경로의 대소문자까지 정확히 일치해야 합니다.

## 6) 글씨·색상·간격 미세 수정

`index.html`의 `<style>` 영역에서 아래 항목을 찾아 조정합니다.

- 전체 색상: `:root` 안의 `--paper`, `--ink`, `--gold`, `--muted`
- 본문 글꼴: `--korean`, `--serif`
- 제목 크기: `.page-eyebrow`, `.page-title`
- 초대 문구: `.invitation-copy`
- 날짜 카드: `.date-card`, `.date-main`, `.date-time`
- 달력: `.calendar-grid`, `.calendar-day`, `.event-day`
- 갤러리: `.postcard-layout`, `.stamp-photo`, `.more-button`
- 예식장/연락처: `.venue-name`, `.venue-address`, `.directions-details`, `.contact-grid`, `.bank-info`
- 마지막 감사 페이지: `.thankyou-script`, `.thankyou-message`, `.thankyou-sign`

글자 크기는 보통 `font-size: 14px`처럼 적혀 있습니다. 예를 들어 초대 문구를 조금 키우려면 `.invitation-copy`의 `font-size` 값을 15px에서 16px로 조정합니다. 간격은 `margin`, `padding`, `gap`, `line-height` 값을 조절합니다.

한 번에 여러 값을 바꾸지 말고 한두 가지씩 바꾼 뒤 저장하고 새로고침해 결과를 확인하는 것을 권장합니다. CSS 규칙이 여러 번 선언된 경우 아래쪽에 있는 규칙이 위쪽 규칙을 덮어쓸 수 있으므로, 같은 선택자가 반복되는지 검색해 주세요.

## 7) 내 컴퓨터에서 먼저 확인하기

- `index.html`을 Chrome 또는 Edge에서 더블클릭합니다.
- 사진이 나오지 않으면 `assets` 폴더가 `index.html`과 같은 폴더에 있는지, 파일명이 정확한지 확인합니다.
- 글꼴은 Google Fonts 연결을 사용하므로 인터넷 연결이 없으면 대체 시스템 글꼴로 표시됩니다.
- 이 버전은 정적 HTML입니다. GitHub Pages에는 서버나 터미널 없이 배포할 수 있습니다.

## 8) GitHub Pages 배포 요약

1. GitHub 계정에 로그인합니다.
2. New repository를 만들고 이름을 `our-ever-after` 등으로 정합니다.
3. GitHub Free를 사용한다면 Pages용 저장소는 Public으로 설정합니다.
4. `Add file` → `Upload files`에서 이 폴더 안의 `index.html`, `.nojekyll`, `README_GITHUB_KO.md`, `assets` 폴더를 업로드합니다. ZIP 파일 자체는 올리지 않습니다.
5. Commit changes를 누릅니다.
6. 저장소의 Settings → Pages로 이동합니다.
7. Build and deployment의 Source를 `Deploy from a branch`로 선택합니다.
8. Branch는 `main`, Folder는 `/(root)`로 선택하고 Save를 누릅니다.
9. Pages 화면에 표시되는 공개 주소를 열어 스마트폰에서 확인합니다.

일반적인 프로젝트 저장소 주소는 `https://깃허브아이디.github.io/저장소이름/` 형태입니다. 실제 주소는 GitHub Pages 화면에 표시된 것을 사용합니다.

## 9) GitHub에서 수정본 올리기

- 텍스트/디자인 수정: `index.html` 파일을 저장소에서 열고 연필(Edit) 아이콘으로 수정한 뒤 Commit changes를 누르거나, 컴퓨터에서 수정 후 같은 이름으로 다시 업로드합니다.
- 사진 수정: `assets` 안의 해당 파일을 같은 이름으로 업로드해 교체합니다.
- 변경 후 Pages가 다시 배포될 수 있으므로 잠시 후 주소를 새로고침합니다.
- 휴대폰에서 이전 화면이 보이면 브라우저 새로고침 또는 캐시 없는 새로고침을 시도합니다.

## 10) 공개 전 꼭 확인할 개인정보

GitHub Pages 공개 사이트와 Public 저장소의 HTML/사진은 누구나 볼 수 있고 복사할 수 있습니다. 특히 이 프로젝트의 `contacts`와 `accounts`에 입력하는 전화번호·계좌번호는 페이지 화면뿐 아니라 저장소 파일에서도 확인될 수 있습니다. 공개해도 되는 정보만 입력하세요. 비밀번호, 인증번호, 주민등록번호, 로그인 토큰 등 비밀정보는 절대로 넣지 마세요.

이 V28에는 Kindly Reply 페이지와 Google Forms 회신 기능이 없습니다. 따라서 이 패키지는 6페이지 정적 청첩장입니다.
