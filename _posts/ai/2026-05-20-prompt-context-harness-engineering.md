---
title: "Prompt Engineering, Context Engineering, Harness Engineering"
excerpt: "AI 에이전트 개발의 핵심 기술: 프롬프트 엔지니어링, 컨텍스트 엔지니어링, 하네스 엔지니어링에 대한 완벽한 가이드"
last_modified_at: 2026-05-20T17:00:00
header:
  image: /assets/images/ai/prompt-context-harness.png
categories:
  - AI
tags:
  - Programming
  - AI
  - Prompt Engineering
  - Context Engineering
  - Harness Engineering
  - LLM
  - Security
  - Agent

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---

# 개요

AI 에이전트를 효과적으로 개발하고 운영하기 위해서는 세 가지 핵심 엔지니어링 분야를 이해해야 합니다:

1. **프롬프트 엔지니어링** - 모델의 출력을 최적화하는 지시문 설계
2. **컨텍스트 엔지니어링** - 관련 정보를 효율적으로 관리하고 활용
3. **하네스 엔지니어링** - 에이전트의 동작을 제어하고 검증하는 프레임워크

이 글에서는 세 가지 기술의 개념, 메커니즘, 아키텍처, 실제 사용 사례, 보안 고려사항을 다룹니다.

---

# Part 1: 프롬프트 엔지니어링 (Prompt Engineering)

## 개념

**프롬프트 엔지니어링**은 자연어를 통해 LLM에 명확한 지시를 전달하여 원하는 결과를 얻도록 하는 기술입니다.

### 핵심 원칙

| 원칙 | 설명 |
|:-----|:-----|
| **명확성** | 모호함 없이 명확한 지시 제공 |
| **구체성** | 구체적인 요구사항과 제약조건 명시 |
| **구조화** | 단계별, 계층적 지시 구조 |
| **예제** | Few-shot 학습을 통한 명확한 예시 |
| **역할 정의** | 에이전트의 역할과 책임 명시 |

## 메커니즘

### 프롬프트 구조

```
┌───────────────────────────────────┐
│  1. 역할 및 목적 (Role & Purpose)   │
│     "당신은 Python 전문가입니다"     │
├───────────────────────────────────┤
│  2. 컨텍스트 정보 (Context)         │
│     "FastAPI 프로젝트 중심"         │
├───────────────────────────────────┤
│  3. 작업 설명 (Task)               │
│     "다음 코드를 검토하세요"         │
├───────────────────────────────────┤
│  4. 제약조건 (Constraints)         │
│     "10줄 이내로 요약하세요"         │
├───────────────────────────────────┤
│  5. 출력 형식 (Output Format)      │
│     "JSON 형식으로 응답하세요"       │
├───────────────────────────────────┤
│  6. 예제 (Examples)                │
│     "예: {example}"               │
└───────────────────────────────────┘
```

### 프롬프트 기법

| 기법 | 설명 | 효과 |
|:-----|:-----|:-----|
| **Zero-shot** | 예제 없이 직접 지시 | 빠르지만 정확도 낮음 |
| **Few-shot** | 2-5개 예제 제공 | 정확도 향상 |
| **Chain-of-Thought** | 단계별 추론 과정 명시 | 복잡한 작업에 효과적 |
| **Role Playing** | 특정 역할 가정 | 출력 스타일 제어 |
| **Prompt Chaining** | 여러 프롬프트 연결 | 복잡한 작업 분해 |

## 아키텍처

### 프롬프트 관리 시스템

```
┌────────────────────────────────────────┐
│         프롬프트 관리 시스템              │
├────────────────────────────────────────┤
│ ┌──────────────────────────────────┐   │
│ │  프롬프트 템플릿 저장소             │   │
│ │  - 버전 관리                      │   │
│ │  - 메타데이터                      │   │
│ └──────────────────────────────────┘   │
├────────────────────────────────────────┤
│ ┌──────────────────────────────────┐   │
│ │  프롬프트 최적화 엔진               │   │
│ │  - 동적 변수 대체                  │   │
│ │  - 토큰 계산                      │   │
│ │  - 품질 평가                      │   │
│ └──────────────────────────────────┘   │
├────────────────────────────────────────┤
│ ┌──────────────────────────────────┐   │
│ │  결과 평가 및 피드백                │   │
│ │  - 출력 검증                      │   │
│ │  - 품질 점수 계산                  │   │
│ │  - 개선 제안                      │   │
│ └──────────────────────────────────┘   │
└────────────────────────────────────────┘
```

