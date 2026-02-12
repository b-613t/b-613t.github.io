---
title: "베이즈 추정 1부: '될 놈 될'의 수학적 증명"
date: 2020-10-18 00:00:00 +0900
categories: [생활지식, 자기계발]
tags: [베이즈, 전략, 확률, 자기계발]
math: true
description: "베이즈 추정(Bayesian Inference)을 연애 상황이라는 실생활 사례로 풀어 설명한 확률 입문 글. 사전 확률(Prior), 우도(Likelihood), 사후 확률(Posterior)의 개념을 눈맞춤 사례로 계산하며 ‘같은 신호도 개인의 베이스라인에 따라 다르게 해석된다’는 베이즈 정리의 핵심 원리를 직관적으로 보여준다. 확률적 사고, 의사결정, 자기계발 전략 관점에서 베이즈 이론을 이해하고 싶은 독자를 위한 글."
---

베이즈 추정에 대해 처음 알게 된 것은 니콜라스 나심 탈레브의 **'행운에 속지 마라'**였다. 이후 조던 엘렌버그의 **'틀리지 않는 법'** 같은 책들에서도 종종 마주쳤다. 주로 감염률이나 오진율을 예로 들어 설명되곤 했는데, 읽을 당시엔 명쾌하게 이해해도 시간이 지나면 그 원리가 피부에 와닿지 않아 금방 잊어버리곤 했다.

예시는 껍데기에 불과하다. 하지만 어떤 껍데기를 씌우느냐에 따라 기억의 수명이 결정된다면, 나만의 쓸만한 예시를 만들어 기록해 둘 필요가 있겠단 생각이 들었다.

---

## 1. 시작하기 전에: 3가지 핵심 개념

본격적인 계산에 앞서 베이즈 추정의 뼈대를 이루는 세 가지 개념을 짚고 넘어가야 한다. 이 개념들만 확실히 알아도 베이즈의 절반은 이해한 셈이다.

1. **사전 확률 (Prior):** 사건이 벌어지기 전, 내가 원래 가지고 있던 데이터나 믿음이다. 여기서는 **'그 남자의 평소 매력(성공률)'**이 해당된다.
2. **우도 (Likelihood):** **"어떤 가설이 참일 때, 이 증거가 나타날 확률"**이다. 예컨대 '상대가 나를 좋아한다'는 가설이 참일 때, '나와 눈을 맞출 확률'이 얼마나 되는지 따져보는 것이다.
3. **사후 확률 (Posterior):** 증거를 확인한 후 최종적으로 업데이트된 확률이다. **"상대가 눈을 맞췄으니(증거), 실제로 나를 좋아할 확률"**을 말한다.

> **우도와 사후 확률을 헷갈리지 말자**
>
> * **우도:** 나를 좋아하면 눈을 맞출까? ($P(E\|H)$)
> * **사후 확률:** 눈을 맞췄으니 나를 좋아하는 걸까? ($P(H\|E)$)
>
> 베이즈 추정은 '사전 확률'에 '우도'를 곱해서 '사후 확률'을 찾아내는 과정이다.
{: .prompt-tip }

---

## 2. 가정을 통한 세팅

이제 매력남과 비호감남의 사례를 통해 이 개념들을 대입해 보자.

### **가정 1: 사전 확률 (성공 베이스라인)**
* **상당한 매력남:** 여성 90%가 반한다. ($P(H) = 0.9$)
* **비호감남:** 여성 1%만 반한다. ($P(H) = 0.01$)

### **가정 2: 우도 (눈맞춤의 신뢰도)**
* 상대에게 호감이 있는 경우, 눈을 맞출 확률: **60%**
* 상대에게 호감이 없는 경우, 눈을 맞출 확률: **20%** (예의상, 혹은 습관적으로)

> **주의할 점**
>
> 위 우도의 두 확률(60%, 20%)은 호감이 있는 집단과 없는 집단이라는 **각각 별개의 표본 집단**에 대한 확률이다. 따라서 둘의 합이 100%가 될 필요가 전혀 없다.
{: .prompt-info }

---

## 3. 매력남의 4분면 상황 분석

