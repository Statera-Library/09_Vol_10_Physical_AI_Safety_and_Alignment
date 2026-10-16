**Volume 10. Physical AI Safety and Alignment**

# Chapter 00. Introduction

## 00.01. Why Safety is Fundamental to Physical AI

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

피지컬 AI(Physical AI)는 그 의사결정이 움직임, 힘, 열, 전력 및 기타 물리적 효과로 변환된다는 점에서 기존의 디지털 AI(Digital AI)와 근본적으로 다르다. 소프트웨어 서비스의 잘못된 예측은 부정확한 정보를 생성하는 데 그칠 수 있지만, 자율 기계(Autonomous Machine)의 잘못된 의사결정은 충돌, 부상, 장비 손상 또는 환경적 위험을 초래할 수 있다. 따라서 안전(Safety)은 선택적으로 추가되는 기능이 아니라 시스템의 근본적인 속성으로 다루어져야 한다.

피지컬 AI 시스템(Physical AI System)은 인지(Perception), 추론(Reasoning), 행동(Action), 물리적 환경(Physical Environment) 사이에서 지속적으로 폐루프(Closed Loop)를 형성한다. 카메라(Camera), 라이다(LiDAR), 레이더(Radar), 촉각 센서(Tactile Sensor), 위치추정 시스템(Localization System) 등의 센서는 현재 세계의 상태를 추정하며, 학습 모델(Learned Model)은 그 상태를 해석하고 행동을 선택한다. 이후 액추에이터(Actuator)가 환경을 변화시키면서 새로운 관측과 의사결정이 발생한다. 따라서 오류는 이러한 폐루프를 통해 전파되어 실제 물리적 결과로 이어질 수 있다.

피지컬 AI는 설계나 학습 단계에서 완전하게 예측할 수 없는 환경에서 동작하기 때문에 안전 문제는 더욱 어려워진다. 사람은 예상하지 못한 방향으로 움직이고, 물체의 위치는 변하며, 표면은 미끄러워질 수 있고, 센서는 가려지거나 통신 연결이 끊어질 수 있으며, 학습 과정에서 경험하지 못한 새로운 상황이 나타날 수 있다. 따라서 안전한 시스템은 불확실성(Uncertainty)과 분포 변화(Distribution Shift)를 처리하면서 자신의 지식이나 인지가 신뢰할 수 있는 행동을 수행하기에 부족한 상황을 스스로 인식해야 한다.

전통적인 자동화(Traditional Automation)는 일반적으로 결정론적 논리(Deterministic Logic), 사전에 정의된 운영 조건(Predefined Operating Conditions), 세밀하게 설계된 안전 경계(Safety Boundary)에 의존한다. 반면 피지컬 AI는 학습 기반 인지(Learned Perception), 월드 모델(World Model), 강화학습(Reinforcement Learning), 파운데이션 모델(Foundation Model), 비전-언어-행동 모델(Vision-Language-Action Model, VLA)을 점차 도입하고 있다. 이러한 구성요소는 적응성과 일반화 능력을 향상시키지만, 그 행동을 항상 단순한 결정론적 규칙으로 표현할 수 있는 것은 아니다. 따라서 안전 공학(Safety Engineering)은 학습 기반 및 확률적 행동(Probabilistic Behavior)과 함께 작동할 수 있어야 한다.

안전은 AI 모델(AI Model) 하나에만 맡길 수 없다. 실제 물리적 피해는 일반적으로 여러 하위 시스템(Subsystem)의 상호작용에서 발생하기 때문이다. 인지 오류(Perception Error)는 위치추정(Localization)을 손상시킬 수 있고, 위치추정의 불확실성은 경로 계획(Planning)을 왜곡할 수 있으며, 그 결과 안전하지 않은 궤적(Trajectory)이 제어기(Controller)에 의해 실행될 수 있다. 여기에 기계적 한계, 액추에이터 고장, 네트워크 지연, 열적 상태 또는 인간의 행동이 문제를 더욱 증폭시킬 수 있다. 따라서 피지컬 AI 안전(Physical AI Safety)은 시스템 수준의 속성(System-Level Property)으로 다루어져야 한다.

유용한 안전 아키텍처(Safety Architecture)는 지능적 능력(Intelligent Capability)과 제한 없는 물리적 행동을 수행할 권한(Physical Action Authority)을 분리한다. AI는 예측, 계획, 궤적 또는 명령을 생성할 수 있지만, 독립적인 안전 메커니즘(Independent Safety Mechanism)은 이러한 출력이 정의된 안전 제약조건(Safety Constraint) 내부에 존재하는지를 검증한다. 동작 제한(Motion Limit), 보호 구역(Protected Zone), 충돌 검사(Collision Check), 안전 제어기(Safety Controller), 비상 정지(Emergency Stop), 런타임 모니터(Runtime Monitor)는 주요 지능 시스템이 잘못되거나 불확실한 결정을 생성하더라도 위험한 행동을 제한할 수 있다.

불확실성(Uncertainty)은 피지컬 AI 시스템이 자신이 이해하고 있는 상황과 내부 모델을 신뢰하기 어려운 상황을 구별해야 한다는 점에서 특히 중요하다. 신뢰도 추정(Confidence Estimation), 분포 외 탐지(Out-of-Distribution Detection, OOD Detection), 센서 상태 모니터링(Sensor Health Monitoring), 예측 일관성(Prediction Consistency), 이상 탐지(Anomaly Detection)는 정상적인 자율 운용을 계속할 수 있는지를 판단하는 근거를 제공한다. 불확실성이 지나치게 증가하면 감속, 정지, 재계획(Replanning), 인간 지원 요청과 같은 보수적 행동(Conservative Behavior)이 지능적 운용의 일부가 되어야 한다.

안전은 모든 구성요소가 항상 정상적으로 작동한다고 가정하는 것이 아니라 고장(Failure)을 명시적으로 고려해야 한다. 센서는 고장날 수 있고, 위치추정 성능은 저하될 수 있으며, AI 추론(Inference)은 허용된 시간 제한을 초과할 수 있다. 프로세서는 과열될 수 있고, 배터리는 위험 수준까지 감소할 수 있으며, 클라우드(Cloud) 또는 플릿(Fleet) 인프라와의 통신이 끊어질 수도 있다. 따라서 강건한 피지컬 AI(Robust Physical AI)는 성능 저하 운용 모드(Degraded Mode), 폴백 제어기(Fallback Controller), 최소 위험 상태(Minimum-Risk Condition), 임무 중단 전략(Mission-Abort Strategy), 명확하게 정의된 안전 상태(Safe State)를 갖추어야 한다.

인간과의 상호작용(Human Interaction)은 또 다른 핵심적인 안전 차원을 형성한다. 로봇은 작업자, 승객, 환자, 보행자, 운영자 또는 다른 사용자 주변에서 동작하는 경우가 많으며, 이들의 의도를 완벽하게 예측할 수는 없다. 기계는 사람을 탐지하고 추적하면서 거리, 속도, 힘 및 작업 공간에 관한 제약조건을 준수해야 한다. 또한 로봇은 자신의 의도(Robot Intent)를 명확하게 전달하여 인간이 자율 행동에 놀라는 대신 움직임을 예측하고 필요한 경우 개입할 수 있도록 해야 한다.

정렬(Alignment)은 이러한 문제를 단순한 충돌 회피(Collision Avoidance) 이상의 영역으로 확장한다. 물리적 능력을 가진 AI 시스템은 인간의 목표와 명령을 물리적, 운영적, 사회적, 안전 제약조건에 부합하는 행동으로 변환해야 한다. 어떤 명령은 기술적으로 수행 가능하더라도 현재 상황에서는 안전하지 않을 수 있다. 따라서 물리적 정렬(Physical Alignment)은 어떤 행동이 목표를 달성할 수 있는지를 판단하는 것뿐만 아니라 현재 조건에서 그 행동을 실제로 실행해야 하는지를 추론할 수 있어야 한다.

자율성(Autonomy)이 증가할수록 런타임 보증(Runtime Assurance)의 중요성도 커진다. 배치 이전 검증(Pre-Deployment Verification)만으로는 실제 운용 중 발생할 수 있는 환경, 인간 행동, 모델 불확실성, 구성요소 성능 저하 및 희귀 사건(Rare Event)의 모든 조합을 검증할 수 없다. 독립적인 런타임 모니터링(Independent Runtime Monitoring)은 인지 상태, 시스템 자원, 궤적, 안전 영역(Safety Envelope), 월드 모델 일관성(World-Model Consistency), AI 신뢰도를 지속적으로 평가하고 행동이 허용할 수 없는 경계에 접근할 경우 보호 메커니즘이 개입할 수 있도록 한다.

안전은 또한 시스템의 전체 생명주기(System Lifecycle)에 걸쳐 유지되어야 한다. 학습 데이터(Training Data), 모델 업데이트(Model Update), 소프트웨어 수정, 센서 교체, 환경 변화 및 지속학습(Continual Learning)은 최초 검증 이후에도 시스템의 행동을 변화시킬 수 있다. 따라서 로깅(Logging), 추적성(Traceability), 시나리오 기반 시험(Scenario-Based Testing), 현장 운용 증거(Field Evidence), 변경 관리(Change Management), 반복적인 검증이 필요하다. 적응형 피지컬 AI(Adaptive Physical AI)의 인증(Certification)은 궁극적으로 시스템이 진화하는 과정에서도 안전에 관한 증거를 지속적으로 유지할 수 있는 능력에 달려 있다.

