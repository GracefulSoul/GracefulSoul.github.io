---
title: "Spring Boot + Ollama + pgvector를 활용한 RAG 시스템 구축"
excerpt: "Spring Boot, PostgreSQL pgvector, Ollama를 활용한 RAG(Retrieval Augmented Generation) 시스템 구현 방법"
last_modified_at: 2026-05-10T20:00:00
header:
  image: /assets/images/ai/spring-boot-ai-rag.png
categories:
  - AI
tags:
  - Programming
  - Spring Boot
  - RAG
  - Ollama
  - pgvector
  - PostgreSQL
  - LLM
  - Vector Database

toc: true
toc_ads: true
toc_sticky: true
use_math: false
---

# 개요

이 문서는 Spring Boot, PostgreSQL의 pgvector 확장, 그리고 Ollama를 활용하여 **RAG(Retrieval Augmented Generation)** 시스템을 구축하는 방법을 소개합니다. RAG는 대형 언어 모델(LLM)의 제한된 지식을 보완하기 위해 외부 데이터 소스에서 관련 정보를 검색한 후, 이를 바탕으로 답변을 생성하는 기술입니다.

# 1. 각 서비스의 개요 및 개념

## 1.1 RAG (Retrieval Augmented Generation)

### 정의
RAG는 **검색 기반 생성** 방식으로, 사용자의 질문에 대해 관련 문서를 먼저 검색하고, 그 문서의 내용을 기반으로 LLM이 답변을 생성하는 기법입니다.

### RAG의 필요성

**기존 LLM의 한계:**
1. **지식 커트오프**: 학습 데이터 이후의 정보를 알 수 없음
2. **할루시네이션**: 존재하지 않는 정보를 마치 사실인 것처럼 생성
3. **도메인 특화 지식 부족**: 특정 분야의 전문 지식 부족
4. **최신 정보 반영 불가**: 실시간 데이터 업데이트 불가

**RAG의 장점:**
- ✅ 최신 정보와 도메인 특화 지식 활용
- ✅ 할루시네이션 감소
- ✅ 답변의 신뢰성 향상
- ✅ 검색된 문서를 참고자료로 제시 가능

### RAG 동작 원리

```
┌──────────────────────────────────────────────┐
│               사용자 질문 입력                 │
└────────────────────┬─────────────────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │  텍스트를 벡터로 변환         │
        │   (Embedding Model)        │
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │  벡터 유사도 검색            │
        │  (Vector Similarity Search)│
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │  관련 문서 검색 및 선택       │
        │  (Top-K Documents)         │
        └────────────┬───────────────┘
                     │
           ┌─────────┴─────────────┐
           │                       │
           ▼                       ▼
┌──────────────────────┐  ┌──────────────────────┐
│ 검색된 문서 (Context)  │  │   사용자 질문         │
└──────────┬───────────┘  └────────┬─────────────┘
           │                       │
           └───────────┬───────────┘
                       │
                       ▼
          ┌────────────────────────┐
          │   LLM (Ollama)         │
          │   답변 생성             │
          └────────────┬───────────┘
                       │
                       ▼
            ┌────────────────────┐
            │   최종 답변 반환     │
            └────────────────────┘
```

## 1.2 Spring Boot

### 특징
- **자동 설정**: 관례에 따른 설정으로 복잡한 설정 최소화
- **내장 서버**: Tomcat, Jetty 등을 내장하여 독립 실행 가능
- **스타터 의존성**: pom.xml의 스타터를 통한 간단한 의존성 관리
- **프로덕션 준비**: 모니터링, 메트릭 등 프로덕션 기능 제공

### 이 프로젝트에서의 역할
REST API 서버로서 RAG 기능을 노출하며, 문서 관리 및 질의응답 엔드포인트를 제공합니다.

## 1.3 pgvector (PostgreSQL 벡터 확장)