## 활용 샘플

### 샘플 1: 코드 리뷰 프롬프트

```
당신은 20년 경력의 소프트웨어 아키텍트입니다.

다음 Python 코드를 기술적으로 검토하세요:
1. 코드 품질 평가 (1-10)
2. 발견된 문제 (심각도: Critical/High/Medium/Low)
3. 성능 최적화 기회
4. 보안 고려사항
5. 개선 방안

응답 형식:
{
  "quality_score": <1-10>,
  "issues": [{"severity": "...", "description": "...", "fix": "..."}],
  "optimizations": ["..."],
  "security_notes": ["..."],
  "summary": "..."
}

코드:
```python
def process_data(data):
    result = []
    for item in data:
        if item > 0:
            result.append(item * 2)
    return result
```
```

### 샘플 2: 기술 문서 작성 프롬프트

```
역할: 기술 문서 전문 작가

작업:
다음 정보를 바탕으로 사용자 가이드를 작성하세요.

제약:
- 마크다운 형식
- 초보자를 위한 명확한 설명
- 각 섹션마다 실제 예제 포함
- 500-1000 단어

구조:
1. 개요
2. 설치
3. 기본 사용법
4. 고급 설정
5. 문제 해결

시작 정보:
- 제품명: FastAPI
- 주요 기능: 빠른 웹 API 개발
- 타겟 사용자: Python 개발자
```

## 주요 코드

### 프롬프트 템플릿 관리자

```python
from typing import Dict, List, Optional
import re

class PromptTemplate:
    """프롬프트 템플릿 클래스"""
    
    def __init__(self, template: str, variables: List[str]):
        self.template = template
        self.variables = variables
        self.version = "1.0"
    
    def render(self, **kwargs) -> str:
        """변수를 치환하여 최종 프롬프트 생성"""
        result = self.template
        
        for var in self.variables:
            if var not in kwargs:
                raise ValueError(f"Missing variable: {var}")
            
            result = result.replace(f"{{{var}}}", str(kwargs[var]))
        
        return result
    
    def get_variable_count(self) -> int:
        """변수 개수 반환"""
        return len(self.variables)

class PromptManager:
    """프롬프트 관리 시스템"""
    
    def __init__(self):
        self.templates: Dict[str, PromptTemplate] = {}
    
    def register_template(self, name: str, template: PromptTemplate):
        """템플릿 등록"""
        self.templates[name] = template
    
    def get_prompt(self, name: str, **kwargs) -> str:
        """프롬프트 생성"""
        if name not in self.templates:
            raise ValueError(f"Template not found: {name}")
        
        return self.templates[name].render(**kwargs)
    
    def estimate_tokens(self, prompt: str) -> int:
        """토큰 수 예측 (단순 계산)"""
        words = len(prompt.split())
        return int(words * 1.3)  # 대략 30% 오버헤드

# 사용 예제
manager = PromptManager()

code_review_template = PromptTemplate(
    template="""당신은 {expertise} 전문가입니다.

다음 {language} 코드를 검토하세요:
{code}

{constraints}

JSON 형식으로 응답하세요.""",
    variables=["expertise", "language", "code", "constraints"]
)

manager.register_template("code_review", code_review_template)

prompt = manager.get_prompt(
    "code_review",
    expertise="Python 아키텍트",
    language="Python",
    code="def hello(): return 'world'",
    constraints="10줄 이내로 요약"
)

print(f"토큰 예측: {manager.estimate_tokens(prompt)}")
```

## 보안 고려사항

### 프롬프트 주입 공격 방지

