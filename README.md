# bom-landing

GitHub Pages로 배포되는 랜딩 콘텐츠 리포지토리입니다. 관리자는 `docs/content/landing.json` 파일을 직접 수정/업로드(커밋/PR)하여 콘텐츠를 배포합니다.

## 구조

- `docs/index.html`: landing.json을 간단히 미리보기 하는 페이지
- `docs/content/landing.json`: 실제 배포되는 랜딩 콘텐츠 JSON
- `docs/assets/`: 이미지 등 정적 자산 경로(예: `/assets/hero.jpg`)
- `schema/landing.schema.json`: JSON 스키마(유효성 검사 용도)
- `.github/workflows/validate.yml`: PR/푸시 시 스키마 검증

Pages URL 예시: `https://<user>.github.io/bom-landing/`
JSON URL: `https://<user>.github.io/bom-landing/content/landing.json`

## 운영 방법

1. `docs/content/landing.json` 수정
2. PR 생성 → CI(스키마 검증) 통과 확인 → 리뷰/머지
3. 머지 후 1~2분 내 Pages 반영

프론트엔드는 위 JSON URL을 `fetch`하여 콘텐츠를 표시합니다.

```js
const url = 'https://<user>.github.io/bom-landing/content/landing.json?v=' + new Date().toISOString().slice(0,10);
const res = await fetch(url, { cache: 'no-store' });
const data = await res.json();
// data.sections를 렌더링
```

## 참고

- 필요 시 캐시 무효화를 위해 쿼리파라미터 버전 또는 파일명 버전을 사용하세요.
- 비공개 운영이 필요하면 Pages 대신 S3/CloudFront 등 대안을 고려하세요.