궁극적인 목표는 안전을 확보하기 위해 지능(Intelligence)을 제거하는 것이 아니라, 증가하는 지능을 통제된 물리적 행동 권한(Controlled Physical Authority)과 양립할 수 있도록 만드는 것이다. 인지, 예측, 추론, 월드 모델(World Model), VLA 정책(VLA Policy), 자율학습(Autonomous Learning)은 기계가 수행할 수 있는 능력의 범위를 확장하며, 안전 아키텍처(Safety Architecture)는 이러한 능력이 어떤 조건에서 실제 행동으로 이어질 수 있는지를 결정한다. 지능, 불확실성 관리(Uncertainty Management), 런타임 보증(Runtime Assurance), 폴백 행동(Fallback Behavior), 인간 감독(Human Oversight)이 하나의 통합 시스템으로 작동할 때 피지컬 AI는 신뢰할 수 있는 시스템으로 발전할 수 있다.

## 00.02. From AI Error to Physical Harm

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

AI 오류(AI Error)는 지능이 물리적 시스템(Physical System)에 연결될 때 근본적으로 다른 의미를 갖게 된다. 디지털 애플리케이션(Digital Application)에서는 잘못된 분류, 예측 또는 생성된 응답이 정보적 실패(Informational Failure)에 머물 수 있다. 그러나 피지컬 AI(Physical AI)에서는 동일한 유형의 계산 오류가 모터, 바퀴, 매니퓰레이터(Manipulator), 차량 또는 기타 액추에이터(Actuator)에 영향을 줄 수 있다. 따라서 정보는 물리적 행동으로 변환되며, 모델 오류(Model Error)에서 현실 세계의 물리적 피해(Physical Harm)로 이어지는 직접적인 경로가 형성된다.

오류에서 피해로의 전환은 일반적으로 하나의 독립된 고장이 아니라 연속적인 인과 사슬(Causal Chain)을 통해 발생한다. 센서는 관측 정보를 생성하고, 인지 모델(Perception Model)은 이를 해석하며, 위치추정(Localization)은 시스템 상태를 추정한다. 이후 계획(Planning)은 궤적이나 행동을 선택하고, 제어(Control)는 그 결정을 액추에이터 명령으로 변환한다. 어느 단계에서 발생한 오류라도 이후 단계로 전파될 수 있으므로 안전 분석(Safety Analysis)은 개별 AI 구성요소를 독립적으로 평가하는 대신 전체 인과 사슬을 분석해야 한다.

인지 오류(Perception Error)는 이러한 오류 전파를 보여주는 명확한 사례이다. 비전 모델(Vision Model)이 보행자를 탐지하지 못하거나, 장애물을 잘못 분류하거나, 물체의 형상을 부정확하게 추정할 수 있다. 그러면 계획기(Planner)는 경로가 비어 있다는 잘못된 가정을 기반으로 궤적을 생성할 수 있다. 이러한 불일치를 독립적인 안전 메커니즘(Independent Safety Mechanism)이 탐지하지 못하면 제어기는 기술적으로는 유효하지만 실제로는 위험한 물리적 움직임을 실행할 수 있다.

위치추정(Localization)과 상태 추정(State Estimation)의 오류 역시 계산상의 오류가 물리적 위험으로 전환되는 또 다른 경로를 만든다. 센서 성능 저하, 지도 오류, 불완전한 시간 동기화(Time Synchronization), 환경적 모호성 때문에 로봇은 자신의 위치, 방향, 속도 또는 주변 물체와의 관계를 잘못 추정할 수 있다. 계획기와 제어기가 입력에 따라 올바르게 작동하더라도 잘못된 상태 추정은 결과적인 움직임이 실제 물리적 경계를 침범하도록 만들 수 있다.

계획 오류(Planning Error)는 정확하게 인식된 환경조차 위험한 행동으로 변환할 수 있다. 계획기는 사람과 지나치게 가까운 궤적을 선택하거나, 속도 제약조건을 위반하거나, 제한 구역에 진입하거나, 충분한 제동 거리(Braking Distance)를 확보하지 못할 수 있다. 학습 기반 계획기(Learned Planner)와 범용 정책(Generalist Policy)은 명시적으로 프로그래밍된 안전 규칙만이 아니라 데이터에서 학습된 패턴에 의존할 수 있기 때문에 추가적인 불확실성을 발생시킬 수 있다.

제어(Control)와 구동(Actuation)은 위험한 결정이 실제 물리적 에너지(Physical Energy)로 전환되는지를 결정한다. 궤적 추종(Trajectory Tracking), 액추에이터 명령, 힘 제어(Force Control), 타이밍 또는 저수준 제어(Low-Level Control)의 오류는 의도한 행동에서 벗어난 움직임을 발생시킬 수 있다. 기계적 관성(Mechanical Inertia), 차량 질량, 매니퓰레이터 페이로드(Payload), 속도 및 액추에이터 출력은 이러한 편차가 얼마나 심각한 결과를 발생시킬지를 결정한다. 따라서 물리적 피해는 오류 발생 여부뿐 아니라 시스템이 보유한 에너지와 행동 권한(Action Authority)에 의해서도 결정된다.

물리적 환경(Physical Environment)은 작은 계산 오류를 증폭시킬 수 있다. 작은 위치추정 오차는 넓은 공간에서는 중요하지 않을 수 있지만 계단, 기계, 차량 또는 사람 가까이에서는 위험할 수 있다. 짧은 인지 지연(Perception Delay)도 저속에서는 거의 영향을 주지 않을 수 있지만 고속 운용에서는 치명적인 문제가 될 수 있다. 따라서 위험(Risk)은 상황 의존적이며, 동일한 AI 오류라도 노출도(Exposure), 환경, 운용 속도, 시스템 질량 및 위험요소와의 거리에 따라 완전히 다른 결과를 발생시킬 수 있다.

오류는 시간이 지나면서 누적될 수도 있다. 월드 모델(World Model)이 다른 에이전트(Agent)의 움직임을 조금 잘못 예측하면 계획기는 최적이 아닌 궤적을 선택할 수 있다. 그 결과 발생한 움직임은 이후 관측 자체를 변화시키고, 이는 다시 예측 불확실성을 증가시켜 추가적인 계획 오류를 발생시킬 수 있다. 폐루프 피지컬 AI(Closed-Loop Physical AI)에서는 반복되는 작은 부정확성이 누적되어 시스템의 내부 표현(Internal Representation)과 실제 물리적 세계 사이에 상당한 차이를 발생시킬 수 있다.

불확실성(Uncertainty)은 시스템이 신뢰하기 어려운 추정 결과를 확실한 정보처럼 취급할 때 위험해진다. AI 모델은 익숙하지 않은 환경, 비정상적인 물체, 성능이 저하된 센서 입력 또는 학습 분포 밖의 상황에서도 높은 신뢰도의 출력을 생성할 수 있다. 따라서 안전 지향 시스템(Safety-Oriented System)은 예측 결과뿐 아니라 그 예측의 신뢰성(Reliability)까지 평가해야 한다. 높은 불확실성은 공격적인 자율 행동을 허용하는 것이 아니라 시스템의 물리적 행동 권한을 감소시키는 방향으로 작용해야 한다.

인간과의 상호작용(Human Interaction)은 사람이 동적이고 다양하며 정확하게 예측하기 어렵기 때문에 오류 전파(Error Propagation)를 특히 중요하게 만든다. 로봇은 사람을 정확하게 탐지하더라도 그 사람의 의도, 미래 움직임 또는 로봇에 대한 인지 상태를 잘못 추론할 수 있다. 따라서 안전한 행동은 예측 오류와 인간 행동의 불확실성을 고려한 안전 여유(Safety Margin)를 필요로 한다. 저속 이동, 더 큰 안전거리, 명확한 의사소통 및 보수적 계획(Conservative Planning)은 불확실한 해석이 위험한 상호작용으로 전환되는 것을 방지할 수 있다.

모든 AI 오류가 액추에이터까지 전달되도록 허용해서는 안 된다. 심층 방어 아키텍처(Defense-in-Depth Architecture)는 지능적 의사결정과 물리적 실행 사이에 독립적인 안전 장벽(Safety Barrier)을 배치한다. 안전 제약조건(Safety Constraint), 충돌 검사(Collision Checking), 보호 구역(Protected Zone), 속도 제한(Speed Limit), 힘 제한(Force Limit), 런타임 모니터(Runtime Monitor), 독립 안전 제어기(Independent Safety Controller)는 위험한 명령을 거부하거나 수정할 수 있다. 이러한 메커니즘은 주요 AI의 실패가 전체 물리 시스템의 실패로 직접 이어지지 않도록 인과 사슬을 차단한다.

정상적인 자율 운용(Autonomous Operation)을 더 이상 신뢰할 수 없는 경우 시스템에는 통제된 폴백 행동(Fallback Behavior)이 필요하다. 상황에 따라 감속, 동작 정지, AI 제어에서 보다 단순한 전통적 제어기(Classical Controller)로의 전환, 중복 센서(Redundant Sensor)의 활용, 인간 지원 요청 또는 사전에 정의된 최소 위험 상태(Minimum-Risk Condition)로의 전환이 포함될 수 있다. 목적은 불확실성, 성능 저하 또는 구성요소 고장이 통제되지 않은 상태로 지속되어 물리적 피해로 이어지는 것을 방지하는 것이다.

AI 오류에서 물리적 피해로 이어지는 경로를 이해하면 AI 안전(AI Safety)의 의미도 달라진다. 정확도(Accuracy)만으로는 충분하지 않다. 비슷한 오류율을 가진 두 모델도 완전히 다른 수준의 물리적 위험을 발생시킬 수 있기 때문이다. 안전은 오류가 어디에서 발생하는지, 오류가 다른 단계로 전파될 수 있는지, 시스템이 얼마나 큰 물리적 행동 권한을 가지고 있는지, 어떤 위험요소에 노출되어 있는지, 그리고 어떤 안전 장벽이 오류의 연쇄를 차단할 수 있는지에 따라 결정된다. 따라서 평가는 모델 성능(Model Performance)을 시스템 행동(System Behavior) 및 실제 세계의 결과(Real-World Consequences)와 연결해야 한다.