### 개념
pgvector는 PostgreSQL의 확장으로 벡터 데이터 타입과 벡터 연산을 지원합니다.

### PostgreSQL 버전별 성능 비교

| 항목 | PostgreSQL 15 | PostgreSQL 16 | PostgreSQL 18 |
|------|---------------|---------------|---------------|
| **벡터 성능** | 기본 | 개선됨 | 최적화 |
| **HNSW 인덱싱** | 미지원 | 부분 지원 | 완전 지원 |
| **병렬 처리** | 제한적 | 향상됨 | 우수 |
| **메모리 효율** | 표준 | 개선됨 | 20% 절감 |
| **쿼리 성능** | 100% | 110% | 130% |
| **SIMD 지원** | 부분 | 대부분 | 완전 |

**성능 향상 예시:**
- 벡터 유사도 검색: 20-30% 빠름
- 대량 임베딩 삽입: 25% 빠름
- 메모리 사용량: 15% 감소

### 주요 기능

#### 벡터 데이터 타입
```sql
-- vector 타입 컬럼
CREATE TABLE documents (
    embedding vector(768)  -- 768차원 벡터
);
```

#### 유사도 측정 연산자

| 연산자 | 이름           | 설명                     |
|--------|----------------|------------------------|
| `<=>` | Cosine 거리     | 각도 기반 유사도 (추천) |
| `<->` | L2 거리 (유클리드) | 직선거리 기반          |
| `<#>` | Inner Product   | 내적 기반              |

#### 인덱싱 방식

| 인덱스 | 특징                              |
|--------|----------------------------------|
| **IVFFlat** | 빠른 근사 검색, 메모리 효율적   |
| **HNSW**    | 정확도 높음, 메모리 사용량 증가 |

### 이 프로젝트에서의 역할
임베딩 벡터 저장 및 유사도 검색을 통해 관련 문서를 빠르게 검색합니다.

## 1.4 Ollama

### 개념
Ollama는 로컬 머신에서 대형 언어 모델을 쉽게 실행할 수 있는 오픈소스 도구입니다.

### 주요 특징
- **로컬 실행**: 인터넷 연결 없이 로컬에서 LLM 실행
- **다양한 모델 지원**: Mistral, Llama2, Neural Chat 등
- **간단한 설치**: 한 줄의 명령어로 모델 설치
- **REST API**: HTTP API를 통한 쉬운 통합

### 지원 모델

| 모델명 | 용도 | 특징 |
|--------|------|------|
| **mistral** | Chat/QA | 빠른 처리, 좋은 품질 |
| **nomic-embed-text** | Embedding | 경량, 768차원 출력 |
| **llama2** | Chat/QA | 높은 정확도 |
| **neural-chat** | Chat | 한국어 지원 우수 |

### 이 프로젝트에서의 역할
- **Embedding 생성**: `nomic-embed-text`로 텍스트를 벡터로 변환
- **답변 생성**: `mistral`로 RAG 기반 답변 생성

# 2. 프로젝트 아키텍처

## 2.1 전체 아키텍처 다이어그램

