# Single Domain Generalization

Keywords : worst-case scenario in model generalization, Out-of-Distribution(OOD) generalization problem, domain augmentation, meata-learning scheme

Out-of-Distribution (OOD): 상관 없는 데이터 (기존의 distribution에서 벗어난 데이터)

training data와 test data가 유사한 통계 안에서 있을 것이라는 주된 가정 하에 최근의 빠르고 강력한 모델들은 성공적인 성능을 보여주었다. 하지만 Out-of-Distiribution test domain 에서는 그러하지 못한다. 

multiple training domain을 통해 이 이슈를 덜어냈다. 그렇다면 어떻게하면 하나의 source domain으로 많은 unseen target domain을 다루고 model generalization을 극대화 할 수 있을까 하는 질문이 이어진다.

소스 도메인과 타겟 도메인의 불일치 (a.k.a domain or covariate variant)는 domain adpatation 과 domain generalization에서 연구되어 왔다. 저자들은 이 연구들과는 다른 새로운 패러다임을 제안하였다. 참고. Figure 1.

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled.png)

Adversarial domain augmentation

Fictitious yest challenging populations

소스 도메인으로부터 가상의 도메인을 만드는 일은 the contradiction of semantic consistency constraint inworts-case formulation 때문에 어렵다.

이 점을 우회하기 위해서 relax the worst-case constraints via a Wasserstein Auto-Encoder (WAE) 를 제안하였다. 이는 큰 input space 의 domain transportation 을 encourage 하기 위함이다.

Adversarial domain augmentation via meta-learning

Primary contribution of this work is meta-learning based scheme that enables single domain generalization.

---

**Domain discrepancy**

Domain discrepancy 은 cross-domain recognition에서 성능을 저하시킨다. domain discrepancy를 줄이기 위해서 있어온 방식들 중 최근 일부 연구는 few-shot domain adaptation 에 초점을 맞추었다.

Domain Adaptation과는 달리 domain generalization은 multiple source domains을 target domains의 접근 없이 학습하는 것에 목표를 둔다. 대부분의 이전 방법들은 domain-invariant space를 domain을 정렬하기 위해서 혹은 domain에 특정한 모듈을 aggregate 하는 방법들이다.

- Domain specific methods : Robust place categorization with deep domain generalization,  Best sources forward: domain generalization through source-specific nets

**Adversarial training**

perturbation : 작은 변화

Adversarial training 은 adversarial perturbations or attacks에 대한 모델 개선을 위해 제시되었다. 이 논문에서 저자들은 "fictitious" domain 생성을 위해서 adversarial training을 single domain generalization 개선을 위해 적용하였다.

**Meta-learning**

Meta-learning은 새로운 컨셉이나 tasks를 어떻게 적은 training examples로 배울 수 있는가에 대한 주제이다. deep neural network의 최적화와 few-shot classification을 위해 널리 사용 되었다. 최근 few-shot learning 과 reinforcement learning을 위한 Model-Augnostic Meta-Learning (MAML)이 제시되었다. MAML의 목적은 좋은 initialization 새로운 tasks에 적은 gradient step으로 빠르게 적응하여 찾는 것에 있다. 

MAML-based approach to solve domain generalization, Adaptive regularizer through meta-learning for cross domain recognition 에 대한 연구들이 있지만 single domain generalization에는 부적합하다.

이 논문에서 저자들은 single domain generalization 을 위해 "fictitious" domains 에서 효과적으로 모델을 학습는 meta-learning scheme을 제안한다.

---

**Method**

모델이 오직 하나의 소스 도메인 S 만을 배우지만 본 적 없는 많은 target domain T에 대해서 일반화를 기대한다는 single domain generalization 문제를 해결하기 위한 방법을 제시하였다.

핵심 아이디어는 out-of-distribution perturbation에 저항하는 robust model을 학습시킨다는 것이다.

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%201.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%201.png)

Equation (1)

더 상세하게 말하자면, worst-case problem에 대해 해결하는 모델을 학습시키는 것이다. 위의 식을 보자. D는 domain distance를 측정하기 위한 similarity metric, $\rho$는 S와 T 사이의 가장 큰 domain discrepancy, $\theta$는 task-specific objective function $L_{task}$에 따른 모델 파라미터이다.

즉 Target domain T와 Source Domain S 사이의 domain distance가 $\rho$ 이하를 충족하는 T 에 대해 task loss를 최소화 하고자 하는 것이 목적이다. ⇒ loss const

Cross entropy loss 를 사용하여 classification 문제에 집중해본다. 

rho는 어떻게 정하는가?

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%202.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%202.png)

Equation (2)