궁극적으로 피지컬 AI 안전(Physical AI Safety)은 AI 오류에서 물리적 피해로 이어지는 경로를 통제하는 공학적 체계로 이해할 수 있다. 인지(Perception), 위치추정(Localization), 예측(Prediction), 계획(Planning), 제어(Control), 하드웨어(Hardware), 인간(Human), 환경(Environment)은 하나의 상호 연결된 인과 시스템(Interconnected Causal System)을 형성한다. 목표는 오류를 완전히 제거할 수 있다고 가정하는 것이 아니라 오류를 탐지하고, 전파를 억제하며, 물리적 결과를 제한하고, 지능이 불확실해지거나 실패하더라도 안전한 행동을 유지하는 것이다.

## 00.03. Safety Security Reliability and Alignment

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

## 00.04. Traditional Robot Safety vs AI Safety

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

전통적인 로봇 안전(Traditional Robot Safety)은 주로 사전에 정의된 프로그램, 결정론적 제어기(Deterministic Controller), 고정된 작업 공간, 알려진 운영 절차에 의해 행동을 제한할 수 있는 기계를 대상으로 발전해 왔다. 위험은 인간의 접근 제한, 동작 제한, 안전 구역(Safety Zone) 설정, 하드웨어 고장 감시, 사전에 정의된 조건 위반 시 안전 상태(Safe State)로의 전환을 통해 관리되었다. 이러한 접근법은 여전히 필수적이지만, 피지컬 AI(Physical AI)는 항상 사전에 완전하게 기술할 수 없는 행동을 새롭게 도입한다.

산업용 로봇(Industrial Robot)은 전통적으로 기계와 주변 환경 사이의 관계를 통제함으로써 안전을 확보한다. 가드(Guard), 펜스(Fence), 인터록(Interlock), 비상 정지(Emergency Stop), 안전 등급 센서(Safety-Rated Sensor), 속도 제한, 힘 제한, 분리 거리 모니터링(Separation Monitoring)은 위험한 움직임에 대한 노출을 감소시킨다. 운용 조건이 명확하게 정의된 경우 엔지니어는 위험 상태(Hazardous State)를 식별하고, 허용할 수 없는 물리적 결과가 발생하기 전에 이를 방지하거나 종료하는 결정론적 메커니즘을 구현할 수 있다.

전통적인 안전 공학(Traditional Safety Engineering)은 제어 시스템의 행동을 사양(Specification), 상태 머신(State Machine), 고장 모드(Failure Mode), 타이밍 제약조건(Timing Constraint), 고장에 대한 예측 가능한 대응을 통해 분석할 수 있다고 가정한다. 검증(Verification)을 통해 정의된 요구사항이 지정된 조건에서 충족되는지를 입증할 수 있다. 복잡한 제어 소프트웨어도 동일한 입력에 대해 반복 가능한 행동을 생성할 것으로 기대되므로 요구사항, 구현, 시험 및 안전 증거(Safety Evidence) 사이의 추적성(Traceability)을 비교적 직접적으로 확보할 수 있다.

AI 안전(AI Safety)은 학습된 행동이 명시적으로 프로그래밍된 규칙만으로 결정되는 것이 아니라 부분적으로 데이터에서 형성되기 때문에 새로운 종류의 불확실성(Uncertainty)을 발생시킨다. 인지 모델(Perception Model)은 환경에 따라 서로 다른 방식으로 일반화할 수 있고, 학습 기반 계획기(Learned Planner)는 학습 분포 밖의 상황을 경험할 수 있으며, VLA 정책(VLA Policy)은 상황에 따라 동일한 명령을 다르게 해석할 수 있다. 따라서 안전 문제에는 모델이 무엇을 학습했는지와 익숙하지 않은 상황에서 어떻게 행동할 것인지에 관한 불확실성도 포함된다.

이러한 차이는 인지(Perception)에서 특히 중요하다. 전통적인 안전 기능은 명시적으로 규정된 탐지 성능과 고장 대응 특성을 가진 센서에 의존하는 경우가 많다. AI 기반 인지(AI-Based Perception)는 단순한 임계값 논리(Threshold Logic)를 훨씬 넘어 복잡한 물체와 상황을 인식할 수 있지만, 그 실패 경계(Failure Boundary)를 완전하게 규정하기는 어렵다. 가림(Occlusion), 조명, 날씨, 비정상적인 물체, 센서 아티팩트(Sensor Artifact), 분포 변화(Distribution Shift)는 전통적인 하드웨어 고장을 발생시키지 않으면서도 모델 성능을 변화시킬 수 있다.

AI 모델(AI Model)은 컴퓨팅 시스템이 기술적으로 정상적인 상태에서도 실패할 수 있다. 프로세서가 정상적으로 동작하고, 메모리에서 탐지 가능한 오류가 없으며, 통신이 정상적으로 유지되고, 모든 센서가 유효한 데이터를 생성하더라도 모델은 잘못된 분류, 예측, 궤적 또는 행동을 생성할 수 있다. 따라서 구성요소의 고장을 탐지하도록 설계된 전통적인 진단(Diagnostics)만으로는 모든 위험한 AI 행동을 식별하기에 충분하지 않다.

전통적인 로봇 안전은 위험한 기계와 인간을 물리적으로 분리하거나, 엄격하게 제한된 조건에서만 협업을 허용하는 경우가 많다. 반면 피지컬 AI는 사람, 차량, 동물, 장비 및 환경 조건이 지속적으로 변화하는 개방형 또는 반구조화 환경(Open or Semi-Structured Environment)에서 점차 운용되고 있다. 따라서 안전 경계(Safety Boundary)는 단순한 기하학적 경계가 아니라 동적으로 변화해야 하며, 시스템은 움직임, 의도(Intent), 불확실성, 예측된 상호작용 및 변화하는 노출 수준을 함께 추론해야 한다.

그러나 결정론적 안전 메커니즘(Deterministic Safety Mechanism)은 AI 기반 로봇에서도 여전히 필수적이다. 비상 정지(Emergency Stop), 안전 토크 차단(Safe Torque Off), 속도 제한, 힘 제한, 보호 정지(Protective Stop), 안전 구역 및 독립 안전 제어기(Independent Safety Controller)는 AI의 정확성에 전적으로 의존하지 않는 제약조건을 제공한다. 따라서 피지컬 AI 안전은 전통적인 로봇 안전을 대체하는 것이 아니라 이를 확장해야 하며, 검증된 보호 메커니즘을 유지하면서 학습 및 적응 행동을 감독할 수 있는 새로운 방법을 추가해야 한다.

핵심적인 아키텍처 원칙은 AI 제어(AI Control)와 안전 제어(Safety Control)를 분리하는 것이다. AI 시스템은 내비게이션(Navigation), 조작(Manipulation), 작업 수행 또는 상호작용을 최적화할 수 있지만, 독립적인 안전 계층(Independent Safety Layer)은 반드시 준수해야 하는 물리적 제약조건을 강제할 수 있다. AI가 생성한 궤적이 속도 제한을 초과하거나, 분리 거리 요구사항을 위반하거나, 충돌이 예측되거나, 승인된 운용 경계(Operational Boundary)를 벗어난다면 안전 계층은 해당 행동을 제한, 수정, 거부 또는 종료해야 한다.

AI 안전은 또한 불확실성(Uncertainty)을 명시적으로 다룰 것을 요구한다. 전통적인 제어 논리는 일반적으로 정의된 상태에서 정의된 결과를 생성하지만, 학습 모델(Learned Model)은 서로 다른 신뢰도(Confidence)를 가진 추정 결과를 생성하는 경우가 많다. 피지컬 AI 시스템은 낮은 신뢰도의 인지, 분포 외 입력(Out-of-Distribution Input), 일관되지 않은 월드 모델 예측(World-Model Prediction), 비정상적인 행동을 인식해야 한다. 불확실성이 증가하면 실패가 명확하게 나타날 때까지 이를 무시하는 것이 아니라 자율성 또는 물리적 행동 권한(Physical Authority)을 점진적으로 감소시켜야 한다.

따라서 런타임 보증(Runtime Assurance)은 전통적인 안전과 AI 안전을 연결하는 핵심적인 가교가 된다. 배치 이전 검증(Pre-Deployment Verification)에만 의존하는 대신 런타임 모니터(Runtime Monitor)는 AI가 허용 가능한 안전 영역(Safety Envelope) 안에서 유지되고 있는지를 지속적으로 평가한다. 센서 상태, 모델 신뢰도, 궤적, 타이밍, 계산 자원, 위치추정 일관성(Localization Consistency), 환경 조건 및 운영 제약조건을 관찰하고, 경계에 접근하거나 이를 위반할 경우 독립적인 메커니즘이 개입할 수 있다.

검증 방법(Verification Method) 역시 발전해야 한다. 전통적인 로봇 안전은 요구사항 기반 시험(Requirement-Based Testing)과 결함 주입(Fault Injection)을 통해 명시적으로 정의된 기능을 검증할 수 있는 경우가 많다. AI 기반 시스템에는 추가적으로 데이터셋 평가(Dataset Evaluation), 시나리오 기반 시험(Scenario-Based Testing), 시뮬레이션(Simulation), 희귀 사건 분석(Rare-Event Analysis), 강건성 평가(Robustness Assessment), 분포 외 시험(Out-of-Distribution Testing), 불확실성 보정(Uncertainty Calibration), 실제 운용 증거(Real-World Operational Evidence)가 필요하다. 개방된 환경에서 동작하는 적응형 시스템(Adaptive System)의 모든 가능한 행동을 유한한 시험 집합만으로 입증할 수는 없다.

