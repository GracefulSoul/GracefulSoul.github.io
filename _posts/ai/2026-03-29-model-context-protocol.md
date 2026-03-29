---
title: "Model Context Protocol - MCP"
excerpt: "AI 애플리케이션을 위한 표준 프로토콜 Model Context Protocol에 대해 알아봅니다."
last_modified_at: 2026-03-29T11:32:00
header:
  image: /assets/images/ai/model-context-protocol.png
categories:
  - AI
tags:
  - Programming
  - MCP
  - AI
  - Protocol

toc: true
toc_ads: true
toc_sticky: true
---

# 소개

Model Context Protocol(MCP)는 AI 애플리케이션에서 대규모 언어 모델(LLM)과 외부 데이터 소스 및 도구를 연결하기 위한 개방형 프로토콜입니다. Anthropic에서 개발한 이 프로토콜은 AI 시스템이 보다 효과적으로 다양한 컨텍스트와 정보에 접근할 수 있도록 지원합니다.

# MCP란?

## 정의

Model Context Protocol은 클라이언트-서버 기반의 통신 프로토콜로, LLM 기반의 클라이언트 애플리케이션이 다양한 데이터 소스, API, 도구에 접근할 수 있도록 표준화된 방식을 제공합니다.

## 특징

- **표준화**: 다양한 AI 애플리케이션과 외부 시스템 간의 상호운용성을 보장
- **확장성**: 새로운 데이터 소스와 도구의 추가가 용이
- **보안**: 프로토콜 레벨에서 인증 및 권한 관리 지원
- **효율성**: 효과적인 컨텍스트 관리로 LLM의 성능 최적화

# 주요 개념

## 클라이언트(Client)

MCP 클라이언트는 LLM 기반의 애플리케이션으로서, 서버로부터 컨텍스트를 요청하고 받아 처리합니다. 예를 들어 Claude와 같은 LLM이 클라이언트 역할을 할 수 있습니다.

## 서버(Server)

MCP 서버는 로컬 파일 시스템, 데이터베이스, API, 또는 기타 정보 소스에 대한 액세스를 제공합니다. 서버는 클라이언트가 요청한 정보를 처리하여 응답합니다.

## 리소스(Resource)

리소스는 서버가 제공하는 데이터의 단위입니다. 파일, 쿼리 결과, API 응답 등이 리소스로 표현됩니다.

## 도구(Tool)

도구는 클라이언트가 실행할 수 있는 함수 또는 명령입니다. 외부 시스템 상태 변경, 데이터 저장, 작업 실행 등의 기능을 제공합니다.

## 제시문(Prompt)

제시문은 클라이언트에게 특정 컨텍스트에서 수행할 액션이나 분석을 제시합니다. 구조화된 지침 형태로 전달됩니다.

# 임베딩 및 구조

## 아키텍처

MCP는 JSON-RPC 2.0 기반의 메시지 프로토콜을 사용합니다:

```
┌─────────────────────────┐
│    LLM Client           │
│  (Claude, etc.)         │
└────────┬────────────────┘
         │ MCP Protocol
         │ (JSON-RPC)
         │
┌────────▼────────────────┐
│    MCP Server           │
│  - File System          │
│  - Database             │
│  - Web APIs             │
│  - Custom Tools         │
└─────────────────────────┘
```

## 메시지 흐름

1. **초기화(Initialize)**: 클라이언트와 서버가 서로의 기능을 선언
2. **리소스 요청(Resource Request)**: 클라이언트가 특정 리소스를 요청
3. **응답(Response)**: 서버가 요청된 데이터 반환
4. **도구 호출(Tool Call)**: 클라이언트가 도구 실행 요청
5. **실행 결과**: 서버가 도구 실행 결과 반환

# 주요 제품 및 도구

## Anthropic Claude

Claude API와 Claude for Enterprise는 MCP를 기본 지원하여, 사용자 정의 리소스와 도구 통합 가능합니다.

## VSCode AI Tools

Visual Studio Code의 AI 확장 기능들이 MCP를 활용하여 로컬 파일 시스템 및 개발 환경과 연동합니다.

## GitHub Copilot

GitHub Copilot이 코드 완성 및 제안 기능에서 MCP를 통해 프로젝트 컨텍스트에 접근합니다.

## 오픈소스 MCP 서버

