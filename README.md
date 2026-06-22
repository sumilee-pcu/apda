# 아프냐 나도아프다

내가 의존하는 AI 서비스들의 컨디션을 한눈에 보는 상태 대시보드. 쟤가 아프면 내 작업도 멈춘다.

각 서비스의 공식 status 페이지(Atlassian Statuspage / Instatus)의 공개 JSON을 브라우저에서 직접 읽어와 "환자 컨디션" 메타포로 보여준다. 백엔드 없이 동작하는 순수 정적 사이트.

## 컨디션 등급

| 등급 | 의미 |
|------|------|
| 건강함 | 정상 (operational) |
| 미열 | 경미한 이상 (minor) |
| 몸살 | 주요 기능 저하 (major) |
| 응급실 | 심각한 장애 (critical) |
| 정기검진 | 점검 중 (maintenance) |
| 무응답 | 상태 확인 불가 |

## 모니터링 대상 (18)

- 모델 · API: OpenAI, Claude, Perplexity, Cohere, Groq, Replicate
- 음성 · 미디어: ElevenLabs, Stability AI, Runway
- 코딩 도구: Cursor, Windsurf, Lovable, v0, GitHub
- 인프라: Pinecone, LangSmith, Supabase, Vercel

## 서비스 추가

`index.html`의 `PATIENTS` 배열에 항목을 추가한다.

```js
{ name: "표시이름", host: "status.example.com", type: "statuspage", cat: "카테고리" }
```

- `type`: `statuspage`(`/api/v2/status.json`) 또는 `instatus`(`/summary.json`)
- CORS가 열려 있어야 브라우저에서 직접 호출된다. (대부분의 Statuspage/Instatus는 `Access-Control-Allow-Origin: *`)

## 로컬 실행

정적 파일이라 서버만 있으면 된다.

```sh
python3 -m http.server 5793 --directory .
```

## 배포

Vercel에 정적 사이트로 그대로 배포.