```
┌──────────────────────────────────────────────────┐
│                    REST Client                   │
│            (Postman, cURL, Frontend)             │
└───────────────────────┬──────────────────────────┘
                        │
                        ▼
        ┌─────────────────────────────────┐
        │   Spring Boot Application       │
        │                                 │
        │  ┌───────────────────────────┐  │
        │  │   RagController           │  │
        │  │  - addDocument()          │  │
        │  │  - searchDocuments()      │  │
        │  │  - generateAnswer()       │  │
        │  └───────────┬───────────────┘  │
        │              │                  │
        │  ┌───────────▼──────────────┐   │
        │  │   RagService (핵심)       │   │
        │  │  - retrieveDocuments()   │   │
        │  │  - generateAnswer()      │   │
        │  │  - addDocument()         │   │
        │  └───────────┬──────────────┘   │
        │              │                  │
        │      ┌───────┴─────────┐        │
        │      │                 │        │
        │      ▼                 ▼        │
        │┌─────────────┐  ┌─────────────┐ │
        ││Embedding    │  │Document     │ │
        ││Service      │  │Repository   │ │
        │└──────┬──────┘  └──────┬──────┘ │
        └───────┼────────────────┼────────┘
                │                │
      ┌─────────▼───┐      ┌─────▼───────────────┐
      │             │      │                     │
      ▼             │      ▼                     ▼
  ┌────────────┐    │  ┌───────────────┐ ┌──────────────┐
  │   Ollama   │    │  │ PostgreSQL +  │ │  Database    │
  │   Server   │    │  │   pgvector    │ │  Persistence │
  │            │    │  │               │ │              │
  │- Mistral   │    │  │- Documents    │ │ - JPA/Hib    │
  │- Embed     │    │  │- Vectors      │ │ - Queries    │
  └────────────┘    │  └───────────────┘ └──────────────┘
                    │
                    └─ Spring Data JPA Native Query
```

## 2.2 계층별 설명

### Presentation Layer (Controller)
- **RagController**: REST API 엔드포인트 제공
- 문서 추가, 검색, 답변 생성 기능 제공

### Business Logic Layer (Service)
- **RagService**: RAG 시스템의 핵심 로직
  - 문서 임베딩 생성
  - 유사도 검색 수행
  - LLM 기반 답변 생성

- **EmbeddingService**: 텍스트를 벡터로 변환
  - Ollama의 `nomic-embed-text` 모델 활용

### Data Access Layer (Repository)
- **DocumentRepository**: pgvector를 활용한 유사도 검색
  - Cosine similarity 기반 검색
  - 임계값을 설정한 검색 제공

### Entity/Model Layer
- **Document**: 문서와 임베딩을 함께 저장
- **DocumentRequest/RagRequest**: API 요청 DTO

## 2.3 데이터 흐름

### 문서 추가 흐름

```
POST /api/rag/documents
    ↓
RagController.addDocument()
    ↓
RagService.addDocument()
    ↓
EmbeddingService.generateEmbedding()
    ↓ (REST API call)
Ollama (nomic-embed-text)
    ↓ (벡터 반환)
Document 생성 (content + embedding)
    ↓
DocumentRepository.save()
    ↓
PostgreSQL (pgvector 저장)
```

### 답변 생성 흐름

```
POST /api/rag/generate
{
  "query": "Spring Boot의 장점은?"
}
    ↓
RagController.generateAnswer()
    ↓
RagService.generateAnswer()
    ├─ EmbeddingService.generateEmbedding(query)
    │  └─ Ollama (embedding 생성)
    │
    ├─ DocumentRepository.findSimilarDocuments()
    │  └─ PostgreSQL (pgvector 유사도 검색)
    │
    ├─ Context 구성 (검색된 문서)
    │
    └─ ChatModel (Ollama mistral)
       + SystemMessage (지시사항 + context)
       + UserMessage (사용자 질문)
       └─ 답변 생성
```

# 3. 주요 코드 설명

## 3.1 Document Entity

```java
@Entity
@Table(name = "documents")
public class Document implements Serializable {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "title", nullable = false)
    private String title;

    @Column(name = "content", columnDefinition = "TEXT")
    private String content;

    // pgvector 벡터 컬럼 - 768차원
    @JdbcTypeCode(SqlTypes.JSON)
    @Column(name = "embedding", columnDefinition = "vector(768)")
    private float[] embedding;

    @JdbcTypeCode(SqlTypes.JSON)
    @Column(name = "metadata", columnDefinition = "jsonb")
    private String metadata;

    @Column(name = "created_at")
    private LocalDateTime createdAt;
}
```

**주요 포인트:**
- `embedding` 컬럼: pgvector의 `vector(768)` 타입
- `@JdbcTypeCode`: Hibernate가 벡터를 JSON으로 처리하도록 지정
- `metadata`: JSON 형식의 추가 정보 저장

