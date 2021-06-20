# 그래프 이론 기반 정신질환 증상 평가 점수 네트워크 분석 SW 개발: <br> 개인 및 사회적 수행 척도와 주관적 안녕감 척도를 중심으로 
`2021-1 KyungHee univ. Software Convergence Capstone Design`<br><br>


## Overview
- **과제 선정 배경 및 필요성**
    - 조현병(schizophrenia), 양극성 장애(bipolar disorder), 우울장애(depressive disorder) 등 최근 많은 사람들이 정신질환을 겪으며 살아간다. 이러한 사회 문제가 대두 됨에 따라, 정신 질환을 정확히 진단하고 효율적으로 치료하기 위한 연구들이 활발히 진행되고 있다. 
    - 효율적 치료를 위해 파악해야 하는 것은 바로 연계 증상과 중심 증상이며, 이는 정신질환 환자들의 증상 평가 점수 설문조사 결과를 네트워크화 함으로써 알 수 있다. 그렇기에 최근 국내 및 해외 신경정신의학 분야에서는 네트워크 분석 기법을 활용한 정신질환 증상 연구가 다수 진행되고 있다.
    - 그러나 정신질환 증상 평가 점수를 입력하여 분석 방법론을 결정하고, 프로그래밍 한 뒤 시각화 결과를 도출하는 과정은 복잡하며, 시간 소요가 많이 되는 단점이 있다. 따라서 환자들의 정신질환 증상 평가 점수 데이터를 즉각적으로 분석하고 시각화하는 웹 기반 interactive SW를 개발한다면 신경정신의학 분야의 더욱 활발 한 연구가 가능해질 것이라 판단하여 해당 주제를 선정하게 되었다.

- **과제 주요 내용**
    - 해당 SW는 실제 환자 진단 및 치료에 사용이 될 수 있기 때문에, 개발에 앞서서 직접 데이터를 분석해봄으로써 네트워크 분석 방법론을 결정하는 것이 중요하다고 판단했다. 
    - 따라서, 해당 프로젝트에서는 환자 731명을 대상으로 한 개인 및 사회적 수행 척도(Personal and Social Performance - PSP)와 주관적 안녕감 척도(Subjective Well-Being under Neuroleptic treatment - SWN) 설문조사 결과 데이터를 이용하여 증상간의 연관성을 평가하고 분석하여 인사이트를 도출하는 과정을 거치고 유의미한 결과인지 판단함으로써 방법론을 선정했다.

- **최종 결과물의 목표**
    - 웹기반 정신질환 증상 평가 네트워크 분석 및 interactive 시각화 SW개발을 목표로 한다. 
    - Input 데이터는 환자들의 정신질환 평가 점수 설문조사 결과 데이터 csv 파일이며, Output은 중심성 지수와 interactive한 네트워크 시각화 결과로 이루어진다. 시각화 결과는 node의 크기, edge의 굵기, 색상을 다양화 하여 통해 증상 간의 연결성이 직관적으로 전달 되도록 함으로써 Insight 도출에 도움을 준다.

## Process
### 과제 수행 방법
- **데이터**
    - 해당 프로젝트에서 사용된 데이터는 환자 731명의 개인 및 사회적 수행 척도(PSP)와 주관적 안녕감 척도(SWN) 설문조사 결과값이다. 
    - 그 중 개인 및 사회적 수행 척도(PSP)는 정신 사회적 기능 상태를 4 가지 영역으로 나누어 평가할 수 있는 도구로, 환자는 각 문항에 대해 `1:없음 (Absent), 2: 경도(Mild), 3: 명백함(Manifest), 4: 현저함(Marked), 5: 심함(Severe), 6: 매우 심함(Very Severe)`으로 평가 한다. 
    - 주관적 안녕감 척도(SWN)은 총 20개의 항목을 통해 항정신병약물을 복용하는 환자들의 주관적 안녕감을 평가할 수 있는 척도로, 환자는 각 문항에 대해 `0.전혀  1.약간  2.어느정도  3.꽤  4.많이  5.아주 많이`로 평가한다.
        