Worst-case formulation (1)에 따라 Meta-Learning based Adversarial Domain Augmentation (M-ADA) 라는 새로운 방법을 제시한다. "fictitious" yest "challenging" domains를 adversarial training을 통해 source doamin을 augment 하기 위해 생성한다. Task model은 Wasserstein Auto-Encoder (WAE, relaxes the worst-case constraint 역할)의 도움을 받아 domain augmentations을 학습한다. Task model과 WAE의 연결을 구성하고 또, domain augmentation procedure 도 함께 구성한다.

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%203.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%203.png)

중간 정리.

- Source domain을 classification 하는 loss task
- 조건에 맞는 Target domain에 대해 Loss를 최소화하여 unseen domain에 대해서도 Task를 잘 수행해야함.
- WAE로 $L_{relax}$를 계산. 자세한 내용은 추후 기술.

**Adversarial Domain Augmentation**

Goal **:** to create multiple augmented domains from the source domain

augmented domains의 발산을 방지하기 위해, the worst-case in equation (1) 역시 만족되어야한다.

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%204.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%204.png)

Loss of Adversarial Domain Augmentation = Loss of classification - loss of constraint + loss of relaxation.

$L_{task}$ : classification loss defined in Eq. (2)

$L_{const}$ : worst-case guarantee defined in Eq. (1)

$L_{relax}$ : it guarantees large domain transportation in Eq. (7)

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%205.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%205.png)

Adversarial samples $X^+$ in the augmented domain $S^+$

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%206.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%206.png)

$L_{const}$

Wasserstein 거리로 측정된 소스 도메인 외부의 일반화 능력을 제어한다.

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%207.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%207.png)

1{$\cdot$} is the 0-1 indicator function, if class label of $X^+$ is different from X, Loss will be $\infin$

$L_{relax}$

to relax the semantic consistency constraint and create large domain transportation

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%208.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%208.png)

여기까지의 이해와 의문점.

- 이 논문의 핵심은 ADA 로 data generate 를 어떻게 할 것인지가 관건이다.
- Loss of const 는 최악의 경우를 보장하기 위함
    - 즉 Loss가 커지는 방향으로 학습, 하지만 divergence가 발생할 위험.
    - 이를 위해 Equation 1을 따르는 경우만으로 한정 지어 Loss를 계산 (즉, 한계를 정한 Loss의 증가)
    - 수식을 보면 squared L2 norm 을 취한 MSE 형식과 유사, z는 embedding space 상의 feature 이기에 distance로 보는 것이 적합
    - z 와 z+ 의 차이의 squared L2 norm을 2로 나눈 값.
        - Class label이 같을때 도메인의 차이를 극대로 벌리기 위해서.
- Loss of ADA를 구할때 Loss of constraint 는 다른 loss 들과 달리 뺄셈 연산.
    - 그런데 Equation (5)에서는 label x 와 label x+가 다를 경우 Loss of const 는 infinite
    - 즉 class 간의 비교에서 **다른 class 와의 비교가 즉, 최악의 경우가 되는건가?**
    - class가 같다면 domain을 최대한 멀도록 하는 것이 유리. (데이터 생성 측면에서)
- Figure 3 에서 Loss of const + Loss of relax의 합이 중간 이미지
    - Loss of ADA에서는 마이너스 연산이었는데 이미지에서는 플러스 연산
    - 실제 덧셈을 의미하는 게 아니라 incorporate 한다는 의미로 받아들이는 중.

Relaxation of Wasserstein Distance Constraint

Loss of relax

- to encourage out-of-domain augmentations
    - source 와는 다른 domain을 만들어야하니까
    - adversasrial smaples x+ in the augmented domain S+
    - V : WAE parameterized by $\psi$
        - V consists of an encoder Q(e|x) and a decoder G(x|e)

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%209.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%209.png)

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%2010.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%2010.png)

Meta-Learning Single Domain Generalization

2. Outer 에서 augmented 된 source domain S+를 생성하고

3. generate를 위한 V(WAE)를 S+로 재학습시킨다.

4. Source Domain에 대해서 loss of  task 를 구함.

5. $\hat{\theta}$를 Source domain 에 대한 loss task로 gradient descent

7. augmented 된 Source domains들에 대해 각각 5에서 updated 된 weight로 loss of task를 계산한다.

8. meta train과 meta test에서 구한 loss들을 모두 합한 loss로 gradient descent를 진행한다. Eq.(9)

![Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%2011.png](Single%20Domain%20Generalization%20a7803e0c71e34bdabc3b806876bb9bc8/Untitled%2011.png)

만약 이 문제에서 ADA 부분을 generation 하지 않고 이미 존재하는 dataset (e.g. PACS, DomainNet) 에서 가지고 와서 학습한다고 하면 Single Domain Generalization이 어떤 식으로 구성될까?

Source 에 대해 meta train을 진행하고 update 된 theta 값을 다른 도메인 데이터로 loss of task를 진행. 그리고 loss의 합으로 update. 그렇게까지 novelty가 있는가는 잘 모르겠다.

내가 활용하기 위한 Single Domain Generalization에 대한 정리는 여기서 끝

Experiment 이후 부분은 생략.