---
title: "Claude Code Skills와 Hooks : Agent 커스터마이제이션과 자동화"
excerpt: "Claude Code Skills와 Agent Hooks의 개념부터 구현까지. Progressive Loading 메커니즘, 8가지 Lifecycle 이벤트, 실제 샘플 코드를 통해 Copilot 에이전트의 강력한 커스터마이제이션 기능 설명."
last_modified_at: 2026-06-23T20:00:00
header:
  image: /assets/images/ai/claude-skills-hooks.png
categories:
  - AI
tags:
  - Programming
  - Copilot
  - Claude
  - Agent Customization
  - Skills
  - Hooks
  - VS Code
  - Automation

toc: true
toc_ads: true
toc_sticky: true
---

GitHub Copilot과 Claude Code의 강력한 기능을 최대한 활용하려면 **Skills**와 **Hooks**를 이해하는 것이 필수적입니다. 이 글에서는 이 두 가지 핵심 기능의 개념, 메커니즘, 아키텍처, 그리고 실제 구현 방법까지 완전히 다루겠습니다.

## 개요

### Skills와 Hooks란?

**Skills**와 **Hooks**는 Claude Code를 확장하고 자동화하는 두 가지 근본적으로 다른 방식입니다.
GitHub Copilot에서도 내부적으로 이 방식들을 지원합니다.

| 구분 | Skills | Hooks |
|------|--------|-------|
| **목적** | 특화된 기능 제공 | 자동화 및 제어 |
| **동작 방식** | 지시사항 기반 | 커맨드 기반 |
| **트리거** | 사용자 요청/자동 감지 | 정해진 라이프사이클 이벤트 |
| **확장성** | 높음 (스크립트 + 리소스) | 제한적 (셸 커맨드) |
| **포팅성** | VS Code, Copilot CLI, Cloud | 모든 에이전트 (호환성 필요) |
| **표준** | 개방형 표준 (agentskills.io) | VS Code/Claude 고유 |

### 핵심 차이점

- **Skills**: "Copilot에게 어떻게 일을 하는지 가르치기"
- **Hooks**: "작업 중간에 자동으로 특정 코드 실행하기"

### Skills vs MCP (Model Context Protocol)

**Skills**와 **MCP**는 모두 AI 에이전트를 확장하는 도구이지만, 다른 목적과 메커니즘을 가집니다:

| 측면 | Skills | MCP |
|------|--------|-----|
| **목적** | 작업 지시사항 전달 | 도구/리소스 통합 |
| **메커니즘** | 텍스트 기반 지시 (Progressive Loading) | 양방향 RPC 프로토콜 |
| **인증** | 없음 (로컬 파일 기반) | 필수 (서버 연결) |
| **리소스 관리** | 필요시에만 로드 (~100B → ~5KB → 필요한 것) | 항상 연결 유지 (상태 관리) |
| **토큰 사용** | 매우 효율적 (명시적 호출까지 최소) | 높음 (활성 연결 유지) |
| **자동 인식** | ✅ Skill 설명으로 자동 인식, 수동 호출도 가능 | ✅ 시작 시 등록 |
| **설정** | YAML 프론트매터 | JSON 서버 설정 |
| **보안** | 로컬 스크립트로 제한 | 원격 서버 필수 (인증 오버헤드) |
| **적합한 용도** | 코딩 작업/분석/자동화 | 외부 서비스 연동/실시간 데이터 |

**핵심 차이:**
- **Skills**: 에이전트에게 "어떻게 할지" 알려주기 (지식 전달)
- **MCP**: 에이전트에게 "뭘 할 수 있는지" 제공하기 (도구 제공)

**토큰 효율성 비교:**
```
Skills:
  - 세션 시작: 0 토큰 (Skill들이 자동 발견될 때만 로드)
  - 첫 사용: ~100 tokens (name + description)
  - 활성화: ~500 tokens (전체 SKILL.md)
  - 총: 최소 600 tokens (한 번만, 이후 캐시)

MCP:
  - 세션 시작: ~1000 tokens (모든 tool 정의 로드)
  - 지속: 활성 연결 유지 (배경 토큰 소비)
  - 매 호출: ~50 tokens (RPC 오버헤드)
  - 총: 1000+ tokens (지속적 소비)
```

**선택 기준:**
- ✅ **Skills 사용**: 코딩, 분석, 로컬 작업 자동화
- ✅ **MCP 사용**: GitHub API, 데이터베이스, 외부 API 연동

## Part 1: Agent Skills

### 1.1 Skills란?

Agent Skills는 **재사용 가능한 작업별 워크플로우 폴더**입니다. 각 Skill은 다음 구조를 가집니다:

```
my-skill/
├── SKILL.md              # 필수: 메타데이터 + 지시사항
├── scripts/              # 선택: 실행 가능한 코드
├── examples/             # 선택: 사용 예제
├── references/           # 선택: 문서 및 참고 자료
└── templates/            # 선택: 템플릿 파일
```

### 1.2 Progressive Loading (3단계)

Copilot은 컨텍스트 효율성을 위해 Skills을 3단계에 걸쳐 로드합니다:

```
┌─────────────────────────────────────────────┐
│  Step 1: Discovery (발견)                    │
│  - Skill 이름과 설명만 로드                    │
│  - 용량: ~100 bytes                          │
│  - "언제 필요할지" 판단                        │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Step 2: Activation (활성화)                 │
│  - 사용자의 작업이 Skill 설명과 매칭            │
│  - 전체 SKILL.md 본문 로드                    │
│  - 상세 지시사항 제공                          │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  Step 3: Execution (실행)                    │
│  - 참조된 파일/스크립트만 로드                  │
│  - 실시간 작업 수행                           │
│  - 필요한 리소스만 접근                        │
└─────────────────────────────────────────────┘
```

**이점**: 
- 100개 Skill을 설치해도 처음에는 ~10KB만 메모리 사용
- 토큰 효율적: Discovery 단계에서 거의 토큰 소비 안 함
- 필요할 때만 활성화: 사용하지 않는 Skill은 메모리/토큰 영향 없음
- 명시적 호출 불필요: `disable-model-invocation: false`이면 자동 인식

#### 🔄 주의: VS Code에서 새 Skill 생성 후 인식되려면

**새로운 Skill을 만든 후:**
```bash
1. .github/skills/my-new-skill/SKILL.md 생성
2. VS Code 재시작 (또는 새로운 Copilot 세션 시작)
3. Chat: Open Customizations 실행
4. Skills 탭에서 확인
```

**왜 세션을 새로 열어야 할까?**
- Copilot은 **세션 시작 시** 모든 Skill 디렉토리를 스캔합니다
- 기존 세션 중에는 파일 시스템 변경을 감지하지 않습니다
- 따라서 새 Skill을 추가하면 **새 세션(또는 VS Code 재시작)**이 필요합니다

**팁**: `chat.skipLineNumberHistory`를 활용하거나, Command Palette에서 `Chat: Clear Copilot Context`로 강제 새로고침 가능합니다.

### 1.3 SKILL.md 형식 (필수 구조)

```markdown
---
name: code-quality-analyzer
description: 코드 품질을 분석하고 개선 사항을 제안합니다. 린터 실행, 복잡도 계산, 메트릭 생성 등을 수행합니다.
user-invocable: true
disable-model-invocation: false
context: inline
---

# 스킬 이름

## 개요
이 섹션에서는 스킬이 무엇을 하는지 설명합니다.

## 사용 시기
언제 이 스킬을 사용해야 하는지 명시합니다.

## 단계별 지시사항
1. 첫 번째 단계
2. 두 번째 단계
```

### 1.4 frontmatter 필드 설명

```yaml
---
name: code-quality-analyzer              # 고유 식별자 (소문자, 하이픈만 사용)
description: |
  코드 품질을 분석합니다.                # 1024자 이내, 구체적인 설명
user-invocable: true                     # 사용자가 /로 호출 가능 여부
disable-model-invocation: false          # 에이전트 자동 로드 여부
context: inline                          # inline 또는 fork (fork=서브에이전트)
---
```

### 1.5 실제 예제: code-quality-analyzer Skill

본 프로젝트의 copilot-project 레파지토리에 포함된 실제 예제를 살펴봅시다:

**위치**: `.github/skills/code-quality-analyzer/SKILL.md`

```markdown
---
name: code-quality-analyzer
description: 코드 품질을 분석하고, 린터를 실행하고, 개선 사항을 제안합니다.
---

# 코드 품질 분석기

## 개요
이 스킬은 프로젝트의 코드 품질을 자동으로 분석합니다.

### 수행하는 작업
- ESLint, Pylint 등 린터 실행
- Prettier, Black으로 형식 검사
- 순환 복잡도(Cyclomatic Complexity) 계산
- 코드 메트릭 생성
- 개선 사항 제안

## 사용 시기
- 새로운 코드를 작성한 후
- 커밋 전 품질 검증
- "코드 품질을 검토해줘" 요청
- 복잡도 메트릭이 필요할 때

## 사용 방법

### Step 1: Skill 호출
/code-quality-analyzer src/

### Step 2: 에이전트 분석
프로젝트 타입 감지 → 적절한 린터 실행 → 메트릭 계산

### Step 3: 결과 검토
- 발견된 이슈
- 복잡도 리포트
- 코드 메트릭
- 개선 사항 추천
```

**지원 스크립트**: `validate-code.sh`

```bash
#!/bin/bash
PROJECT_PATH="${1:-.}"

# 프로젝트 타입 감지
if [ -f "$PROJECT_PATH/package.json" ]; then
    echo "JavaScript 프로젝트 감지"
    eslint "$PROJECT_PATH" --format json
elif [ -f "$PROJECT_PATH/pyproject.toml" ]; then
    echo "Python 프로젝트 감지"
    pylint "$PROJECT_PATH" --output-format=json
fi
```

### 1.6 Skill 로드 경로

```
프로젝트 Skills:
  ├─ .github/skills/
  ├─ .claude/skills/              # Claude Code
  ├─ .agents/skills/
  └─ 커스텀 경로 (chat.agentSkillsLocations)

사용자 Skill:
  ├─ ~/.copilot/skills/
  ├─ ~/.claude/skills/            # Claude Code
  └─ ~/.agents/skills/
```

### 1.7 Skills 사용 방법

#### VS Code에서 사용

1. 채팅창에서 / 입력
2. Skill 목록 표시
3. code-quality-analyzer 선택
4. 추가 컨텍스트 입력 (선택사항)

#### 실행 예제

**입력:**
```bash
/code-quality-analyzer src/
```