## 3.2 DocumentRepository (pgvector 검색)

```java
@Repository
public interface DocumentRepository extends JpaRepository<Document, Long> {

    /**
     * Cosine Similarity 기반 유사도 검색
     * <=> 연산자: 코사인 거리 계산 (낮을수록 유사)
     */
    @Query(value = "SELECT * FROM documents " +
           "WHERE embedding IS NOT NULL " +
           "ORDER BY embedding <=> CAST(:embedding AS vector) " +
           "LIMIT :limit", nativeQuery = true)
    List<Document> findSimilarDocuments(
        @Param("embedding") String embedding, 
        @Param("limit") int limit);
}
```

**SQL 쿼리 해석:**
```sql
SELECT * FROM documents
WHERE embedding IS NOT NULL
ORDER BY embedding <=> CAST(:embedding AS vector)
LIMIT :limit
```

1. `<=>` 연산자: 두 벡터 간의 코사인 거리 계산
2. `ORDER BY ... LIMIT`: 가장 유사한 상위 N개 반환
3. `CAST(:embedding AS vector)`: 문자열을 벡터로 변환

## 3.3 EmbeddingService

```java
@Service
@RequiredArgsConstructor
public class EmbeddingService {

    private final EmbeddingModel embeddingModel;

    public float[] generateEmbedding(String text) {
        log.debug("Generating embedding for text of length: {}", text.length());
        var embedding = embeddingModel.embed(text);
        
        // 벡터를 float 배열로 변환
        return embedding.stream()
                .mapToDouble(Double::doubleValue)
                .mapToFloat(d -> (float) d)
                .toArray();
    }
}
```

**Ollama 통합:**
- `EmbeddingModel` bean은 Spring AI의 자동 설정으로 생성
- `application.yml`의 설정에 따라 Ollama 연결

## 3.4 RagService (핵심 비즈니스 로직)

```java
@Service
@RequiredArgsConstructor
public class RagService {

    private final DocumentRepository documentRepository;
    private final EmbeddingService embeddingService;
    private final ChatModel chatModel;

    /**
     * RAG 기반 답변 생성
     */
    public String generateAnswer(String query) {
        // 1. 질문을 벡터로 변환
        float[] queryEmbedding = embeddingService.generateEmbedding(query);
        
        // 2. 유사한 문서 검색
        List<Document> documents = documentRepository.findSimilarDocuments(
                convertEmbeddingToString(queryEmbedding), 5);
        
        // 3. 문서 내용으로 Context 구성
        String context = buildContext(documents);
        
        // 4. System Message와 함께 LLM 호출
        String systemPrompt = "당신은 도움이 되는 AI입니다. " +
                "다음 문서를 기반으로 답변하세요:\n" + context;
        
        SystemMessage systemMessage = new SystemMessage(systemPrompt);
        UserMessage userMessage = new UserMessage(query);
        Prompt prompt = new Prompt(List.of(systemMessage, userMessage));
        
        // 5. Ollama (Mistral) 모델로 답변 생성
        return chatModel.call(prompt)
                .getResult()
                .getOutput()
                .getContent();
    }

    private String buildContext(List<Document> documents) {
        return documents.stream()
                .map(doc -> String.format(
                    "[문서] %s\n내용: %s\n출처: %s\n",
                    doc.getTitle(),
                    doc.getContent(),
                    doc.getSource()))
                .collect(Collectors.joining("\n---\n"));
    }
}
```

## 3.5 RagController (REST API)

