# MCP 서버 등록 방법

한국일보 MCP 서버를 AI 클라이언트에 **원격 커넥터**로 등록하는 방법입니다.

> 각 클라이언트의 설정 UI 명칭·위치는 버전에 따라 달라질 수 있습니다.

| 항목 | 값 |
| --- | --- |
| 전송 방식 | streamable HTTP (원격 서버) |
| 인증 | 없음 (표준 MCP 클라이언트가 URL로 바로 접속) |
| 엔드포인트 | `https://mcp.hankookilbo.com/mcp` |
| 도구 | 모두 읽기 전용 (목록: [`tools.md`](tools.md)) |

---

## Claude Desktop

커스텀 커넥터(원격 MCP)로 등록합니다. 커스텀 커넥터는 Pro·Max·Team·Enterprise 플랜에서 사용할 수 있습니다.

1. 좌측 하단 프로필 → **설정(Settings)**
2. **커넥터(Connectors)** → **맞춤 설정(커스텀)**
3. 우측 상단 **`+`** → **커스텀 커넥터 추가**
4. 아래 값을 입력하고 **추가** → 도구 목록이 로딩되는지 확인
5. (선택) 권한을 **항상 허용**으로 변경 — 읽기 전용 도구만 제공하므로 안전합니다.

입력 값:

| 항목 | 값 |
| --- | --- |
| 이름 | 임의 (예: 한국일보 MCP) |
| 원격 MCP 서버 URL | `https://mcp.hankookilbo.com/mcp` |

- 인증이 없으므로 OAuth(클라이언트 ID·시크릿)·고급 설정은 입력하지 않아도 됩니다.

---

## Claude Code

CLI에서 원격(streamable HTTP) MCP 서버로 등록합니다. 인증이 없어 헤더 옵션은 필요 없습니다.

```bash
claude mcp add --transport http hankookilbo https://mcp.hankookilbo.com/mcp
```

- 기본 스코프는 `local` (현재 프로젝트, 본인 전용).
- 모든 프로젝트에서 쓰려면 `--scope user` 를 붙입니다:

```bash
claude mcp add --transport http hankookilbo --scope user https://mcp.hankookilbo.com/mcp
```

- 등록 확인: `claude mcp list` (상세: `claude mcp get hankookilbo`)
- Claude Code 안에서 상태 보기: 슬래시 명령 `/mcp`
- 제거: `claude mcp remove hankookilbo`

---

## ChatGPT (웹)

개발자 모드에서 원격 MCP 커넥터로 등록합니다. 개발자 모드는 Plus·Pro·Business·Enterprise·Education 계정(웹)에서 쓸 수 있고, ChatGPT는 원격(HTTPS) MCP 서버만 지원합니다.

1. [chatgpt.com](https://chatgpt.com) 접속 → 좌측 하단 프로필 → **설정(Settings)**
2. **보안 및 로그인(Security)** → **개발자 모드(Developer mode)** ON
3. 좌측 상단 **플러그인/커넥터** 진입
4. 우측 상단 **`+`** → **등록/만들기**
5. 아래 값을 입력해 등록

입력 값:

| 항목 | 값 |
| --- | --- |
| 이름 | 임의 (예: 한국일보 MCP) |
| 연결(MCP 서버 엔드포인트) | `https://mcp.hankookilbo.com/mcp` |
| 인증 | 없음 |

---

## 기타 MCP 클라이언트

원격/streamable HTTP MCP 서버를 지원하는 클라이언트면, 서버 URL로 `https://mcp.hankookilbo.com/mcp`(인증 없음)를 등록하면 됩니다.

## 참고

- 현재 권장 전송 방식은 **streamable HTTP**이며, 구형 **SSE**는 단계적으로 폐기되고 있습니다.
- 서버가 응답하는 경로는 `/mcp`입니다.