```python
import re

class PromptSecurityValidator:
    """프롬프트 보안 검증"""
    
    INJECTION_PATTERNS = [
        r"(?i)ignore.*instruction",
        r"(?i)override.*rule",
        r"(?i)execute.*code",
        r"(?i)system.*prompt",
        r"\{\{.*\}\}",  # Template injection
        r"\[\[.*\]\]",
    ]
    
    @classmethod
    def is_safe(cls, prompt: str) -> bool:
        """주입 공격 패턴 검사"""
        for pattern in cls.INJECTION_PATTERNS:
            if re.search(pattern, prompt):
                return False
        return True
```

---

# Part 2: 컨텍스트 엔지니어링 (Context Engineering)

## 개념

**컨텍스트 엔지니어링**은 AI 에이전트가 작업을 수행할 때 필요한 정보를 효율적으로 관리, 검색, 조직화하는 기술입니다.

### 컨텍스트의 유형

| 유형 | 설명 | 예제 |
|:-----|:-----|:-----|
| **작업 컨텍스트** | 현재 수행 중인 작업 | 코드 리뷰, 문서 작성 |
| **히스토리 컨텍스트** | 이전 상호작용 기록 | 대화 히스토리 |
| **도메인 컨텍스트** | 분야별 전문 지식 | 기술 가이드, 코딩 표준 |
| **사용자 컨텍스트** | 사용자 선호도, 프로필 | 사용자 역할, 권한 |
| **환경 컨텍스트** | 시스템 상태 정보 | 시간, 리소스, 설정 |

## 메커니즘

### 컨텍스트 윈도우 관리

```
LLM 토큰 제한: 100,000 토큰
├─ 시스템 프롬프트: 500 토큰 (필수)
├─ 도메인 지식: 10,000 토큰 (우선순위 높음)
├─ 히스토리: 30,000 토큰 (우선순위 중간)
├─ 현재 입력: 5,000 토큰 (필수)
└─ 예약: 54,500 토큰 (출력 공간)
```

### 컨텍스트 검색 (Retrieval)

```python
from typing import List, Tuple, Dict
import math

class ContextRetriever:
    """관련 컨텍스트 검색"""
    
    def __init__(self, documents: List[Dict]):
        self.documents = documents
        self.embeddings = self._generate_embeddings(documents)
    
    def _generate_embeddings(self, documents):
        """임베딩 생성 (간단한 예제)"""
        return [{
            'id': i,
            'text': doc['text'],
            'keywords': doc['text'].lower().split()
        } for i, doc in enumerate(documents)]
    
    def retrieve(self, query: str, top_k: int = 3) -> List[Dict]:
        """쿼리와 관련된 상위 k개 컨텍스트 반환"""
        query_keywords = set(query.lower().split())
        scores = []
        
        for i, emb in enumerate(self.embeddings):
            overlap = len(query_keywords & set(emb['keywords']))
            score = overlap / (len(query_keywords) + len(emb['keywords']))
            scores.append((i, score))
        
        top_results = sorted(scores, key=lambda x: x[1], reverse=True)[:top_k]
        return [self.documents[idx] for idx, _ in top_results]
```

## 아키텍처

### 컨텍스트 관리 시스템

```
┌───────────────────────────────────┐
│     사용자 입력 (User Input)        │
└────────────┬──────────────────────┘
             │
             ▼
┌───────────────────────────────────┐
│  컨텍스트 수집 (Collection)         │
│  - 히스토리 검색                    │
│  - 관련 문서 검색                   │
│  - 메타데이터 추출                  │
└────────────┬──────────────────────┘
             │
             ▼
┌───────────────────────────────────┐
│  컨텍스트 랭킹 (Ranking)            │
│  - 관련성 점수                      │
│  - 최신성 고려                      │
│  - 중요도 평가                      │
└────────────┬──────────────────────┘
             │
             ▼
┌───────────────────────────────────┐
│  컨텍스트 압축 (Compression)        │
│  - 요약화                          │
│  - 중복 제거                       │
│  - 토큰 최적화                      │
└────────────┬──────────────────────┘
             │
             ▼
┌───────────────────────────────────┐
│  최종 컨텍스트 (Final Context)      │
└───────────────────────────────────┘
```

## 활용 샘플