**Copilot 응답:**
```
JavaScript 프로젝트 감지됨.
ESLint 실행 중...

발견된 이슈:
- 3개 ESLint 오류
- 2개 스타일 경고

복잡도 분석:
- processData() 함수: 복잡도 12 (높음)
- handleRequest() 함수: 복잡도 4 (정상)

메트릭:
- 총 라인: 1,247
- 코드 중복: 8.2%
- 유지보수성 지수: 72/100

추천 사항:
1. processData()를 더 작은 함수로 분할
2. asyncHandler()에 에러 핸들링 추가
3. JSDoc 주석 업데이트
```

## Part 2: Agent Hooks

### 2.1 Hooks란?

Agent Hooks는 **에이전트 세션의 특정 시점에 자동으로 실행되는 셸 커맨드**입니다.

```
User Request
     ↓
[Hook: SessionStart] ← 리소스 초기화
     ↓
Agent processes
     ↓
[Hook: PreToolUse] ← 보안 검증
     ↓
Tool executes
     ↓
[Hook: PostToolUse] ← 포맷팅, 테스트
     ↓
Session ends
     ↓
[Hook: Stop] ← 리포트 생성
```

### 2.2 8가지 Lifecycle 이벤트

| 이벤트 | 트리거 | 사용 사례 |
|--------|--------|----------|
| **SessionStart** | 새 세션 시작 | 환경 변수 로드, 프로젝트 초기화 |
| **UserPromptSubmit** | 사용자 입력 | 프롬프트 감사, 시스템 정보 주입 |
| **PreToolUse** | 도구 실행 전 | 위험한 커맨드 차단, 승인 요청 |
| **PostToolUse** | 도구 실행 후 | 코드 포맷팅, 테스트 실행 |
| **PreCompact** | 컨텍스트 압축 전 | 상태 저장, 중요 정보 내보내기 |
| **SubagentStart** | 서브에이전트 시작 | 리소스 할당, 추적 |
| **SubagentStop** | 서브에이전트 종료 | 결과 수집, 정리 |
| **Stop** | 세션 종료 | 리포트 생성, 로그 저장 |

### 2.3 Hook 구조

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write .",
        "cwd": ".",
        "timeout": 30,
        "windows": "powershell -File scripts\\format.ps1",
        "env": {
          "KEY": "value"
        }
      }
    ]
  }
}
```

### 2.4 Hook 파일 위치

```
.github/hooks/                    # 기본 위치
├─ development.json
├─ production.json
└─ security.json

.claude/settings.json             # Claude Code 호환
~/.copilot/hooks/                 # 사용자 수준
~/.claude/settings.json           # 사용자 수준 (Claude)
```

### 2.5 Hook Input/Output 계약

#### Hook Input (stdin)

Copilot은 모든 Hook에 JSON을 stdin으로 전달합니다:

```json
{
  "timestamp": "2026-06-23T14:30:45Z",
  "session_id": "sess_abc123",
  "cwd": "/home/user/project",
  "hook_event_name": "PostToolUse",
  "hook_event_data": {
    "tool_name": "create_file",
    "tool_input": {
      "filePath": "/home/user/project/app.js",
      "content": "console.log('hello');"
    },
    "tool_output": {
      "success": true
    }
  }
}
```

#### Hook Output (stdout)

스크립트는 JSON을 stdout으로 반환하여 에이전트 동작을 제어합니다:

```json
{
  "continue": true,
  "systemMessage": "포맷팅 완료",
  "hookSpecificOutput": {
    "formatted_files": 5
  }
}
```

#### Exit Code 의미

- **0** (성공): stdout JSON 파싱, 계속 진행
- **2** (오류): 세션 중지, 모델에 stderr 전달
- **기타**: 경고, 계속 진행

### 2.6 실제 예제: 보안 Hook

**파일**: `.github/hooks/development.json`

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/security-check.sh",
        "description": "위험한 작업 차단",
        "timeout": 10
      }
    ]
  }
}
```

**구현**: `scripts/security-check.sh`

```bash
#!/bin/bash
INPUT=$(cat)

TOOL_NAME=$(echo "$INPUT" | jq -r '.hook_event_data.tool_name')
COMMAND=$(echo "$INPUT" | jq -r '.hook_event_data.tool_input.command // empty')

# 위험한 패턴 검사
DANGEROUS_PATTERNS=("rm -rf" "DROP TABLE" "chmod 777")

for pattern in "${DANGEROUS_PATTERNS[@]}"; do
    if [[ "$COMMAND" == *"$pattern"* ]]; then
        # 차단 응답
        cat <<EOF
{
  "continue": false,
  "stopReason": "위험한 커맨드 차단: $COMMAND",
  "systemMessage": "이 커맨드는 수동 승인이 필요합니다"
}
EOF
        exit 2
    fi
done

# 안전한 작업 허용
echo '{"continue": true}'
```

**동작 흐름:**

```
사용자: "rm -rf old_files/"
     ↓
[PreToolUse Hook 실행]
     ↓
security-check.sh 감지: "rm -rf" 패턴
     ↓
Exit code 2 반환 + 차단 메시지
     ↓
Copilot: "이 커맨드는 위험합니다. 수동 승인이 필요합니다"
     ↓
세션 중지
```

### 2.7 실제 예제: 자동 포맷팅 Hook