- **사용한 언어 및 Package**
    - R 언어
    - bootnet package
    - huge package
    - qgraph package

- **Hierarchical Clustering**
    - 분석에 앞서 각 특성을 지닌 집단 사이에 어떤 차이점과 공통점이 있는지 알아보기 위해 개인 및 사회적 수행 척도(PSP) 점수의 합과 주관적 안녕감 척도(SWN) 평가 점수 합 데이터를 이용하여 dendrogram을 구축한다. 
    - 이어서 hierarchical clustring을 통해 데이터를 4개의 cluster로 군집화 한다. 전체 데이터와 클러스터 별로 군집화 한 데이터, 총 5개의 시각화 결과 도출을 목적으로 한다.
    - 각 Cluster는 아래와 같은 특징을 지닌다.
        - Cluster1: 66개의 데이터, PSP가 낮고 SWN이 높은 집단
        - Clsuter2: 223개의 데이터, PSP와 SWN 모두 높은 집단
        - Cluster3: 150개의 데이터, PSP가 높고 SWN이 낮은 집단
        - Clsuter4: 292개의 데이터, PSP와 SWN 모두 낮은 집단
    
<p align="center"><img width="547" alt="20210621_060012" src="https://user-images.githubusercontent.com/64299475/122688231-07835500-d256-11eb-81c0-954d9e95b7e2.png"></p>

- **CN vs GGM**
    - CN(correlation network)는 Correlation에 따라 node를 단순히 연결한 네트워크다. 직/간접적 연관성 구분이 없고 대규모 데이터에서 연관성이 과다하게 나타나서 시각화 결과를 한 눈에 파악하는 것이 어려운 것이 단점이다. 
    - GGM(Gaussian Graphical Model)은 미미한 상관관계를 0으로 축소하여 시각화 결과를 한 눈에 파악하기 쉬우며 직/간접적 연관성을 정확히 구분하는 네트워크 구조다. 더욱 효과적인 분석과 시각화 결과 제공을 위해 네트워크를 GGM으로 만들어준다.


<p align="center"><img width="538" alt="20210621_060021" src="https://user-images.githubusercontent.com/64299475/122688233-0f42f980-d256-11eb-88b7-b132ed1368d4.png"></p>

- **상관계수**
    - 일반적으로 Ordinal Data의 상관관계를 구할 때는 단조성을 강조하는 Spearman 상관계수를 사용한다. 그러나 해당 프로젝트에서는 데이터를 정규분포화 함과 동시에 GGM을 안전하게 대체 가능한 skeptic 공식을 사용하여 상관관계를 도출했다.                         
    - skeptic 공식은 huge package의 npn 함수를 통해 사용할 수 있으며, skeptic 공식은 spearman을 아래 식과 같이 변환해 사용할 수 있다. <br>
    
        ~~~R
        x = 2 * sin(pi/6 * cor(x, method = "spearman"))
        ~~~

   - 데이터의 correlation matrix를 구축하는 bootnet estimateNetwork 함수에서도 npn 함수를 사용할 수 있으나, skeptic 공식이 아닌 shrunkun ECDF 공식을 사용하기 때문에 trace 함수를 사용하여 estimateNetwork 함수를 아래처럼 수정해 줘야 한다.  <br>

        ~~~R
        trace(bootnet:::estimateNetwork, edit = T)
        ~~~
        
        ~~~R
        if (corMethod == "npn") {
           data <- huge::huge.npn(data, npn.func = "skeptic")
           corMethod <- "cor"
        }
        ~~~
   