### 샘플: 멀티턴 대화 컨텍스트 관리

```python
from dataclasses import dataclass, field
from datetime import datetime
from typing import List, Dict

@dataclass
class ConversationContext:
    """멀티턴 대화 컨텍스트"""
    
    conversation_id: str
    user_id: str
    task_type: str
    
    messages: List[Dict] = field(default_factory=list)
    memory: Dict = field(default_factory=dict)
    metadata: Dict = field(default_factory=dict)
    
    def add_message(self, role: str, content: str):
        """메시지 추가"""
        self.messages.append({
            'role': role,
            'content': content,
            'timestamp': datetime.now().isoformat(),
            'turn': len(self.messages) // 2
        })
    
    def get_recent_context(self, turns: int = 5) -> str:
        """최근 n개 턴의 컨텍스트 반환"""
        recent_msgs = self.messages[-(turns*2):]
        
        context = "최근 대화:\n"
        for msg in recent_msgs:
            context += f"{msg['role']}: {msg['content']}\n"
        
        return context
    
    def store_session_memory(self, key: str, value: any):
        """세션 메모리 저장"""
        self.memory[key] = {
            'value': value,
            'stored_at': datetime.now().isoformat(),
            'turn': len(self.messages) // 2
        }
```

## 주요 코드

### 벡터 기반 컨텍스트 검색

```python
import numpy as np
from typing import List

class VectorContextRetriever:
    """벡터 기반 컨텍스트 검색"""
    
    def __init__(self):
        self.documents = []
        self.vectors = []
    
    def add_document(self, text: str):
        """문서 추가"""
        self.documents.append(text)
        vector = self._simple_vectorize(text)
        self.vectors.append(vector)
    
    def _simple_vectorize(self, text: str) -> np.ndarray:
        """간단한 벡터화"""
        words = text.lower().split()
        vector = np.zeros(100)
        
        for word in words[:100]:
            idx = hash(word) % 100
            vector[idx] += 1
        
        return vector / (np.linalg.norm(vector) + 1e-10)
    
    def retrieve(self, query: str, top_k: int = 3) -> List[str]:
        """유사한 문서 검색"""
        query_vector = self._simple_vectorize(query)
        
        similarities = []
        for i, doc_vector in enumerate(self.vectors):
            similarity = np.dot(query_vector, doc_vector)
            similarities.append((i, similarity))
        
        top_results = sorted(similarities, key=lambda x: x[1], reverse=True)[:top_k]
        return [self.documents[idx] for idx, _ in top_results]
```

## 보안 고려사항

### 컨텍스트 누수 방지

```python
class ContextSecurityManager:
    """컨텍스트 보안 관리"""
    
    SENSITIVE_PATTERNS = [
        r'password\s*[:=]',
        r'api[_-]?key',
        r'secret',
        r'token',
        r'credential',
    ]
    
    @staticmethod
    def is_sensitive(text: str) -> bool:
        """민감한 정보 감지"""
        import re
        text_lower = text.lower()
        
        for pattern in ContextSecurityManager.SENSITIVE_PATTERNS:
            if re.search(pattern, text_lower):
                return True
        
        return False
    
    @staticmethod
    def redact(text: str) -> str:
        """민감한 정보 마스킹"""
        import re
        
        text = re.sub(r'(sk_|pk_)[A-Za-z0-9]{20,}', '[REDACTED_KEY]', text)
        text = re.sub(
            r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}',
            '[REDACTED_EMAIL]',
            text
        )
        text = re.sub(r'\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}', '[REDACTED_IP]', text)
        
        return text
```

---

# Part 3: 하네스 엔지니어링 (Harness Engineering)

## 개념

**하네스 엔지니어링**은 AI 에이전트의 동작을 제어, 모니터링, 검증하는 프레임워크입니다. 에이전트가 정해진 규칙과 제약 조건 내에서 동작하도록 보장합니다.

### 하네스의 역할

