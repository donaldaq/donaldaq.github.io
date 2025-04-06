---
layout: post
title: LLM-as-a-Judge의 평가문제 
excerpt: "LLM Evaluation"
categories: [LLM]
comments: true
---

**Image DeepLearning Engineer입니다. AI 모든 분야에 관심이 많습니다. 
NLP 연구개발 공부하고 관심갖는 사람으로서 논문과 정리된 내용을 좀 더 쉽게 이해하는데 집중하여 작성하였습니다.**

## LLM-as-a-Judge의 평가 문제 



최근 LLM을 활용한 모델 평가 방식인 LLM-as-a-Judge가 사용되고 있습닏.  
하지만 이 방법은 평가에 내용에 편향(Bias)가 발생하고 있습니다. 

- 위치 편향(Position Bias)로 LLM이 특정 위치의 답변을 선호하는 경향성이 나타나는 현상입니다.  
- 길이 편향(Length Bias) or 장황함 편향(Verbosity Bias)에 문제가 나타나고 있습니다. (긴 답변을 더 선호하는 경향) 
- 자기 중심 편향(Egocentric Bias) or 자기 강화 편향(Self-enhancement Bias)으로 LLM에서 출력된 것을 선호하는 문제가 발생
- 수학 및 추론 문제 채점 능력 한계(Limited capability in grading math and reasoning questions)가 있어 잘못된 결과의 판단

**Paper: Preference Leakage - A Contamination Problem in LLM-as-a-Judge**라는 논문에서는 위와 같은 문제를 **Preference Leakage(선호도 유출)**로 정의하여 설명하고 있습니다.  

