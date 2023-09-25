# 그래프 이론 기반 정신질환 증상 평가 점수 네트워크 분석 및 시각화
## Overview
- **연구 배경**
    - 조현병 (Schizophrenia)은 개인 및 사회적으로 큰 영향을 미치고 기능적으로 심각한 증상을 보이는 질병이다.  
    - 효율적이고 개인화된 조현병 치료를 위해 환자 기능을 저해하는 주요 요인을 팡가하는 것은 매우 중요한 문제이다. 특히 연계 증상과 중심 증상을 정신질환 환자들의 증상 평가 점수 설문조사 결과를 네트워크화 함으로써 알 수 있다.
    - 네트워크 분석 방법을 통해 정신 질환 데이터를 분석하면, 조현병 환자의 만성화에 영향을 미치는 핵심 증상 및 동반 이환을 유발하는 증상 간의 관계를 알아볼 수 있으며, 이러한 결과는 조현병 치료 및 연구에 활용 가능하다.

- **선행 연구**
    - 네트워크 분석을 이용하여 수행된 정신병리학적 증상 연구는 아래와 같다.
        - Gregory P Strauss, et al. Network analysis reveals the latent structure of negative symptoms in schizophrenia, Schizophr Bull. 2019.
        - Sandra Schlegl et al. Using network analysis to compare diagnosis-specific and age-specific symptom network sin eating disorders, Int J Eat Disord. 2021.
        - Hua Ye et al. Network analysis of symptom comorbidity in schizophrenia, Schizophr Bull. 2021.

## Process
### 연구 방법
- **사용한 언어 및 Package**
    - R
        - bootnet package
        - huge package
        - qgraph package
    - Python
        - scikit-learn

- **연구 대상 및 측정 도구**
    - 해당 연구에서는 조현병 환자 794명을 대상으로 한 개인 및 사회적 수행 척도(Personal and Social Performance - PSP)와 주관적 안녕감 척도(Subjective Well-Being under Neuroleptic treatment - SWN) 설문조사 데이터를 사용하였다.
    - 그 중 개인 및 사회적 수행 척도(PSP)는 정신 사회적 기능 상태를 4가지 영역으로 나누어 평가할 수 있는 도구로, 환자는 각 문항에 대해 `1:없음 (Absent), 2: 경도(Mild), 3: 명백함(Manifest), 4: 현저함(Marked), 5: 심함(Severe), 6: 매우 심함(Very Severe)`으로 평가 한다. 
    - 주관적 안녕감 척도(SWN)은 정신기능(mental functioning), 자기통제(self-control),  정서 조절(emotional regulation),  신체기능(physical functioning), 사회적 조화 (social integration)와 관련된 총 20개의 항목을 통해 항정신병약물을 복용하는 환자들의 주관적 안녕감을  평가할 수 있는 척도로, 환자는 각 문항에 대해 `0.전혀  1.약간  2.어느정도  3.꽤  4.많이  5.아주 많이`로 평가한다.

- **계층적 군집 분석**
    - 분석에 앞서 각 특성을 지닌 집단 사이에 어떤 차이점과 공통점이 있는지 알아보기 위해 개인 및 사회적 수행 척도(PSP) 점수의 합과 주관적 안녕감 척도(SWN) 평가 점수 합 데이터를 이용하여 dendrogram을 구축한다. 
    - 이어서 계층적 군집분석 (hierarchical clustring)을 통해 데이터를 4개의 환자 그룹으로 군집화 한다. 전체 데이터와 클러스터 별로 군집화 한 데이터, 총 5개의 시각화 결과 도출을 목적으로 한다.
    - 각 환자 그룹은 아래와 같은 특징을 지닌다.
        - 환자그룹-1 : PSP가 낮고 SWN-K가 높은 그룹 (115명)
        - 환자그룹-2 : PSP와 SWN-K가 모두 높은 그룹 (233명)
        - 환자그룹-3 : PSP가 높고 SWN-K가 낮은 그룹 (119명)
        - 환자그룹-4 : PSP와 SWN-K가 모두 낮은 그룹 (327명)
    - 이러한 군집 분석은 이질적인 특성을 가지고 있는 환자들을 세분화하여 진단 기준의 개발 및 환자 맞춤화 치료 방법 제안 등에 활용 가능하다.