| 역할 | 설명 | 목적 |
|:-----|:-----|:-----|
| **제어 (Control)** | 에이전트 동작 조절 | 의도된 행동만 수행 |
| **검증 (Validation)** | 출력 검증 | 품질 보증 |
| **모니터링 (Monitoring)** | 실시간 추적 | 문제 조기 발견 |
| **로깅 (Logging)** | 모든 작업 기록 | 감시 및 분석 |
| **복구 (Recovery)** | 오류 처리 | 시스템 안정성 |

## 메커니즘

### 에이전트 실행 파이프라인

```
┌────────────────────┐
│ 사용자 요청          │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 입력 검증 및 살균    │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 컨텍스트 준비        │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 프롬프트 생성        │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ LLM 호출            │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 출력 파싱           │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 검증 및 필터링       │
└──────────┬─────────┘
           │
           ▼
┌────────────────────┐
│ 결과 반환           │
└────────────────────┘
```

## 아키텍처

### 하네스 시스템 아키텍처

```
┌───────────────────────────────────────────┐
│           에이전트 하네스 시스템             │
├───────────────────────────────────────────┤
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │    정책 엔진 (Policy Engine)         │  │
│  │  - 실행 규칙                         │  │
│  │  - 권한 관리                         │  │
│  │  - 리소스 할당                       │  │
│  └─────────────────────────────────────┘  │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │    검증 엔진 (Validation Engine)     │  │
│  │  - 출력 검증                         │  │
│  │  - 품질 평가                         │  │
│  │  - 안전성 확인                       │  │
│  └─────────────────────────────────────┘  │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │    모니터링 엔진 (Monitoring Engine)  │  │
│  │  - 리소스 사용량 추적                  │  │
│  │  - 성능 메트릭                        │  │
│  │  - 이상 탐지                         │  │
│  └─────────────────────────────────────┘  │
│                                           │
│  ┌─────────────────────────────────────┐  │
│  │    로깅 엔진 (Logging Engine)        │  │
│  │  - 모든 작업 기록                     │  │
│  │  - 감시 추적                         │  │
│  │  - 분석 데이터                       │  │
│  └─────────────────────────────────────┘  │
│                                           │
└───────────────────────────────────────────┘
```

## 활용 샘플

### 샘플: 에이전트 하네스 구현