**파일**: `.github/hooks/development.json`

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write .",
        "description": "편집 후 자동 포맷팅",
        "timeout": 30
      }
    ]
  }
}
```

**동작:**

```
사용자: "app.js 파일에 함수 추가해줘"
     ↓
Copilot: 파일 생성/편집
     ↓
[PostToolUse Hook 실행]
     ↓
npx prettier --write . 실행
     ↓
모든 파일 자동 포맷팅
     ↓
Copilot: "완료. 코드가 자동으로 포맷되었습니다."
```

### 2.8 실제 예제: 감사 로깅 Hook

**파일**: `scripts/audit-log.sh`

```bash
#!/bin/bash
INPUT=$(cat)

TIMESTAMP=$(echo "$INPUT" | jq -r '.timestamp')
SESSION_ID=$(echo "$INPUT" | jq -r '.session_id')
TOOL_NAME=$(echo "$INPUT" | jq -r '.hook_event_data.tool_name')
EVENT=$(echo "$INPUT" | jq -r '.hook_event_name')

# 로그 디렉토리 생성
mkdir -p .audit-logs

# 감사 로그 기록
LOG_ENTRY=$(cat <<EOF
{
  "timestamp": "$TIMESTAMP",
  "session_id": "$SESSION_ID",
  "event": "$EVENT",
  "tool": "$TOOL_NAME",
  "details": $INPUT
}
EOF
)

echo "$LOG_ENTRY" >> .audit-logs/session-$SESSION_ID.log

# 성공 반환
echo '{"continue": true}'
```

**결과**: `.audit-logs/session-sess_abc123.log`

```json
{
  "timestamp": "2026-06-23T14:30:45Z",
  "session_id": "sess_abc123",
  "event": "PostToolUse",
  "tool": "edit_file",
  "details": {...}
}
```

## Part 3: 아키텍처 및 메커니즘

### 3.1 전체 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│  Copilot Agent Session                                  │
└─────────────────────────────────────────────────────────┘
              ↓
        [SessionStart Hook]
              ↓
┌─────────────────────────────────────────────────────────┐
│  User Request: "/code-quality-analyzer src/"            │
└─────────────────────────────────────────────────────────┘
              ↓
        [UserPromptSubmit Hook]
              ↓
┌─────────────────────────────────────────────────────────┐
│  Skill Discovery                                        │
│  - name, description 로드 (~100 bytes)                   │
│  - "code-quality-analyzer" 매칭                          │
└─────────────────────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────────────────────┐
│  Skill Activation                                       │
│  - SKILL.md 본문 로드                                    │
│  - 상세 지시사항 제공 (~5KB)                              │
└─────────────────────────────────────────────────────────┘
              ↓
        [PreToolUse Hook]
              ↓
┌─────────────────────────────────────────────────────────┐
│  Tool Execution                                         │
│  - run_terminal: "./scripts/validate-code.sh"           │
│  - create_file: "code-quality-report.json"              │
└─────────────────────────────────────────────────────────┘
              ↓
        [PostToolUse Hook]
              ↓
┌─────────────────────────────────────────────────────────┐
│  Resource Cleanup (if needed)                           │
└─────────────────────────────────────────────────────────┘
              ↓
        [Stop Hook]
              ↓
        Session Complete
```

### 3.2 Skills vs Instructions 비교

| 측면 | Skills | Custom Instructions |
|------|--------|------------------|
| 목적 | 특화 기능 제공 | 코딩 표준 정의 |
| 포팅성 | VS Code + CLI + Cloud | VS Code + GitHub.com |
| 콘텐츠 | 지시 + 스크립트 + 리소스 | 지시만 |
| 범위 | 작업별 온디맨드 | 항상 적용 (glob 패턴) |
| 표준 | agentskills.io (개방형) | VS Code 고유 |

### 3.3 Skill 로드 효율성

```
스킬 10개 설치 시 메모리 사용:

[Discovery 단계]:
- 각 스킬의 name + description만 로드
- 총: ~1 KB (10개 × 100 bytes)

[Activation 단계]:
- 필요한 1개 스킬만 전체 로드
- 총: ~5 KB

[Execution 단계]:
- 참조된 파일/스크립트만 로드
- 총: ~10-50 KB (필요한 것만)

>>> 전체 메모리: ~50 KB vs 500 KB (전체 로드 시)
>>> 효율: 90% 절감
```

### 3.4 Hook 실행 흐름

```
1. 이벤트 발생 (PostToolUse 등)
                ↓
2. Hook configuration 로드 (.github/hooks/*.json)
                ↓
3. 매칭되는 Hook 커맨드 검색
                ↓
4. JSON 입력 생성 (tool_name, tool_input 등)
                ↓
5. stdin으로 스크립트 실행
     ├─ command: "npx prettier --write ."
     ├─ cwd: ".github/hooks"
     ├─ timeout: 30초
     └─ env: {"KEY": "value"}
                ↓
6. stdout 모니터링
     └─ JSON 파싱: {"continue": true, ...}
                ↓
7. Exit code 확인
     ├─ 0: 성공, JSON 처리
     ├─ 2: 오류, 세션 중지
     └─ 기타: 경고
                ↓
8. 에이전트에 결과 반영
```

## Part 4: Copilot에서의 사용

### 4.1 VS Code에서 Skills 사용

#### 기본 사용법