```java
@RestController
@RequestMapping("/rag")
@RequiredArgsConstructor
public class RagController {

    private final RagService ragService;

    /**
     * 문서 추가
     * POST /api/rag/documents
     */
    @PostMapping("/documents")
    public ResponseEntity<Document> addDocument(@RequestBody DocumentRequest request) {
        Document document = ragService.addDocument(
            request.getTitle(),
            request.getContent(),
            request.getSource(),
            request.getMetadata());
        return ResponseEntity.status(HttpStatus.CREATED).body(document);
    }

    /**
     * 답변 생성
     * POST /api/rag/generate
     */
    @PostMapping("/generate")
    public ResponseEntity<Map<String, Object>> generateAnswer(@RequestBody RagRequest request) {
        String answer = ragService.generateAnswer(request.getQuery());
        List<Document> documents = ragService.retrieveDocuments(request.getQuery(), 3);
        
        return ResponseEntity.ok(Map.of(
            "query", request.getQuery(),
            "answer", answer,
            "documents", documents));
    }
}
```

# 4. 활용 샘플

## 4.1 프로젝트 구성 및 실행

### 전제 조건

1. **Java 17 이상**
2. **PostgreSQL 18** (권장, pgvector 최적화)
3. **Ollama**

### Docker Compose를 이용한 빠른 시작

```bash
# PostgreSQL과 Ollama를 한번에 실행
cd spring-boot-ai-vectordb
docker-compose up -d

# 로그 확인
docker-compose logs -f
```

### 수동 설치

#### PostgreSQL + pgvector 설정

```bash
# PostgreSQL 18 실행
docker run -d \
  --name postgres-vectordb \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=vectordb \
  -p 5432:5432 \
  pgvector/pgvector:pg18

# PostgreSQL 접속
psql -h localhost -U postgres -d vectordb

# pgvector 설치
CREATE EXTENSION IF NOT EXISTS vector;

# 샘플 데이터 삽입
psql -h localhost -U postgres -d vectordb -f init.sql
```

#### Ollama 설치 및 모델 다운로드

```bash
# Ollama 설치 (Windows)
# https://ollama.ai에서 다운로드

# Ollama 실행
ollama serve

# 다른 터미널에서 모델 설치
ollama pull mistral
ollama pull nomic-embed-text

# 모델 확인
ollama list
```

### Spring Boot 애플리케이션 실행

```bash
# Maven으로 빌드 및 실행
mvn clean spring-boot:run

# 또는 패키지로 빌드 후 실행
mvn clean package
java -jar target/spring-boot-ai-vectordb-1.0.0.jar
```

## 4.2 API 사용 예제

### 예제 1: 문서 추가

```bash
curl -X POST http://localhost:8080/api/rag/documents \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Spring Boot의 자동 설정",
    "content": "Spring Boot는 @SpringBootApplication 어노테이션과 자동 설정을 통해 복잡한 스프링 설정을 간단하게 합니다. ConditionalOnMissingBean 등의 조건부 어노테이션으로 필요한 Bean만 생성됩니다.",
    "source": "https://spring.io/projects/spring-boot",
    "metadata": "{\"category\": \"Spring Boot\", \"difficulty\": \"beginner\"}"
  }'
```

응답:
```json
{
  "id": 1,
  "title": "Spring Boot의 자동 설정",
  "content": "Spring Boot는...",
  "source": "https://spring.io/projects/spring-boot",
  "embedding": [0.123, -0.456, ...], // 768차원
  "metadata": "{\"category\": \"Spring Boot\", \"difficulty\": \"beginner\"}",
  "createdAt": "2026-05-10T10:00:00"
}
```

### 예제 2: 문서 검색

```bash
curl -X POST http://localhost:8080/api/rag/search \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Spring Boot의 특징",
    "limit": 5
  }'
```

응답:
```json
[
  {
    "id": 1,
    "title": "Spring Boot의 자동 설정",
    "content": "Spring Boot는...",
    "source": "https://spring.io/projects/spring-boot",
    "createdAt": "2026-05-10T10:00:00"
  },
  ...
]
```

### 예제 3: RAG 기반 답변 생성

