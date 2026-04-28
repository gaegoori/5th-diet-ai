# 5th-diet-ai
# DIET: Legal AI Assistant (RAG + QLoRA)

## Overview
DIET (Distilled Intelligent Efficient Thinking)는 학교 및 공공기관 환경에서 **안전하게 사용할 수 있는 법률 AI 시스템**을 목표로 개발된 프로젝트입니다.

기존 AI 서비스는 개인정보 및 내부 문서를 외부 서버로 전송해야 하는 문제로 인해, 학교나 공무적 사용에서의 활용이 어려웠습니다.  
본 프로젝트는 이러한 문제를 해결하기 위해 **로컬 기반 + RAG + Fine-tuning 구조**를 결합하여 보안성과 정확성을 동시에 확보하기 위해 기획되어졌습니다. 

---

## Problem Definition

실제 당진시 선생님의 인터뷰 결과:

> 개인정보나 비공개 문서를 외부 서버에 보낼 수 없어 AI를 활용할 수 없음

### 주요 문제
- 보안 문제 (외부 API 사용 제한)
- 법률 정보의 높은 정확성 요구
- 최신 규정 반영 필요

---

## Solution

본 프로젝트는 다음과 같은 Hybrid 구조를 사용합니다:

| 영역 | 방식 |
|------|------|
| 변하지 않는 법률 지식 | Fine-tuning |
| 최신 규정 / 문서 | RAG |

-> 데이터에 특화하여 Fine-tuning과 RAG를 결합하여 정확성과 최신성을 동시에 확보

---

## Model & Training

### Base Model
- Qwen2.5-3B Instruct

### Fine-tuning 방식
- QLoRA (Quantized LoRA)
- 4-bit Quantization

### 학습 설정
- Training Steps: 약 1000 step
- Loss: 약 0.81
- 과적합 방지 전략 적용

### 사용 기술
- Unsloth (QLoRA 최적화)
- HuggingFace Transformers
- Xformers

---

## Dataset

### 1. Fine-tuning Dataset

- 약 19,000개 이상의 법률 질의응답 데이터
- 한국어 법률 및 행정 규정 기반
- 대화형 구조 데이터로 구성

### 데이터 출처
- 국가법령정보센터
- 교육부 및 시도교육청 공개 자료
- 공무원 복무 규정 및 행정 지침
- 공공기관 공개 법률 문서

---

### 2. RAG Document Dataset

- PDF 형태의 법률 및 행정 문서
- 최신 규정 및 자주 변경되는 문서 중심

### 전처리 과정
1. pypdf를 이용한 텍스트 추출
2. 법률 조항 단위로 문서 분할
3. RecursiveCharacterTextSplitter를 활용한 chunking
4. ChromaDB에 벡터 형태로 저장

---

## Retrieval System
---

## RAG 전체 파이프라인
User Question -> Query Rewriting -> Document Retrieval (Vector DB) -> Context Augmentation -> Prompt 구성 (문서 + 규칙 + 질문) -> LLM (Qwen2.5 + LoRA) -> 최종 답변 생성



### 1. Query Rewriting
사용자의 질문을 검색에 적합하게 변환

예:
- “유튜브” → “영리 업무”
- “돈 벌기” → “보수 수령”

---

### 2. Hybrid Search

#### Dense Search
- SentenceTransformer (ko-sroberta-multitask)
- 의미 기반 검색

#### Sparse Search
- BM25 (rank_bm25)
- 키워드 기반 검색

-> RRF (Reciprocal Rank Fusion)로 결합

---

### 3. Context Augmentation
- 검색된 법률 조항들을 하나의 context로 구성
- LLM 입력에 포함

---

## Prompt Engineering

### Sandwich 구조

| 위치 | 내용 |
|------|------|
| 상단 | 검색된 법률 문서 |
| 중단 | 답변 규칙 |
| 하단 | 사용자 질문 |

### 특징
- 근거 기반 답변 유도
- 환각 및 추측 방지

---

## System Features

### PDF 업로드
- 법률 문서 업로드
- 자동 텍스트 추출 및 벡터화

### 질의응답
- 문서 기반 답변 생성
- 참고 법 조항 및 페이지 제공

### DB 상태 확인
- 저장된 문서 수
- 벡터 DB 상태 확인

---

## Evaluation

- RAGAS 기반 평가
- 주요 지표:
  - Faithfulness
  - Answer Relevancy

-> 문서 수 증가 시 성능 향상 확인

---

## Limitations

- 3B 모델 기반으로 경량화는 성공
- 복잡한 법률 추론에서는 성능 한계 존재

---

## Future Work

- 더 큰 모델(7B 이상) 적용
- 법률 데이터셋 확장
- 실시간 법령 업데이트 시스템 구축
- Prompt 최적화

---

## 👨‍💻 Team

- 김수진
- 김동빈
- 김태건
- 조규형

---

## References

- 국가법령정보센터
- 공공데이터포털
- HuggingFace
- RAGAS