AI의 행동은 학습 데이터(Training Data), 모델 가중치(Model Weight), 프롬프트(Prompt), 정책(Policy), 파운데이션 모델(Foundation Model) 또는 적응 메커니즘(Adaptation Mechanism)이 변경될 때 달라질 수 있기 때문에 변경 관리(Change Management) 역시 더욱 어려워진다. 평균적인 작업 성능을 향상시키는 변경이라도 드물게 발생하는 안전 중요 행동(Safety-Critical Behavior)을 변화시킬 수 있다. 따라서 안전 증거는 데이터 출처(Data Provenance), 모델 버전, 검증 결과, 배치 구성, 런타임 관측, 사고 및 이후의 업데이트를 연결하면서 전체 모델 생명주기(Model Lifecycle)를 따라 관리되어야 한다.

따라서 전통적인 로봇 안전(Traditional Robot Safety)과 AI 안전(AI Safety)의 차이를 기존 공학을 새로운 AI 기술이 대체하는 것으로 이해해서는 안 된다. 전통적인 안전은 결정론적 보호(Deterministic Protection), 독립성(Independence), 고장 처리(Fault Handling), 물리적 위험 감소를 제공한다. AI 안전은 학습 모델의 실패, 불확실성, 일반화(Generalization), 적응 행동(Adaptive Behavior), 월드 모델 오류(World-Model Error), 자율 추론(Autonomous Reasoning)에 대응하는 메커니즘을 추가한다. 피지컬 AI에서는 이 두 가지 안전 체계가 상호 보완적인 계층으로 함께 작동해야 한다.

결과적으로 피지컬 AI의 안전 철학(Safety Philosophy)은 예측 가능한 보호 메커니즘과 지능적이지만 지속적으로 감독되는 자율성(Supervised Autonomy)을 결합하는 방향으로 발전한다. AI는 인지, 추론, 예측, 적응 및 범용 행동을 제공할 수 있지만, 전통적인 안전 공학은 지능이 자유롭게 위반할 수 없는 경계를 설정한다. 고도화된 자율성이 독립적인 모니터링(Independent Monitoring), 제한된 물리적 행동 권한(Constrained Physical Authority), 검증된 폴백 행동(Verified Fallback Behavior), 전체 생명주기에 걸친 안전 증거에 의해 보호될 때 신뢰할 수 있는 피지컬 AI(Trustworthy Physical AI)를 구현할 수 있다.

## 00.05. Deterministic Control vs Learned Behavior

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

결정론적 제어(Deterministic Control)와 학습된 행동(Learned Behavior)은 피지컬 AI(Physical AI)에서 행동을 생성하는 근본적으로 서로 다른 두 가지 방식을 나타낸다. 결정론적 제어기는 명시적으로 설계된 규칙, 수학적 모델, 상태 머신(State Machine), 제약조건을 기반으로 출력을 생성하는 반면, 학습 시스템은 데이터나 경험에서 획득한 패턴을 기반으로 행동을 생성한다. 현대의 로봇은 안전한 운용을 위해 예측 가능성(Predictability)과 적응성(Adaptability)이 동시에 필요하기 때문에 두 가지 접근법을 점차 결합하고 있다.

결정론적 제어에서는 엔지니어가 측정 가능한 상태와 입력에 대해 시스템이 어떻게 반응해야 하는지를 명시적으로 정의한다. 동일한 초기 조건, 센서 값, 제어기 파라미터 및 타이밍 조건이 주어진다면 시스템은 예측 가능한 반응을 생성할 것으로 기대된다. PID 제어기(PID Controller), 모델 기반 제어기(Model-Based Controller), 궤적 추종기(Trajectory Tracker), 상태 머신, 인터록(Interlock), 규칙 기반 안전 로직(Rule-Based Safety Logic)은 이러한 철학을 대표하며, 행동을 비교적 투명하게 만들고 체계적인 검증(Verification)을 가능하게 한다.

이러한 예측 가능성은 안전 중요 기능(Safety-Critical Function)에서 특히 중요하다. 최대 속도, 가속도, 조향각, 관절 위치, 액추에이터 힘, 제동 동작, 보호 구역(Protected Zone), 비상 정지(Emergency Stop) 반응은 명시적인 제약조건으로 표현할 수 있다. 엔지니어는 이러한 제한이 충족되는지를 분석하고 위반될 경우 제어기가 어떻게 반응하는지를 결정할 수 있다. 따라서 결정론적 메커니즘(Deterministic Mechanism)은 반드시 준수해야 하는 물리적 경계(Physical Boundary)를 강제하는 강력한 기반을 제공한다.

그러나 사전에 정의된 규칙으로 효율적으로 표현할 수 없는 복잡성이 환경에 포함되면 결정론적 제어는 점점 어려워진다. 사람, 차량, 장애물, 변화하는 지형 및 익숙하지 않은 물체 사이에서 운용되는 이동 로봇(Mobile Robot)은 매우 많은 가능한 상황을 경험할 수 있다. 모든 조합에 적절한 대응을 명시적으로 프로그래밍하면 복잡성이 급격히 증가하며, 그럼에도 개방된 세계(Open World)에서 발생하는 모든 조건을 사전에 예측할 수는 없다.

학습된 행동(Learned Behavior)은 모델과 정책(Policy)이 데이터, 시연(Demonstration), 시뮬레이션(Simulation), 강화 신호(Reinforcement Signal) 또는 상호작용에서 유용한 표현과 행동 전략을 추출하도록 함으로써 이러한 한계를 해결한다. 신경망 기반 인지 모델(Neural Perception Model)은 복잡한 물체를 인식할 수 있고, 학습 기반 계획기(Learned Planner)는 고차원 상황을 평가할 수 있으며, 비전-언어-행동 모델(Vision-Language-Action Model, VLA)은 의미적 명령(Semantic Instruction)을 물리적 행동과 연결할 수 있다. 이를 통해 엔지니어가 명시적으로 정의한 제한된 조건을 넘어 일반화(Generalization)할 수 있다.

따라서 학습된 행동의 장점은 적응성(Adaptability)이지만, 적응성은 동시에 불확실성(Uncertainty)을 발생시킨다. 모델은 학습 분포(Training Distribution)에서는 우수하게 작동하면서도 익숙하지 않은 물체, 비정상적인 조명, 드문 인간 행동, 센서 성능 저하 또는 새로운 환경에서는 예상하지 못한 반응을 보일 수 있다. 기존 소프트웨어 고장과 달리 모델은 계산적으로 정상적인 상태를 유지하면서도 잘못된 결정을 생성할 수 있다. 결과적으로 정상 행동과 위험 행동 사이의 경계(Failure Boundary)를 완전하게 정의하기 어려워질 수 있다.

학습된 행동은 확률적(Probabilistic)이거나 상황 의존적(Context-Dependent)일 수도 있다. 관측, 모델 상태, 프롬프트(Prompt), 메모리 또는 환경적 맥락의 작은 차이가 예측과 행동을 변화시킬 수 있다. 파운데이션 모델(Foundation Model)과 VLA 정책(VLA Policy)은 인지, 언어, 추론 및 행동 생성을 결합하면서 이러한 행동 공간(Behavioral Space)을 더욱 확장한다. 이러한 유연성은 범용 로보틱스(General-Purpose Robotics)에 유용하지만 가능한 모든 입력과 행동의 관계를 완전하게 명세하는 것을 현실적으로 어렵게 만든다.

결정론적 시스템과 학습 시스템의 차이를 기존 기술과 새로운 기술 중 하나를 선택하는 문제로 단순화해서는 안 된다. 결정론적 제어는 요구사항을 명시적으로 정의할 수 있고 엄격한 보장이 필요한 영역에서 가장 강점을 가지며, 학습된 행동은 인지, 예측, 의미 이해(Semantic Understanding), 적응 및 일반화가 중요한 영역에서 강점을 가진다. 피지컬 AI 아키텍처(Physical AI Architecture)는 각각의 장점에 따라 서로 다른 책임을 두 접근법에 할당할 수 있다.

따라서 유용한 아키텍처는 지능적 행동 생성(Intelligent Action Generation)과 안전 권한(Safety Authority)을 분리한다. 학습 모델은 환경을 인식하고, 미래 상태를 예측하며, 목표를 선택하거나 궤적을 제안할 수 있지만, 결정론적이거나 독립적으로 검증된 메커니즘은 물리적 제약조건을 강제한다. AI는 어떤 행동이 효과적인지를 제안할 수 있지만, 안전 제어기(Safety Controller)는 해당 행동이 속도, 힘, 분리 거리, 작업 공간, 충돌 및 운용 제한 내에서 허용될 수 있는지를 결정한다.

이러한 분리는 AI 신뢰도(AI Confidence)가 감소할 때 특히 중요해진다. 학습 기반 계획기는 인지가 불확실하거나 환경이 학습 분포 밖에 존재하는 상황에서도 궤적을 제안할 수 있다. 런타임 보증(Runtime Assurance)은 신뢰도, 분포 외 조건(Out-of-Distribution Condition), 센서 상태, 월드 모델 일관성(World-Model Consistency), 궤적 실행 가능성(Trajectory Feasibility), 시스템 자원을 모니터링할 수 있다. 불확실성이 증가하면 아키텍처는 학습된 행동에 부여된 권한을 감소시키고 더욱 보수적인 제어(Conservative Control)로 전환할 수 있다.