```bash
curl -X POST http://localhost:8080/api/rag/generate \
  -H "Content-Type: application/json" \
  -d '{
    "query": "Spring Boot의 주요 장점을 설명해주세요",
    "limit": 3
  }'
```

응답:
```json
{
  "query": "Spring Boot의 주요 장점을 설명해주세요",
  "answer": "Spring Boot의 주요 장점은 다음과 같습니다:\n\n1. 자동 설정: @SpringBootApplication 어노테이션과 자동 설정으로 복잡한 스프링 설정을 간단하게 합니다.\n\n2. 내장 서버: Tomcat, Jetty 등이 내장되어 별도의 서버 설치 없이 jar 파일로 독립 실행이 가능합니다...",
  "documents": [
    {
      "id": 1,
      "title": "Spring Boot의 자동 설정",
      "content": "Spring Boot는...",
      "source": "https://spring.io/projects/spring-boot"
    }
  ]
}
```

## 4.3 Java 코드 예제

### 문서 추가 (Java)

```java
@RestController
@RequiredArgsConstructor
public class DocumentController {
    
    private final RagService ragService;
    
    public void addSampleDocuments() {
        // 문서 1
        ragService.addDocument(
            "pgvector 소개",
            "pgvector는 PostgreSQL의 벡터 확장으로 벡터 유사도 검색을 지원합니다. " +
            "IVFFlat 및 HNSW 인덱싱을 통한 빠른 검색이 가능합니다.",
            "https://github.com/pgvector/pgvector",
            "{\"type\": \"database\"}"
        );
        
        // 문서 2
        ragService.addDocument(
            "Ollama 소개",
            "Ollama는 로컬 머신에서 LLM을 쉽게 실행할 수 있는 도구입니다. " +
            "Mistral, Llama2 등 다양한 모델을 지원합니다.",
            "https://ollama.ai",
            "{\"type\": \"llm\"}"
        );
    }
}
```

### RAG 질의응답 (Java)

```java
public void demonstrateRag() {
    // 질문
    String question = "벡터 데이터베이스의 사용 사례는?";
    
    // RAG 기반 답변 생성
    String answer = ragService.generateAnswer(question);
    
    // 검색된 관련 문서 조회
    List<Document> relevantDocs = ragService.retrieveDocuments(question, 5);
    
    System.out.println("질문: " + question);
    System.out.println("답변: " + answer);
    System.out.println("참고 문서: " + relevantDocs.size() + "개");
    
    relevantDocs.forEach(doc -> 
        System.out.println("  - " + doc.getTitle())
    );
}
```

# 5. 성능 최적화 및 고려사항

## 5.1 pgvector 인덱싱

### IVFFlat 인덱스 (추천)

```sql
CREATE INDEX idx_documents_embedding ON documents 
USING ivfflat (embedding vector_cosine_ops)
WITH (lists = 100);
```

**특징:**
- 빠른 근사 검색 (Approximate Nearest Neighbor)
- 메모리 효율적
- 대규모 데이터셋에 적합

### HNSW 인덱스

```sql
CREATE INDEX idx_documents_embedding ON documents 
USING hnsw (embedding vector_cosine_ops)
WITH (m = 16, ef_construction = 64);
```

**특징:**
- 높은 정확도
- 메모리 사용량 증가
- 소규모 데이터셋에 적합

## 5.2 쿼리 최적화

### 유사도 임계값 설정

```java
// 낮은 유사도만 필터링
List<Document> docs = documentRepository.findSimilarDocumentsWithThreshold(
    embeddingStr, 
    0.5f,  // threshold
    10     // limit
);
```

### 배치 임베딩 생성

```java
public void addDocumentsBatch(List<DocumentRequest> requests) {
    // 배치로 임베딩 생성
    float[][] embeddings = embeddingService.generateEmbeddings(
        requests.stream()
            .map(DocumentRequest::getContent)
            .toList()
    );
    
    // 문서 저장
    for (int i = 0; i < requests.size(); i++) {
        Document doc = Document.builder()
            .title(requests.get(i).getTitle())
            .content(requests.get(i).getContent())
            .embedding(embeddings[i])
            .build();
        documentRepository.save(doc);
    }
}
```

