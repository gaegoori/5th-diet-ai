# DIET: Legal AI Assistant (RAG + QLoRA)

보안이 중요한 학교 및 공공기관 환경을 위한 법률 AI 시스템입니다.  
Fine-tuning과 RAG 구조를 결합하여 정확성과 최신성을 동시에 확보합니다.

---

## 프로젝트 소개

DIET는 외부 API 없이도 법률 질의응답이 가능하도록 설계된 AI 시스템입니다.  

법률 도메인에 특화된 Fine-tuning과 최신 문서를 반영하는 RAG 구조를 결합하여, 정확하고 신뢰할 수 있는 답변을 제공합니다.

---

## 문제 정의

- 외부 AI 사용 시 개인정보 유출 위험  
- 법률 정보의 높은 정확성 요구  
- 최신 법령 및 규정 반영 필요  

---

## 해결 방법

- Fine-tuning을 통해 법률 기본 지식 학습  
- RAG를 통해 최신 문서 기반 답변 생성  

---

## 모델

- Qwen2.5-3B Instruct  
- QLoRA (4-bit Quantization)  
- Unsloth / HuggingFace 기반 학습  

---

## 데이터셋

- 약 19,000개 이상의 한국어 법률 질의응답 데이터  
- 계약, 행정, 공무원 규정 등 다양한 법률 주제 포함  
- 국가법령정보센터, 교육부 및 시도교육청 공개 자료 활용  

- 문서 내용을 기반으로 QA 형태로 재구성하여 학습 데이터 구축  
- Fine-tuning용 데이터와 RAG용 데이터를 분리하여 사용  

---

## 기술 스택

### Language
- Python  

### Framework / Library
- PyTorch  
- HuggingFace Transformers  
- Unsloth  

### Fine-tuning
- QLoRA (4-bit Quantization)  
- ChatML 데이터 포맷  

### RAG
- SentenceTransformer (Dense Retrieval)  
- BM25 (Sparse Retrieval)  
- RRF (Reciprocal Rank Fusion)  

### Evaluation
- RAGAS  

---

## 데이터 처리 및 학습

- 법률 및 행정 규정 기반 데이터로 도메인 특화 학습 수행  
- ChatML 형식으로 질의응답 구조 학습  
- 약 1000 step 학습으로 과적합 방지 및 성능 확보  

---

## RAG 파이프라인

User Question → Query Rewriting → Document Retrieval → Context 생성 → LLM 응답  

---

## 팀

- 김수진  
- 김동빈  
- 김태건  
- 조규형  
