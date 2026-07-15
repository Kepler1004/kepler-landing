# Kepler Academy — Malaysian Curriculum Landing Page

정적 랜딩페이지 (빌드 과정 없음). EN / BM / 中文 3개 언어 지원, 상담 버튼은 WhatsApp 직결.

## 파일 구조

```
index.html        구조 · 디자인 · 문구 (전부 여기)
images/
  kepler-logo.svg   로고 (원본 .ai에서 벡터 추출 — 무한 확대 가능)
  campus.webp       학원 외관 사진
  hero-students.*   히어로 학생 사진 — 아직 없음
  og.jpg            공유 미리보기 이미지 (1200×630) — 아직 없음
```

## 로컬에서 보기

VSCode 확장 **Live Server** 설치 → `index.html` 우클릭 → *Open with Live Server*

> `index.html`을 브라우저에 그냥 드래그해도 열리지만, 경로 문제로 이미지가 안 뜰 수 있습니다.

## 자주 하는 수정

### 문구 변경

`index.html` 하단 `<script>` 안의 **`T` 객체**를 수정합니다.

```js
const T = {
  en: { "hero.cta1": "Book my free academic review", ... },
  ms: { "hero.cta1": "Tempah semakan akademik percuma", ... },
  zh: { "hero.cta1": "预约免费学术评估", ... }
};
```

> ⚠️ HTML 본문에도 같은 문구가 보이지만, 페이지 로드 시 `T` 객체가 **덮어씁니다.**
> 반드시 `T` 객체를 고쳐야 화면에 반영됩니다.

### WhatsApp 번호

```js
const WHATSAPP_NUMBER = "60123456789";
```

국가코드 포함, **숫자만** (`+`, 공백, 하이픈 없이).
예: 011-1234 5678 → `60111234567 8` → `601112345678`

### FAQ 추가

각 언어의 `faqs` 배열에 한 줄씩 추가하면 자동 렌더링됩니다.

```js
faqs: [
  { q: "수업료는 얼마인가요?", a: "학년과 과목에 따라 다릅니다..." },
]
```

### 과목 추가

각 언어의 `stages` 배열 → 해당 단계의 `subs` 배열.

### 색상 변경

CSS 최상단 `:root` 의 변수만 고치면 사이트 전체에 반영됩니다.

```css
--kepler: #2a7bf0;   /* 메인 블루 */
--gold:   #fd7e01;   /* CTA · 강조 — 로고 오렌지 */
--ink:    #0b1c3f;   /* 딥 네이비 */
```

## 사진 교체

1. [squoosh.app](https://squoosh.app) 에서 **폭 1200px · WebP · Quality 75** 로 변환
2. `images/` 에 저장
3. `index.html` 의 `<img src="...">` 경로 수정

> 학생 얼굴이 나오는 사진은 **학부모 서면 동의**가 필요합니다 (말레이시아 PDPA).

## 배포

`main` 브랜치에 push하면 Vercel이 자동으로 재배포합니다 (약 1분).

```bash
git add .
git commit -m "수정 내용"
git push
```

**롤백** — Vercel → Deployments → 이전 배포 → *Promote to Production*

## 남은 작업

- [ ] `WHATSAPP_NUMBER` 실제 번호로 교체
- [ ] `og:image` / `og:url` / `canonical` 의 `https://example.com` → 실제 도메인
- [ ] `images/og.jpg` (1200×630) 제작
- [ ] 푸터 주소 · 전화번호
- [ ] 히어로 학생 사진 (1200×1200) — `index.html` 의 `.hero-ph` 블록 삭제 후 `<img>` 주석 해제
- [ ] 학원 외관 사진 원본으로 교체 (현재 326×216 — 확대되어 흐릿함)
- [ ] Google Analytics / Meta Pixel (광고 집행 시)