## 5.3 모니터링

### 쿼리 성능 확인

```sql
-- 쿼리 실행 계획 확인
EXPLAIN ANALYZE
SELECT * FROM documents
ORDER BY embedding <=> '[...]'::vector
LIMIT 5;
```

### 인덱스 크기 확인

```sql
SELECT
    indexrelname,
    pg_size_pretty(pg_relation_size(indexrelid)) as index_size
FROM pg_stat_user_indexes
WHERE relname = 'documents';
```

# 6. 한계 및 개선 방향

## 6.1 현재 구현의 한계

| 한계 | 설명 | 해결책 |
|------|------|-------|
| **싱글 스레드 Ollama** | 동시 요청 처리 제한 | Ollama 클러스터링 또는 비동기 처리 |
| **메모리 제약** | 로컬 LLM의 메모리 사용 | 더 작은 모델 사용 또는 메모리 증설 |
| **컨텍스트 길이 제한** | 입력 텍스트 길이 제한 | 토큰 최적화 또는 청킹 기법 |
| **실시간성** | 벡터 임베딩 생성 시간 | 배치 처리 또는 사전 임베딩 |

## 6.2 개선 방향

### 1. 임베딩 캐싱
```java
@Cacheable("embeddings")
public float[] generateEmbedding(String text) {
    return embeddingService.generateEmbedding(text);
}
```

### 2. 청킹 전략
대용량 문서를 작은 청크로 분할:
```java
public List<Document> addDocumentWithChunking(String title, String content) {
    List<String> chunks = chunkText(content, 1000);  // 1000자 단위
    return chunks.stream()
        .map(chunk -> addDocument(title + " (청크)", chunk, ...))
        .toList();
}
```

### 3. 하이브리드 검색
벡터 검색 + 키워드 검색:
```sql
SELECT * FROM documents
WHERE to_tsvector('korean', content) @@ plainto_tsquery('korean', 'Spring')
OR embedding <=> query_embedding < 0.5
ORDER BY similarity DESC;
```

# 7. 참고 자료 및 링크

## 공식 문서
- [Spring AI 공식 문서](https://github.com/spring-projects/spring-ai){:target="_blank"}
- [Spring Boot 가이드](https://spring.io/guides/gs/spring-boot/){:target="_blank"}
- [PostgreSQL 공식 문서](https://www.postgresql.org/docs/){:target="_blank"}
- [pgvector GitHub](https://github.com/pgvector/pgvector){:target="_blank"}
- [Ollama 공식 사이트](https://ollama.ai){:target="_blank"}

## 관련 기술
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa){:target="_blank"}
- [Hibernate ORM](https://hibernate.org/){:target="_blank"}
- [벡터 데이터베이스 비교](https://www.wikipedia.org/wiki/Vector_database){:target="_blank"}

## RAG 관련 참고
- [RAG 논문: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401){:target="_blank"}
- [LangChain RAG 가이드](https://python.langchain.com/docs/use_cases/question_answering/){:target="_blank"}
- [Mistral 모델 소개](https://mistral.ai/){:target="_blank"}

## 유사 프로젝트
- [Spring AI + Weaviate](https://github.com/spring-projects/spring-ai/tree/main/vector-stores/spring-ai-weaviate-store-spring-boot-starter){:target="_blank"}
- [LangChain Python RAG](https://python.langchain.com/docs/use_cases/question_answering/){:target="_blank"}
- [Azure OpenAI RAG Pattern](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview){:target="_blank"}

---

**소스 코드**: [spring-boot-ai-vectordb](https://github.com/GracefulSoul/spring-boot-ai-vectordb){:target="_blank"}에서 전체 프로젝트를 확인할 수 있습니다.