![image](https://github.com/2017100898/swcon_cd/assets/64299475/c7eb1709-22cf-450e-99d9-cb07dd4d4c53)

- **CN vs GGM**
    - CN(correlation network)는 Correlation에 따라 node를 단순히 연결한 네트워크다. 직/간접적 연관성 구분이 없고 대규모 데이터에서 연관성이 과다하게 나타나서 시각화 결과를 한 눈에 파악하는 것이 어려운 것이 단점이다. 
    - GGM(Gaussian Graphical Model)은 미미한 상관관계를 0으로 축소하여 시각화 결과를 한 눈에 파악하기 쉬우며 직/간접적 연관성을 정확히 구분하는 네트워크 구조다. 더욱 효과적인 분석과 시각화 결과 제공을 위해 네트워크를 GGM으로 만들어준다.

![image](https://github.com/2017100898/swcon_cd/assets/64299475/ad633b4d-1915-49c7-93ec-62a1f89d858b)

- **상관계수**
    - 일반적으로 Ordinal Data의 상관관계를 구할 때는 단조성을 강조하는 Spearman 상관계수를 사용한다. 그러나 해당 프로젝트에서는 데이터를 정규분포화 함과 동시에 GGM을 안전하게 대체 가능한 skeptic 공식을 사용하여 상관관계를 도출했다.                         
    - skeptic 공식은 huge package의 npn 함수를 통해 사용할 수 있으며, skeptic 공식은 spearman을 아래 식과 같이 변환해 사용할 수 있다. <br>
    
        ~~~R
        x = 2 * sin(pi/6 * cor(x, method = "spearman"))
        ~~~

   - 데이터의 correlation matrix를 구축하는 bootnet estimateNetwork 함수에서도 npn 함수를 사용할 수 있으나, skeptic 공식이 아닌 shrunkun ECDF 공식을 사용하기 때문에 trace 함수를 사용하여 bootnet_correlate 함수를 아래처럼 수정해 줘야 한다.  <br>

        ~~~R
        trace(bootnet:::bootnet_correlate, edit=T)
        ~~~
        
        ~~~R
        if (corMethod == "npn") {
           corMat <- huge::huge.npn(data, npn.func = "skeptic")
        }
        ~~~
   
- **Tuning Parameter**
    - tuning parameter은 EBIC 값을 뜻하며, 0.005, 0.01, 0.05, 0.1, 0.5 값으로 시각화 결과를 만들었을 때, 0.1 값에서 가장 직관적인 해석이 가능한 네트워크 구조가 도출 된다고 판단하여 0.1로 선정하였다.
    - 이 과정을 통해 임계값보다 작은 Correlation을 0으로 대치하여 edge의 개수를 줄일 수 있으며 아래 함수를 통해 최종적으로 network matrix를 추정할 수 있게 된다. <br>
    
        ~~~R
        Ne1 <- estimateNetwork(cl1, default = "EBICglasso" ,  
            threshold =FALSE, corMethod = "npn", tuning = 0.1)
        ~~~
    
    
- **중심성 지표**
    - 중심성 지표는 네트워크 내에서 특정 노드의 영향력을 반영하는 수치이며, 중심성이 높은 노드는 네트워크 내에서 평균 이상의 영향을 미치는 것으로 간주된다. 본 연구에서는 강도 중심성  (strength  centrality),  매개  중심성  (betweenness centrality), 그리고 근접 중심성 (closeness centrality)을 계산함으로써 각 환자그룹별 핵심 증상을 파악했다. 
    - 강도 중심성은 증상들 중 중심 증상을 파악하는 데에 중요한 역할을 한다. 이는 node(증상)의 중요도를 평가하는 지표로, weight 값을 모두 더하여 알아볼 수 있다.
    - 매개 중심성은 해당 노드를 제외한 두 노드를 선택하여 최단 경로를 산출할 때, 해당 노드가 얼마나  자주  포함되는지를  계산한  값이다. 
    - 근접 중심성은 다른 모든 노드들에 대한 평균적인 거리를 뜻한다. 

- **시각화**
    - 도출된 network matrix 중 '증상'을 node로, 증상 간의 상관관계를 edge로 하여 네트워크를 시각화할 수 있다. 
    - edge 중 음의 상관관계를 지니는 값은 빨간색으로, 양의 상관관계를 지니는 값은 파란색으로 나타낸다. 또한, 상관관계 값이 높을 수록 굵은 edge 값을 나타내며, PSP은 분홍색 node를, SWN은 초록색 node 색을 띤다.
    
        ~~~R
        groups =  list("PSP" = 1:4, "SWN" = 5:24)

        plot(Ne1, title="PSP+SWN Cluster 1", groups=groups, color=c( "#DEA5A4", "#C9DECF"),
            posCol = "#005666", negCol = "red", vsize=6, esize=25, borders=FALSE)
        ~~~

<br>

### 기대 효과
- **기대 효과**
    - 정신질환의 증상은 대개 독립적이지 않으며 증상끼리 영향을 주고 받거나 동시다발적으로 발생할 수 있다. 따라서 다양한 증상 중에서도 표적 치료를 할 증상을 파악하는 것은 중요하며, 이를 네트워크 분석을 통해 파악할 수 있다.
    - 네트워크 분석을 통해 정신질환 데이터를 분석하면, 증상 간의 관계를 파악하는 것뿐만 아니라 병리학적 매커니즘을 이해하고 정신 장애 자체를 이해하는 데에 있어 새로운 통찰력을 제공하는 장점이 있다. 
    - 이러한 분석 과정 및 인사이트 도출을 통해 효율적인 치료를 할 뿐만 아니라 정신 질환 별 중심 증상을 파악함으로써 정신질환을 예방하는 단계로 나아갈 수 있을 것이다.
    - 또한, 개인 및 사회적 수행 척도(PSP)와 주관적 안녕감 척도(SWN)를 함께 분석한 것처럼 여러가지 척도를 한 번에 분석할 수 있으므로, 척도 간의 연관성을 파악할 수 있고 이를 통해 새로운 증상 평가 척도를 만들 수도 있을 것이다.

 


## Result
### 증상 네트워크
![image](https://github.com/2017100898/swcon_cd/assets/64299475/f52b2a3a-c815-4aaa-9fb0-d1420db76b58)
![image](https://github.com/2017100898/swcon_cd/assets/64299475/fa49025e-9194-46b7-815f-0e8771a371c4)
![image](https://github.com/2017100898/swcon_cd/assets/64299475/d67f828e-4a47-45b6-8c88-468300f1616a)
![image](https://github.com/2017100898/swcon_cd/assets/64299475/2f7e88a8-c21b-4a0e-87c9-423f74503a59)
![image](https://github.com/2017100898/swcon_cd/assets/64299475/3524cf46-f667-4ded-a566-6654ef403bee)

### 중심성 지표
![image](https://github.com/2017100898/swcon_cd/assets/64299475/ab231e3e-d22a-4c29-86ca-359cd67e7347)

## Conclusion
- 본  연구에서는  조현병  환자의  개인  및  사회적  수행  척도(PSP)와 주관적 안녕감 척도(SWN-K) 평가 점수 데이터를 이용하여, 각 환자를 하위 그룹으로 나누고 정신병리학적 네트워크 분석을 통해 각 그룹의 증상 네트워크 구조, 핵심 증상 및 증상 간 상관관계를 비교 분석하였다.
- 본 연구에서 나타난 핵심 증상, 연계 증상에 대한 결과는 조현병 증상에 대한 기존 이론적 이해를 실험적으로 뒷받침하며, 조현병 증상에 관해 범진단적 치료개입에 중요한 시사점을 제공하였다. 
- 따라서 네트워크 분석을 통해 조현병 진단 평가 척도 개발 및 환자 맞춤형 치료 방법 제안에 활용할 수 있을 것으로 기대한다. 

## Acknowledgement