매력남($P(H)=0.9$)과 여자가 대화를 할 때, 확률 분포는 다음과 같다.

<table style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr>
      <th style="border: 1px solid #ddd; padding: 8px;">구분</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">눈을 맞춤 ($E$)</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">눈을 피함 ($E^c$)</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">계</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>호감 있음 ($H$)</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.9 \times 0.6 = \mathbf{0.54}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.9 \times 0.4 = \mathbf{0.36}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.90$</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>호감 없음 ($H^c$)</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.1 \times 0.2 = \mathbf{0.02}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.1 \times 0.8 = \mathbf{0.08}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.10$</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>계</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.56$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.44$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$1.00$</td>
    </tr>
  </tbody>
</table>
#### **결론: 눈이 마주쳤을 때의 실제 확률**

눈이 마주친 사건($E$)이 발생했을 때, 실제로 호감이 있을 사후 확률은 다음과 같다.

$$P(H|E) = \frac{0.54}{0.54 + 0.02} \approx \mathbf{96.4\%}$$

원래 90%였던 확률이 '눈맞춤'이라는 우도를 만나 **96.4%**로 높아졌다. 이 남자 입장에선 눈이 마주친 것만으로 실패 확률이 거의 3분의 1로 줄어든다.

---

## 4. 비호감남의 사례: '될 놈 될'

단 1%의 여성에게만 어필할 수 있는 비호감남은 어떨까?

<table style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr>
      <th style="border: 1px solid #ddd; padding: 8px;">구분</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">눈을 맞춤 ($E$)</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">눈을 피함 ($E^c$)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>호감 있음 ($H$)</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.01 \times 0.6 = \mathbf{0.006}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.01 \times 0.4 = \mathbf{0.004}$</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>호감 없음 ($H^c$)</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.99 \times 0.2 = \mathbf{0.198}$</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">$0.99 \times 0.8 = \mathbf{0.792}$</td>
    </tr>
  </tbody>
</table>

이 남자가 눈이 마주쳤을 때 실제로 여자가 호감이 있을 확률은 다음과 같다.

$$P(H|E) = \frac{0.006}{0.006 + 0.198} \approx \mathbf{2.9\%}$$

성공률이 1%에서 2.9%로 3배나 뛰었지만, 여전히 처참하다. 비호감남과 눈을 맞춰주는 여자의 **97.1%는 단지 예의상** 그러고 있을 뿐이다.

같은 사건(눈맞춤)을 겪었음에도 결과는 **96.4% vs 2.9%**. 한마디로 요약하면 **'될 놈 될'**이다.

---

## 5. 뒤로 자빠져도 코가 깨지는 원리

매력남이 아이컨택을 하지 못한 경우($E^c$)도 여자의 호감 가능성을 계산해 보자.

$$P(H|E^c) = \frac{0.36}{0.36 + 0.08} \approx \mathbf{81.8\%}$$

매력남은 상대가 자기를 쳐다보지 않는 상황에서도 **81.8%**라는 압도적인 승률을 가진다. 비호감남이 기적적으로 눈을 맞췄을 때(2.9%)보다 매력남이 눈길 한번 얻지 못하고 있을 때(81.8%)의 성공률이 훨씬 높다. 

---

### 요약 및 결론

상대가 나를 좋아하는 줄 알았는데 알고 보니 오해였다는 경험이 많다면, 나의 사전 확률(매력)이 시원찮았기 때문일 가능성이 크다. 

막연한 교과서적 예시보다는 이렇게 실생활에 와닿는 비유가 원리를 훨씬 오래 기억하게 해줄 것이다. 2부에서는 이 냉혹한 수학적 현실 앞에서, '안 될 놈'은 과연 어떤 전략을 짜야 하는지 다뤄보겠다.

---
### 베이즈 시리즈 목록
* **1부: '될 놈 될'의 수학적 증명**
* [2부: '안 될 놈'을 위한 베이즈적 생존 전략](/posts/bayesian-inference-part2)
* [3부: 사전 확률의 업데이트, 지능적인 탐험가로 진화하기](/posts/bayesian-inference-part3)