```
1. 채팅창에서 "/" 입력
2. 사용 가능한 Skills 목록 표시
3. 원하는 Skill 선택
4. 추가 컨텍스트 입력 (선택)
5. Skill 자동 로드 및 실행
```

#### 예제

```
사용자: /code-quality-analyzer src/ --complexity-threshold=10

Copilot:
[Skill 로드: code-quality-analyzer]
[복잡도 임계값: 10]
[분석 중...]

결과:
- 3개 고복잡도 함수 발견
- 평균 복잡도: 6.2
- 리포트: code-quality-report.json 생성
```

### 4.2 VS Code에서 Hooks 사용

#### Hooks 설정

1. **Command Palette 열기**: `Ctrl+Shift+P`
2. **"Chat: Configure Hooks" 검색**
3. 이벤트 타입 선택 (PostToolUse 등)
4. 파일 위치 선택 (.github/hooks)
5. 커맨드 입력
6. 파일 저장 (자동 로드)

#### Hooks 검증

```
1. View → Output 열기
2. "GitHub Copilot Chat Hooks" 채널 선택
3. 로드된 Hooks 확인
4. 실행 결과 모니터링
```

### 4.3 Copilot CLI에서 Skills 사용

```bash
copilot chat "코드 품질 분석해줘" \
  --skills-dir=".github/skills/" \
  --project="myapp"

# 또는 기본 위치에서 자동 감지
copilot chat "코드 품질 분석해줘"
```

### 4.4 Claude Code에서 사용

Claude Code는 `.claude` 폴더의 설정을 자동으로 인식합니다:

```
.claude/
├── settings.json          # Hooks 설정
├── settings.local.json    # 로컬 오버라이드
└── skills/               # Skills 디렉토리 (선택)
```