### LLM-as-a-Judge란?
![image](https://github.com/user-attachments/assets/6fb88042-0fd4-4c76-9ab1-ffc36bad17c9)

- LLM-as-a-Judge는 생성된 데이터셋과 실제 데이터셋을 비교하여 평가하고, 이를 통해 모델의 응답 품질을 지속적으로 개선하는 평가방식을 뜻합니다. 
- LLM-as-a-judge로 Chatbot Arena를 MT-bench 방식으로 LLM 평가함. 
 - 논문에 결과에 따르면 MT-bench의 전문가 투표와 Chatbot Arena에서 수집된 크라우드 투표 결과를 비교했을 때, GPT-4 judge와 사람의 평가에 대한 선호의 일치도가 80% 이상 사람간의 평가와 유사한 성능을 보여주었습니다. 
 (https://arxiv.org/abs/2306.05685)
- LLM-as-a-Judge 장점 
 - Scalability: 사람이 평가하는 작업보다 효과적으로 시간과 비용을 절감하여 대규모 평가 작업을 효율적으로 수행할 수 있습니다.
 - Explainble: LLM이 제공하는 평가 결과에서는 결과에 대한 이유가 설명될 수 있어, 평가 과정이 투명하고 이해하기 용이.
 - Same human preference: LLM을 사용한 평가가 인간의 평가와 높은 일치 상관성이 보이므로 평가 신뢰성을 갖을 수 있습니다.. 
-  LLM-as-a-Judge 프로세스
 - 1. **평가 기준 파악하기** - 먼저 hallucination, toxicity, accuracy 또는 기타 특성 등을 결정합니다. 
 - 2. **평가 프롬프트 작성** - 평가를 안내할 프롬프트 템플릿을 작성합니다. 이 템플릿은 출력을 효과적으로 평가하기 위해 초기 프롬프트와 LLM의 응답 모두에서 필요한 변수를 명확하게 정의합니다. 
 - 3. **평가 LLM 선택** - 특정 평가를 수행하기 위해 사용 가능한 옵션 중에서 가장 적합한 LLM을 선택합니다. 
 - 4. **평가 생성 및 결과 보기** - 데이터 전체에서 평가를 실행합니다.  프로세스를 통해 수동적인 주석을 하지 않고 포괄적인 테스트가 가능해집니다. 또한, 신속하게 반복하고 LLM의 프롬프트를 구체화

이 방법은 특히 RAG(질문 응답 생성) 시스템의 평가에도 유용하게 사용될 수 있습니다.

### Preference Leakage란?
> LLM이 데이터 생성과 동시 평가를 수행할 때 발생하는 평가 오염문제를 나타냄 
> 데이터 생성과 평가 모델이 연관성을 갖을 경우, 평가 모델이 모델 자신과 관련된 출력을 더 선호하는 현상이 발생합니다.  
> 기존 데이터 오염(Data Contamination)문제와 유사하나 더 알아채기 어렵게 발생하여 검출하기 어려움이 있습니다. 

## **LLM-as-a-Judge 프로세스**

LLM-as-a-Judge는 다음과 같은 과정을 거쳐 사용됩니다:

1. **평가 기준 파악하기** - 먼저 hallucination, toxicity, accuracy 또는 기타 특성 등 무엇을 평가할지 결정합니다.
2. **평가 프롬프트 작성** - 평가를 안내할 프롬프트 템플릿을 작성하세요. 이 템플릿은 출력을 효과적으로 평가하기 위해 초기 프롬프트와 LLM의 응답 모두에서 필요한 변수를 명확하게 정의해야 합니다.
3. **평가 LLM 선택** - 특정 평가를 수행하기 위해 사용 가능한 옵션 중에서 가장 적합한 LLM을 선택합니다.
4. **평가 생성 및 결과 보기** - 데이터 전체에서 평가를 실행합니다. 이 프로세스를 사용하면 수동으로 주석을 달 필요 없이 포괄적인 테스트를 수행할 수 있으므로 신속하게 반복하고 LLM의 프롬프트를 구체화할 수 있습니다.

이 방법은 특히 RAG(질문 응답 생성) 시스템의 평가에도 유용하게 사용될 수 있습니다.

### **LLM-as-a-judge의 한계**

- Position bias(위치 편향)

LLM이 특정 위치의 답변을 선호하는 경향성을 나타낼 때 발생합니다.

- Verbosity bias(장황함 편향)

LLM 심사위원이 더 짧고 명확하며 고품질이거나 정확한 답변보다 더 길고 장황한 답변을 선호하는 경향이 있습니다.

- Self-enhancement bias(자기 강화 편향)

일부 LLM 심사위원이 특정 모델을 선호하는 것을 관찰할 수 있었으나 데이터가 제한적이고 차이가 작기 때문에 이 연구에서는 모델이 자기 강화 편향을 나타내는지 여부를 결정할 수 없었습니다.

- Limited capability in grading math and reasoning questions(수학 및 추론 문제 채점 능력 제한)

GPT-4는 (별도로 질문할 경우) 문제를 풀 수 있음에도 불구하고 제공된 답변에 의해 잘못된 판단을 내렸습니다.

Preference Leakage의 주요 원인

- 논문에서는 LLM 데이터 생성기(Generator)와 평가자(Judge) 간의 **세 가지 유형의 관련성(Relatedness)**을 정의함.
- 1. 동일한 모델(Same Model)
    - 데이터 생성과 평가를 같은 LLM이 수행. 예: GPT-4가 데이터를 생성하고, 다시 GPT-4가 이를 평가하는 경우.
- 2. 계승 관계(Inheritance Relationship)
    - 데이터 생성 모델이 평가 모델에서 파생됨.
    - 예: GPT-4가 데이터를 생성하고, 이를 기반으로 Mistral-7B를 학습한 뒤, 다시 GPT-4가 이를 평가하는 경우.

같은 모델 계열(Same Model Family)

- 동일한 모델 패밀리(GPT, Gemini, LLaMA 등) 내에서 데이터 생성과 평가가 이루어집니다.
    - 예: GPT-4가 데이터를 생성하고, GPT-3.5가 이를 평가하는 경우.
- Preference Leakage가 발생하는 이유
    - 데이터 생성기와 평가 모델이 같은 특성을 공유하기 때문입니다. 데이터 생성 과정에서 특정 스타일, 형식, 표현 방식이 반영되며, 평가 모델이 이를 인식하고 선호하는 경향이 발생.
    
    - 특히 Supervised Fine-Tuning(SFT) 과정에서 이러한 편향이 더 심해집니다.

## 실험 및 주요 결과

- 실험 설정
    - 데이터 생성 및 평가 모델로 사용된 LLMs:
        - GPT-4o (2024-11-20)
        - Gemini-1.5-flash
        - LLaMA-3.3-70B-Instruct-turbo

실험 대상 학생 모델(Student Models):

- Mistral-7B-v0.1
- Qwen-2.5-14B

평가 데이터셋:

- Arena-Hard
- AlpacaEval 2.0

측정 지표: Preference Leakage Score (PLS)

- 평가 모델이 자신의 관련 모델을 얼마나 더 선호하는지를 정량적으로 측정.
- 값이 클수록 평가 편향이 심함.

실험 결과

1. Preference Leakage는 실제로 발생하며, 심각한 문제가 있습니다. .

- 대부분의 모델 조합에서 평가 모델이 자신의 관련 모델을 더 선호하는 경향을 보입니다.
- 예를 들어, GPT-4o는 LLaMA-3.3을 더 선호하는 경향을 보였습니다. 

2. 모델의 크기와 성능이 높을수록 Preference Leakage가 더 심해집니다.

- *Qwen-2.5-14B (더 큰 모델)**이 Mistral-7B보다 더 높은 Preference Leakage Score를 기록했습니다. 
- 이는 성능이 좋은 모델이 더 강하게 패턴을 학습하기 때문으로 추정됩니다.

3. Supervised Fine-Tuning(SFT)이 가장 큰 Preference Leakage를 유발합니다.

- SFT 방식으로 학습한 모델은 Preference Leakage Score가 23.6%로 가장 높았습니다.
- 반면, **DPO(Direct Preference Optimization)**는 5.2%, **ICL(In-Context Learning)**은 -2.7%로 훨씬 낮았습니다.

4. 데이터 혼합(Data Mixing) 전략이 Preference Leakage에 영향을 줍니다.

- 합성 데이터(Synthetic Data) 비율이 높을수록 Preference Leakage Score가 증가.
- 70% 합성 데이터가 포함된 경우 Preference Leakage Score가 최대 30%까지 증가.

5. 평가 모델은 자신의 학생 모델 출력을 정확히 인식하지 못하지만, 특정 패턴을 학습합니다.

- LLM 평가자는 학생 모델의 출력을 직접 식별하는 능력이 낮았습니다.
- 하지만 BERT 기반 분류 모델을 학습하면 학생 모델의 출력을 높은 정확도로 구분할 수 있었습니다 → 학생 모델이 특정 스타일, 형식을 계승하고 있습니다.


### 해결 방법 및 시사점

해결 방안

1. 평가 모델과 데이터 생성 모델을 분리해야 합니다.

- 예: GPT-4가 데이터를 생성하면, 평가에는 Gemini-1.5를 사용합니다.

2. Supervised Fine-Tuning(SFT)보다 DPO, ICL 같은 학습 방법 사용합니다.

- SFT는 Preference Leakage를 심화시키므로, **DPO(Direct Preference Optimization)**가 더 적합합니다.

3. 합성 데이터의 비율을 줄이고, 다양한 모델에서 생성한 데이터를 혼합합니다.

- 특정 모델이 생성한 데이터만 학습할 경우, 편향이 심화됩니다.

4. 새로운 평가 벤치마크 개발.

- 현재 AlpacaEval 2.0, Arena-Hard 등도 Preference Leakage 영향을 받고 있습니다.
- 편향을 줄이기 위한 새로운 데이터셋 및 평가 방식 필요합니다 .

시사점

- LLM-as-a-Judge는 비용 효율적이지만, 모델 편향(Bias) 문제를 해결하지 않으면 신뢰할 수 없습니다.
- 특히 Preference Leakage는 기존의 데이터 오염(Data Contamination) 문제보다 더 은밀하고 검출하기 어려움이 있습니다.
- 평가 모델의 공정성을 확보하려면 데이터 생성과 평가 모델을 분리하고, 새로운 학습 기법과 평가 기준을 개발해야 합니다.






### References:
- https://devocean.sk.com/blog/techBoardDetail.do?ID=166628&boardType=techBlog
- https://kashnep.tistory.com/30


