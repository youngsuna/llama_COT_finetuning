Abstract

LIMA(Less is More Alignments) 논문은 Fine-tuning 시 신중하게 선별된 소량의 고품질 데이터로도 뛰어난 성능을 달성할 수 있음을 입증했다. 본 연구에서는 LLaMa2-7B과 LLaMa3-8B를 이용하여 재현 실험을 진행하였으며, Chain-of-Thought(CoT) 방식을 결합하여 성능에 미치는 영향을 분석했다. 또한, 실험을 통해 학습 데이터 수 증량에 따른 LIMA 방법론의 개선 효과를 알아보았다. 본 연구에서는 LIMA 방법론을 적용한 LLaMa3-8B 모델의 5-shot 성능이 크게 개선되었음을 확인할 수 있었다.


1 Introduction

기존의 대형 언어 모델 학습에서는 대용량 데이터의 중요성이 강조되어 왔다. 언어 이해 및 생성
작업에서 높은 성능을 발휘하기 위해서는 방대한 양의 학습 데이터가 필요하다는 가정에 기반한
것이다. 그러나, LIMA(Less is More Alignments) 논문은 이러한 기존의 가정을 뒤집는 결과를
제시하였다. LIM는대용량의데이터가아닌,신중하게선별된소량의고품질데이터로도뛰어난
성능을 달성할 수 있음을 입증하였다. 단, 1000개의 프롬프트와 응답만으로 강력한 성능을 보였
으며, 이는 기존의 대규모 데이터 기반 접근법에 비해 효율성과 비용 측면에서 큰 이점을 제공하
였다. LIMA논문에서 활용한 백본 모델은 LLaMa를 기반으로 하였으나, 이후 LLaMa2, LLaMa3
까지 더욱 발전된 모델들이 등장하였다. 따라서 본 연구에서는 백본 모델을 최신의 LLaMa2와
LLaMa3로 변경했을 때 성능이 얼마나 향상되는지를 실험하고자 한다. 더 나아가, 많은 task에
서 성능 개선 효과를 보여준 Chain-of-Thought 방식을 LIMA와 결합하였을 때, 성능에 긍정적인
영향을 미치는지 분석하고자 하였다.

2 Related Work

2.1 LIMA: Less Is More for Alignment

LIMA(Less Is More for Alignments) 모델은 대규모 데이터 학습의 필요성을 줄이고, 적은 양의
고품질 데이터로도 우수한 성능을 달성할 수 있음을 보여준 연구이다. 사전 훈련된 대형 언어
모델을 기반으로 하여, 단 1,000개의 양질의 데이터만으로도 매우 강력한 성능을 달성할 수 있
음을 입증했다. (Zhou et al., 2023). LIMA는 GPT-4와 비교하여 43%의 경우 동등하거나 더 나은
응답을 제공하였고, Bard와 비교했을 때 58%, DaVinci003과 비교했을 때 65% 선호되는 응답을
생성하였다.

2.2 Chain-of-Thought Prompting Elicits Reasoning in Large Language Models

Chain-of-Thought(CoT) 기법은 복잡한 추론 작업을 수행할 때 대형 언어 모델의 성능을 크게
향상시키는 방법으로, 일련의 중간 추론 단계를 생성함으로써 모델의 추론 능력을 끌어내는 접
근법이다. COT 기법은 수학적, 상식적, 상징적 추론 등 다양한 작업에서 단순한 프롬프트 기법을
능가하는 성능을 보이며, 모델의 크기가 클수록 더욱 극적으로 효과가 향상된다(Wei et al., 2022).
단,몇가지예시만을추가함으로써쉽게CoT기법을적용할수있다는장점이있으며,답에어떻
게 도달했는지, 어디서 추론이 잘못되었는 지 등 대형 언어 모델의 행동을 해석할 수 있게 해준다.

3 Methodology

3.1 LLaMa 경량 모델을 이용한 성능 재현

LIMA(Less Is More for Alignments) 모델은 초기 연구에서 LLaMa 백본 모델을 사용하여 뛰어난
성능을 달성한 바 있다. 그러나, Table 1과 같이, Meta가 최근 출시한 LLaMa2와 LLaMa3는 구
조적 개선과 훈련 데이터 양의 증가를 통해 더욱 향상된 성능을 보인다. Meta의 초기 대형 언어
모델인LLaMa는기본적인언어이해능력을제공한다. LLaMa2는훈련데이터와맥락길이가늘
어나며성능이향상되지만,여전히제한적인코드생성능력을보인다. LLaMa3는훈련데이터의
양을 크게 증가시키고 맥락 길이를 8K 토큰으로 확장하며, 더 나은 토크나이저와 효율적인 그룹
쿼리 어텐션(GQA) 메커니즘을 통해 응답의 다양성과 정확성을 대폭 향상시킨다. 이는 LIMA에
서도 LLaMa는 백본 모델로 이용되며, LLaMa의 개선된 버전으로 LIMA의 성능 향상이 되기를
기대한다.

3.2 Chain-of-Thought 적용에 따른 성능 개선

본 연구에서는 LIMA 방법론에 Chain-of-Thought(이하 CoT) 기법을 적용하여 성능 개선을 시도
한다. 이를 위해 KoCoT 2000 데이터셋을 활용하고, CoT 기법 유무에 따른 LIMA 모델의 성능을
비교 분석한다.