학습 기반 자율성(Learned Autonomy)과 결정론적 폴백(Deterministic Fallback) 사이의 전환 자체도 신중하게 설계되어야 한다. 정상적인 조건에서는 AI에 복잡한 상황을 최적화하고 적응할 수 있는 상당한 자유도를 부여할 수 있다. 그러나 신뢰도, 시스템 상태 또는 환경 조건이 악화되면 속도를 낮추고, 운용 경계를 축소하거나, 보다 단순한 제어기를 활성화할 수 있다. 심각한 위반 상황에서는 보호 정지(Protective Stop), 최소 위험 행동(Minimum-Risk Behavior), 인간 개입(Human Intervention) 또는 임무 종료(Mission Termination)를 실행할 수 있다.

검증(Verification) 방식 역시 두 접근법에서 차이를 가진다. 결정론적 제어기는 명시적인 요구사항을 기준으로 분석, 시뮬레이션, 결함 주입(Fault Injection), 경계 시험(Boundary Testing), 추적 가능한 테스트 케이스를 이용하여 평가할 수 있는 경우가 많다. 학습된 행동은 추가적으로 데이터셋 평가(Dataset Evaluation), 강건성 시험(Robustness Testing), 불확실성 보정(Uncertainty Calibration), 분포 외 시험(Out-of-Distribution Testing), 시나리오 탐색(Scenario Exploration), 대규모 시뮬레이션 및 실제 운용 증거(Operational Evidence)를 필요로 한다. 올바른 행동을 소스 코드나 제어 방정식만으로 판단할 수 없기 때문이다.

배치 이후에도 학습이 계속되면 두 방식의 차이는 더욱 복잡해진다. 온라인 적응(Online Adaptation), 지속학습(Continual Learning), 정책 업데이트(Policy Update), 새로운 파운데이션 모델 또는 변화하는 프롬프트는 기계 시스템 자체를 변경하지 않고도 행동을 변화시킬 수 있다. 따라서 이전에 검증된 운용 가정이 더 이상 유효하지 않을 수 있다. 모델 버전 관리(Model Versioning), 데이터 출처(Data Provenance), 변경 영향 분석(Change Impact Analysis), 회귀 시험(Regression Testing), 런타임 모니터링(Runtime Monitoring), 통제된 배치(Controlled Deployment)가 적응형 피지컬 AI(Adaptive Physical AI)의 안전 생명주기에서 필수적인 요소가 된다.

궁극적으로 결정론적 제어(Deterministic Control)와 학습된 행동(Learned Behavior)은 서로 경쟁하는 아키텍처가 아니라 상호 보완적인 계층(Complementary Layer)을 형성해야 한다. 학습은 로봇이 인지하고, 이해하고, 예측하고, 수행할 수 있는 범위를 확장하는 반면, 결정론적이고 독립적으로 보증된 메커니즘(Independently Assured Mechanism)은 이러한 지능이 물리적 세계에 영향을 미칠 수 있는 방식을 제한한다. 이러한 결합을 통해 피지컬 AI는 전체 행동 공간을 사전에 완전히 알 수 없는 학습 행동에 무제한의 권한을 부여하지 않으면서도 적응성을 확보할 수 있다.

따라서 핵심적인 설계 원칙은 통제된 지능(Controlled Intelligence)이다. 의미 있는 능력을 제공하는 영역에서는 학습과 자율성을 확대하면서도 안전 중요 물리 행동(Safety-Critical Physical Action)에는 명시적인 경계를 유지해야 한다. 신뢰할 수 있는 피지컬 AI(Trustworthy Physical AI)는 모든 지능적 행동이 결정론적일 것을 요구하지 않는다. 대신 불확실한 학습 행동이 필요할 때 물리적 행동을 모니터링하고, 제한하고, 무효화하며, 성능을 단계적으로 낮추고, 안전하게 종료할 수 있는 아키텍처 내부에서 동작하도록 보장해야 한다.

## 00.06. Open World and Uncertainty Challenges

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

피지컬 AI(Physical AI)는 배치(Deployment) 이전에 환경을 완전하게 정의할 수 없는 오픈 월드(Open World)에서 동작한다. 통제된 산업용 작업 셀과 달리 자율 로봇(Autonomous Robot)은 익숙하지 않은 물체, 예상하지 못한 인간 행동, 변화하는 지형과 날씨, 임시 구조물, 손상된 인프라 또는 학습 데이터에 존재하지 않았던 상황을 만날 수 있다. 따라서 안전(Safety)은 알려진 위험뿐만 아니라 시스템이 한 번도 경험하지 못한 조건에 대한 불확실성(Uncertainty)까지 다루어야 한다.

오픈 월드 환경(Open-World Environment)은 시스템이 모든 관련 물체, 사건 또는 상태가 사전에 정의된 가능성의 집합에 속한다고 가정할 수 없다는 점에서 폐쇄 세계 가정(Closed-World Assumption)과 다르다. 로봇은 새로운 물체 범주, 익숙한 물체들의 비정상적인 조합, 예상하지 못한 장애물 또는 이전에 경험하지 못한 상호작용을 만날 수 있다. 인식된 레이블(Label)이 없다는 사실을 위험이 없다는 의미로 해석할 수 없으므로 알려지지 않은 조건(Unknown Condition)은 피지컬 AI 추론(Physical AI Reasoning)의 명시적인 일부가 되어야 한다.

불확실성(Uncertainty)은 모든 측정이 물리적 세계를 불완전하게 표현하기 때문에 센싱(Sensing) 단계에서부터 시작된다. 카메라는 조명, 눈부심, 어둠, 날씨 및 가림(Occlusion)의 영향을 받고, 라이다(LiDAR)와 레이더(Radar)는 노이즈와 환경적 아티팩트(Environmental Artifact)를 포함하며, 위치추정 센서는 드리프트(Drift)가 발생하거나 기준 정보를 잃을 수 있다. 보정 오류(Calibration Error), 동기화 문제, 센서 노화, 오염 및 부분적인 고장도 관측에 영향을 미친다. 따라서 피지컬 AI는 현실의 정확한 표현이 아니라 불완전하고 불확실한 증거를 기반으로 추론해야 한다.

인지 모델(Perception Model)은 센서 측정값을 의미적 이해(Semantic Understanding)로 변환하는 과정에서 추가적인 불확실성을 발생시킨다. 모델은 물체를 잘못 분류하거나, 부분적으로 가려진 사람을 탐지하지 못하거나, 비정상적인 형상을 잘못 이해하거나, 익숙하지 않은 입력에 높은 신뢰도를 부여할 수 있다. 특히 실제 운용 환경은 학습 데이터의 통계적 조건을 정확하게 재현하지 않기 때문에 분포 변화(Distribution Shift)가 중요하다. 따라서 신뢰할 수 있는 인지는 예측 품질뿐만 아니라 모델 지식의 한계까지 인식해야 한다.

상태 추정(State Estimation)과 위치추정(Localization)은 또 다른 불확실성 계층을 추가한다. 위치, 방향, 속도, 객체 추적(Object Track), 점유 상태(Occupancy), 환경 상태는 절대적인 사실이 아니라 추정값이다. GNSS 성능 저하, SLAM 드리프트(SLAM Drift), 모호한 랜드마크, 동적 장면, 불완전한 지도 또는 센서 간 불일치로 오류가 발생할 수 있다. 따라서 실제 추정값에 상당한 불확실성이 포함되어 있음에도 하나의 정밀한 상태값만을 기준으로 계획(Planning)하는 것은 위험할 수 있다.

예측(Prediction)은 불확실성을 미래로 확장한다. 피지컬 AI는 보행자, 차량, 로봇 또는 조작되는 물체가 어디로 움직일지, 그리고 환경이 어떻게 변화할지를 예측해야 하는 경우가 많다. 동일한 관측에서도 여러 미래 결과가 가능하기 때문에 미래 행동은 본질적으로 불확실하다. 따라서 안전한 월드 모델(World Model)은 하나의 예측 궤적이 반드시 실현된다고 가정하는 대신 여러 가능한 미래(Alternative Futures), 신뢰도(Confidence), 시간적 불확실성(Temporal Uncertainty)을 표현해야 한다.

인간 행동(Human Behavior)은 특히 어려운 오픈 월드 불확실성을 발생시킨다. 사람은 갑자기 방향을 바꾸거나, 예상된 교통 규칙을 따르지 않거나, 로봇의 의도를 잘못 이해하거나, 제한 구역에 진입하거나, 예상하지 못한 방식으로 기계와 상호작용할 수 있다. 인간 행동은 상황, 주의력, 문화, 긴급성 및 직접 관측할 수 없는 개인의 판단에 영향을 받는다. 따라서 피지컬 AI는 인간의 의도가 예측 가능해 보이는 상황에서도 충분한 안전 여유(Safety Margin)를 유지해야 한다.

학습 정책(Learned Policy)과 파운데이션 모델(Foundation Model)은 AI 자체의 능력에 대한 인식론적 불확실성(Epistemic Uncertainty)을 추가한다. 모델은 특정 상황에 대한 경험이 충분하지 않더라도 그럴듯해 보이는 응답을 생성할 수 있다. 비전-언어-행동 모델(Vision-Language-Action Model, VLA) 역시 모호한 명령, 익숙하지 않은 객체 관계 또는 학습 범위를 넘어서는 지식이 필요한 작업을 만날 수 있다. 따라서 시스템은 환경에서 발생하는 불확실성과 자체 학습 표현의 한계에서 발생하는 불확실성을 구별해야 한다.

우연적 불확실성(Aleatoric Uncertainty)과 인식론적 불확실성(Epistemic Uncertainty)은 이러한 문제를 구분하는 유용한 개념이다. 우연적 불확실성은 예측하기 어려운 보행자 움직임이나 측정 노이즈와 같이 세계 자체의 본질적인 변동성 또는 잡음에서 발생한다. 인식론적 불확실성은 불완전한 지식, 제한된 학습 데이터, 부적절한 모델 또는 익숙하지 않은 상황에서 발생한다. 추가적인 관측은 인식론적 불확실성을 감소시킬 수 있지만, 일부 우연적 불확실성은 보수적인 의사결정(Conservative Decision)과 안전 여유를 통해 관리해야 한다.

