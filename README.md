# 스캠레이더 (ScamRadar)

최신 보이스피싱·스미싱·투자사기 등 사기 수법을 정리하는 정적 사이트입니다. 빌드 도구 없이 순수 HTML/CSS로 작성되어 있습니다.

## 파일 구성

- `index.html`, `about.html`, `privacy.html`, `contact.html` — 핵심 페이지
- `articles/*.html` — 콘텐츠 글 15개
- `css/style.css` — 공통 스타일
- `sitemap.xml`, `robots.txt` — 검색엔진용 파일

---

## 1단계. 배포 전 준비: 도메인 주소 반영

모든 HTML 파일과 `sitemap.xml`, `robots.txt`에 `https://info-site.github.io` 이라는 임시 주소가 들어 있습니다. 실제 도메인(또는 GitHub Pages 주소)이 정해지면 전체 파일에서 이 문자열을 일괄 치환해야 합니다.

예: 도메인이 `https://www.myscamsite.com` 이라면 프로젝트 폴더에서 아래 명령 실행 (Git Bash 기준):

```bash
grep -rl "info-site.github.io" . | xargs sed -i "s|info-site.github.io|www.myscamsite.com|g"
```

GitHub Pages를 그대로 쓴다면 도메인은 `내계정.github.io/저장소이름` 형태가 됩니다.

`contact.html`의 `contact@info-site.github.io` 이메일 주소도 실제 사용할 이메일로 바꿔주세요.

---

## 2단계. GitHub Pages로 배포하기

1. [github.com](https://github.com)에서 새 저장소(Repository)를 만듭니다. (예: `scamradar`)
2. 이 프로젝트 폴더에서 git 초기화 후 푸시합니다.
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/내계정/scamradar.git
   git push -u origin main
   ```
3. GitHub 저장소 페이지 → **Settings → Pages** 로 이동합니다.
4. "Build and deployment" 에서 Source를 **Deploy from a branch**, Branch를 **main / (root)** 로 설정 후 저장합니다.
5. 1~2분 후 `https://내계정.github.io/scamradar/` 로 접속되는지 확인합니다.
6. (선택) 커스텀 도메인이 있다면 같은 Pages 설정 화면에서 Custom domain에 입력하고, 도메인 등록업체(가비아, 후이즈 등)에서 CNAME 레코드를 GitHub Pages로 연결합니다.

> 커스텀 도메인을 쓸 계획이라면, 1단계의 URL 치환을 커스텀 도메인 기준으로 하는 것이 좋습니다 (나중에 바꾸면 검색엔진에 다시 인식시켜야 함).

---

## 3단계. Google Search Console 등록

1. [Google Search Console](https://search.google.com/search-console)에 접속해 Google 계정으로 로그인합니다.
2. "속성 추가" → **URL 접두어** 방식을 선택하고 사이트 주소(`https://내계정.github.io/scamradar/` 또는 커스텀 도메인)를 입력합니다.
3. 소유권 확인 방법 중 **HTML 태그** 방식을 선택하면 `<meta name="google-site-verification" content="...">` 태그를 줍니다. 이 태그를 각 페이지의 `<head>`에 넣는 대신, `index.html`의 `<head>` 맨 위에 한 줄만 추가하면 됩니다 (홈페이지에만 있어도 인증됨).
4. 태그를 추가한 뒤 다시 배포(git push)하고, Search Console에서 "확인" 버튼을 클릭합니다.
5. 확인이 완료되면 왼쪽 메뉴의 **Sitemaps**로 이동해 `sitemap.xml`을 제출합니다. (예: `sitemap.xml`만 입력)
6. "URL 검사" 도구로 홈페이지와 주요 글의 URL을 넣고 "색인 생성 요청"을 눌러 빠른 색인을 유도할 수 있습니다.

---

## 4단계. 네이버 서치어드바이저 등록

1. [네이버 서치어드바이저](https://searchadvisor.naver.com)에 네이버 계정으로 로그인합니다.
2. "사이트 등록" 메뉴에서 사이트 주소를 입력합니다.
3. 소유 확인 방법으로 **HTML 태그** 또는 **HTML 파일 업로드** 중 하나를 선택합니다.
   - HTML 태그 방식: 발급된 `<meta name="naver-site-verification" ...>` 태그를 `index.html`의 `<head>`에 추가합니다.
   - HTML 파일 업로드 방식: 발급된 파일을 프로젝트 루트 폴더에 그대로 추가합니다.
4. 배포 후 "소유확인" 버튼을 클릭합니다.
5. 등록 완료 후 좌측 메뉴 **요청 → 사이트맵 제출**에서 `sitemap.xml`을 제출합니다.
6. **요청 → 웹마스터 도구 → RSS 제출**은 해당 없음(정적 사이트라 RSS 없음), 대신 "요청 → 웹페이지 수집"에서 주요 URL을 개별 제출하면 색인 속도를 높일 수 있습니다.

---

## 5단계. Google AdSense 신청 (참고)

애드센스는 사이트 등록만으로 자동 승인되지 않으며, 아래 조건을 충분히 갖춘 뒤 신청하는 것이 승인율을 높입니다.

- **트래픽 확보 우선**: 신규 사이트는 검색 유입이 거의 없는 상태에서 심사를 넣으면 반려되기 쉽습니다. Search Console/네이버 등록 후 최소 2~4주간 콘텐츠를 추가하며 자연 유입을 어느 정도 확보한 뒤 신청하는 것을 권장합니다.
- **콘텐츠 볼륨**: 현재 15개 글로 시작했지만, 꾸준히 추가해 20~30개 이상으로 늘리면 심사에 유리합니다.
- **필수 페이지 확인**: `privacy.html`(개인정보처리방침), `about.html`(사이트 소개), `contact.html`(문의)은 이미 포함되어 있습니다.
- **신청 절차**:
  1. [Google AdSense](https://www.google.com/adsense)에 가입하고 사이트 URL을 등록합니다.
  2. 발급받은 `<meta name="google-adsense-account" content="ca-pub-...">` 태그를 `index.html`의 `<head>`에 추가하고 배포합니다. (또는 자동광고 코드 스니펫을 `</body>` 직전에 추가)
  3. 심사에는 보통 며칠~몇 주가 소요됩니다.
  4. 승인 후에는 저장소 루트에 `ads.txt` 파일을 만들고 애드센스가 안내하는 내용(`google.com, pub-XXXXXXXXXXXXXXXX, DIRECT, f08c47fec0942fa0`)을 넣어야 광고가 정상적으로 수익화됩니다.

---

## 6단계. 콘텐츠 지속 운영 팁

- 새 글을 추가할 때는 `articles/` 폴더에 기존 파일을 복사해 구조를 유지하고, `index.html`과 `sitemap.xml`에 링크를 추가하는 것을 잊지 마세요.
- 실제 발생한 신종 수법은 경찰청, 금융감독원, 한국인터넷진흥원(KISA) 보도자료를 참고해 업데이트하면 정보의 신뢰도와 최신성을 유지할 수 있습니다.
- 검색 유입을 늘리려면 "OO 문자 사기", "OO 보이스피싱 대처법"처럼 사람들이 실제로 검색하는 구체적인 키워드로 글 제목을 잡는 것이 효과적입니다.