- **Tuning Parameter**
    - tuning parameter은 Lasso에서의 lambda 값을 뜻하며, 0.005, 0.01, 0.05, 0.1, 0.5 값으로 시각화 결과를 만들었을 때, 0.1 값에서 가장 직관적인 해석이 가능한 네트워크 구조가 도출 된다고 판단하여 0.1로 선정하였다.
    - 이 과정을 통해 임계값보다 작은 Correlation을 0으로 대치하여 edge의 개수를 줄일 수 있으며 아래 함수를 통해 최종적으로 network matrix를 추정할 수 있게 된다. <br>
    
        ~~~R
        Ne1 <- estimateNetwork(cl1, default = "EBICglasso" ,  
            threshold =FALSE, corMethod = "npn", tuning = 0.1)
        ~~~
    
    
- **강도 중심성**
    - 강도 중심성은 증상들 중 중심 증상을 파악하는 데에 중요한 역할을 한다. 이는 node(증상)의 중요도를 평가하는 지표로, weight 값을 모두 더하여 알아볼 수 있다.

- **시각화**
    - 도출된 network matrix 중 '증상'을 node로, 증상 간의 상관관계를 edge로 하여 네트워크를 시각화할 수 있다. 
    - edge 중 음의 상관관계를 지니는 값은 빨간색으로, 양의 상관관계를 지니는 값은 파란색으로 나타낸다. 또한, 상관관계 값이 높을 수록 굵은 edge 값을 나타내며, PSP은 분홍색 node를, SWN은 초록색 node 색을 띤다.
    
        ~~~R
        groups =  list("PSP" = 1:4, "SWN" = 5:24)

        plot(Ne1, title="PSP+SWN Cluster 1", groups=groups, color=c( "#DEA5A4", "#C9DECF"),
            posCol = "#005666", negCol = "red", vsize=6, esize=25, borders=FALSE)
        ~~~

<br>
<br>

### 기대 효과 및 활용 방안
- **기대 효과**
    - 정신질환의 증상은 대개 독립적이지 않으며 증상끼리 영향을 주고 받거나 동시다발적으로 발생할 수 있다. 따라서 다양한 증상 중에서도 표적 치료를 할 증상을 파악하는 것은 중요하며, 이를 네트워크 분석을 통해 파악할 수 있다.
    - 네트워크 분석을 통해 정신질환 데이터를 분석하면, 증상 간의 관계를 파악하는 것뿐만 아니라 병리학적 매커니즘을 이해하고 정신 장애 자체를 이해하는 데에 있어 새로운 통찰력을 제공하는 장점이 있다. 
    - 이러한 분석 과정 및 인사이트 도출을 통해 효율적인 치료를 할 뿐만 아니라 정신 질환 별 중심 증상을 파악함으로써 정신질환을 예방하는 단계로 나아갈 수 있을 것이다.
    - 또한, 개인 및 사회적 수행 척도(PSP)와 주관적 안녕감 척도(SWN)를 함께 분석한 것처럼 여러가지 척도를 한 번에 분석할 수 있으므로, 척도 간의 연관성을 파악할 수 있고 이를 통해 새로운 증상 평가 척도를 만들 수도 있을 것이다.

- **활용 방안**
    - 그래프 이론 기반 정신질환 증상 평가 점수 네트워크 분석 SW를 신경정신의학 분야의 전문가가 사용하게 된다면, 분석을 위한 일련의 과정들을 제거하고, 곧바로 시각화 결과를 제공해줌으로써 지금보다 더욱 빠르고 활발한 연구가 가능해질 것이라 생각한다.
 


