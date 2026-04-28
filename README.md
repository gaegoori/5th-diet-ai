# DIET: Legal AI Assistant (RAG + QLoRA)

## Overview
DIET는 학교 및 공공기관 환경에서 사용할 수 있는  
**보안 중심 법률 AI 시스템**입니다.

외부 API 없이도 법률 질의응답이 가능하도록  
**Fine-tuning + RAG 구조**를 결합하여 정확성과 최신성을 동시에 확보했습니다.

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
- 약 19K 법률 QA 데이터
- 국가법령정보센터, 교육부, 공공기관 자료 기반

---

## 🔹 Fine-tuning

- 정적인 법률 지식 학습
- ChatML 형식 데이터 사용
- 약 1000 step 학습

-> 기본적인 법률 질의응답 능력 향상

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