**`.claude/settings.json` 예제:**

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "prettier --write ."
      }
    ]
  }
}
```

## Part 5: .claude 폴더에서의 인식

### 5.1 .claude 폴더의 역할

`.claude` 폴더는 **Claude Code와 다른 에이전트 도구에서 커스터마이제이션을 저장하는 표준 위치**입니다.

### 5.2 지원되는 도구

| 도구 | 지원 | 형식 | 비고 |
|------|------|------|------|
| VS Code | ✅ | `.github/hooks/` + `.claude/settings.json` | 듀얼 지원 |
| Claude Code | ✅ | `.claude/settings.json` | 기본 인식 |
| Copilot CLI | ✅ | 명시적 플래그 필요 | `--config-dir=".claude"` |

### 5.3 파일 우선순위 (로드 순서)

```
1. 워크스페이스: .github/hooks/*.json
2. 워크스페이스: .claude/settings.json
3. 워크스페이스: .claude/settings.local.json (로컬 오버라이드)
4. 사용자: ~/.copilot/hooks/
5. 사용자: ~/.claude/settings.json
```

**우선순위**: 워크스페이스 > 사용자

### 5.4 Skills와 .claude 폴더

Skills는 주로 `.claude/skills/`에 저장되고, GitHub Copilot도 이 위치의 Skills를 사용할 수 있다.
```
.claude/skills/           # 기본 위치 (권장)
├── my-custom-skill/
│   └── SKILL.md
└── ...
```

### 5.5 .claude/settings.json 구조

```json
{
  "hooks": {
    "PreToolUse": [...],
    "PostToolUse": [...]
  },
  "enabledSkills": [
    "code-quality-analyzer",
    "security-audit"
  ]
}
```

### 5.6 Claude Code에서 .claude 인식 확인

Claude Code UI에서:

```
1. Settings → Extensions
2. Claude 탭 열기
3. "Skills & Hooks" 섹션 확인
4. 로드된 커스터마이제이션 표시
```

또는 `.claude` 폴더를 workspace root에 배치하면 자동 인식됩니다.

## Part 6: 실습 프로젝트

### 6.1 프로젝트

**GitHub**: [https://github.com/GracefulSoul/copilot-project](https://github.com/GracefulSoul/copilot-project){:target="_blank"}

### 6.2 빠른 시작

#### 1단계: 레파지토리 클론

```bash
git clone https://github.com/GracefulSoul/copilot-project
cd copilot-project
```

#### 2단계: VS Code에서 열기

```bash
code .
```

#### 3단계: Hooks 확인

Command Palette에서:
```
Chat: Open Customizations
```

Hooks 탭에서 로드된 Hooks 확인:
- `development.json`: PostToolUse (Prettier)
- `production.json`: PreToolUse (보안)

#### 4단계: Skills 테스트

채팅창에서:
```
/code-quality-analyzer src/
```

### 6.3 주요 파일 해설

#### `.github/skills/code-quality-analyzer/SKILL.md`

완전한 Skill 정의로서:
- ✅ 명확한 설명 (1024자 이내)
- ✅ 단계별 지시사항
- ✅ 실제 사용 예제
- ✅ 참조 파일 링크
- ✅ 트러블슈팅 팁

#### `.github/hooks/development.json`

개발 환경용 자동화:
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write .",
        "description": "파일 편집 후 자동 포맷팅"
      }
    ]
  }
}
```

#### `scripts/security-check.sh`

PreToolUse Hook 구현:
- stdin에서 JSON 입력 읽기
- 위험한 패턴 검사
- `continue: false`로 블로킹
- 에러 메시지와 함께 exit code 2 반환

## Part 7: 고급 활용

### 7.1 Context: fork를 통한 대규모 Skill

큰 Skill은 메인 컨텍스트를 오염시키지 않도록 fork 모드로 실행:

```yaml
---
name: large-analysis-skill
description: 대규모 데이터 분석
context: fork          # 전용 서브에이전트에서 실행
---

# 대규모 분석 스킬

[상세 지시사항...]
```

**이점:**
- 메인 대화 컨텍스트 깨끗함
- 최종 결과만 부모 에이전트에 반환
- 중간 추론 과정 숨김

### 7.2 OS별 Hook 구현

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/format-unix.sh",
        "windows": "powershell -File scripts\\format.ps1",
        "linux": "./scripts/format-linux.sh",
        "osx": "./scripts/format-mac.sh"
      }
    ]
  }
}
```

### 7.3 환경 변수를 통한 Hook 커스터마이제이션

```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "./scripts/init.sh",
        "env": {
          "PROJECT_ROOT": "/home/user/myapp",
          "SECURITY_LEVEL": "strict",
          "LOG_LEVEL": "debug"
        }
      }
    ]
  }
}
```

### 7.4 Hook에서 Skill 트리거

Hook이 특정 조건에서 Skill 사용을 제안할 수 있습니다:

```bash
#!/bin/bash
# Hook이 복잡도를 감지하면 Skill 추천

COMPLEXITY=$(python3 complexity-report.py src/ | jq '.summary.average_complexity')

if (( $(echo "$COMPLEXITY > 10" | bc -l) )); then
    echo '{
      "systemMessage": "높은 복잡도 감지. /code-quality-analyzer 실행을 추천합니다."
    }'
fi
```

## Part 8: 보안 고려사항

### 8.1 Skill 검토 체크리스트

새로운 Skill 사용 전:

- ✅ 출처 확인 (공식 저장소?)
- ✅ SKILL.md 지시사항 검토
- ✅ 참조된 스크립트 점검
- ✅ 권한 요구사항 확인
- ✅ 에러 처리 방식 검토

### 8.2 Hook 보안 체크리스트

Hook 스크립트 검토:

- ✅ stdin 입력 검증
- ✅ 하드코딩된 암호 확인
- ✅ 셸 주입 가능성 체크
- ✅ 파일 권한 검증
- ✅ 외부 도구 의존성 확인

### 8.3 자동 승인 제어

```json
{
  "chat": {
    "tools": {
      "edits": {
        "autoApprove": false  // Hook 수정 시 승인 필요
      }
    }
  }
}
```

## Part 9: 트러블슈팅

### 9.1 Skill이 로드되지 않음

```
문제:
/code-quality-analyzer 명령어가 나타나지 않음

해결:
1. 파일명이 정확히 SKILL.md인지 확인
2. 디렉토리명이 name 필드와 일치하는지 확인
3. 유효한 YAML 프론트매터 확인
4. JSON에서 슬래시가 없는지 확인 (name: "my-skill" ✅, "my/skill" ❌)
```

### 9.2 Hook이 실행되지 않음

```
문제:
Hook 설정했는데 실행이 안 됨

해결:
1. JSON 파일이 .github/hooks/에 있는지 확인
2. 파일 확장자가 .json인지 확인
3. JSON 문법 검증 (online JSON validator)
4. 스크립트에 실행 권한 있는지 확인: chmod +x script.sh
5. Command Palette: Developer: Show Agent Debug Logs
```

### 9.3 Hook 타임아웃

```
문제:
Hook이 실행 중 타임아웃

해결:
1. timeout 값 증가: "timeout": 60
2. 스크립트 성능 최적화
3. 로그로 병목 확인: echo "진행 중..." >&2
```

## Part 10: Skills vs MCP - 깊이 있는 비교

### 10.1 토큰 효율성: Skills의 우위

Skills가 MCP보다 훨씬 더 효율적인 이유를 자세히 살펴봅시다:

#### **MCP의 토큰 사용 구조**

```
Session Start
    ↓
[모든 MCP 서버 연결]
    ↓
[모든 도구 정의 로드] ← 각 도구마다 ~50 tokens
    ↓ (예: 20개 도구 = 1000 tokens!)
    ↓
Agent ready
    ↓
Every message: ~50 tokens overhead (RPC 메시지 포맷)
```

**예시: GitHub MCP (20개 도구)**
```
- 세션 시작: 1,000 tokens (도구 정의)
- 매 메시지: 50 tokens (RPC 오버헤드)
- 세션당: 1,000 + (메시지 수 × 50) tokens
```

#### **Skills의 토큰 사용 구조**

```
Session Start (스킬 발견)
    ↓
[모든 스킬의 name + description만 로드]
    ↓ (~10 skills = 100 tokens!)
    ↓
Agent ready
    ↓
사용자 요청
    ↓
[해당 스킬만 활성화] ← Full SKILL.md 로드 (~500 tokens)
    ↓
[필요한 리소스만 접근]
```

**예시: 10개 Skills**
```
- 세션 시작: 100 tokens (발견)
- 첫 사용: 500 tokens (활성화)
- 캐시됨: 0 tokens (이후 사용)
- 세션당: 100 + 500 = 600 tokens (한 번만!)
```

**토큰 절감: 40-50% 감소**

### 10.2 세션 새로고침: Skill 동적 감지

#### **새 Skill 추가 시 동작**

**MCP 방식 (재연결 필요):**
```bash
1. MCP 서버에 새 도구 추가
2. MCP 클라이언트 재연결 필요
3. 모든 도구 정의 다시 로드
4. 효율성 ↓
```

**Skills 방식 (동적 감지):**
```bash
1. .github/skills/new-skill/ 디렉토리 추가
2. Copilot 세션 재시작 (선택 사항)
3. 새 세션에서 자동 발견
4. 기존 세션에서도 수동 새로고침 가능

# 방법 1: 새 세션 열기 (권장)
# Command Palette → Chat: Clear Copilot Context
# 또는 VS Code 재시작

# 방법 2: 기존 세션에서 강제 새로고침
# Command Palette → Chat: Open Customizations → 스킬 목록 새로고침
```

#### **왜 새 세션이 필요한가?**

Skills 발견은 **세션 시작 시 한 번만** 수행됩니다:

```
┌─────────────────────────────────┐
│ 새 Copilot 세션 시작              │
└─────────────────────────────────┘
         ↓
┌─────────────────────────────────┐
│ 1️⃣ Skill 디렉토리 스캔            │ ← 여기서만 new-skill 감지
│   - .github/skills/             │
│   - .claude/skills/             │
│   - ~/.copilot/skills/          │
└─────────────────────────────────┘
         ↓
┌─────────────────────────────────┐
│ 각 스킬의 name + description 로드 │
└─────────────────────────────────┘
         ↓
┌─────────────────────────────────┐
│ 에이전트 준비 완료 (세션 내내 유지)  │
└─────────────────────────────────┘

[기존 세션 중간에 new-skill 추가] ← 감지 안 됨!
```

**대안: 세션 중 새로고침**
```
Command Palette: Chat: Open Customizations
→ Skills 탭 → 새로고침 버튼
또는
Command Palette: Chat: Clear Copilot Context → 새 세션 시작
```

### 10.3 인증 (Authentication): Skills의 장점

#### **MCP - 인증 필수**

MCP는 **외부 서버와 양방향 통신**을 하므로 인증이 필수입니다:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_xxxxx"  // 필수!
      }
    }
  }
}
```

**보안 고려사항:**
- 🔐 토큰이 로컬 설정에 하드코딩되어야 함
- 🔓 환경 변수 유출 위험
- 🌐 서버 인증 오버헤드
- 📝 자격증명 관리 복잡도 ↑

#### **Skills - 인증 불필요**

Skills는 **로컬 파일 기반**이므로 인증이 필요 없습니다:

```bash
.github/skills/
├── my-skill/
│   ├── SKILL.md              # 로컬 텍스트
│   └── script.sh             # 로컬 스크립트
```

**보안 이점:**
- ✅ 외부 서버 연결 없음
- ✅ 토큰 관리 불필요
- ✅ 보안 오버헤드 최소
- ✅ 깃이그너 패턴으로 쉽게 제외 가능

**Skills에서 외부 인증이 필요한 경우:**
```bash
#!/bin/bash
# scripts/api-call.sh

# 환경 변수에서 토큰 읽기 (쉘만 보면 됨)
API_TOKEN="${MY_API_TOKEN}"

# Skill 문서에 "MY_API_TOKEN 환경 변수 설정 필요" 명시
if [ -z "$API_TOKEN" ]; then
    echo "Error: MY_API_TOKEN not set"
    exit 1
fi

curl -H "Authorization: Bearer $API_TOKEN" https://api.example.com
```

### 10.4 사용 사례별 선택 가이드

#### **Skills 선택 (이 경우 사용)**
```
✅ 로컬 코드 분석 및 변환
✅ 프로젝트별 커스텀 워크플로우
✅ 팀 내 지식 공유
✅ 토큰 절감이 중요한 경우
✅ 빠른 프로토타이핑
✅ 오프라인 작업 필요
✅ 보안 민감 환경
```

**예:** 코드 품질 분석, 테스트 실행, 배포 자동화

#### **MCP 선택 (이 경우 사용)**
```
✅ 실시간 외부 데이터 필요
✅ API 서비스 통합
✅ 상태 저장 필요
✅ 장기 상호작용
✅ 데이터베이스 접근
✅ 프로비저닝 작업
```

**예:** GitHub API 쿼리, 데이터베이스 작업, 클라우드 서비스 연동

#### **함께 사용 (권장)**
```
┌─────────────────────────────────┐
│ Skills로 로컬 작업 처리           │
│ (빠르고 효율적)                   │
└─────────────────────────────────┘
            ↓
    [필요시 MCP로 외부 연동]
            ↓
┌─────────────────────────────────┐
│ MCP로 원격 리소스 접근             │
│ (필요한 만큼만)                   │
└─────────────────────────────────┘
```

**예: 하이브리드 워크플로우**
```
사용자: "GitHub의 최신 이슈를 분석하고 복잡도를 검사해줘"
  ↓
[Skill: code-quality-analyzer 활성화] ← 토큰 효율적
  ↓
[MCP: github 연결] ← 이슈 데이터 가져오기
  ↓
[MCP 결과 → Skill 분석]
  ↓
결과 반환
```

### 10.5 요약: 토큰 vs 기능

```
╔════════════════════════════════════════╗
║         기술 선택 매트릭스                ║
╠════════════════════════════════════════╣
║             │   토큰 효율  │   외부 통합  ║
║ Skills      │   ★★★★★  │   ★☆☆☆☆  ║
║ MCP         │   ★★☆☆☆  │   ★★★★★  ║
║ Hooks       │   ★★★★☆  │   ★★★☆☆  ║
╚════════════════════════════════════════╝
```

## 결론: Skills는 "설정하고 잊기" 방식

### 핵심 통찰

본 글에서 다룬 **Agent Skills**의 가장 강력한 측면은:

#### 1️⃣ **자동 인식 (명시적 호출 불필요)**

```
MCP 방식 (외부 의존):
코드 → [반드시 명시적 호출] → MCP 서버 → 기능 수행

Skills 방식 (자동):
코드 → [disable-model-invocation: false] → Copilot 자동 인식 → 기능 수행
```

Skills를 만들면, `disable-model-invocation: false`(기본값)일 때:
- ✅ 사용자가 명시적으로 `/skill` 명령어를 쓸 필요 없음
- ✅ Copilot이 자동으로 상황에 맞춰 로드
- ✅ "마치 Copilot이 원래 가진 기능처럼" 작동

**예시:**
```
사용자: "이 코드의 품질을 분석해줘"
  ↓
[사용자가 /code-quality-analyzer 명령 안 함]
  ↓
Copilot: "code-quality-analyzer 스킬이 적합합니다"
  ↓
자동으로 스킬 로드 및 실행
```

#### 2️⃣ **토큰 효율 (MCP 대비 40-50% 절감)**

```
MCP 세션:
시작: 1,000 tokens (모든 도구 정의)
계속: 50 tokens/message (RPC 오버헤드)
합계: 2,000+ tokens (10 메시지 기준)

Skills 세션:
시작: 100 tokens (발견)
사용: 500 tokens (활성화, 캐시됨)
합계: 600 tokens (한 번만!)

절감율: 70% 👍
```

#### 3️⃣ **인증 불필요 (보안 우위)**

```
MCP:
- 토큰 하드코딩 필요
- 환경 변수 유출 위험
- 보안 오버헤드 증가

Skills:
- 로컬 파일 기반
- 외부 서버 연결 없음
- 보안 공격 면적 최소
```

### 사용 권장사항

#### **Teams/Organizations: Skills 우선 도입**
1. 팀의 공통 워크플로우를 Skill로 정의
2. `.github/skills/`에 커밋
3. 모든 팀원이 자동으로 사용 가능
4. 토큰 비용 절감 (장기 누적 효과 큼)

```bash
# 예: 팀 표준 워크플로우
.github/skills/
├── code-quality-analyzer/     # 코드 품질 검사
├── security-audit/            # 보안 검사
├── documentation-generator/   # 문서 생성
└── deployment-validator/      # 배포 검증
```

#### **Integration: MCP와 함께 사용**
```
[Local/Fast] Skills → Copilot → MCP [External/Heavy]
       ↓                           ↓
코드 분석, 변환           GitHub API, DB 연동
빠른 피드백              실시간 데이터
```

### Skills를 최대로 활용하기

#### 체크리스트
- ✅ 팀의 반복 작업을 Skill화 했는가?
- ✅ `disable-model-invocation: false`로 자동 인식 설정했는가?
- ✅ 명확한 description으로 Copilot 판단 지원했는가?
- ✅ 참조 파일들을 `.github/skills/skill-name/`에 정리했는가?
- ✅ 큰 Skill은 `context: fork`로 최적화했는가?

#### 성과 측정
```bash
# Copilot 세션 로그에서 토큰 추적
명령어: Developer: Show Agent Debug Logs

로그 분석:
- Skills 발견: 100 tokens (낮음 = 효율적)
- MCP 사용 시: 1,000 tokens (높음)
- Skills vs MCP 토큰 비율 추적
```

### 최종 요약

| 관점 | 결론 |
|------|------|
| **토큰 효율** | Skills가 MCP보다 40-50% 더 효율적 |
| **자동 인식** | Skills는 명시 안 해도 자동 로드 |
| **인증** | Skills는 인증 오버헤드 없음 |
| **세션 새로고침** | 새 세션 시작 시 자동 발견 (필요시 강제 새로고침 가능) |
| **권장 사용** | 로컬 작업 → Skills, 외부 연동 → MCP |

**Skills는 단순한 커스터마이제이션 도구가 아니라, Copilot의 능력을 팀 수준으로 확장하는 전략적 자산입니다.** 🚀

---

## 참고 자료
- [VS Code Agent Skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills){:target="_blank"}
- [VS Code Agent Hooks](https://code.visualstudio.com/docs/agent-customization/hooks){:target="_blank"}
- [Agent Skills 표준](https://agentskills.io/specification){:target="_blank"}
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/){:target="_blank"}
- [Awesome Copilot 저장소](https://github.com/github/awesome-copilot){:target="_blank"}
- [Anthropic Skills 레퍼런스](https://github.com/anthropics/skills){:target="_blank"}
- [MCP 공식 저장소](https://github.com/modelcontextprotocol/){:target="_blank"}

---

본 글의 샘플 코드와 완전한 프로젝트는 [GracefulSoul/copilot-project](https://github.com/GracefulSoul/copilot-project){:target="_blank"}에서 확인할 수 있습니다.