따라서 분포 외 탐지(Out-of-Distribution Detection, OOD Detection)는 중요하지만 오픈 월드 문제 전체를 해결할 수는 없다. 시스템은 관측이 학습 분포와 다르다는 사실을 탐지할 수 있지만, 그러한 차이가 실제로 위험한지를 판단하는 것은 또 다른 문제이다. 알려지지 않은 상황은 명확한 이상 현상으로 갑자기 나타나는 것이 아니라 점진적으로 발생할 수도 있다. 따라서 피지컬 AI는 모델 신뢰도, 센서 간 일치성(Sensor Agreement), 예측 일관성(Prediction Consistency), 신규성 탐지(Novelty Detection), 런타임 행동 모니터링(Runtime Behavioral Monitoring) 등 여러 지표를 함께 활용해야 한다.

불확실성(Uncertainty)은 자율 행동에 부여되는 권한(Authority)에 직접 영향을 주어야 한다. 인지가 신뢰할 수 있고 환경 조건이 검증된 경계 안에 있을 때 시스템은 정상적인 자율성(Normal Autonomy)으로 동작할 수 있다. 불확실성이 증가하면 속도, 힘, 계획 범위(Planning Horizon), 운용 영역 또는 기동 복잡성을 감소시킬 수 있다. 불확실성이 허용 가능한 한계를 초과하면 시스템은 정지하거나 최소 위험 상태(Minimum-Risk Condition)로 전환하고, 인간의 지원을 요청하거나 검증된 폴백 메커니즘(Verified Fallback Mechanism)으로 제어를 이전할 수 있다.

오픈 월드 조건은 배치 이전에 완전히 검증할 수 없기 때문에 런타임 보증(Runtime Assurance)이 필수적이다. 런타임 모니터(Runtime Monitor)는 중복 센서(Redundant Sensor)를 비교하고, 일관되지 않은 상태 추정을 탐지하며, 월드 모델 예측을 평가하고, AI 신뢰도를 모니터링하며, 궤적 실행 가능성(Trajectory Feasibility)과 시스템 상태를 확인할 수 있다. 아키텍처는 AI가 지속적으로 신뢰할 수 있다고 가정하는 대신 현재의 증거가 실제로 실행 중인 자율성 수준을 계속 정당화할 수 있는지를 반복적으로 평가해야 한다.

오픈 월드 안전(Open-World Safety)은 완전한 자율성과 완전한 실패 사이의 이분법적 선택이 아니라 점진적 성능 저하(Graceful Degradation)를 필요로 한다. 하나의 센서 손실, 위치추정 성능 저하, 불확실한 인지, 통신 장애 또는 익숙하지 않은 지형은 점진적으로 제한된 운용을 요구할 수 있다. 로봇은 속도를 줄이고, 분리 거리(Separation Margin)를 확대하며, 복잡한 기동을 피하고, 운용 영역을 제한하거나, 이미 알고 있는 영역으로 복귀할 수 있다. 성능 저하는 통제되지 않은 위험을 수용하지 않으면서 유용한 기능을 유지하기 위한 의도적인 안전 전략(Safety Strategy)이 된다.

시험(Testing) 역시 정상적인 시나리오에만 집중하는 것이 아니라 이러한 불확실성을 반영해야 한다. 시뮬레이션(Simulation), 도메인 무작위화(Domain Randomization), 시나리오 생성(Scenario Generation), 결함 주입(Fault Injection), 적대적 조건(Adversarial Condition), 희귀 사건 탐색(Rare-Event Exploration), 분포 외 평가(Out-of-Distribution Evaluation), 현장 시험(Field Testing)은 시스템을 더욱 광범위한 변화에 노출시킬 수 있다. 그러나 어떠한 유한한 검증 프로그램도 완전한 오픈 월드를 모두 열거할 수 없다. 따라서 안전 증거(Safety Evidence)는 배치 이전 시험, 런타임 모니터링 및 실제 운용 피드백(Operational Feedback)을 결합해야 한다.

오픈 월드 피지컬 AI(Open-World Physical AI)의 근본적인 과제는 단순히 예측 정확도(Prediction Accuracy)를 높이는 것이 아니라 시스템이 자신이 알고 있는 것의 한계를 인식하도록 만드는 것이다. 지능(Intelligence)은 불확실성을 인식하는 능력, 증거의 신뢰성이 약해질 때 행동 권한을 감소시키는 메커니즘, 그리고 확실하게 해석할 수 없는 상황에 대한 안전한 대응을 포함해야 한다. 따라서 신뢰할 수 있는 시스템(Trustworthy System)은 모든 것을 이해할 수 있다고 가정하는 시스템이 아니라, 세계가 자신의 이해 범위를 넘어서는 상황에서도 안전을 유지할 수 있는 시스템이다.

## 00.07. Defense in Depth for Physical AI

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

피지컬 AI(Physical AI)의 심층 방어(Defense in Depth)는 어떠한 단일 모델, 제어기, 센서 또는 안전 메커니즘도 물리적 피해(Physical Harm)를 방지하는 유일한 장벽으로 신뢰해서는 안 된다는 원칙이다. 자율 시스템은 인지(Perception), 예측(Prediction), 계획(Planning), 제어(Control), 구동(Actuation)의 연쇄 과정을 통해 동작하므로 여러 지점에서 실패가 발생할 수 있다. 따라서 위험한 행동이 물리적 세계에 도달하기 전에 이를 탐지하고, 억제하고, 차단하기 위해 독립적이고 상호 보완적인 여러 보호 계층(Protection Layer)이 필요하다.

로봇에 학습 기반 인지(Learned Perception), 월드 모델(World Model), 파운데이션 모델(Foundation Model), VLA 정책(VLA Policy), 적응형 계획(Adaptive Planning)이 도입될수록 계층화된 보호(Layered Protection)의 필요성은 더욱 커진다. 이러한 구성요소는 강력한 기능을 제공하지만 기존의 하드웨어 진단(Hardware Diagnostics)으로 탐지하기 어려운 방식으로 실패할 수 있다. 모델은 계산적으로 정상인 상태에서도 환경을 잘못 이해할 수 있다. 심층 방어는 지능형 구성요소가 때때로 잘못될 수 있음을 전제로 하고, 이러한 오류에도 주변 시스템이 안전을 유지하도록 설계한다.

첫 번째 방어 계층(Defensive Layer)은 센싱(Sensing)과 데이터 무결성(Data Integrity)에서 시작된다. 카메라, 라이다(LiDAR), 레이더(Radar), 촉각 센서(Tactile Sensor), 위치추정 시스템(Localization System) 및 기타 입력은 가용성, 보정(Calibration), 타이밍, 일관성 및 성능 저하 여부를 모니터링해야 한다. 중복 또는 상호 보완적 센싱(Redundant or Complementary Sensing)은 중요한 위험요소에 대한 독립적인 증거를 제공할 수 있다. 측정값을 교차 검증(Cross-Checking)하면 하나의 손상되거나 가려지거나 지연되거나 고장난 센서가 안전 중요 물리적 의사결정의 유일한 근거가 될 가능성을 줄일 수 있다.

두 번째 계층은 AI 인지(AI Perception)와 상태 추정(State Estimation)을 다룬다. 모델 신뢰도(Model Confidence), 분포 외 탐지(Out-of-Distribution Detection), 센서 간 일치성(Sensor Agreement), 위치추정 일관성(Localization Consistency), 신규성 탐지(Novelty Detection), 시간적 일관성(Temporal Consistency)은 시스템 내부 표현(Internal Representation)을 신뢰하기 어려운 조건을 식별하는 데 활용할 수 있다. 목표는 모든 인지 결과가 정확하다는 것을 입증하는 것이 아니라, 이용 가능한 증거가 너무 약하거나 서로 모순되어 정상적인 자율 권한(Autonomous Authority)을 정당화하기 어려운 상황을 인식하는 것이다.

예측(Prediction)과 월드 모델링(World Modeling)은 미래 상태가 본질적으로 불확실하기 때문에 또 다른 보호 계층을 필요로 한다. 로봇은 보행자의 움직임, 차량 궤적, 물체 동역학(Object Dynamics) 또는 자신의 행동이 가져올 결과를 잘못 예측할 수 있다. 안전 지향 예측(Safety-Aware Prediction)은 하나의 예측 결과에 전적으로 의존하기보다는 여러 가능한 미래(Multiple Plausible Futures)와 불확실성을 표현해야 한다. 미래의 변화를 충분한 신뢰도로 추정할 수 없을 때는 보수적인 안전 여유(Conservative Margin)를 통해 시스템을 보호할 수 있다.

계획(Planning)은 명령이 저수준 제어(Low-Level Control)에 도달하기 전에 위험한 행동을 방지할 수 있는 또 하나의 기회를 제공한다. 후보 궤적(Candidate Trajectory)과 행동은 충돌 제약조건, 속도 제한, 제동 거리(Braking Distance), 보호 구역(Protected Zone), 안정성 조건, 인간과의 분리 거리(Human Separation), 운용 경계(Operational Boundary)를 기준으로 검사할 수 있다. 학습 기반 계획기(Learned Planner)는 유연한 해결책을 제안할 수 있지만, 독립적인 검증 메커니즘(Independent Validation Mechanism)이 제안된 행동이 허용 가능한 안전 영역(Safety Envelope) 내부에 있는지를 판단해야 한다.

