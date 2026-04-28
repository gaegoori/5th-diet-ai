# DIET: Legal AI Assistant (RAG + QLoRA)

## Overview
DIET는 학교 및 공공기관 환경에서 사용할 수 있는 **보안 중심 법률 AI 시스템**입니다.

외부 API 없이도 법률 질의응답이 가능하도록 **Fine-tuning + RAG 구조**를 결합하여 정확성과 최신성을 동시에 확보했습니다.

---

## 🎯 Problem
- 외부 AI 사용 시 개인정보 유출 위험
- 법률 정보의 높은 정확성 요구
- 최신 규정 반영 필요

---

## 💡 Solution
- **Fine-tuning** → 법률 기본 지식 학습
- **RAG** → 최신 문서 기반 답변 생성

---

## 🧠 Model
- Qwen2.5-3B Instruct
- QLoRA (4-bit Quantization)
- Unsloth / HuggingFace

---

## 📂 Dataset
- 약 19,000개 이상의 한국어 법률 질의응답 데이터
- 계약, 행정, 공무원 규정 등 다양한 법률 주제
- 국가법령정보센터, 교육부 및 시도교육청 공개 자료, 공공기관 법률 문서 기반 구축
- 문서 내용을 기반으로 QA 형태로 재구성하여 Fine-tuning에 활용
- 데이터셋을 Fine-tuning용과 RAG용으로 분리하여 사용
  - 정적인 법률 지식 → Fine-tuning
  - 최신 규정 및 문서 → RAG

---

## 🔹 Fine-tuning

- 법률 및 행정 규정 기반 데이터로 도메인 특화 학습 수행
- ChatML 형식의 대화형 데이터로 모델 응답 구조 학습
- QLoRA (4-bit Quantization) 기반 효율적인 파인튜닝
- 약 1000 step 학습을 통해 과적합을 방지하면서 성능 확보

-> 일반 모델 대비 법률 질의응답 정확도 및 응답 일관성 향상
---

## 🔹 RAG (Retrieval-Augmented Generation)

### Pipeline
User Question  
→ Query Rewriting  
→ Document Retrieval  
→ Context 생성  
→ LLM 응답

### 핵심 구성
- Dense Search (SentenceTransformer)
- Sparse Search (BM25)
- RRF 기반 결과 결합

-> 최신 문서 기반 정확한 답변 생성

---

## ⚙️ Key Features
- PDF 법률 문서 업로드
- 문서 기반 질의응답
- 근거 포함 답변 생성

---

## 📈 Evaluation
- RAGAS 기반 평가
- Faithfulness / Answer Relevancy 개선

---

## ⚠️ Limitations
- 3B 모델로 복잡한 추론 한계 존재

---

## 👨‍💻 Team
- 김수진
- 김동빈
- 김태건
- 조규형