```python
from typing import Dict, Any, Optional
from enum import Enum
import json
import time

class ValidationResult:
    """검증 결과"""
    
    def __init__(self, is_valid: bool, errors: list = None):
        self.is_valid = is_valid
        self.errors = errors or []

class AgentHarness:
    """에이전트 실행 하네스"""
    
    def __init__(self, agent_config: Dict):
        self.config = agent_config
        self.execution_log = []
        self.metrics = {
            'total_executions': 0,
            'successful': 0,
            'failed': 0,
            'total_time': 0.0,
        }
    
    def execute(self, task: Dict, context: Dict) -> Dict:
        """에이전트 작업 실행"""
        start_time = time.time()
        
        try:
            # 1단계: 입력 검증
            validation = self._validate_input(task)
            if not validation.is_valid:
                return {
                    'success': False,
                    'errors': validation.errors,
                    'execution_time': time.time() - start_time
                }
            
            # 2단계: 컨텍스트 준비
            prepared_context = self._prepare_context(context)
            
            # 3단계: 프롬프트 생성
            prompt = self._build_prompt(task, prepared_context)
            
            # 4단계: LLM 호출
            llm_output = self._call_llm(prompt)
            
            # 5단계: 출력 파싱
            parse_result = self._parse_output(llm_output)
            if not parse_result['success']:
                return {
                    'success': False,
                    'error': 'Failed to parse output',
                    'execution_time': time.time() - start_time
                }
            
            # 6단계: 최종 검증
            final_validation = self._validate_output(parse_result['data'])
            if not final_validation.is_valid:
                return {
                    'success': False,
                    'errors': final_validation.errors,
                    'execution_time': time.time() - start_time
                }
            
            execution_time = time.time() - start_time
            self._log_execution(task, parse_result['data'], True, execution_time)
            self.metrics['successful'] += 1
            self.metrics['total_time'] += execution_time
            
            return {
                'success': True,
                'data': parse_result['data'],
                'execution_time': execution_time
            }
            
        except Exception as e:
            execution_time = time.time() - start_time
            self._log_execution(task, str(e), False, execution_time)
            self.metrics['failed'] += 1
            
            return {
                'success': False,
                'error': str(e),
                'execution_time': execution_time
            }
        finally:
            self.metrics['total_executions'] += 1
    
    def _validate_input(self, task: Dict) -> ValidationResult:
        """입력 검증"""
        errors = []
        
        if 'type' not in task:
            errors.append("Missing 'type' field")
        
        if 'payload' not in task:
            errors.append("Missing 'payload' field")
        
        if len(str(task.get('payload', ''))) > 100000:
            errors.append("Payload too large")
        
        return ValidationResult(len(errors) == 0, errors)
    
    def _prepare_context(self, context: Dict) -> Dict:
        """컨텍스트 준비"""
        cleaned = {}
        for key, value in context.items():
            if not key.startswith('_'):
                cleaned[key] = value
        
        return cleaned
    
    def _build_prompt(self, task: Dict, context: Dict) -> str:
        """프롬프트 생성"""
        return f"""
        Task Type: {task.get('type')}
        Payload: {task.get('payload')}
        Context: {json.dumps(context)}
        """
    
    def _call_llm(self, prompt: str) -> str:
        """LLM 호출"""
        return "Mock LLM Response"
    
    def _parse_output(self, output: str) -> Dict:
        """출력 파싱"""
        try:
            if '{' in output and '}' in output:
                json_str = output[output.find('{'):output.rfind('}')+1]
                data = json.loads(json_str)
                return {'success': True, 'data': data}
            
            return {'success': True, 'data': {'text': output}}
        except json.JSONDecodeError:
            return {'success': False, 'error': 'Failed to parse JSON'}
    
    def _validate_output(self, output: Dict) -> ValidationResult:
        """출력 검증"""
        errors = []
        
        if not output:
            errors.append("Empty output")
        
        if 'markdown' in output and not isinstance(output['markdown'], str):
            errors.append("Invalid markdown field")
        
        return ValidationResult(len(errors) == 0, errors)
    
    def _log_execution(self, task, result, success, exec_time):
        """실행 로깅"""
        self.execution_log.append({
            'task': task,
            'result': result,
            'success': success,
            'execution_time': exec_time,
            'timestamp': time.time()
        })
    
    def get_metrics(self) -> Dict:
        """메트릭 조회"""
        return {
            **self.metrics,
            'average_time': (
                self.metrics['total_time'] / self.metrics['successful']
                if self.metrics['successful'] > 0 else 0
            ),
            'success_rate': (
                self.metrics['successful'] / self.metrics['total_executions'] * 100
                if self.metrics['total_executions'] > 0 else 0
            )
        }
```

## 주요 코드

### 검증 프레임워크

```python
from abc import ABC, abstractmethod
from typing import Any

class Validator(ABC):
    """검증자 기본 클래스"""
    
    @abstractmethod
    def validate(self, data: Any) -> ValidationResult:
        pass

class JSONValidator(Validator):
    """JSON 검증"""
    
    def __init__(self, schema: Dict):
        self.schema = schema
    
    def validate(self, data: Any) -> ValidationResult:
        import json
        
        errors = []
        
        try:
            if isinstance(data, str):
                json.loads(data)
            
            for key in self.schema.get('required', []):
                if key not in data:
                    errors.append(f"Missing required field: {key}")
            
        except json.JSONDecodeError as e:
            errors.append(f"Invalid JSON: {str(e)}")
        
        return ValidationResult(len(errors) == 0, errors)
```

## 보안 고려사항

### 하네스 보안 정책

```python
class SecurityPolicy:
    """보안 정책"""
    
    def __init__(self):
        self.policies = {
            'max_execution_time': 30,
            'max_tokens': 4000,
            'allowed_domains': ['api.openai.com', 'api.anthropic.com'],
            'blocked_keywords': ['password', 'secret', 'private_key'],
            'require_authentication': True,
            'rate_limit_per_minute': 60,
        }
    
    def check_execution(self, task: Dict) -> tuple:
        """실행 전 보안 확인"""
        
        task_str = str(task).lower()
        for keyword in self.policies['blocked_keywords']:
            if keyword in task_str:
                return False, f"Blocked keyword detected: {keyword}"
        
        if self.policies['require_authentication'] and 'auth_token' not in task:
            return False, "Authentication required"
        
        return True, None
```