제어(Control)와 구동(Actuation)은 상위 수준의 지능이 실패하더라도 효과적으로 작동하는 보호 기능을 필요로 한다. 결정론적 안전 제어기(Deterministic Safety Controller), 안전 토크 차단(Safe Torque Off), 속도 및 힘 제한, 비상 정지(Emergency Stop), 보호 정지(Protective Stop), 액추에이터 모니터링(Actuator Monitoring), 하드웨어 인터록(Hardware Interlock)은 물리적 에너지를 직접 제한할 수 있다. 이러한 메커니즘은 잘못된 소프트웨어 의사결정과 위험한 움직임, 힘 또는 기계적 상호작용 사이에 최종적인 장벽을 제공할 수 있다는 점에서 특히 중요하다.

계층 간 독립성(Independence)은 효과적인 심층 방어(Defense in Depth)의 핵심 요구사항이다. 동일한 AI 모델이 행동을 생성하고, 자신의 신뢰도를 평가하며, 그 행동이 안전한지까지 판단한다면 하나의 공통 고장(Common Failure)이 세 가지 기능을 동시에 무력화할 수 있다. 따라서 중요한 안전 의사결정에는 충분히 독립적인 메커니즘, 정보원(Information Source), 소프트웨어 경로, 하드웨어 자원 또는 공학적 원리를 사용하여 하나의 실패가 모든 보호 장벽을 자동으로 손상시키지 않도록 해야 한다.

다양성(Diversity)은 공통 원인 고장(Common-Mode Failure)을 감소시킴으로써 독립성을 보완한다. 신경망 기반 인지 시스템(Neural Perception System)은 기하학적 제약조건(Geometric Constraint)으로 교차 검증할 수 있고, 학습 기반 궤적 계획기는 결정론적 충돌 검사(Deterministic Collision Checking)를 통해 감독할 수 있으며, 의미적 월드 모델(Semantic World Model)은 직접적인 센서 측정값과 비교할 수 있다. 서로 다른 기술은 서로 다른 실패 특성을 갖기 때문에 이를 신중하게 결합하면 하나의 잘못된 가정이 탐지되지 않은 채 전체 시스템을 통과하기 어려워진다.

런타임 보증(Runtime Assurance)은 실제 운용 중 이러한 계층들을 서로 연결한다. 지속적인 모니터링(Continuous Monitoring)은 센서 상태, 위치추정, AI 신뢰도, 월드 모델 일관성(World-Model Consistency), 궤적 실행 가능성(Trajectory Feasibility), 계산 타이밍, 통신 상태, 액추에이터 상태 및 환경 조건을 평가할 수 있다. 하나 이상의 지표가 악화되면 런타임 보증은 치명적인 실패가 명확하게 나타날 때까지 기다리지 않고 주요 AI에 부여된 자율성(Autonomy)을 점진적으로 제한할 수 있다.

폴백 행동(Fallback Behavior)은 또 다른 핵심 방어 계층을 형성한다. 정상적인 자율 운용을 더 이상 정당화할 수 없을 경우 시스템에는 감속, 분리 거리 확대, 기동 단순화, 검증된 제어기(Verified Controller)로의 전환, 운용 영역 제한, 안전 정지(Safe Stop), 인간 지원 요청 등의 사전에 정의된 대안이 필요하다. 비상 전환 과정 자체가 불안정하거나 예측 불가능한 행동을 발생시킨다면 신뢰할 수 있는 안전 장벽이 될 수 없으므로 폴백 자체도 반드시 검증되어야 한다.

인간 감독(Human Oversight)은 자동화된 메커니즘만으로 확실하게 해결할 수 없는 상황에 대한 추가적인 보호를 제공한다. 운영자는 모호한 명령을 확인하고, 비정상적인 시스템 상태를 검토하며, 특수한 운용을 승인하고, 자율 행동을 중단하거나, 정의된 조건에서 제어권을 인수할 수 있다. 인간 개입(Human Intervention)이 부족한 공학적 설계를 보완하는 수단이 되어서는 안 되지만, 불확실성, 신규성(Novelty), 충돌하는 목표 또는 예상하지 못한 환경 조건이 자동화 시스템의 능력을 넘어서는 경우 추가적인 독립 방어 계층이 될 수 있다.

사이버보안(Cybersecurity) 역시 손상된 정보가 정상적으로 설계된 안전 로직(Safety Logic)을 우회할 수 있기 때문에 심층 방어에 포함되어야 한다. 인증(Authentication), 권한 부여(Authorization), 보안 통신(Secure Communication), 무결성 검사(Integrity Checking), 신뢰할 수 있는 소프트웨어 업데이트(Trusted Software Update), 접근 제어(Access Control), 네트워크 분할(Network Segmentation), 이상 탐지(Anomaly Detection)는 물리적 의사결정이 의존하는 정보를 보호한다. 공격자가 피해 방지를 위해 설계된 메커니즘 자체를 비활성화하거나 조작하지 못하도록 안전 장벽 역시 악의적인 변경으로부터 보호되어야 한다.

심층 방어(Defense in Depth)는 런타임 아키텍처(Runtime Architecture)를 넘어 검증(Verification)과 생명주기 관리(Lifecycle Management)까지 확장된다. 개별 계층은 시나리오 시험(Scenario Testing), 결함 주입(Fault Injection), 시뮬레이션(Simulation), 강건성 평가(Robustness Evaluation), 보안 시험(Security Testing), 물리적 검증(Physical Validation)을 통해 독립적으로 그리고 결합된 상태로 시험되어야 한다. 엔지니어는 한 계층을 통과한 실패를 다른 계층이 실제로 탐지하는지, 공통 의존성이 숨겨진 단일 고장점(Single Point of Failure)을 만드는지를 검토해야 한다. 안전 증거(Safety Evidence)는 전체 보호 사슬의 효과성을 입증해야 한다.

데이터, 모델, 정책(Policy), 소프트웨어, 센서 또는 하드웨어의 업데이트는 방어 계층 사이의 관계를 변화시킬 수 있다. 새로운 인지 모델은 신뢰도 특성을 변화시킬 수 있으며, 계획기 업데이트는 기존 안전 검사가 이전과 다른 방식으로 처리해야 하는 궤적을 생성할 수 있다. 따라서 전체 시스템 생명주기에 걸쳐 심층 방어를 유지하기 위해 구성 관리(Configuration Management), 회귀 시험(Regression Testing), 모델 버전 관리(Model Versioning), 변경 영향 분석(Change Impact Analysis), 운용 모니터링(Operational Monitoring), 사고 피드백(Incident Feedback)이 필요하다.

핵심 철학은 개별 구성요소가 완벽하지 않더라도 피지컬 AI(Physical AI)가 안전을 유지해야 한다는 것이다. 지능은 실패할 수 있고, 센서는 성능이 저하될 수 있으며, 통신은 끊어질 수 있고, 모델은 익숙하지 않은 상황을 만날 수 있으며, 인간은 예상하지 못한 행동을 할 수 있다. 독립적인 센싱, 모니터링, 제약조건, 안전 제어(Safety Control), 폴백 행동, 사이버보안, 인간 감독 및 생명주기 보증(Lifecycle Assurance)이 불확실성과 물리적 피해 사이에 여러 개의 방어 장벽을 형성할 때 신뢰할 수 있는 피지컬 AI(Trustworthy Physical AI)를 구현할 수 있다.

## 00.08. Roadmap of Physical AI Safety and Alignment

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

피지컬 AI 안전 및 정렬(Physical AI Safety and Alignment)의 로드맵은 로봇이 결정론적 자동화(Deterministic Automation)에서 적응적이고 추론하며 점점 더 자율적인 시스템으로 발전함에 따라 보호 체계가 어떻게 진화해야 하는지를 설명한다. 안전(Safety)은 더 이상 지능 개발이 완료된 이후 추가되는 최종 보호 계층으로 취급할 수 없다. 증가하는 지능이 통제되지 않은 물리적 행동 권한(Physical Authority)으로 이어지지 않도록 인지(Perception), 월드 모델링(World Modeling), 계획(Planning), 학습(Learning), 물리적 능력 및 자율성(Autonomy)과 함께 발전해야 한다.

출발점은 기존의 기능 안전(Functional Safety)과 로봇 안전(Robot Safety)이며, 여기에서는 명확하게 정의된 행동을 가진 결정론적 메커니즘(Deterministic Mechanism)을 통해 위험요소(Hazard)를 통제한다. 비상 정지(Emergency Stop), 안전 토크 차단(Safe Torque Off), 인터록(Interlock), 보호 구역(Protected Zone), 속도 제한, 힘 제한, 안전 등급 센싱(Safety-Rated Sensing), 고장 모니터링(Fault Monitoring)은 물리적 안전의 기반을 형성한다. 첨단 AI는 학습된 행동으로 이러한 검증된 안전 장벽을 대체하는 것이 아니라 계승해야 하므로, 이러한 메커니즘은 로드맵 전체에서 계속 중요하다.

다음 단계에서는 안전을 AI 기반 인지(AI-Enabled Perception)와 상태 추정(State Estimation)으로 확장한다. 자율 기계는 사람 탐지, 객체 분류, 주행 가능성(Traversability) 추정, 장면 이해(Scene Understanding), 멀티모달 센서 정보 융합을 위해 점점 더 신경망(Neural Network)에 의존한다. 따라서 안전 공학(Safety Engineering)은 기존의 하드웨어 진단에만 의존하지 않고 모델 신뢰도(Model Confidence), 센서 일관성, 분포 변화(Distribution Shift), 보정(Calibration), 타이밍, 위치추정 불확실성(Localization Uncertainty), 인지 성능 저하를 평가해야 한다.