- **git-mcp**: Git 저장소 정보 접근
- **postgres-mcp**: PostgreSQL 데이터베이스 쿼리
- **web-scraper-mcp**: 웹 크롤링 및 정보 추출
- **filesystem-mcp**: 파일 시스템 접근
- **slack-mcp**: Slack 통합

# 활용 샘플

## 1. 코드 분석 및 리뷰

```
사용자: "이 프로젝트의 main.py를 분석해서 보안 취약점을 찾아줄래?"

Claude (MCP 클라이언트):
├─ filesystem-mcp 서버에 main.py 파일 요청
├─ 파일 내용 수신
├─ 코드 분석
└─ 보안 취약점 리포트 제공
```

## 2. 데이터베이스 쿼리

```
사용자: "지난 3개월간 매출이 가장 높은 상위 5개 제품을 보여줄래?"

Claude (MCP 클라이언트):
├─ postgres-mcp 서버에 쿼리 요청
├─ SELECT query 실행
├─ 결과 수신
└─ 자연어로 결과 해석 및 설명
```

## 3. 멀티소스 정보 통합

```
사용자: "우리 깃허브 저장소의 최근 이슈와 로컬 프로젝트 문서를 바탕으로 현재 상태를 요약해줄래?"

Claude (MCP 클라이언트):
├─ git-mcp 서버: 최근 커밋 및 이슈 정보 요청
├─ filesystem-mcp 서버: README.md, DOCUMENTATION.md 요청
├─ 정보 통합 및 분석
└─ 종합 요약 제공
```

# 주요 코드

## Python에서 MCP 클라이언트 구현

```python
import json
import subprocess
import asyncio

class MCPClient:
    def __init__(self, server_command):
        """MCP 서버 초기화"""
        self.server_process = subprocess.Popen(
            server_command,
            stdin=subprocess.PIPE,
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True
        )
        self.request_id = 1

    async def send_request(self, method, params=None):
        """MCP 서버에 JSON-RPC 요청 전송"""
        request = {
            "jsonrpc": "2.0",
            "id": self.request_id,
            "method": method,
            "params": params or {}
        }
        self.request_id += 1

        # 요청 전송
        self.server_process.stdin.write(json.dumps(request) + "\n")
        self.server_process.stdin.flush()

        # 응답 읽기
        response_line = self.server_process.stdout.readline()
        response = json.loads(response_line)

        return response

    async def initialize(self):
        """MCP 서버와의 통신 초기화"""
        response = await self.send_request("initialize", {
            "protocolVersion": "2024-11-05",
            "capabilities": {
                "roots": {
                    "listChanged": True
                },
                "sampling": {}
            },
            "clientInfo": {
                "name": "example-client",
                "version": "1.0.0"
            }
        })
        return response

    async def list_resources(self):
        """서버에서 제공하는 리소스 목록 조회"""
        response = await self.send_request("resources/list")
        return response.get("result", {}).get("resources", [])

    async def read_resource(self, uri):
        """특정 리소스 읽기"""
        response = await self.send_request("resources/read", {
            "uri": uri
        })
        return response.get("result", {})

    async def list_tools(self):
        """서버에서 제공하는 도구 목록 조회"""
        response = await self.send_request("tools/list")
        return response.get("result", {}).get("tools", [])

    async def call_tool(self, name, arguments):
        """특정 도구 실행"""
        response = await self.send_request("tools/use", {
            "name": name,
            "arguments": arguments
        })
        return response.get("result", {})

# 사용 예제
async def main():
    # filesystem 서버 가정
    client = MCPClient(["node", "node_modules/.bin/mcp-server-filesystem"])

    # 초기화
    await client.initialize()

    # 리소스 목록 조회
    resources = await client.list_resources()
    print("Available resources:", resources)

    # 파일 읽기
    content = await client.read_resource("file:///path/to/file.txt")
    print("File content:", content)

    # 도구 목록 조회
    tools = await client.list_tools()
    print("Available tools:", tools)

    # 도구 실행
    result = await client.call_tool("grep", {
        "path": "/path/to/dir",
        "pattern": "error"
    })
    print("Tool result:", result)

# 실행
asyncio.run(main())
```

## Node.js에서 MCP 서버 구현