---

# 통합 활용 예제

이 세 기술을 함께 사용하는 실제 예제:

```python
class AIAgentSystem:
    """AI 에이전트 시스템 (통합)"""
    
    def __init__(self):
        self.prompt_manager = PromptManager()
        self.context_retriever = ContextRetriever([])
        self.harness = AgentHarness({'timeout': 30})
    
    def process_task(self, user_request: str) -> Dict:
        """사용자 요청 처리"""
        
        # 1. 컨텍스트 엔지니어링: 관련 정보 검색
        context = self.context_retriever.retrieve(user_request, top_k=3)
        
        # 2. 프롬프트 엔지니어링: 최적화된 프롬프트 생성
        prompt = self.prompt_manager.get_prompt(
            'general_task',
            request=user_request,
            context=context
        )
        
        # 3. 하네스 엔지니어링: 안전하게 실행
        result = self.harness.execute(
            task={'type': 'general', 'payload': prompt},
            context={'user_request': user_request}
        )
        
        return result
```

---

# 보안 체크리스트

## 프롬프트 엔지니어링
- [ ] 프롬프트 주입 공격 감지 구현
- [ ] 입력 길이 제한 설정
- [ ] 특수 문자 이스케이프
- [ ] 금지된 명령어 패턴 차단

## 컨텍스트 엔지니어링
- [ ] 민감한 정보 자동 마스킹
- [ ] 접근 권한 확인
- [ ] 컨텍스트 크기 제한
- [ ] 데이터 암호화 (전송/저장)

## 하네스 엔지니어링
- [ ] 모든 실행 로깅
- [ ] 출력 검증 규칙 적용
- [ ] 타임아웃 설정
- [ ] 리소스 제한 강제

---

# 참고 자료 및 링크

## 공식 문서

- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering){:target="_blank"}
- [Anthropic Claude Documentation](https://docs.anthropic.com){:target="_blank"}
- [Google Gemini API Documentation](https://ai.google.dev/docs){:target="_blank"}
- [LangChain Documentation](https://python.langchain.com/){:target="_blank"}

## 참고 문서

- [Prompt Engineering Techniques](https://github.com/dair-ai/Prompt-Engineering-Guide){:target="_blank"}
- [OpenAI Cookbook - Prompt Engineering](https://github.com/openai/openai-cookbook){:target="_blank"}
- [Vector Databases Guide](https://www.pinecone.io/learn/vector-database/){:target="_blank"}
- [RAG (Retrieval Augmented Generation)](https://www.deeplearning.ai/short-courses/retrieval-augmented-generation-rag/){:target="_blank"}
- [Llamaindex Documentation](https://docs.llamaindex.ai/){:target="_blank"}
- [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT){:target="_blank"}
- [Crew AI](https://crewai.com/){:target="_blank"}
- [Microsoft Semantic Kernel](https://github.com/microsoft/semantic-kernel){:target="_blank"}
- [OWASP AI Security](https://owasp.org/www-project-ai-security/){:target="_blank"}
- [Prompt Injection Defense](https://github.com/ScottishFold007/awesome-prompt-injection){:target="_blank"}
- [Advanced Prompt Engineering](https://www.deeplearning.ai/short-courses/prompt-engineering-for-developers/){:target="_blank"}
- [Building AI Agents](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/){:target="_blank"}

---

# 결론

프롬프트 엔지니어링, 컨텍스트 엔지니어링, 하네스 엔지니어링은 AI 에이전트 개발의 세 가지 핵심 축입니다:

- **프롬프트 엔지니어링**: "정확하게 지시하기"
- **컨텍스트 엔지니어링**: "올바른 정보 제공하기"  
- **하네스 엔지니어링**: "안전하게 제어하기"

이 세 기술을 균형 있게 활용하면 강력하고 신뢰할 수 있는 AI 에이전트를 구축할 수 있습니다.