## Result
`전체 PSP+SWN 데이터의 시각화 결과 및 Insight 도출 결과`
<br>
![슬라이드11](https://user-images.githubusercontent.com/64299475/122685291-6d1b1580-d245-11eb-897d-c8ae5ec0e97d.png)
![슬라이드12](https://user-images.githubusercontent.com/64299475/122685293-6e4c4280-d245-11eb-9417-749f1a35b66f.png)
<br>
---

`Cluster1 데이터의 시각화 결과 및 Insight 도출 결과`
<br>
![슬라이드13](https://user-images.githubusercontent.com/64299475/122685294-6f7d6f80-d245-11eb-9a26-02a0b1ee4460.png)
![슬라이드14](https://user-images.githubusercontent.com/64299475/122685296-70ae9c80-d245-11eb-9f93-ee611427561e.png)
<br>
---

`Cluster2 데이터의 시각화 결과 및 Insight 도출 결과`
<br>
![슬라이드15](https://user-images.githubusercontent.com/64299475/122685298-71473300-d245-11eb-8d10-3e20849e6f66.png)
![슬라이드16](https://user-images.githubusercontent.com/64299475/122685301-72786000-d245-11eb-95a9-1e88b674f7e1.png)
<br>
---

`Cluster3 데이터의 시각화 결과 및 Insight 도출 결과`
<br>
![슬라이드17](https://user-images.githubusercontent.com/64299475/122685302-73a98d00-d245-11eb-9381-06b52c32d06e.png)
![슬라이드18](https://user-images.githubusercontent.com/64299475/122685304-74daba00-d245-11eb-89b6-f8b2496ddad1.png)
<br>
---

`Cluster4 데이터의 시각화 결과 및 Insight 도출 결과`
<br>
![슬라이드19](https://user-images.githubusercontent.com/64299475/122685305-76a47d80-d245-11eb-879d-370b4092433a.png)
![슬라이드20](https://user-images.githubusercontent.com/64299475/122685307-773d1400-d245-11eb-91ca-a1f467cf2c34.png)
<br>
---

## Conclusion
- 분석 및 인사이트 도출 결과 Cluster 별로 다른 연계 증상, 중심 증상이 나타난다. 그렇기 때문에 개인 및 사회적 수행 척도(PSP)와 주관적 안녕감 척도(SWN) 합의 값이 다른 환자라면, 같은 정신 질환을 앓고 있더라도 증상에 따른 다른 치료법이 필요하다는 것을 알 수 있다.
- 또한, 단순히 양의 상관관계의 증상을 파악하는 것 외에도 음의 상관관계, 커뮤니티의 양상, 중심성 지수 값에 따라서도 다른 인사이트를 도출할 수 있다.
- 모든 Cluster에서 높은 중심성 지수를 띠는 17번 (명확한 생각의 어려움) 증상은 환자의 특징과 크게 관련 없이 표적 치료 증상이 될 수 있을 것이다. 마찬가지로 Cluster에 관계 없이 높은 상관관계를 띠는 증상들도 존재하는데, A-B(직업활동/학습 - 대인관계), 19-15(적절한 행동 - 나와 타인의 구별) 또한 정신 질환 증상 연구에 활용이 가능할 것이다.
- 정신질환 증상 평가 점수 네트워크 분석 SW 개발을 위해 앞선 과정을 레퍼런스 삼아 동일한 방법론으로 Python으로 프로그래밍 언어를 변경할 계획이다. 이때 가우시안 그래피컬 모델을 만들 수 있는 skggm, sklearn을 이용할 것이며, dash, networkx package를 이용해 웹 기반 시각화 대시보드를 제작하여 연구를 희망하는 신경정신의학 전문가들에게 배포할 예정이다.

## Schedule

| 추진 내용  | 3월 | 4월 | 5월 | 6월 | 7월~ |
| -------- | -- | -- | -- | -- | -- |
| 선행 연구 공부 및 네트워크 분석 공부  | ✔️ |  |  |  |  |
| GGM 및 Lasso 공부  |  | ✔️ |   |  |  |
| 계층적 클러스터링 |   | ✔️ |   |  |  |
| 상관계수 선정 및 방법론 결정  |   |  | ✔️ |  |  |
| network matrix 제작 |   |  | ✔️ |  |  |
| 시각화 결과 분석 및 인사이트 도출  |    |  | | ✔️ |  |
| 대시보드 제작  |    |  |  |  | ✔️ |