자율성이 확대되면서 불확실성 인식 지능(Uncertainty-Aware Intelligence)이 핵심 요구사항이 된다. 피지컬 AI는 현재 어떤 일이 발생하고 있는지를 추정할 뿐만 아니라 현재 상황을 얼마나 확실하게 이해하고 있는지도 평가해야 한다. 우연적 불확실성(Aleatoric Uncertainty), 인식론적 불확실성(Epistemic Uncertainty), 분포 외 탐지(Out-of-Distribution Detection), 신규성 인식(Novelty Recognition), 예측 일관성(Prediction Consistency), 센서 간 일치성(Sensor Agreement)은 운용 의사결정의 입력이 된다. 낮은 신뢰도는 속도, 기동 복잡성, 운용 권한 또는 허용되는 자율 행동의 범위를 점진적으로 감소시켜야 한다.

월드 모델(World Model)은 현재의 관측에만 반응하는 것을 넘어 시간적 변화(Temporal Evolution)를 추론할 수 있는 능력을 제공한다. 로봇은 미래 상태를 예측하고, 대안적인 결과를 평가하며, 상호작용을 예상하고, 후보 행동의 결과를 추정할 수 있다. 이에 따라 안전은 즉각적인 충돌이나 제어 경계에 진입한 이후 대응하는 반응형 보호(Reactive Protection)에서 잠재적 위험이 발생하기 전에 이를 식별하는 예측적 안전(Predictive Safety)로 발전해야 하며, 불확실성도 계획 의사결정으로 전달되어야 한다.

계획(Planning)과 행동 생성(Action Generation)은 다음의 중요한 전환점을 형성한다. 학습 기반 계획기(Learned Planner), 강화학습 정책(Reinforcement-Learning Policy), 파운데이션 모델(Foundation Model), 비전-언어-행동 모델(Vision-Language-Action Model, VLA)은 사전에 완전히 명세할 수 없는 유연한 행동을 생성할 수 있다. 따라서 이러한 출력은 독립적인 행동 검증(Independent Action Validation)을 통과해야 한다. 충돌 제약조건, 안정성, 제동 거리, 인간과의 분리 거리, 힘 제한, 운용 경계 및 안전 영역(Safety Envelope)을 기준으로 지능이 제안한 행동을 실제 물리적 행동으로 허용할 것인지 결정해야 한다.

시스템이 배치 이전에 완전히 검증할 수 없는 조건에서 운용될수록 런타임 보증(Runtime Assurance)의 중요성이 증가한다. 독립적인 모니터(Independent Monitor)는 인지 상태, 위치추정 일관성, 월드 모델 예측, AI 신뢰도, 궤적 실행 가능성(Trajectory Feasibility), 계산 상태, 통신 및 액추에이터 상태를 지속적으로 평가한다. 런타임 보증은 안전을 정적인 인증 활동(Static Certification Activity)에서 현재 조건에서 어느 정도의 자율성을 안전하게 행사할 수 있는지를 지속적으로 판단하는 동적인 과정으로 변화시킨다.

로드맵은 점진적 성능 저하(Graceful Degradation)와 폴백 행동(Fallback Behavior)도 발전시켜야 한다. 신뢰할 수 있는 로봇은 센서 성능이 저하되거나, 위치추정이 불확실해지거나, 통신이 끊기거나, AI 신뢰도가 급격히 감소했을 때 완전한 자율 운용에서 통제되지 않은 실패로 즉시 전환되어서는 안 된다. 대신 속도를 점진적으로 낮추고, 안전 여유를 확대하며, 행동을 단순화하고, 운용 영역을 제한하거나, 검증된 제어(Verified Control)로 전환하고, 인간의 지원을 요청하거나, 최소 위험 상태(Minimum-Risk State)로 진입할 수 있어야 한다.

정렬(Alignment)은 피지컬 AI가 사전에 정의된 작업을 실행하는 수준에서 목표를 해석하고 자체적으로 중간 행동을 생성하는 수준으로 발전할수록 더욱 중요해진다. 시스템은 명령의 문자적인 요구를 충족하면서도 안전 요구사항, 운영 규칙, 사회적 기대 또는 사용자의 실제 의도(User Intent)를 위반할 수 있다. 따라서 물리적 정렬(Physical Alignment)은 안전 제약조건과 승인된 운용 경계가 작업 최적화(Task Optimization)보다 우선하는 계층적 구조 안에서 목표를 해석하도록 요구한다.

인간 감독(Human Oversight)은 기계의 능력이 향상된다고 해서 사라지는 것이 아니라 자율성과 함께 발전해야 한다. 초기 시스템은 빈번한 감독이 필요할 수 있지만, 고도화된 시스템은 장시간 독립적으로 동작하면서 모호하거나 새롭거나 위험도가 높은 상황만 인간에게 에스컬레이션(Escalation)할 수 있다. 의미 있는 인간 통제(Meaningful Human Control)를 위해서는 이해 가능한 시스템 상태, 명확한 로봇 의도, 적절한 권한 부여, 추적 가능한 의사결정, 효과적인 개입 메커니즘, 자율 운용과 감독 운용 사이의 명확한 전환이 필요하다.

로봇이 플릿 시스템(Fleet System), 온프레미스 인프라(On-Premise Infrastructure), 클라우드 서비스(Cloud Service), 원격 운영자(Remote Operator), 공유 모델과 연결될수록 사이버보안(Cybersecurity)은 안전과 분리할 수 없게 된다. 손상된 명령, 지도, 센서 스트림, 모델 업데이트 또는 정책은 물리적 행동에 직접 영향을 줄 수 있다. 따라서 인증(Authentication), 권한 부여(Authorization), 무결성 보호(Integrity Protection), 네트워크 분할(Network Segmentation), 보안 업데이트(Secure Update), 이상 탐지(Anomaly Detection), 보호된 안전 채널(Protected Safety Channel)은 자율 능력과 함께 발전해야 한다.

검증 및 확인(Verification and Validation) 역시 구성요소 시험에서 시스템 수준의 증거(System-Level Evidence)로 발전해야 한다. 결정론적 기능은 명시적인 요구사항을 기준으로 평가할 수 있는 경우가 많지만, 학습 시스템에는 데이터셋 분석(Dataset Analysis), 시나리오 시험(Scenario Testing), 시뮬레이션(Simulation), 강건성 평가(Robustness Evaluation), 결함 주입(Fault Injection), 분포 외 시험(Out-of-Distribution Testing), 불확실성 보정(Uncertainty Calibration), 실제 운용 증거(Operational Evidence)가 추가적으로 필요하다. 자율성이 증가할수록 AI, 제어, 하드웨어, 인간 및 환경의 상호작용이 허용 가능한 수준의 안전을 유지한다는 더욱 강력한 증거가 요구된다.

적응형 및 지속학습 시스템(Adaptive and Continually Learning System)은 배치 이후에도 안전이 변하지 않는다고 가정할 수 없기 때문에 로드맵의 한층 더 발전된 단계를 형성한다. 새로운 데이터, 모델 버전, 정책, 프롬프트(Prompt), 환경 및 학습 경험은 시스템 행동을 변화시킬 수 있다. 따라서 지속적인 진화 과정에서 추적 가능한 안전 논증(Safety Case)을 유지하기 위해 데이터 출처(Data Provenance), 구성 관리(Configuration Management), 회귀 시험(Regression Testing), 변경 영향 분석(Change Impact Analysis), 통제된 배치(Controlled Deployment), 런타임 모니터링, 사고 피드백(Incident Feedback), 롤백 기능(Rollback Capability)이 필요하다.

더 높은 수준의 자율성에서는 안전(Safety)과 정렬(Alignment)이 독립된 공학 기능이 아니라 전체 지능 아키텍처(Intelligence Architecture)의 속성이 되어야 한다. 인지, 월드 모델, 의미 추론(Semantic Reasoning), 계획, 학습, 제어, 런타임 보증, 사이버보안, 인간 거버넌스(Human Governance)는 신뢰도, 제약조건, 위험 및 행동 권한에 관한 정보를 서로 교환해야 한다. 지능 관리(Intelligence Management)는 시스템이 무엇을 할 수 있는지를 결정하는 것을 넘어 각각의 운용 조건에서 어느 정도의 자율성을 허용해야 하는지까지 결정해야 한다.

다중 로봇 및 플릿 규모 피지컬 AI(Multi-Robot and Fleet-Scale Physical AI)에서는 로드맵이 개별 안전(Individual Safety)에서 집단 안전(Collective Safety)으로 확장된다. 로봇은 지도, 관측 정보, 학습 경험, 월드 상태(World State), 협력 계획(Coordinated Plan)을 공유할 수 있다. 따라서 공유된 정보를 검증 없이 신뢰하면 하나의 로컬 오류(Local Error)가 다른 에이전트에 영향을 미칠 수 있다. 플릿 아키텍처에는 데이터 출처 추적(Provenance), 신뢰 관리(Trust Management), 일관성 검사(Consistency Checking), 협력 제약조건(Coordination Constraint), 분산 모니터링(Distributed Monitoring), 잘못된 집단 지식이 협력된 물리적 피해로 이어지는 것을 방지하는 메커니즘이 필요하다.

장기적인 목표는 증가하는 지능에 대응하여 불확실성 인식(Uncertainty Awareness), 제약조건 강제(Constraint Enforcement), 런타임 보증(Runtime Assurance), 인간 거버넌스(Human Governance), 통제된 물리적 행동 권한(Controlled Physical Authority)이 함께 발전하는 안전 정렬 피지컬 AI(Safety-Aligned Physical AI)를 구현하는 것이다. 따라서 발전 수준은 로봇이 얼마나 독립적으로 인지하고, 추론하고, 학습하고, 행동할 수 있는지만으로 평가해서는 안 된다. 자신의 한계를 인식하고, 불확실성 속에서도 안전을 유지하며, 능력이 확장되는 과정에서도 인간의 의도와 안전 요구사항에 지속적으로 정렬될 수 있는지가 핵심적인 발전 기준이 되어야 한다.
