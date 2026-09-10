# 아이자란 법무 문서 사이트

아이자란(모바일 앱)의 **개인정보처리방침 / 이용약관** 공개 페이지 + AdMob `app-ads.txt`.
스토어 제출·심사에 필요한 URL을 제공하기 위한 정적 사이트.

원본(정본)은 앱 저장소의 `docs/legal/privacy-policy.md`, `docs/legal/terms-of-service.md`.
이 사이트를 고치면 정본과 `apps/mobile/lib/legal.ts`도 함께 맞춘다.

## 파일

| 파일 | 용도 |
|---|---|
| `index.html` | 루트 랜딩 (두 문서로 링크) |
| `privacy.html` | 개인정보처리방침 |
| `terms.html` | 이용약관 |
| `app-ads.txt` | Google AdMob 인증 (아래 "app-ads.txt 주의" 참고) |
| `.nojekyll` | GitHub Pages Jekyll 처리 비활성화 |

페이지 간 링크는 상대경로(`./privacy.html` 등)라 루트 도메인·서브경로 어디에 올려도 동작한다.

## 배포 전 채울 값 (3곳)

HTML에서 **노란 하이라이트(`__...__`)** 로 표시된 자리를 찾아 바꾼다.

| 토큰 | 넣을 값 | 나오는 곳 |
|---|---|---|
| `__게시일__` | 예: `2026년 9월 15일` | privacy.html 3곳, terms.html 2곳 |
| `__보호책임자_성명__` | 개인정보 보호책임자 성명 | privacy.html 1곳 |
| `__보호책임자_직위__` | 예: `대표` | privacy.html 1곳 |
| `__문의_이메일__` | 정책 문의용 이메일 | privacy.html 3곳, terms.html 2곳 |

> `class="fill"` 스타일도 함께 지우면 하이라이트가 사라진다(선택).

## 배포 (GitHub Pages)

1. 이 폴더 내용을 legal 저장소 루트에 복사 → 커밋·푸시
2. 저장소 **Settings → Pages** → Source: `main` 브랜치 `/ (root)`
3. 게시 URL:
   - `https://<username>.github.io/<repo>/privacy.html`
   - `https://<username>.github.io/<repo>/terms.html`

## app-ads.txt 주의 — GitHub Pages 서브경로면 동작 안 함

AdMob은 **개발자 웹사이트 루트 도메인**의 `/app-ads.txt` 만 크롤링한다
(`https://도메인/app-ads.txt`). 서브경로(`https://<username>.github.io/<repo>/app-ads.txt`)는
읽지 않는다. 아래 중 하나가 필요하다.

- **(권장) 커스텀 도메인 연결**: 이 저장소 Pages에 커스텀 도메인(`aizaran.app` 등)을 붙이면
  `https://커스텀도메인/app-ads.txt` 로 서빙된다. 스토어 등록정보 "웹사이트" 필드에 이 도메인을 넣는다.
- **사용자 페이지 저장소 사용**: 저장소 이름을 `<username>.github.io` 로 만들면 루트
  (`https://<username>.github.io/app-ads.txt`)에 서빙된다. 이 경우 스토어 "웹사이트"에
  `https://<username>.github.io` 를 넣는다.

`app-ads.txt` 내용(고정):

```
google.com, pub-3987136272559709, DIRECT, f08c47fec0942fa0
```

- `pub-3987136272559709` = AdMob 게시자 ID (App ID `ca-app-pub-3987136272559709~…` 에서 추출)
- `f08c47fec0942fa0` = Google 고정 인증 기관 ID (모든 AdMob 게시자 공통)
- AdMob 콘솔 → 앱 → app-ads.txt 에서 "app-ads.txt 파일 확인" 실행 (전파에 수 시간~하루)
- 스토어 등록정보의 "웹사이트" 도메인과 app-ads.txt가 올라간 도메인이 **일치**해야 한다