```javascript
const stdio = require("stdio");

class MCPServer {
  constructor() {
    this.requestHandlers = {
      "initialize": this.handleInitialize.bind(this),
      "resources/list": this.handleListResources.bind(this),
      "resources/read": this.handleReadResource.bind(this),
      "tools/list": this.handleListTools.bind(this),
      "tools/use": this.handleUseTool.bind(this)
    };
  }

  async handleInitialize(params) {
    return {
      protocolVersion: "2024-11-05",
      capabilities: {
        resources: {},
        tools: {},
        prompts: {}
      },
      serverInfo: {
        name: "example-server",
        version: "1.0.0"
      }
    };
  }

  async handleListResources(params) {
    return {
      resources: [
        {
          uri: "file:///home/user/documents",
          name: "Documents",
          description: "User documents directory",
          mimeType: "text/plain"
        }
      ]
    };
  }

  async handleReadResource(params) {
    const { uri } = params;
    // 실제 파일 시스템에서 리소스 읽기
    const fs = require("fs");
    const path = uri.replace("file://", "");

    try {
      const content = fs.readFileSync(path, "utf-8");
      return {
        contents: [
          {
            uri: uri,
            mimeType: "text/plain",
            text: content
          }
        ]
      };
    } catch (error) {
      return {
        error: {
          code: -32603,
          message: `Failed to read resource: ${error.message}`
        }
      };
    }
  }

  async handleListTools(params) {
    return {
      tools: [
        {
          name: "grep",
          description: "Search for patterns in files",
          inputSchema: {
            type: "object",
            properties: {
              path: {
                type: "string",
                description: "Directory or file path to search"
              },
              pattern: {
                type: "string",
                description: "Pattern to search for"
              },
              recursive: {
                type: "boolean",
                description: "Search recursively",
                default: true
              }
            },
            required: ["path", "pattern"]
          }
        }
      ]
    };
  }

  async handleUseTool(params) {
    const { name, arguments: args } = params;

    if (name === "grep") {
      const { path, pattern, recursive } = args;
      // 도구 로직 구현
      return {
        content: [
          {
            type: "text",
            text: `Search results for '${pattern}' in ${path}`
          }
        ]
      };
    }

    return {
      error: {
        code: -32601,
        message: `Unknown tool: ${name}`
      }
    };
  }

  async processMessage(message) {
    const { jsonrpc, id, method, params } = message;

    const handler = this.requestHandlers[method];
    if (!handler) {
      return {
        jsonrpc: "2.0",
        id: id,
        error: {
          code: -32601,
          message: `Method not found: ${method}`
        }
      };
    }

    try {
      const result = await handler(params);
      return {
        jsonrpc: "2.0",
        id: id,
        result: result
      };
    } catch (error) {
      return {
        jsonrpc: "2.0",
        id: id,
        error: {
          code: -32603,
          message: error.message
        }
      };
    }
  }
}

// 표준 입출력을 통한 MCP 통신
const server = new MCPServer();

process.stdin.on("data", async (data) => {
  const message = JSON.parse(data.toString());
  const response = await server.processMessage(message);
  process.stdout.write(JSON.stringify(response) + "\n");
});

console.error("MCP Server started");
```

# MCP의 장점

1. **상호운용성**: 표준화된 프로토콜로 다양한 시스템 연동 용이
2. **보안**: 프로토콜 레벨의 인증 및 권한 관리
3. **확장성**: 새로운 리소스와 도구의 쉬운 추가
4. **성능**: 효율적인 컨텍스트 관리로 LLM 토큰 사용량 최적화
5. **표준화**: 개발자 간 일관된 인터페이스 제공

# 활용 분야

- **소프트웨어 개발**: IDE 통합, 코드 리뷰, 문서 분석
- **데이터 분석**: 데이터베이스 쿼리, 통계 분석
- **콘텐츠 생성**: 검색 결과 기반 콘텐츠 작성
- **자동화**: 업무 자동화, 워크플로우 최적화
- **통합**: 엔터프라이즈 시스템 통합

# 참조

- [Anthropic MCP 공식 문서](https://modelcontextprotocol.io){:target="_blank"}
- [MCP GitHub 저장소](https://github.com/anthropics/model-context-protocol){:target="_blank"}
- [MCP 서버 구현 가이드](https://modelcontextprotocol.io/docs/server){:target="_blank"}
- [JSON-RPC 2.0 명세](https://www.jsonrpc.org/specification){:target="_blank"}
- [Claude API 문서 - MCP](https://docs.anthropic.com){:target="_blank"}

