**Volume 10. Physical AI Safety and Alignment**

# Chapter 05. Human Robot Safety Interfaces

## 05.01. Human Robot Safety Interface Principles

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

인간-로봇 안전 인터페이스(Human--Robot Safety Interfaces)는 사람이 물리 AI 시스템(Physical AI System)의 행동을 인지하고, 이해하며, 영향을 미치고, 필요할 경우 중단할 수 있도록 하는 경계를 형성한다. 기존의 사용자 인터페이스(User Interface)와 달리 이러한 인터페이스는 오해, 의사소통 지연 또는 접근하기 어려운 제어 수단이 부상이나 장비 손상으로 이어질 수 있기 때문에 물리적 위험 관리(Physical Risk Management)에 직접 참여한다. 따라서 인간 상호작용(Human Interaction), 로봇 자율성(Robot Autonomy), 독립적인 안전 메커니즘(Independent Safety Mechanisms)을 일관된 운영 관계로 연결하도록 설계되어야 한다.

기본적인 원칙은 안전 관련 정보(Safety-Relevant Information)가 로봇의 행동에 영향을 받을 수 있는 사람들에게 관찰 가능해야 한다는 것이다. 사람은 로봇이 정상적으로 동작하고 있는지, 대기하고 있는지, 양보하고 있는지, 작업을 수행하고 있는지, 제한 구역(Restricted Area)에 진입하고 있는지, 불확실성(Uncertainty)을 경험하고 있는지 또는 보호 상태(Protective State)로 전환하고 있는지를 인식할 수 있어야 한다. 표시 정보는 전문가의 해석이 필요한 내부 기술 상태만을 노출하기보다 운영상의 의미를 전달해야 한다.

인터페이스는 또한 안전한 인간-로봇 협조(Human--Robot Coordination)를 위해 로봇의 행동을 충분히 예측 가능하게 만들어야 한다. 특히 인공지능(AI)이 변화하는 환경에 맞추어 행동을 적응시키는 경우 모든 움직임이 항상 동일할 필요는 없다. 대신 로봇은 이해 가능한 움직임 규칙(Motion Conventions), 안전 영역(Safety Envelopes), 상호작용 규칙(Interaction Rules) 내에서 행동해야 한다. 갑작스러운 가속, 설명되지 않는 경로 변경, 예상하지 못한 조작 또는 일관되지 않은 양보 행동은 개별 행동이 기술적으로 가능하더라도 위험을 발생시킬 수 있다.

인간 인식(Human Awareness)과 로봇 인식(Robot Awareness)은 인터페이스를 구성하는 상호보완적인 요소로 작동해야 한다. 로봇은 사람을 탐지하고 위치와 움직임을 추정하며 적절한 분리 거리(Separation Distance)를 유지할 수 있어야 하고, 사람은 로봇의 현재 행동과 의도된 행동을 이해할 수 있는 신호를 제공받아야 한다. 이를 통해 로봇이 인간의 활동을 관찰하는 동시에 자신의 상태와 의도를 주변 사람들에게 관찰 가능하게 만드는 양방향 안전 관계(Bidirectional Safety Relationship)가 형성된다.

안전 인터페이스(Safety Interface)는 잠재적으로 중요한 물리적 행동이 시작되기 전에 로봇의 의도(Intent)를 전달해야 한다. 이동 로봇(Mobile Robot)은 이동하려는 방향을 표시할 수 있고, 매니퓰레이터(Manipulator)는 움직임이 시작될 것임을 알릴 수 있으며, 자율 시스템(Autonomous System)은 비정상적이거나 일반적이지 않은 작업을 수행하기 전에 확인을 요청할 수 있다. 이러한 사전 의사소통은 사람이 상황을 해석하고 안전하게 대응할 시간을 제공하여 인터페이스를 수동적인 상태 표시 장치에서 선제적 위험 감소(Anticipatory Risk Reduction)의 능동적 구성요소로 전환한다.

어떠한 단일 의사소통 채널도 모든 운용 조건에서 항상 신뢰할 수 있는 것은 아니므로 다중 통신 양식(Multiple Communication Modalities)이 중요하다. 시각 표시(Visual Indicators)는 방향, 조명, 가림 또는 거리 때문에 확인하기 어려울 수 있으며, 청각 경고(Auditory Warnings)는 산업 현장의 소음에 묻힐 수 있다. 햅틱 피드백(Haptic Feedback), 디스플레이(Display), 투영 정보(Projected Information), 물리적 표시 장치(Physical Indicators), 자연어 메시지(Natural-Language Messages)는 상호보완적인 채널을 제공할 수 있다. 이러한 중복성(Redundancy)은 과도한 경보나 상충되는 신호를 발생시키지 않으면서 이해도를 향상시켜야 한다.

안전 신호(Safety Signals)의 의미는 가능한 한 다양한 운용 모드(Operating Modes)에서 일관성을 유지해야 한다. 색상, 소리, 아이콘, 움직임 패턴 또는 인터페이스 메시지가 자율 운전(Autonomous Operation), 원격조작(Teleoperation), 유지보수(Maintenance), 성능 저하 모드(Degraded Mode)에서 예측할 수 없게 다른 의미를 갖는다면 사용자는 잘못된 기대를 형성할 수 있다. 일관된 의미 체계(Consistent Semantics)는 인지 부하(Cognitive Load)를 감소시키고 로봇이 위험, 요청, 상태 전환 및 개입 기회(Intervention Opportunities)를 전달하는 방식에 대해 신뢰할 수 있는 정신 모델(Mental Model)을 형성하도록 한다.

자율 행동(Autonomous Behavior)이 안전하지 않거나 혼란스럽거나 상황에 적합하지 않을 경우 인간 개입(Human Intervention)이 가능해야 한다. 시스템에 따라 개입에는 움직임 정지, 행동 거부, 명령 수정, 감독 제어(Supervisory Control) 전환, 원격조작(Teleoperation) 시작 또는 비상 기능(Emergency Function) 활성화가 포함될 수 있다. 일상적인 명령 취소(Command Cancellation), 보호 정지(Protective Stop), 비상 정지(Emergency Stop)는 서로 다른 운용 및 안전 기능을 의미하므로 이러한 메커니즘은 목적에 따라 명확하게 구별되어야 한다.

안전 필수 개입 경로(Safety-Critical Intervention Path)는 개입 대상이 되는 행동을 발생시킨 동일한 인공지능 구성요소에 전적으로 의존해서는 안 된다. 학습 기반 인식 모델(Learned Perception Model), 추론 모델(Reasoning Model), 비전-언어-행동 정책(Vision-Language-Action Policy, VLA Policy), 자율 플래너(Autonomous Planner)가 실패하더라도 인간은 시스템을 안전한 상태(Safe Condition)로 전환할 수 있는 신뢰할 수 있는 수단을 확보해야 한다. 이는 지능형 상호작용 기능(Intelligent Interaction Functions)과 독립적으로 보증된 안전 메커니즘(Independently Assured Safety Mechanisms)을 구조적으로 분리하는 심층 방어(Defense-in-Depth) 원칙의 필요성을 보여준다.

불확실성(Uncertainty)이 인간의 의사결정에 영향을 미칠 수 있는 경우 인터페이스는 이를 명시적으로 표현해야 한다. 인공지능 시스템은 객체를 신뢰성 있게 식별하거나, 명령을 정확하게 해석하거나, 인간의 의도를 추정하거나, 계획된 경로의 안전성을 판단하지 못할 수 있다. 이러한 불확실성을 숨기면 잘못된 확신(False Confidence)이 형성될 수 있다. 대신 인터페이스는 낮아진 신뢰도(Confidence)를 전달하고, 명확화를 요청하며, 실행 속도를 낮추거나 중단하고, 물리적 결과가 발생하기 전에 인간 감독자(Human Supervisor)에게 상황을 에스컬레이션(Escalation)할 수 있다.

안전 상호작용(Safety Interaction)은 서로 다른 인간의 역할과 전문성 수준을 고려해야 한다. 훈련된 운영자(Trained Operator)는 상세한 진단 정보를 이해할 수 있지만, 창고 작업자, 승객, 환자, 방문자 또는 보행자는 전문적인 지식 없이 로봇을 접할 수 있다. 따라서 시스템의 외부 안전 행동(External Safety Behavior)은 광범위한 교육을 전제로 하지 않고도 이해할 수 있어야 하며, 전문 인터페이스는 권한을 가진 운영자, 기술자 및 안전 담당자에게 더욱 상세한 정보와 제어 기능을 제공할 수 있어야 한다.

인터페이스는 모드 혼동(Mode Confusion)이 발생할 가능성을 최소화해야 한다. 물리 AI 시스템은 자율 운전(Autonomous Operation), 감독 자율성(Supervised Autonomy), 공유 제어(Shared Control), 원격조작(Teleoperation), 성능 저하 운전(Degraded Operation), 유지보수(Maintenance), 복구(Recovery), 비상 상태(Emergency State) 사이를 전환할 수 있다. 사람이 자율 기능이 활성화되어 있는데도 로봇이 정지되어 있다고 잘못 판단하거나, 수동 제어로 전환되었는데도 로봇이 스스로 제어되고 있다고 생각한다면 위험한 행동이 발생할 수 있다. 따라서 운용 모드(Mode), 권한(Authority), 제어권(Control Ownership)은 명확하게 표시되어야 한다.

명령 인터페이스(Command Interface)는 명령을 수신하는 것과 해당 명령을 안전하게 실행할 수 있는지를 판단하는 것을 구별해야 한다. 자연어 명령(Natural-Language Commands), 제스처(Gestures), 그래픽 제어(Graphical Controls), 원격 명령(Remote Commands)은 인간의 의도(Human Intent)를 표현할 수 있지만 물리적 제약(Physical Constraints)이나 안전 정책(Safety Policies)을 자동으로 우회해서는 안 된다. 견고한 인터페이스는 확인(Confirmation), 명확화(Clarification), 제약 조건 검사(Constraint Checking), 필요한 경우 명령 거부(Rejection)를 지원함으로써 인간의 권한을 존중하면서도 모든 명령을 즉시 실행 가능한 것으로 취급하지 않도록 해야 한다.

인간-로봇 안전 인터페이스는 정상 운전과 비상 정지에만 의존하지 않고 단계적인 에스컬레이션(Graceful Escalation)을 지원해야 한다. 위험이 증가하면 시스템은 먼저 불확실성을 전달하고, 속도를 낮추고, 분리 거리를 증가시키며, 인간의 주의를 요청하고, 행동을 일시 중지하거나, 감독 운전(Supervised Operation)으로 전환하거나, 최소 위험 상태(Minimum-Risk Condition)에 진입할 수 있다. 이러한 단계적 대응(Graduated Response)은 불확실한 상황이 심각한 위험이나 불필요한 비상 상황으로 직접 발전하는 것을 방지하면서 가능한 범위에서 유용한 운전을 유지하도록 한다.

신뢰(Trust)는 로봇을 항상 신뢰할 수 있는 것처럼 보이게 만드는 목표가 아니라 조정된 운영 속성(Calibrated Operational Property)으로 다루어야 한다. 불확실성을 숨기거나 시스템의 능력을 과장하는 인터페이스는 자동화에 대한 과도한 의존(Overreliance)을 유발할 수 있으며, 지나치게 많은 경고는 불신과 경보 피로(Alarm Fatigue)를 발생시킬 수 있다. 안전 중심 투명성(Safety-Oriented Transparency)은 사용자가 로봇이 무엇을 하고 있는지, 무엇을 하려고 하는지, 현재 어떤 제한이 적용되는지, 언제 인간의 개입이 필요한지를 이해하도록 하여 자동화에 대한 적절하게 조정된 신뢰를 형성해야 한다.

인터페이스 지연시간(Interface Latency) 자체도 중요한 안전 요소이다. 인간 탐지(Human Detection), 경고 생성(Warning Generation), 시각화(Visualization), 명령 전송(Command Transmission), 확인(Acknowledgment), 오버라이드 처리(Override Processing), 물리적 대응(Physical Response)에는 모두 시간이 필요하다. 이론적으로 정확한 경고라도 사람이 이미 위험 구역(Hazardous Region)에 진입한 이후 전달된다면 보호 효과가 거의 없다. 따라서 안전 인터페이스 설계는 로봇 속도, 정지 거리(Stopping Distance), 통신 지연(Communication Delay), 인간 반응 시간(Human Reaction Time), 주변 환경의 동역학(Dynamics)을 종단 간 응답 시간(End-to-End Response Time)과 함께 고려해야 한다.

원격 및 플릿 운용(Remote and Fleet Operations)은 안전 인터페이스를 직접적인 물리적 근접 범위 이상으로 확장한다. 감독자는 로봇이 현장에서 계속 동작하는 동안 대시보드(Dashboard), 경고(Alert), 지도(Map), 영상 피드(Video Feed), 미션 제어 시스템(Mission-Control System)을 통해 여러 로봇을 관찰할 수 있다. 원격 인터페이스(Remote Interface)는 어떤 로봇에 주의가 필요한지, 왜 개입해야 하는지, 어떤 정보가 지연되거나 불완전할 수 있는지, 원격 운영자가 현재 어떤 권한을 가지고 있는지를 전달해야 한다. 통신이 손실될 경우 원격 감독에 통제되지 않은 방식으로 의존하기보다 사전에 정의된 로컬 안전 행동(Local Safety Behavior)이 실행되어야 한다.

안전 인터페이스는 정보 과부하(Information Overload)에도 대응해야 한다. 물리 AI 시스템은 방대한 센서 데이터(Sensor Data), 신뢰도 점수(Confidence Scores), 궤적(Trajectories), 진단 정보(Diagnostics), 예측(Predictions), 이벤트 로그(Event Logs)를 제공할 수 있지만 모든 정보를 표시한다고 해서 반드시 안전성이 향상되는 것은 아니다. 인터페이스는 긴급성(Urgency), 결과의 심각성(Consequence), 필요한 인간 행동(Required Human Action)에 따라 정보를 우선순위화해야 한다. 중요한 위험은 명확하게 부각되어야 하며, 우선순위가 낮은 진단 정보는 즉각적인 주의를 방해하지 않도록 더 깊은 인터페이스 계층에서 제공할 수 있다.

인터페이스 요소의 물리적 배치(Physical Placement)와 접근성(Accessibility)은 논리적 설계만큼 중요하다. 비상 제어(Emergency Controls), 상태 표시기(Status Indicators), 확인 장치(Acknowledgment Devices), 수동 개입 메커니즘(Manual Intervention Mechanisms)은 실제 운용 조건에서도 접근 가능하고 식별 가능해야 한다. 설계자는 관찰 방향, 보호 장비(Protective Equipment), 환경 소음, 조명, 이동성 제한(Mobility Limitations), 장갑 착용, 스트레스 상황뿐 아니라 개입이 필요한 사람이 주 운영자 위치(Primary Operator Station)에 있지 않을 가능성까지 고려해야 한다.

인간-로봇 안전 인터페이스는 독립적인 사용성 기능(Isolated Usability Features)이 아니라 전체 안전 아키텍처(Safety Architecture)의 일부로 평가되어야 한다. 시험에서는 사람이 로봇의 상태를 올바르게 인식하고, 경고를 이해하며, 움직임을 예측하고, 불확실성을 인식하고, 제어 권한(Control Authority)을 식별하며, 실제 상황에서 효과적으로 개입할 수 있는지를 확인해야 한다. 평가는 정상 운전뿐 아니라 비정상 조건(Abnormal Conditions), 통신 장애(Communication Failures), 모호한 상호작용(Ambiguous Interactions), 예상하지 못한 인간 행동, 성능이 저하된 자율성(Degraded Autonomy), 시간 임계 상황(Time-Critical Events)을 포함해야 한다.

물리 AI(Physical AI)에서 가장 강력한 안전 인터페이스는 인간의 의도(Human Intent), 로봇 인식(Robot Perception), 자율 의사결정(Autonomous Decision Making), 물리적 행동(Physical Action), 독립적 보호(Independent Protection) 사이에 지속적이고 이해 가능한 관계를 구축한다. 따라서 인간 탐지(Human Detection), 근접 관리(Proximity Management), 의도 인식(Intent Recognition), 로봇 의도 전달(Robot Intent Communication), 경고(Warnings), 명령 확인(Command Confirmation), 공유 제어(Shared Control), 원격조작(Teleoperation), 비상 개입(Emergency Intervention), 신뢰(Trust), 예측 가능성(Predictability)은 개별적인 인터페이스 기능이 아니라 서로 연결된 역량으로 이해해야 한다. 이러한 관계는 이후 장에서 다루는 보다 전문화된 인간-로봇 안전 메커니즘(Human--Robot Safety Mechanisms)의 기반을 제공한다.

## 05.02. Human Detection and Tracking

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

인간 탐지 및 추적(Human Detection and Tracking)은 물리 AI 시스템(Physical AI System)과 사람 사이의 안전한 상호작용을 위한 지각적 기반(Perceptual Foundation)을 제공한다. 로봇이 사람이 어디에 있으며 어떻게 움직이는지를 판단하지 못한다면 분리 거리(Separation)를 안정적으로 관리하거나, 이동 우선권을 양보하거나, 의도를 전달하거나, 보호 행동(Protective Behavior)을 시작하기 어렵다. 탐지(Detection)는 관찰 가능한 환경에서 사람을 식별하고, 추적(Tracking)은 시간에 따라 사람의 식별 정보, 위치, 운동 상태 및 궤적을 지속적으로 유지한다.

일반적인 객체 탐지(Object Detection)와 달리 안전 중심 인간 탐지(Safety-Oriented Human Detection)는 동적이고 불완전한 물리적 조건에서도 동작해야 한다. 사람은 서로 다른 거리, 방향, 자세 및 속도로 나타날 수 있으며 기계, 선반, 차량, 가구 또는 다른 사람에 의해 부분적으로 가려질 수도 있다. 의복, 조명, 날씨, 반사, 복잡한 배경 및 센서 잡음(Sensor Noise) 역시 사람의 외관을 변화시키므로 탐지 시스템은 통제된 환경을 넘어서는 조건에서도 유용한 성능을 유지해야 한다.

물리 AI 시스템은 각 센서가 사람의 존재에 대해 서로 다른 정보를 제공하기 때문에 일반적으로 여러 센싱 양식(Sensing Modalities)을 결합한다. 카메라(Camera)는 사람을 인식하고 자세를 추정하기 위한 풍부한 시각적 특징을 제공하며, 라이다(LiDAR)는 시각적 외관이 변화하는 상황에서도 유용한 기하학적 위치 및 거리 정보를 제공한다. 레이더(Radar), 깊이 카메라(Depth Camera), 열 센서(Thermal Sensor), 초음파 장치(Ultrasonic Device), 전용 안전 센서(Safety Sensor)도 운용 환경과 요구되는 안전 무결성(Safety Integrity)에 따라 추가적인 정보를 제공할 수 있다.

센서 배치(Sensor Placement)는 인간 탐지 설계에서 매우 중요한 요소이다. 아무리 뛰어난 지각 모델(Perception Model)이라도 사람이 관찰 가능한 시야(Field of View) 밖에 있거나 로봇 구조에 의해 지속적으로 가려져 있다면 탐지할 수 없다. 따라서 이동 로봇(Mobile Robot), 매니퓰레이터(Manipulator), 자율주행차(Autonomous Vehicle), 휴머노이드(Humanoid)는 가능한 움직임에 적합한 센싱 범위(Sensing Coverage)를 확보해야 한다. 차체 주변, 적재물 뒤, 매니퓰레이터 주변 또는 도킹 구조물 옆의 사각 영역(Blind Region)은 안전 분석 과정에서 식별되어야 한다.

탐지(Detection)는 현재 사람이 관찰되는지를 판단하지만 안전한 상호작용을 위해서는 일반적으로 시간적 이해(Temporal Understanding)가 필요하다. 추적(Tracking)은 연속적인 관측에서 탐지 결과를 연결하여 사람이 정지해 있는지, 접근하는지, 멀어지는지, 로봇의 경로를 가로지르는지 또는 로봇과 함께 이동하는지를 추정한다. 시간적 연속성(Temporal Continuity)은 개별적인 탐지 누락으로 발생하는 불안정한 행동을 감소시키고 안전 시스템이 독립된 센서 프레임이 아니라 변화하는 상호작용 과정을 판단하도록 한다.

추적 시스템(Tracking System)은 일반적으로 위치(Position), 속도(Velocity), 방향(Direction), 불확실성(Uncertainty)을 포함하는 인간 상태(Human State)를 유지한다. 응용 분야에 따라 가속도(Acceleration), 신체 방향(Body Orientation), 자세(Pose), 예측 궤적(Predicted Trajectory)을 추가로 추정할 수 있다. 이러한 상태는 새로운 센서 관측이 들어올 때마다 지속적으로 갱신된다. 결과적으로 하위 안전 기능은 서로 단절된 탐지 경계 상자(Bounding Box)나 위치 측정값보다 인간의 움직임을 더욱 유용하게 표현하는 정보를 활용할 수 있다.

데이터 연관(Data Association)은 다중 인간 추적(Multi-Human Tracking)의 핵심적인 문제 중 하나이다. 여러 사람이 서로 가까이 이동하거나, 경로가 교차하거나, 장애물 뒤에서 일시적으로 사라지거나, 센서 범위에 진입하고 이탈하는 경우 시스템은 새로운 관측이 기존에 추적하던 어느 사람과 대응되는지를 판단해야 한다. 잘못된 연관은 식별자 전환(Identity Switch), 불연속적인 궤적 또는 부정확한 운동 추정을 발생시켜 근접 관리(Proximity Management)와 단기 예측(Short-Term Prediction)의 성능을 저하시킬 수 있다.

가림(Occlusion)은 안전 응용에서 특히 보수적으로 처리해야 한다. 사람이 선반, 차량, 기계 또는 다른 사람 뒤로 사라졌다고 해서 반드시 환경에서 벗어났다고 판단해서는 안 된다. 추적 시스템은 일정 시간 동안 잠재 추적 상태(Latent Track)를 유지하고 불확실성을 증가시키면서 예상 상태를 전파할 수 있다. 이후 충분한 증거가 확보되어 해당 추적 정보를 제거할 수 있을 때까지 안전 로직(Safety Logic)은 사람이 여전히 주변에 존재할 가능성을 고려할 수 있다.

인간 추적(Human Tracking)은 결정론적인 좌표(Deterministic Coordinates)만 생성하기보다 불확실성(Uncertainty)을 함께 표현해야 한다. 센서 잡음, 부분적인 관측, 모호한 연관 관계, 낮은 가시성 및 예측 오류는 위치와 운동 추정 모두에 불확실성을 발생시킨다. 불확실성이 증가할수록 사람이 존재할 가능성이 있는 영역도 확대된다. 안전 메커니즘(Safety Mechanism)은 이러한 정보를 활용하여 보호 여유(Protective Margin)를 확대하고, 로봇 속도를 낮추며, 추가 관측을 요청하거나, 더욱 보수적인 궤적을 선택할 수 있다.

탐지 신뢰도(Detection Confidence) 역시 신중하게 해석해야 한다. 높은 신경망 신뢰도 점수(Neural-Network Confidence Score)가 반드시 안전 필수 추정(Safety-Critical Estimate)의 신뢰성을 의미하지는 않으며, 특히 분포 변화(Distribution Shift)나 익숙하지 않은 환경 조건에서는 더욱 그렇다. 물리 AI 시스템은 센서 상태(Sensor Health), 환경 조건, 센서 간 일관성(Cross-Sensor Consistency), 추적 이력(Tracking History), 현재 상황이 개발 및 검증 조건과 얼마나 유사한지를 함께 고려하여 모델 신뢰도(Model Confidence)와 전체적인 운용 확실성(Operational Certainty)을 구분해야 한다.

다중 센서 융합(Multi-Sensor Fusion)은 상호보완적인 관측을 결합하여 인간의 존재와 움직임에 대한 공통 표현(Common Representation)을 생성함으로써 견고성(Robustness)을 향상시킬 수 있다. 카메라 탐지 결과는 라이다 클러스터(LiDAR Cluster), 깊이 측정(Depth Measurement), 레이더 반사 신호(Radar Return) 또는 다른 센서 정보와 연결될 수 있다. 융합은 원시 데이터(Raw Data), 특징(Feature), 탐지(Detection), 추적(Track) 수준에서 수행할 수 있으며 적절한 구조는 계산 자원, 동기화 요구사항, 센서 기하 구조, 지연시간 및 안전 아키텍처에서 요구되는 독립성에 따라 결정된다.

여러 센서 또는 움직이는 플랫폼에서 관측 정보가 생성되는 경우 정확한 좌표 변환(Coordinate Transformation)이 필수적이다. 인간에 대한 측정값은 개별 센서 좌표계(Sensor Coordinate Frame)에서 로봇, 차량, 지도 또는 월드 좌표계(World Coordinate Frame)로 변환되어야 하는 경우가 많다. 캘리브레이션 오류(Calibration Error), 시간 오프셋(Timing Offset), 위치추정 오류(Localization Error), 센서 사이의 기계적 움직임은 추정 위치를 왜곡할 수 있다. 따라서 추적 정확도는 탐지 알고리즘뿐만 아니라 캘리브레이션, 동기화, 위치추정 및 시스템 통합에도 의존한다.

지연시간(Latency)은 인간 추적의 안전 가치를 직접적으로 좌우한다. 센싱(Sensing), 전처리(Preprocessing), 추론(Inference), 연관(Association), 필터링(Filtering), 통신(Communication), 계획(Planning), 구동(Actuation)을 포함한 모든 단계는 시스템이 물리적 세계를 인식하는 시간을 지연시킨다. 상대 속도가 높을수록 작은 지연도 추정된 인간 위치와 실제 위치 사이에 상당한 차이를 만들 수 있다. 따라서 안전 설계에서는 종단 간 지각 지연시간(End-to-End Perception Latency)을 로봇 속도, 정지 성능(Stopping Capability), 필요한 분리 거리와 함께 평가해야 한다.

추적 주기(Tracking Frequency)와 시간적 안정성(Temporal Stability)은 적절하게 균형을 이루어야 한다. 높은 갱신 속도(Update Rate)는 인간의 움직임 변화에 빠르게 대응하도록 하지만 잡음이 많은 추정값은 속도나 궤적 계산을 불안정하게 만들 수 있다. 필터링(Filtering)과 시간 모델(Temporal Model)은 안정성을 향상시킬 수 있지만 지나친 평활화(Smoothing)는 추가적인 지연을 발생시킨다. 따라서 추적 아키텍처는 불필요한 제동, 반복적인 경고 또는 로봇 행동의 진동을 유발하는 급격한 변동을 방지하면서 충분히 빠른 추정 결과를 제공해야 한다.

인간 자세(Human Pose)와 신체 구성(Body Configuration)은 사람의 중심 위치만으로는 얻을 수 없는 추가적인 안전 정보를 제공할 수 있다. 팔, 손, 다리, 머리 방향 및 신체 자세는 사람의 전체 위치가 허용 가능한 것으로 보이더라도 신체 일부가 위험 영역(Hazardous Region)에 진입하고 있음을 나타낼 수 있다. 자세 추정(Pose Estimation)은 의도 인식(Intent Recognition)과 협업 상호작용(Collaborative Interaction)에도 활용할 수 있지만, 안전 필수 의사결정에 사용하기 전에는 불확실성과 실패 모드(Failure Modes)를 함께 고려해야 한다.

단기 궤적 예측(Short-Horizon Trajectory Prediction)은 현재 움직임의 추정에서 미래에 사람이 점유할 가능성이 있는 영역을 예상하는 단계로 추적 기능을 확장한다. 통로 교차점으로 접근하는 사람, 이동 로봇 방향으로 걸어오는 사람 또는 매니퓰레이터 작업 공간으로 손을 뻗는 사람은 즉각적인 보호 영역에 진입하기 전에도 예측 가능한 충돌 가능성을 발생시킬 수 있다. 예측을 통해 조기에 속도를 낮추거나 재계획(Replanning)을 수행할 수 있지만 인간의 움직임은 본질적으로 불확실하므로 예측 궤적은 확정된 미래 경로가 아니라 가능한 경로로 표현되어야 한다.

인간 탐지(Human Detection)는 근접 관리(Proximity Management) 및 안전 영역 로직(Safety-Zone Logic)과 긴밀하게 연결되어야 한다. 추적된 위치와 예측 움직임을 이용하여 사람이 상호작용 영역 밖에 있는지, 주의 영역(Caution Zone)에 접근하는지, 감속 영역(Reduced-Speed Region)에 진입하는지 또는 보호 경계(Protective Boundary)를 통과하는지를 판단할 수 있다. 이러한 상태 전환은 점진적으로 강화되는 대응을 활성화하여 지각 기능을 인간-로봇 안전 인터페이스(Human--Robot Safety Interface)의 단계적 안전 행동(Graduated Safety Behavior)과 직접 연결한다.

요구되는 위험 감소 수준이 더 강력한 보증을 필요로 하는 경우 학습 기반 지각(Learned Perception)이 독립적으로 보증된 보호 센싱(Independently Assured Protective Sensing)을 자동으로 대체해서는 안 된다. AI 기반 인간 탐지는 의미적 이해(Semantic Understanding), 예측 및 유연한 환경 인식을 제공할 수 있으며, 인증되거나 독립적으로 설계된 안전 센서(Safety Sensor)는 핵심적인 보호 기능을 수행할 수 있다. 이러한 역할 분리는 모든 안전 기능이 복잡한 학습 모델의 정확성에 의존하지 않으면서 고급 지능을 활용하여 상호작용을 향상시킬 수 있도록 한다.

런타임 모니터링(Runtime Monitoring)은 인간 탐지 및 추적 하위 시스템이 현재 운용에 충분한 신뢰성을 유지하고 있는지를 지속적으로 평가해야 한다. 유용한 지표에는 센서 가용성(Sensor Availability), 프레임 속도(Frame Rate), 추론 지연시간(Inference Latency), 탐지 일관성(Detection Consistency), 추적 연속성(Track Continuity), 캘리브레이션 상태(Calibration Status), 예상하지 못한 관측 패턴 및 센싱 양식 간 불일치가 포함된다. 지각 품질이 허용 가능한 임계값 이하로 떨어지면 로봇은 속도를 낮추고 안전 여유를 확대하거나 성능 저하 운전(Degraded Operation) 또는 안전 상태(Safe State)로 전환할 수 있다.

평가(Evaluation)는 평균적인 탐지 정확도만 측정하는 것이 아니라 어려운 시나리오를 포함해야 한다. 부분 및 전체 가림, 혼잡한 환경, 비정상적인 자세, 빠른 움직임, 저조도 환경, 반사 표면, 필요한 경우 악천후, 센서 오염, 통신 지연 및 이전에 가려져 있던 영역에서 갑자기 사람이 나타나는 상황을 시험해야 한다. 특히 거짓 음성(False Negative)은 탐지되지 않은 사람으로 인해 하위 안전 메커니즘이 보호 행동의 필요성을 인식하지 못할 수 있으므로 매우 중요하다.

시스템 수준 평가(System-Level Evaluation)는 지각 오류가 실제 로봇 행동에 어떠한 영향을 미치는지도 측정해야 한다. 탐지 정밀도(Precision)와 재현율(Recall), 추적 연속성, 위치 오차(Localization Error), 식별자 전환(Identity Switch), 지연시간, 궤적 오차(Trajectory Error)는 유용한 기술적 지표이지만 궁극적인 안전성은 전체 시스템이 적절한 분리 거리를 유지하고 올바르게 대응하는지에 달려 있다. 따라서 시나리오 기반 시험(Scenario-Based Testing)은 지각 성능을 경고, 감속, 재계획, 보호 정지(Protective Stop), 비상 개입(Emergency Intervention)과 연결하여 평가해야 한다.

인간 탐지 및 추적(Human Detection and Tracking)은 궁극적으로 독립적인 컴퓨터 비전 기능(Computer-Vision Function)이 아니라 주변 사람에 대한 지속적으로 갱신되는 안전 표현(Safety Representation)으로 이해해야 한다. 탐지(Detection)는 인간의 존재를 확인하고, 추적(Tracking)은 시간적 연속성을 유지하며, 센서 융합(Sensor Fusion)은 견고성을 향상시키고, 불확실성(Uncertainty)은 불완전한 지식을 표현하며, 예측(Prediction)은 잠재적인 충돌을 사전에 파악한다. 이러한 기능은 함께 근접 관리, 속도 및 분리 모니터링(Speed and Separation Monitoring), 의도 인식 및 이후의 인간-로봇 안전 인터페이스를 위한 인간 인식 계층(Human-Awareness Layer)을 제공한다.

## 05.03. Safety Zones and Proximity Management

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

안전 영역(Safety Zones)과 근접 관리(Proximity Management)는 인간의 위치 정보를 물리 AI 시스템(Physical AI System)이 사람 주변에서 어떻게 움직일 수 있는지를 규정하는 공간적 규칙(Spatial Rules)으로 변환한다. 안전을 자유로운 움직임과 비상 정지(Emergency Stop)라는 단순한 두 상태로 구분하는 대신, 환경을 단계적으로 다른 로봇 행동이 적용되는 여러 영역으로 나눌 수 있다. 이러한 영역은 인간 탐지(Human Detection), 거리 추정(Distance Estimation), 운동 제어(Motion Control), 경고(Warning), 보호 기능(Protective Functions), 개입(Intervention)을 구조적으로 연결한다.

안전 영역(Safety Zone)은 특정한 조건, 제약 또는 대응이 적용되는 공간적 영역을 의미한다. 응용 분야에 따라 안전 영역은 로봇 전체, 개별 매니퓰레이터(Manipulator), 움직이는 도구, 적재물(Payload), 도킹 메커니즘(Docking Mechanism) 또는 위험 작업 공간(Hazardous Workspace)을 둘러싸도록 설정할 수 있다. 영역의 크기는 임의의 고정 거리로 결정하기보다 로봇 형상, 가능한 움직임, 속도, 정지 성능, 센싱 성능, 환경 조건 및 잠재적 접촉의 심각성을 반영해야 한다.

유용한 안전 아키텍처(Safety Architecture)는 하나의 보호 경계(Protective Boundary)보다 여러 단계의 영역으로 구성되는 경우가 많다. 모니터링 영역(Monitoring Region)은 주변 사람에 대한 인식을 시작하고, 주의 영역(Caution Region)은 경고 또는 강화된 관찰을 활성화하며, 감속 영역(Reduced-Speed Region)은 속도를 제한할 수 있다. 보호 영역(Protective Region)은 정지 또는 다른 안전 대응을 실행한다. 이러한 단계적 구조는 위험 변화에 비례하여 대응하면서 충분한 분리 거리가 확보된 경우 생산적인 운전을 유지하도록 한다.

근접 관리(Proximity Management)는 사람이 경계를 통과할 때까지 기다리는 대신 인간과 로봇 사이의 공간적 관계를 지속적으로 평가한다. 주요 변수에는 현재 분리 거리(Separation Distance), 상대 속도(Relative Velocity), 접근 방향(Direction of Approach), 로봇 궤적(Robot Trajectory), 인간 궤적(Human Trajectory), 정지 거리(Stopping Distance), 불확실성(Uncertainty)이 포함된다. 따라서 동일한 거리에 있는 두 사람도 한 사람이 정지하거나 멀어지고 다른 사람이 로봇의 계획 경로로 빠르게 접근한다면 서로 다른 위험 수준을 나타낼 수 있다.

안전 영역(Safety Zones)은 반드시 원형이거나 기하학적으로 균일할 필요가 없다. 전진하는 이동 로봇(Mobile Robot)은 후방보다 진행 방향에 더 큰 보호 영역이 필요할 수 있으며, 매니퓰레이터는 링크(Link)와 엔드 이펙터(End Effector)의 스윕 볼륨(Swept Volume)을 따라 형성된 영역이 필요할 수 있다. 방향 의존 영역(Direction-Dependent Region)과 구성 의존 영역(Configuration-Dependent Region)은 고정된 대칭 경계보다 물리적 위험을 정확하게 표현할 수 있으며, 그 동작은 이해 가능하고 충분히 검증되어야 한다.

동적 안전 영역(Dynamic Safety Zones)은 운용 조건에 따라 영역의 크기를 변경함으로써 이러한 개념을 확장한다. 로봇 속도가 증가하면 정지 거리와 필요한 반응 시간이 증가하여 전방 안전 여유(Safety Margin)가 확대될 수 있다. 속도가 감소하면 적절한 조건에서 더 가까운 상호작용을 허용할 수 있다. 적재물 질량(Payload Mass), 매니퓰레이터 구성, 바닥 상태, 위치추정 품질(Localization Quality), 센서 성능, 가시성(Visibility), 불확실성도 동적으로 관리되는 안전 영역의 크기에 영향을 줄 수 있다.

분리 거리(Separation)는 상대적인 속성이므로 인간의 움직임(Human Motion)을 고려해야 한다. 사람이 로봇을 향해 걸어오면 로봇 자체가 천천히 움직이더라도 사용 가능한 반응 시간이 감소할 수 있다. 따라서 추적 정보(Tracking Information)를 이용하여 상대 운동(Relative Motion)과 잠재적 상호작용까지의 시간을 추정할 수 있다. 단기 예측(Short-Horizon Prediction)을 추가하면 인간과 로봇의 궤적이 수렴하는지를 파악하여 사람이 직접적인 보호 경계에 도달하기 전에 선제적으로 감속하거나 재계획(Replanning)할 수 있다.

정지 성능(Stopping Capability)은 근접 관리에서 중요한 물리적 제약을 형성한다. 로봇은 허용할 수 없는 상호작용 조건에 도달하기 전에 정지할 수 없는 속도로 안전하게 운전할 수 없다. 전체 정지 과정에는 센싱 지연(Sensing Delay), 지각 처리(Perception Processing), 안전 판단 시간, 통신 지연(Communication Latency), 제어기 응답, 액추에이터 동역학(Actuator Dynamics), 제동 성능(Braking Performance), 기계적 정지 거리가 포함된다. 따라서 안전 여유는 단순한 제동 거리뿐 아니라 전체 응답 체인(Response Chain)을 고려해야 한다.

불확실성(Uncertainty)은 안전 여유를 조용히 약화시키는 것이 아니라 오히려 확대시키는 방향으로 반영되어야 한다. 인간 위치 추정에는 센서 오류, 추적 불확실성, 캘리브레이션 오류(Calibration Error), 일시적인 가림(Occlusion)이 포함될 수 있으며 로봇의 위치추정 및 운동 추정 역시 불완전할 수 있다. 인간과 로봇의 상대적 구성에 대한 확신이 낮아지면 근접 관리 로직(Proximity Management Logic)은 보호 영역을 보수적으로 확대하고 허용 속도를 낮추거나 신뢰할 수 있는 관측이 복구될 때까지 더 제한적인 운용 모드로 전환할 수 있다.

가림(Occlusion)은 공간적 안전 관리에서 특히 중요한 문제를 발생시킨다. 사람이 선반, 기계, 차량, 적재물 또는 구조물 뒤로 사라졌더라도 로봇의 미래 경로 근처에 계속 존재할 수 있다. 따라서 시스템은 이전에 사람이 점유했던 공간을 즉시 비어 있는 것으로 판단해서는 안 된다. 지속 추적(Persistent Tracking), 점유 메모리(Occupancy Memory), 보수적인 은폐 공간 가정(Conservative Hidden-Space Assumptions) 또는 추가 센싱을 활용하여 가려진 사람이 즉각적인 위험을 더 이상 발생시키지 않는다는 충분한 증거가 확보될 때까지 보호 상태를 유지할 수 있다.

안전 영역 전환(Safety-Zone Transition)은 불안정한 스위칭(Unstable Switching)을 방지하도록 설계해야 한다. 사람이 경계 주변에서 반복적으로 움직이는 경우 작은 측정값 변동만으로 정상 운전, 감속 및 정지가 빠르게 반복될 수 있다. 히스테리시스(Hysteresis), 시간 필터링(Temporal Filtering), 최소 유지 시간(Minimum Dwell Time), 적절하게 분리된 임계값(Thresholds)은 이러한 행동을 안정화할 수 있다. 다만 안정성을 향상시키는 메커니즘이 실제 위험 증가에 대한 대응을 과도하게 지연시키지 않도록 설계해야 한다.

각 영역에 연결되는 대응(Response)은 안전 판단이 가능할 정도로 명확하고 결정론적(Deterministic)이어야 한다. 외곽 영역에 진입하면 모니터링을 강화하거나 시각적 표시를 활성화할 수 있으며, 중간 영역에 진입하면 속도를 낮추고 계획된 궤적을 수정할 수 있다. 더 가까운 보호 영역에서는 보호 정지(Protective Stop)를 실행할 수 있으며, 즉각적인 위험 상태에서는 더 강력한 개입이 필요할 수 있다. 구체적인 대응 관계는 로봇, 환경, 작업 및 적용되는 안전 아키텍처에 따라 달라진다.

안전 영역 관리(Safety-Zone Management)는 현재의 물리적 형상뿐 아니라 로봇의 의도(Robot Intent)와 미래 스윕 볼륨(Future Swept Volume)도 고려해야 한다. 정지해 있는 매니퓰레이터가 회전을 준비하거나 이동 로봇이 방향 전환을 준비한다면 현재는 비어 있는 공간을 곧 점유할 수 있다. 계획 시스템(Planning System)은 의도된 움직임을 환경에 투영하고 미래의 로봇 점유 영역과 추적 또는 예측된 인간 점유 영역을 비교함으로써 실제 움직임이 즉각적인 충돌을 만들기 전에 위험한 계획을 제한할 수 있다.

이동 로봇(Mobile Robot)의 경우 안전 영역은 일반적으로 플랫폼과 함께 이동하며 속도와 조향 방향에 따라 변화한다. 모서리, 후진 동작, 제자리 회전(Rotation in Place), 좁은 통로, 교차로 및 도킹 작업은 서로 다른 공간적 위험을 발생시킬 수 있다. 따라서 근접 시스템(Proximity System)은 플랫폼을 기하학적 중심에 위치한 하나의 점으로 표현하기보다 로봇의 전체 풋프린트(Footprint)와 예측된 스윕 경로(Predicted Swept Path)를 고려해야 한다.

매니퓰레이터와 모바일 매니퓰레이터(Mobile Manipulator)의 경우 여러 로봇 구성요소가 동시에 움직일 수 있기 때문에 근접 관리가 더욱 복잡해진다. 이동 베이스(Base), 로봇 팔 링크(Arm Links), 엔드 이펙터, 운반 물체(Carried Object), 부착 도구(Attached Tool)는 각각 서로 다른 위험 영역을 만들 수 있다. 따라서 안전 표현(Safety Representation)은 관절 속도(Joint Velocity)와 가능한 미래 구성을 고려하면서 인간의 신체 또는 신체 일부와 여러 이동 로봇 형상 사이의 최소 거리를 평가해야 할 수 있다.

인간 신체 표현(Human Body Representation) 역시 근접 계산에 영향을 미친다. 사람을 하나의 점으로 표현하면 팔, 손, 다리 또는 머리가 로봇 방향으로 뻗어 있을 때 위험을 과소평가할 수 있다. 센싱 능력과 응용 요구사항에 따라 인간은 경계 볼륨(Bounding Volume), 골격 모델(Skeletal Model), 신체 부위 영역(Body-Part Region), 점유 분포(Occupancy Distribution), 불확실성 영역(Uncertainty Envelope) 등으로 표현할 수 있다. 더 상세한 표현은 가까운 협업을 지원하지만 신뢰할 수 있는 지각과 세심한 검증이 필요하다.

안전 영역은 인간을 대상으로 하는 경고(Human-Facing Warnings) 및 로봇 의도 전달(Robot Intent Communication)과 일관되게 상호작용해야 한다. 사람이 제한 영역(Restricted Region)에 접근하면 로봇의 움직임을 크게 제한하기 전에 시각적 또는 청각적 정보를 제공할 수 있다. 더 가까워질수록 강한 경고와 더욱 제한적인 로봇 대응을 적용할 수 있다. 이러한 조정된 행동은 사람이 로봇의 감속, 양보, 정지 또는 재계획 이유를 이해하도록 하여 자율 행동의 변화가 설명되지 않은 것처럼 느껴지는 상황을 줄인다.

위험 수준이 요구하는 경우 근접 관리(Proximity Management)는 독립적인 안전 메커니즘(Independent Safety Mechanisms)과 연결되어야 한다. AI 지각(AI Perception)과 예측(Prediction)은 유연한 의미적 인식(Semantic Awareness)과 적응형 안전 영역(Adaptive Safety Zones)을 제공할 수 있지만, 안전 필수 보호 기능에는 독립적인 센싱, 안전 등급 제어기(Safety-Rated Controller) 또는 별도로 보증된 모니터링이 필요할 수 있다. 따라서 고급 물리 AI는 지능적인 동적 안전 영역 안에서 작동하면서 필요할 경우 더 보수적인 보호 계층이 기본적인 안전 한계를 강제하도록 구성할 수 있다.

런타임 보증(Runtime Assurance)은 안전 영역을 지원하는 가정들이 계속 유효한지를 모니터링해야 한다. 센서 고장, 위치추정 성능 저하, 과도한 지연시간, 제동 성능 저하, 예상하지 못한 적재물 변화, 캘리브레이션 오류 또는 낮은 환경 가시성은 이전에 허용되었던 분리 거리를 더 이상 안전하지 않게 만들 수 있다. 이러한 성능 저하가 탐지되면 시스템은 안전 영역을 확대하고 최대 속도를 낮추며 자율 기능을 제한하거나 인간 지원을 요청하고 최소 위험 상태(Minimum-Risk Condition)로 전환할 수 있다.

평가(Evaluation)는 안전 영역의 기하학적 구성과 사람이 해당 영역과 상호작용할 때 발생하는 로봇 행동을 모두 시험해야 한다. 시나리오에는 느리거나 빠른 접근, 교차 궤적(Crossing Trajectories), 갑작스러운 출현, 여러 사람, 가림, 좁은 공간, 후진, 방향 전환, 매니퓰레이터 도달 영역, 센서 성능 저하 및 불확실한 위치추정이 포함되어야 한다. 시험은 단순히 경계가 탐지되는지를 넘어 경고, 감속, 재계획, 정지 및 복구가 충분한 시간과 일관성을 가지고 수행되는지를 검증해야 한다.

거짓 양성(False Positive)과 거짓 음성(False Negative)은 서로 다른 운용상의 결과를 발생시킨다. 지나치게 보수적인 안전 영역 활성화는 불필요한 정지를 빈번하게 발생시켜 생산성을 저하시키고 사람이 경고를 무시하거나 안전 절차를 우회하도록 만들 수 있다. 반대로 충분히 보수적이지 않은 활성화는 사람을 허용할 수 없는 위험에 노출시킬 수 있다. 따라서 효과적인 근접 관리는 요구되는 위험 감소 수준과 운용 가용성(Operational Availability)의 균형을 유지하도록 신중하게 검증된 임계값과 불확실성 여유를 필요로 한다.

안전 영역 이벤트(Safety-Zone Event) 이후의 복구(Recovery) 역시 통제되어야 한다. 사람이 잠시 경계 밖으로 이동했다는 이유만으로 로봇이 즉시 제한 없는 움직임을 재개해서는 안 된다. 이벤트에 따라 시스템은 안정적인 분리 거리, 회복된 센서 신뢰도, 계획 경로가 안전하다는 재확인 또는 운영자 확인(Operator Acknowledgment)을 요구할 수 있다. 통제된 복구는 반복적인 정지와 재시작을 방지하고 근본적인 위험 상호작용이 해결되지 않은 상태에서 움직임이 재개될 가능성을 줄인다.

안전 영역(Safety Zones)과 근접 관리(Proximity Management)는 궁극적으로 지각 정보를 로봇 행동 주변에서 지속적으로 변화하는 공간적 안전 영역(Spatial Safety Envelope)으로 변환한다. 인간 추적(Human Tracking)은 사람이 어디에 있을 수 있는지를 파악하고, 예측(Prediction)은 사람이 어디로 이동할 수 있는지를 추정하며, 로봇 계획(Robot Planning)은 미래 점유 공간을 정의하고, 불확실성(Uncertainty)은 주의해서 다루어야 할 영역을 확대한다. 이러한 요소들은 함께 속도 및 분리 모니터링(Speed and Separation Monitoring), 의도 인식 기반 상호작용(Intent-Aware Interaction), 보호 정지, 예측 가능한 인간-로봇 공존(Predictable Human--Robot Coexistence)을 위한 공간적 기반을 제공한다.

## 05.04. Speed and Separation Monitoring

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

속도 및 분리 모니터링(Speed and Separation Monitoring)은 인간과의 근접성(Human Proximity)을 로봇의 움직임 제약(Robot Motion Constraints)과 직접 연결한다. 그 목적은 안전한 조건에서는 유용한 운전을 허용하면서 사람과 위험한 로봇 움직임 사이에 충분한 거리를 유지하는 것이다. 고정된 장벽이나 완전 정지에만 의존하는 대신 시스템은 분리 거리, 상대 운동(Relative Motion), 로봇 속도, 정지 성능(Stopping Capability), 지각 품질(Perception Quality), 불확실성(Uncertainty)을 지속적으로 평가하여 적절한 움직임 수준을 결정한다.

핵심 개념은 허용 가능한 로봇 속도(Allowable Robot Speed)가 사람과 로봇의 관련 이동 부위 사이에 확보된 분리 거리(Separation Distance)에 따라 달라진다는 것이다. 분리 거리가 충분히 크면 정상 운전을 허용할 수 있다. 사람이 가까워지면 허용 속도를 점진적으로 낮출 수 있으며, 결국 보호 정지(Protective Stop)가 필요한 수준까지 감소할 수 있다. 이는 모든 인간의 존재에 동일하게 대응하는 대신 거리와 속도 사이에 동적인 관계(Dynamic Relationship)를 형성한다.

분리 거리는 추상적인 기준점 사이가 아니라 실제 위험 형상(Hazardous Geometry)을 기준으로 측정해야 한다. 이동 로봇(Mobile Robot)의 경우 차체(Chassis), 적재물(Payload), 돌출 장비 또는 예측된 스윕 풋프린트(Predicted Swept Footprint)가 관련 형상에 포함될 수 있다. 매니퓰레이터(Manipulator)의 경우 개별 링크(Link), 엔드 이펙터(End Effector), 도구 및 운반 물체가 포함될 수 있다. 인간의 신체 영역과 움직이는 로봇 형상 사이의 의미 있는 최소 거리가 안전 판단의 기초가 되는 경우가 많다.

분리 거리는 빠르게 변할 수 있으므로 인간의 움직임(Human Motion) 역시 중요하다. 수 미터 떨어져 정지해 있는 사람은 즉각적인 위험이 낮을 수 있지만, 로봇을 향해 빠르게 움직이는 사람은 짧은 시간 안에 사용 가능한 안전 여유(Safety Margin)를 소진할 수 있다. 따라서 추적(Tracking)은 위치, 속도, 방향 및 불확실성을 제공하며, 모니터링 기능은 이를 이용하여 접근 속도(Closing Speed)를 추정하고 인간과 로봇이 서로 접근하는지, 멀어지는지 또는 비슷한 방향으로 이동하는지를 판단할 수 있다.

로봇 속도(Robot Velocity)는 물리적 상호작용의 발생 가능성과 잠재적인 심각성 모두에 영향을 미친다. 일반적으로 속도가 높아질수록 정지 거리가 증가하고 지각, 의사결정 및 개입에 사용할 수 있는 시간이 감소한다. 따라서 모니터링 시스템은 하나의 플랫폼 속도만 이용하기보다 병진 속도(Translational Velocity), 회전 속도(Rotational Velocity), 매니퓰레이터 관절 운동(Joint Motion), 관련 구성요소의 속도를 평가해야 한다. 로봇의 각 부위는 주변 사람을 향해 서로 다른 국부 접근 속도(Local Approach Speed)를 만들 수 있다.

정지 거리(Stopping Distance)는 정지 명령이 액추에이터(Actuator)에 도달한 이후 측정되는 기계적 제동 거리(Mechanical Braking Distance)만을 의미하지 않는다. 완전한 안전 분석에는 센싱 시간(Sensing Time), 지각 처리, 인간 추적, 통신, 안전 로직(Safety Logic), 제어기 응답, 액추에이터 지연, 제동 동역학(Braking Dynamics), 이러한 단계에서 이동하는 거리까지 포함된다. 요구되는 분리 거리는 보호 행동이 허용할 수 없는 접촉을 방지할 만큼 충분히 일찍 시작되도록 전체 응답 체인(Response Chain)을 고려해야 한다.

상대 접근 속도(Relative Approach Speed)는 로봇 속도만 사용하는 것보다 위험을 더 유용하게 나타낸다. 로봇과 사람이 서로를 향해 움직이면 각자의 개별 속도만으로 예상하는 것보다 분리 거리가 빠르게 감소할 수 있다. 반대로 같은 방향으로 움직이는 경우 접근률(Closing Rate)은 훨씬 낮을 수 있다. 따라서 모니터링은 보호된 공간 조건(Protected Spatial Condition)이 침해되기까지 남은 시간을 추정할 때 인간과 로봇 움직임의 결합 운동학(Combined Kinematics)을 고려해야 한다.

실제 시스템은 분리 거리에 따라 점진적으로 제한되는 운용 상태(Operating States)를 정의할 수 있다. 장거리에서는 주변 상황을 인식하면서 정상 운전을 수행할 수 있고, 중간 거리에서는 관찰을 강화하거나 경고를 발생시킬 수 있다. 분리 거리가 더 감소하면 속도와 가속도(Acceleration)를 제한할 수 있다. 계산된 보호 분리 거리(Protective Separation)를 더 이상 유지할 수 없는 경우 시스템은 보호 정지 또는 사전에 정의된 최소 위험 대응(Minimum-Risk Response)을 시작할 수 있다.

동적 속도 제한(Dynamic Speed Limits)은 안전을 유지하면서 로봇의 생산성을 보존할 수 있도록 한다. 사람이 넓은 작업 공간에 진입할 때마다 정지시키는 대신 제어기는 측정된 거리와 현재 조건에 따라 허용 속도를 감소시킬 수 있다. 사람이 멀어지고 안정적인 분리 거리가 다시 확보되면 속도를 점진적으로 증가시킬 수 있다. 이러한 적응은 공유 산업 공간, 물류창고, 병원, 서비스 환경 및 협업 조작(Collaborative Manipulation) 작업에서 특히 유용하다.

현재 속도만으로 미래의 움직임을 설명할 수 없기 때문에 가속도와 방향 변화(Direction Changes)도 고려해야 한다. 천천히 이동하는 로봇이 사람 방향으로 가속하거나 회전할 준비를 하고 있을 수 있으며, 매니퓰레이터가 현재 비어 있는 공간으로 링크를 이동하려 할 수도 있다. 따라서 모니터링은 명령된 움직임(Commanded Motion), 계획 궤적(Planned Trajectory), 가속도 제한, 예측된 스윕 볼륨(Predicted Swept Volume)을 포함하여 미래의 로봇 행동이 확보된 분리 거리와 양립할 수 있는지를 판단할 수 있다.

인간 궤적 예측(Human Trajectory Prediction)은 추가적인 반응 시간을 제공할 수 있다. 추적 결과 사람이 로봇의 계획 경로를 가로지를 가능성이 있다고 판단되면 최소 분리 거리에 도달하기 전에 감속 또는 재계획(Replanning)을 시작할 수 있다. 그러나 인간의 움직임은 갑자기 변화할 수 있으므로 예측은 보수적으로 처리해야 한다. 시스템은 하나의 미래 궤적을 확정적으로 가정하기보다 가능한 미래 점유 영역(Plausible Future Occupancy)을 고려하고 예측 행동의 불확실성이 증가할수록 안전 여유를 확대할 수 있다.

불확실성(Uncertainty)은 속도 및 분리 모니터링의 핵심 구성요소이다. 인간의 위치와 속도, 로봇 위치추정(Localization), 캘리브레이션(Calibration), 타이밍(Timing), 정지 성능에는 모두 오류 또는 변동이 존재한다. 이러한 불확실성이 큰 상황에서 시스템은 추정된 분리 거리를 정확한 물리적 값으로 간주해서는 안 된다. 보수적인 여유(Conservative Margin)를 통해 불완전한 정보를 보상하고 불확실성이 검증된 조건을 넘어 증가하면 허용 속도를 감소시킬 수 있다.

따라서 지각 성능 저하(Perception Degradation)는 움직임 제한에 직접 영향을 주어야 한다. 낮은 조도, 센서 오염, 가림(Occlusion), 프레임 손실(Dropped Frames), 위치추정 성능 저하, 과도한 추론 지연(Inference Latency), 센서 간 불일치는 측정된 인간-로봇 관계에 대한 신뢰도를 감소시킬 수 있다. 지각 성능이 저하된 상태에서 동일한 속도를 유지하는 것은 사실상 안전 여유를 소모하는 것과 같다. 견고한 시스템은 필요한 분리 거리를 확대하고 속도를 줄이거나 움직임을 제한하며 보호 상태(Protective State)로 전환할 수 있다.

지연시간(Latency)은 속도 및 분리 추정이 항상 어느 정도 이전 시점의 물리적 세계를 나타낸다는 점에서 특히 중요하다. 센싱, 추론, 필터링, 통신 및 제어가 완료되는 동안 인간과 로봇은 모두 이동할 수 있다. 따라서 모니터링은 제한된 종단 간 지연시간(Bounded End-to-End Latency)을 가정하고 필요한 경우 추정 상태를 현재 의사결정 시점까지 전파해야 한다. 예상하지 못한 지연시간 증가는 이전에 허용되었던 운용 한계를 무효화할 수 있으므로 탐지되어야 한다.

샘플링 주기(Sampling Frequency)와 시간적 안정성(Temporal Stability)도 성능에 영향을 미친다. 갱신 속도가 너무 느리면 빠르게 변화하는 상호작용을 포착하지 못할 수 있으며, 잡음이 많은 고주파 추정은 반복적인 속도 변화나 불필요한 정지를 발생시킬 수 있다. 필터링(Filtering), 히스테리시스(Hysteresis), 시간적 일관성 검사(Temporal Consistency Check)는 제어 판단을 안정화할 수 있지만 실제 위험을 억제해서는 안 된다. 따라서 모니터링 아키텍처는 모호한 전환 상황에서 보수적인 행동을 유지하면서 응답성과 견고성 사이의 균형을 확보해야 한다.

이동 로봇(Mobile Robot)의 경우 속도 및 분리 모니터링은 플랫폼의 전체 풋프린트(Footprint)와 조향 행동(Maneuvering Behavior)을 고려해야 한다. 전진, 후진, 방향 전환, 제자리 회전(Rotation in Place), 도킹(Docking)은 서로 다른 접근 형상을 발생시킨다. 로봇 옆에 서 있는 사람은 로봇의 중심 위치가 거의 변하지 않더라도 플랫폼이 회전을 시작하면 위험에 노출될 수 있다. 따라서 로봇 경계 주변의 국부 속도(Local Velocity)가 질량 중심(Center of Mass)의 속도보다 중요할 수 있다.

매니퓰레이터에서는 관절 운동(Joint Motion)과 직교좌표계 운동(Cartesian Motion) 사이의 관계가 중요하다. 서로 다른 링크는 사람을 향해 서로 다른 속도로 움직일 수 있으며, 개별 관절 속도가 낮더라도 엔드 이펙터는 빠르게 이동할 수 있다. 모니터링은 계획된 움직임 전체에서 관련 로봇 형상을 평가하고 인간과 로봇 사이에서 가장 가까운 관계를 식별해야 한다. 모바일 매니퓰레이터(Mobile Manipulator)는 이동 베이스와 관절형 로봇 팔에 대해 이러한 판단을 동시에 수행해야 한다.

인간 신체 표현(Human Body Representation)을 사용하면 분리 거리 계산을 더욱 정교하게 만들 수 있다. 탐지된 사람의 중심점까지의 거리만 측정하면 로봇 작업 공간으로 들어온 팔, 손, 다리 또는 머리를 놓칠 수 있다. 경계 볼륨(Bounding Volume), 골격 표현(Skeletal Representation), 신체 부위 추적(Body-Part Tracking), 점유 영역(Occupancy Envelope)은 보다 의미 있는 분리 거리 추정을 제공할 수 있다. 필요한 표현 수준은 응용 분야, 센싱 능력, 상호작용 거리 및 검증 과정에서 입증된 신뢰성에 맞추어야 한다.

속도 및 분리 모니터링은 단순히 성능 중심의 충돌 회피(Performance-Oriented Collision Avoidance)와 구별되어야 한다. 계획 알고리즘(Planning Algorithm)은 사람을 효율적으로 회피하려 할 수 있지만 안전 모니터링은 물리적 제약이 허용 가능한 범위에 있는지를 독립적으로 판단해야 한다. AI 플래너(AI Planner)가 요구되는 분리 거리나 속도 제한을 위반하는 궤적을 제안하면 안전 계층(Safety Layer)은 플래너가 예상하는 작업상의 이점과 관계없이 해당 움직임을 제한하거나 거부하거나 정지시킬 수 있어야 한다.

이러한 책임 분리(Separation of Responsibilities)는 심층 방어(Defense in Depth)를 지원한다. AI 지각(AI Perception), 궤적 예측(Trajectory Prediction), 적응형 계획(Adaptive Planning)은 풍부한 상황 이해를 제공할 수 있으며, 독립적인 안전 센싱(Independent Safety Sensing)과 제어 메커니즘은 필요한 경우 기본적인 보호 제약을 강제할 수 있다. 지능형 계층(Intelligent Layer)은 허용된 안전 영역 안에서 움직임을 최적화할 수 있지만 학습 기반 플래너나 월드 모델(World Model)의 실패가 위험한 속도를 제한하거나 보호 정지를 수행하는 메커니즘까지 제거해서는 안 된다.

런타임 보증(Runtime Assurance)은 허용 가능한 움직임을 계산하는 데 사용되는 가정이 계속 유효한지를 지속적으로 검증해야 한다. 관련 변수에는 센서 가용성(Sensor Availability), 추적 품질(Tracking Quality), 위치추정 정확도, 통신 지연, 제어기 타이밍, 제동 성능, 적재물 구성(Payload Configuration), 환경 조건이 포함된다. 이러한 변수 중 하나라도 검증된 범위를 벗어나면 기존에 계산된 분리 거리 요구사항이 충분하지 않을 수 있으므로 속도 감소, 안전 여유 확대, 성능 저하 운전(Degraded Operation) 또는 안전 상태 전환(Safe-State Transition)이 필요하다.

평가(Evaluation)는 정적인 거리 시험만 수행하기보다 실제적인 인간과 로봇 움직임의 조합을 포함해야 한다. 중요한 시나리오에는 정면 접근, 경로 교차(Crossing Paths), 추월(Overtaking), 갑작스러운 인간 진입, 로봇 후진, 빠른 방향 전환, 매니퓰레이터 도달, 여러 사람, 가림, 센서 성능 저하, 적재물 변화가 포함된다. 시험은 정상 조건뿐 아니라 현실적으로 발생 가능한 지연과 불확실성의 조합에서도 시스템이 충분한 여유를 확보하여 감속하고 정지하는지를 검증해야 한다.

지나치게 보수적인 모니터링은 불필요한 감속과 정지를 빈번하게 발생시킬 수 있으므로 운용 성능(Operational Performance)도 평가해야 한다. 이러한 행동은 생산성을 감소시키고 사용자가 안전 메커니즘을 우회하도록 유도할 수 있다. 반대로 공격적인 임계값(Aggressive Thresholds)은 처리량(Throughput)을 유지하면서 보호 수준을 낮출 수 있다. 따라서 효과적인 설계는 요구되는 위험 감소 수준을 훼손하지 않으면서 로봇 가용성(Robot Availability)과 유용한 속도를 최대화할 수 있는 검증된 운용 영역(Validated Operating Envelope)을 추구한다.

감속 또는 보호 정지 이후의 복구(Recovery)는 최초 대응만큼 신중하게 제어되어야 한다. 충분한 분리 거리가 다시 확보되고 관련 지각 및 시스템 상태 조건이 안정된 이후에만 속도를 증가시켜야 한다. 응용 분야에 따라 복구 과정에서 궤적 재평가(Trajectory Reevaluation) 또는 인간의 확인(Human Acknowledgment)이 추가로 필요할 수 있다. 이를 통해 로봇이 경계 주변에서 반복적으로 가속과 정지를 수행하거나 해결되지 않은 상호작용 상황으로 다시 움직이는 것을 방지할 수 있다.

속도 및 분리 모니터링(Speed and Separation Monitoring)은 궁극적으로 인간의 움직임과 허용 가능한 로봇 움직임 사이에 실시간 결합(Real-Time Coupling)을 형성한다. 인간 탐지(Human Detection)는 사람의 존재를 확인하고, 추적(Tracking)은 상대 운동을 추정하며, 안전 영역(Safety Zones)은 공간적 구조를 제공하고, 정지 모델(Stopping Model)은 필요한 안전 여유를 결정하며, 불확실성(Uncertainty)은 이러한 여유를 보수적으로 조정한다. 이러한 메커니즘을 통해 물리 AI 시스템은 사람과 물리적 환경을 공유하면서 예측 가능한 방식으로 감속하고, 양보하고, 재계획하고, 정지하고, 다시 운전을 복구할 수 있다.

## 05.05. Intent Recognition and Human Awareness

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

의도 인식(Intent Recognition)과 인간 인식(Human Awareness)은 인간-로봇 안전(Human--Robot Safety)을 단순히 사람이 어디에 있는지를 탐지하는 수준에서 그 사람이 무엇을 하려고 하는지를 이해하는 수준으로 확장한다. 사람 주변에서 동작하는 물리 AI 시스템(Physical AI System)은 인간 행동이 본질적으로 불확실하다는 점을 인식하면서 움직임, 자세, 제스처, 주의 상태, 작업 맥락 및 상호작용 이력을 해석해야 한다. 이를 통해 로봇은 잠재적인 상호작용을 예상하고 위험한 공간 관계가 형성되기 전에 행동을 조정할 수 있다.

인간 인식(Human Awareness)은 로봇 환경에 존재하는 사람들에 대한 지속적으로 갱신되는 표현(Representation)에서 시작된다. 탐지(Detection)는 사람의 존재를 확인하고, 추적(Tracking)은 위치와 움직임을 추정하며, 자세 추정(Pose Estimation)은 신체 구성에 관한 정보를 제공한다. 의도 인식은 이러한 관측을 기반으로 로봇 경로 횡단, 작업장 접근, 물체를 향한 손 뻗기, 지원 요청 또는 상호작용 영역에서 벗어나는 것과 같은 가능한 목표나 단기 행동을 추론한다.

의도(Intent)는 직접 관찰할 수 있는 물리량으로 취급해서는 안 된다. 센서는 영상, 깊이, 움직임, 위치, 방향, 음향 및 기타 신호를 측정하지만 의도는 이러한 관측에서 나타나는 패턴을 기반으로 추론해야 한다. 동일한 움직임도 상황에 따라 서로 다른 의도를 의미할 수 있다. 로봇을 향해 걸어오는 사람은 로봇의 경로를 가로지르거나, 로봇과 상호작용하거나, 주변의 물체를 가져가거나, 단순히 해당 공간을 통과하려는 것일 수 있으므로 확률적 해석(Probabilistic Interpretation)이 필수적이다.

신체 움직임(Body Motion)은 단기 의도 인식(Short-Term Intent Recognition)에 중요한 단서를 제공한다. 보행 방향, 속도, 가속도, 몸통 방향(Torso Orientation), 머리 방향, 팔 움직임, 손 위치 및 자세 변화는 가능한 미래 행동을 나타낼 수 있다. 작업자가 로봇 통로 방향으로 몸을 돌리는 것은 곧 통로를 횡단할 가능성을 나타낼 수 있으며, 공유 작업 공간으로 손을 뻗는 행동은 임박한 상호작용을 의미할 수 있다. 이러한 단서는 하나의 관측보다 시간에 따른 연속적인 변화로 해석할 때 더 유용하다.

인간의 시선(Gaze)과 주의 상태(Attention)는 인식 상태와 의도된 행동에 대한 추가적인 정보를 제공할 수 있지만 신중하게 해석해야 한다. 머리 방향이나 추정된 시선은 사람이 로봇을 인지했는지, 로봇의 움직임을 관찰하고 있는지 또는 다른 대상에 집중하고 있는지를 나타낼 수 있다. 그러나 시각적 주의가 있다고 해서 상황을 이해했거나 특정 행동을 할 것이라는 보장은 없다. 따라서 안전 판단은 사람이 로봇을 본 것으로 보인다는 이유만으로 양보할 것이라고 가정해서는 안 된다.

제스처(Gesture)는 운용 환경에서 그 의미가 정의되어 있는 경우 보다 명시적인 상호작용 신호를 제공할 수 있다. 손을 들거나, 가리키거나, 정지 동작을 하거나, 방향을 표시하거나, 작업별 신호를 사용하는 것은 요청이나 명령을 전달할 수 있다. 신뢰성 있는 활용을 위해서는 명확한 제스처 정의, 충분한 센싱 범위(Sensing Coverage), 모호한 인식 결과를 처리하는 메커니즘이 필요하다. 신뢰도가 충분하지 않거나 여러 해석이 가능한 경우 안전 필수 행동(Safety-Critical Behavior)이 하나의 제스처 해석에 의존해서는 안 된다.

맥락(Context)은 의도 인식의 정확성과 유용성을 크게 향상시킨다. 독립적으로 보면 모호한 인간 행동도 작업 공간의 형상, 작업 상태(Task State), 통행 규칙, 물체 위치, 로봇 임무 및 이전 상호작용과 결합하면 보다 명확하게 이해할 수 있다. 이송 작업 중 적재 스테이션(Loading Station)에 접근하는 사람은 제한 없는 복도에서 동일한 궤적으로 이동하는 사람과 다른 의도를 가질 가능성이 있다. 따라서 맥락은 인간 지각(Human Perception)을 로봇의 월드 모델(World Model) 및 작업 이해(Task Understanding)와 연결한다.

상호작용 이력(Interaction History)은 또 다른 시간적 정보의 원천을 제공한다. 반복적인 관측을 통해 사람이 대기하고 있는지, 로봇을 따라가고 있는지, 작업장에 반복적으로 접근하고 있는지 또는 협업 작업(Collaborative Task)에 참여하고 있는지를 파악할 수 있다. 관련된 단기 이력(Short-Term History)을 유지하면 일시적인 움직임과 목적을 가진 상호작용을 구별할 수 있다. 그러나 과거 행동이 동일한 미래 행동을 보장한다고 부당하게 가정하지 않으면서 예측에 활용해야 한다.

인간은 자신의 결정을 빠르게 변경할 수 있기 때문에 의도 인식에는 본질적인 불확실성(Uncertainty)이 존재한다. 계속 걸어갈 것으로 예측된 사람이 갑자기 멈추거나, 방향을 바꾸거나, 가속하거나, 로봇 작업 공간으로 손을 뻗을 수 있다. 따라서 시스템은 하나의 해석을 너무 일찍 확정하기보다 여러 가능한 의도 또는 미래 궤적(Future Trajectories)을 표현해야 한다. 불확실성이 높은 경우 감속, 분리 거리 확대 또는 추가 관찰과 같은 보수적인 행동을 통해 안전을 유지할 수 있다.

인간 인식은 사람을 탐지하는 것과 그 사람이 로봇을 인식하고 있는지를 추정하는 것을 구별해야 한다. 주변 작업자는 화면을 보고 있거나, 로봇을 등지고 있거나, 청력 보호 장비를 착용하거나, 다른 작업에 집중하고 있을 수 있다. 로봇은 사람이 탐지되었다는 이유만으로 상호 인식(Mutual Awareness)이 형성되었다고 가정해서는 안 된다. 인간의 인식 상태가 불확실한 경우 로봇의 의도를 더욱 명확하게 전달하거나 안전 여유를 확대하는 방식으로 상호작용 전략을 조정할 수 있다.

로봇 의도 전달(Robot Intent Communication)은 인간 의도 인식(Human Intent Recognition)을 보완한다. 안전한 상호작용은 양방향(Bidirectional)으로 이루어진다. 로봇은 사람이 무엇을 할 가능성이 있는지를 이해하는 동시에 자신이 계획하는 행동을 사람이 이해할 수 있도록 해야 한다. 움직임 단서(Motion Cues), 조명, 디스플레이, 소리, 투영 경로(Projected Path) 등의 신호를 통해 로봇이 이동, 회전, 양보, 정지 또는 작업 공간 진입을 계획하고 있음을 나타낼 수 있다. 예측 가능한 로봇 행동은 사람이 정확한 기대를 형성하도록 하여 양측의 모호성을 감소시킨다.

의도 인식 기반 계획(Intent-Aware Planning)은 즉각적인 근접 제약이 침해되기 전에 인간 행동 예측을 활용할 수 있다. 사람이 로봇의 이동 경로를 가로지를 가능성이 있다면 플래너(Planner)는 감속하거나, 양보하거나, 다른 경로를 선택하거나, 공유 영역으로의 진입을 지연시킬 수 있다. 작업자가 협업 작업 공간으로 손을 뻗을 가능성이 있다면 손이 보호 영역(Protective Zone)에 들어오기 전에 매니퓰레이터의 움직임을 조정할 수 있다. 이러한 선제적 행동(Anticipatory Behavior)은 단순한 반응형 정지보다 부드럽고 안전한 상호작용을 가능하게 한다.

그러나 의도 인식은 항상 물리적 안전 제약(Physical Safety Constraints)에 종속되어야 한다. 사람이 멀어질 의도가 있다고 예측되었다고 해서 요구되는 분리 거리 또는 속도 제한을 위반할 수 있는 것은 아니다. 인간의 실제 행동은 예측된 의도와 달라질 수 있으며 지각 시스템도 실패할 수 있다. 따라서 안전 영역(Safety Zones), 속도 및 분리 모니터링(Speed and Separation Monitoring), 보호 정지(Protective Stopping), 독립적인 안전 메커니즘(Independent Safety Mechanisms)은 의도 모델의 해석과 관계없이 기본적인 제약을 계속 강제해야 한다.

다중 양식 지각(Multi-Modal Perception)은 시각, 기하학적 정보, 움직임 및 상호작용 정보를 결합하여 인간 인식을 강화할 수 있다. 카메라는 자세와 제스처 단서를 제공하고, 라이다(LiDAR) 또는 깊이 센서(Depth Sensor)는 공간적 관계를 제공하며, 레이더(Radar)는 움직임 정보를 추가할 수 있다. 음성 또는 명시적인 인터페이스 명령(Interface Command)은 의미적 맥락(Semantic Context)을 추가할 수 있다. 센서 융합(Fusion)은 견고성을 향상시킬 수 있지만 서로 충돌하는 신호는 부당하게 높은 확신으로 통합하기보다 불확실성을 증가시키는 방향으로 처리해야 한다.

집단 행동(Group Behavior)은 추가적인 복잡성을 발생시킨다. 여러 사람은 서로에게 영향을 주고, 함께 이동하거나, 예상하지 못하게 분리되거나, 서로의 신체 움직임을 가릴 수 있다. 군중이나 공유 작업 공간에서 운용되는 로봇은 개별 인간의 의도뿐 아니라 집단적인 이동 패턴(Collective Movement Patterns)도 판단해야 할 수 있다. 특히 교차로, 출입구, 작업장 및 경로가 분기되는 영역에서는 집단의 모든 사람이 동일한 궤적을 따를 것이라고 가정해서는 안 된다.

역할 및 작업 인식(Role and Task Awareness)은 의도 해석을 더욱 정교하게 만들 수 있다. 권한이 있는 운영자, 유지보수 기술자, 협업 작업자, 방문자, 승객 또는 보행자는 동일한 로봇과 서로 다른 방식으로 상호작용할 수 있다. 역할 정보가 적법하고 신뢰성 있게 제공되는 경우 예상되는 상호작용 패턴과 허용된 명령을 해석하는 데 활용할 수 있다. 그러나 안전이 신뢰할 수 없는 신원 가정에 의존해서는 안 되며, 익숙하지 않은 사람도 로봇에 대한 전문적인 지식 없이 적절한 보호를 받을 수 있어야 한다.

의도 모델(Intent Model)은 인간 행동이 학습 또는 검증 데이터와 달라지는 분포 변화(Distribution Shift) 상황에서 실패할 수 있다. 문화적 차이에 따른 제스처, 특이한 의복, 이동 보조기구(Mobility Aid), 비정형적인 신체 움직임, 익숙하지 않은 작업 절차, 혼잡한 환경 또는 새로운 공간 배치는 예측 품질을 감소시킬 수 있다. 런타임 모니터링(Runtime Monitoring)은 낮은 신뢰도, 일관되지 않은 예측 또는 익숙하지 않은 관측을 탐지하고 시스템이 더욱 보수적인 근접 및 움직임 정책으로 전환하도록 해야 한다.

지연시간(Latency) 역시 의도 인식의 유용성에 영향을 미친다. 정확한 해석이라도 관련된 인간 행동이 이미 시작된 이후에 도착한다면 예방적 가치가 크게 감소한다. 따라서 지각, 자세 추정, 시간 모델링(Temporal Modeling), 예측, 계획 및 제어는 상호작용 속도에 적합한 종단 간 시간 예산(End-to-End Timing Budget) 안에서 수행되어야 한다. 빠르게 변화하는 환경에서는 더 이른 예측 범위가 필요하지만 장기 예측에서 증가하는 불확실성 역시 신중하게 관리해야 한다.

잘못된 의도 예측(False Intent Prediction)은 유형에 따라 서로 다른 결과를 발생시킨다. 실제로 발생하지 않을 상호작용을 예측하면 불필요한 감속이나 양보가 발생할 수 있지만, 실제 횡단이나 손 뻗기 행동을 예측하지 못하면 사용할 수 있는 반응 시간이 감소할 수 있다. 따라서 평가는 단순한 분류 정확도(Classification Accuracy)뿐 아니라 오류가 실제 운용에 미치는 결과도 고려해야 한다. 위험한 의도를 놓치는 비용이 불필요한 주의 행동보다 훨씬 큰 경우 안전 중심 임계값은 의도적으로 보수적인 대응을 선택할 수 있다.

평가(Evaluation)는 정해진 제스처나 예측 가능한 궤적만이 아니라 모호하고 변화하는 인간 행동을 포함해야 한다. 유용한 시나리오에는 갑작스러운 방향 변경, 중단된 접근, 부분 가림, 주의가 분산된 사람, 서로 충돌하는 신체 단서, 여러 사람이 경로를 교차하는 상황, 예상하지 못한 손 뻗기, 망설임, 로봇 신호를 무시하는 사람이 포함된다. 시험에서는 불확실성이 적절하게 표현되는지와 의도 예측이 잘못된 경우에도 전체 로봇 대응이 안전하게 유지되는지를 측정해야 한다.

인간 인식은 런타임 보증(Runtime Assurance)과도 통합되어야 한다. 시스템은 탐지 연속성(Detection Continuity), 자세 품질(Pose Quality), 예측 신뢰도(Prediction Confidence), 센서 일치도(Sensor Agreement), 상호작용 맥락 및 추론된 의도의 안정성을 모니터링할 수 있다. 이러한 지표가 악화되면 로봇은 의도 예측에 대한 의존도를 낮추고 직접적인 공간 보호(Spatial Protection) 중심으로 전환할 수 있다. 이러한 점진적 성능 저하(Graceful Degradation)는 고급 행동 추론이 안전 아키텍처의 단일 실패 지점(Single Point of Failure)이 되는 것을 방지한다.

의도 인식의 목적은 인간의 생각을 읽는 것이 아니라 물리적 상호작용을 개선하는 데 유용한 불확실성 인식 예측(Uncertainty-Aware Prediction)을 제공하는 것이다. 인간 탐지는 누가 존재하는지를 설명하고, 추적은 사람이 어떻게 움직이는지를 나타내며, 자세와 맥락은 행동 단서를 제공하고, 의도 추론(Intent Inference)은 사람이 다음에 무엇을 할 가능성이 있는지를 추정한다. 이러한 예측은 독립적으로 강제되는 안전 한계의 제약을 유지하면서 더 이른 양보, 속도 조정, 재계획, 의사소통 및 보호 행동을 지원할 수 있다.

따라서 의도 인식(Intent Recognition)과 인간 인식(Human Awareness)은 인간 지각(Human Perception)과 로봇 행동(Robot Action) 사이에 선제적 계층(Anticipatory Layer)을 형성한다. 관측된 움직임, 신체 구성, 주의 단서, 제스처, 환경 맥락, 상호작용 이력 및 불확실성을 결합함으로써 물리 AI 시스템은 즉각적인 위험이 발생하기 전에 가능한 인간 행동을 추론할 수 있다. 근접 관리(Proximity Management) 및 속도 및 분리 모니터링(Speed and Separation Monitoring)과 통합된 이러한 역량은 더욱 안전하고 예측 가능하며 자연스러운 인간-로봇 공존(Human--Robot Coexistence)을 지원한다.

## 05.06. Robot Intent Communication

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 의도 전달(Robot Intent Communication)은 물리적 행동이 시작되기 전과 행동이 진행되는 동안 로봇이 계획한 행동을 주변 사람들이 이해할 수 있도록 한다. 물리 AI 시스템(Physical AI System)은 인간을 탐지하고 해석하는 것뿐만 아니라 다음에 무엇을 하려는지에 대한 관찰 가능한 단서(Observable Cues)를 제공해야 한다. 이동, 방향, 양보, 정지, 작업 전환 및 불확실성을 전달하면 모호성(Ambiguity)을 줄이고 사람이 자율 기계와 동적인 공간을 공유할 때 적절한 기대를 형성하도록 도울 수 있다.

의도 전달(Intent Communication)은 단순히 현재 상태를 설명하는 것이 아니라 근본적으로 예측적(Predictive)이어야 한다. 로봇의 움직임이 시작된 이후에야 행동을 설명하는 신호는 예방적 가치가 제한적이다. 효과적인 인터페이스는 사람이 신호를 인지하고 해석하며 대응할 수 있을 만큼 충분히 이른 시점에 예정된 행동을 알려야 한다. 필요한 선행 시간(Lead Time)은 로봇 속도, 상호작용 거리, 환경 복잡성, 인간의 주의 상태 및 의도를 잘못 이해했을 때 발생할 수 있는 결과에 따라 달라진다.

로봇의 움직임(Robot Motion) 자체는 가장 중요한 의사소통 채널 중 하나이다. 점진적인 감속은 양보를 나타낼 수 있고, 의도적인 방향 변화는 이동하려는 방향을 보여줄 수 있으며, 부드러운 접근은 통제된 상호작용을 전달할 수 있다. 따라서 움직임은 기계적 효율성뿐 아니라 이해 가능성(Legibility)을 고려하여 설계해야 한다. 갑작스러운 가속, 불필요한 진동, 급격한 경로 변경 및 반복적인 망설임은 기술적으로 안전한 행동이라도 사람이 예측하기 어렵게 만들 수 있다.

움직임만으로 충분한 정보를 제공하기 어려운 경우 시각 표시(Visual Indicators)를 통해 로봇 의도를 보완할 수 있다. 조명, 발광 밴드(Illuminated Bands), 방향 표시기, 아이콘 및 디스플레이는 이동, 양보, 대기, 회전, 정지 또는 통행 허가 요청 등의 상태를 전달할 수 있다. 이러한 신호는 실제 관찰 조건에서도 단순하고 명확하게 구분되어야 한다. 지나치게 많은 색상, 빠르게 변화하는 패턴 또는 복잡한 상징적 의미는 상황 이해(Situational Understanding)를 향상시키기보다 인지 부하(Cognitive Load)를 증가시킬 수 있다.

방향 의도 전달(Directional Communication)은 사람의 판단이 로봇의 다음 이동 방향에 따라 달라지는 경우가 많기 때문에 이동 로봇(Mobile Robot)에서 특히 중요하다. 표시기를 통해 예정된 회전, 출발, 후진 또는 교차로 통과 경로를 전달할 수 있다. 적합한 환경에서는 투영 경로(Projected Path) 또는 바닥 표시(Floor Indicator)를 이용하여 추가적인 공간 정보를 제공할 수 있다. 그러나 자율 플래너(Autonomous Planner)는 환경 변화에 따라 궤적을 수정할 수 있으므로 이러한 인터페이스는 로봇의 계획을 보수적으로 표현해야 한다.

청각 의사소통(Auditory Communication)은 시각 신호가 사람의 시야 밖에 있거나 즉각적인 주의가 필요한 상황에서 효과적으로 관심을 유도할 수 있다. 음향 신호, 경보, 음성 메시지 및 방향성 음향(Directional Sound)을 통해 접근, 후진, 경고 또는 요청을 전달할 수 있다. 청각 인터페이스는 주변 소음, 청력 보호 장비, 여러 대의 로봇, 언어 차이 및 경보 피로(Alarm Fatigue)를 고려해야 한다. 빈번하거나 모호한 소리는 실제로 중요한 사건과 거의 연결되지 않는다고 사람들이 학습하게 되면 효과가 감소할 수 있다.

디스플레이(Display)와 텍스트 기반 인터페이스(Text-Based Interface)는 사용자가 정보를 읽을 수 있는 충분한 시간과 거리를 확보한 환경에서 더욱 풍부한 의미 정보를 전달할 수 있다. 로봇은 대기 중, 경로 변경 중, 지원 요청 중, 제한 운전 진입 또는 자율적으로 계속 진행할 수 없는 상태 등을 표시할 수 있다. 그러나 사람이 주의가 분산되어 있거나 언어에 익숙하지 않거나 현재 위치에서 디스플레이를 볼 수 없을 수 있으므로 텍스트는 즉각적으로 이해할 수 있는 움직임 및 안전 단서를 대체하기보다 보완해야 한다.

다중 양식 의사소통(Multi-Modal Communication)은 움직임, 시각, 청각 및 인터페이스 신호를 결합하여 중요한 의도가 하나의 채널에만 의존하지 않도록 한다. 예를 들어 로봇이 양보를 준비할 때 감속하고, 대기 상태를 표시하며, 동시에 간단한 시각 신호를 제공할 수 있다. 일관된 중복성(Consistent Redundancy)은 특히 성능 저하 조건에서 인식 가능성을 향상시킬 수 있다. 그러나 서로 다른 양식은 서로 호환되는 의미를 전달해야 하며, 상충되는 단서는 하나의 명확한 신호보다 오히려 로봇 행동을 예측하기 어렵게 만들 수 있다.

사람이 반복적인 상호작용을 통해 안정적인 기대를 학습할 수 있도록 일관성(Consistency)이 유지되어야 한다. 실용적으로 가능한 범위에서 동일한 신호는 항상 동일한 일반적 로봇 행동을 나타내야 한다. 하나의 조명 패턴이 어떤 상황에서는 양보를 의미하고 다른 상황에서는 즉시 이동을 의미한다면 사람은 신뢰할 수 있는 해석을 형성할 수 없다. 따라서 인터페이스 규칙은 운용 모드, 로봇 상태 및 유사한 플랫폼에서 안정적으로 유지되어야 하며 불가피한 차이는 위험한 오해를 방지할 정도로 명확하게 구분되어야 한다.

로봇의 의사소통은 실제 실행 가능한 의도(Executable Intent)를 반영해야 하며, 실행되지 않을 가능성이 있는 내부 계획을 전달해서는 안 된다. 자율 시스템은 최종 행동을 선택하거나 수정하기 전에 여러 후보 궤적(Candidate Trajectories)을 생성하는 경우가 많다. 불안정한 계획 가설(Planning Hypotheses)을 외부에 전달하면 주변 사람을 혼란스럽게 할 수 있다. 따라서 의도 신호는 적절한 확정 수준(Commitment Level)에 도달한 계획과 대응해야 하면서도 인간의 예측과 안전한 상호작용을 지원할 만큼 충분히 일찍 제공되어야 한다.

계획 변경(Plan Changes)은 명시적으로 고려해야 한다. 로봇이 직진할 것이라고 표시한 이후 새롭게 탐지된 장애물 때문에 회전하기로 결정했다면 의사소통 인터페이스도 신속하고 일관되게 갱신되어야 한다. 주변 사람은 이전 신호를 기준으로 이미 행동하고 있을 수 있으므로 전환 과정에서 로봇의 속도를 낮출 필요도 있다. 의사소통 설계는 표시된 의도가 변경된 이후에도 인간의 기존 기대(Human Expectations)가 일정 시간 지속될 수 있다는 점을 고려해야 한다.

인간이 항상 로봇에 주의를 기울이고 있다고 가정해서는 안 된다. 사람은 로봇을 등지고 있거나, 휴대전화를 사용하거나, 보호 장비를 착용하거나, 작업에 집중하거나, 다른 사람과 상호작용하고 있을 수 있다. 인간 인식 추정(Human-Awareness Estimation)은 일반적인 의사소통이 실제로 인지되었을 가능성을 판단하는 데 도움을 줄 수 있다. 인간의 인식 여부가 불확실한 경우 로봇은 분리 거리를 확대하고, 속도를 낮추고, 적절한 신호를 반복하거나 강화하며, 충분한 상호 인식(Mutual Awareness)이 확보될 때까지 인간의 협조에 의존하지 않을 수 있다.

의사소통은 상호작용 역할(Interaction Role)에 맞게 구성되어야 한다. 운영자(Operator)는 상세한 시스템 상태가 필요할 수 있지만 보행자는 주로 즉각적인 이동 의도를 이해하면 된다. 협업 작업자(Collaborative Worker)는 작업 전환이나 매니퓰레이터 행동에 관한 정보가 필요할 수 있으며, 방문자는 보편적으로 이해할 수 있는 단서만 이해할 수 있다. 인터페이스는 모든 사람이 로봇의 내부 아키텍처나 자율성 상태를 이해하도록 요구하지 않으면서 안전한 판단에 필요한 정보를 제공해야 한다.

매니퓰레이터(Manipulator)의 경우 의도 전달을 통해 미래의 로봇 팔 움직임을 더욱 예측 가능하게 만들 수 있다. 움직임 준비(Motion Preparation), 방향 표시기, 작업 공간 조명(Workspace Illumination), 투영 영역(Projected Region), 작업 상태 디스플레이 등을 통해 로봇 팔이 곧 물체에 접근하거나, 물체를 전달하거나, 회전하거나, 공유 작업 공간에 진입할 것임을 표시할 수 있다. 특히 현재 매니퓰레이터 자세만으로 미래의 스윕 볼륨(Swept Volume)을 쉽게 예상하기 어렵거나 여러 관절이 예상하지 못한 움직임을 만들 수 있는 경우 이러한 의사소통이 중요하다.

모바일 매니퓰레이터(Mobile Manipulator)는 이동 베이스와 로봇 팔이 동시에 서로 다른 의도를 나타낼 수 있기 때문에 조정된 의사소통(Coordinated Communication)이 필요하다. 플랫폼이 정지한 상태에서 로봇 팔이 움직일 수도 있고, 매니퓰레이터가 적재물을 유지한 상태에서 베이스가 위치를 변경할 수도 있다. 신호는 로봇의 어느 부분이 움직이려 하는지와 어떤 공간이 점유될 수 있는지를 사람이 이해하도록 해야 한다. 서로 다른 하위 시스템에서 조정되지 않은 표시가 제공되면 전체 로봇 행동에 대한 잘못된 기대를 형성할 수 있다.

의도 전달(Intent Communication)은 안전 영역(Safety Zones) 및 근접 관리(Proximity Management)와 통합되어야 한다. 외곽 상호작용 영역(Outer Interaction Region)에서는 강력한 제한이 필요하기 전에 정보성 신호를 활성화할 수 있다. 사람이 가까워지면 로봇 속도를 감소시키면서 의사소통 신호를 더욱 명확하게 만들 수 있다. 보호 경계(Protective Boundary)에 도달하면 의사소통보다 물리적 안전 메커니즘(Physical Safety Mechanisms)이 우선해야 한다. 이러한 단계적 관계는 로봇이 전달하는 정보와 실제 행동 사이에 일관성을 형성한다.

속도 및 분리 모니터링(Speed and Separation Monitoring)은 의사소통만으로 충분한지 여부를 판단하는 데에도 활용될 수 있다. 로봇은 부족한 정지 거리나 과도한 접근 속도를 경고 신호로 보상해서는 안 된다. 신호는 인간의 이해를 향상시킬 수 있지만 사람이 반드시 이를 보고, 이해하고, 따를 것이라는 보장은 없다. 따라서 필요한 분리 거리, 속도 제한, 보호 정지(Protective Stopping) 및 기타 물리적 제약은 의사소통의 성공 여부와 독립적으로 강제될 수 있어야 한다.

불확실성(Uncertainty)은 지나치게 확신에 찬 신호 뒤에 숨기기보다 로봇 행동에 반영되어야 한다. 지각, 의도 인식, 위치추정 또는 계획이 불확실한 경우 로봇은 신뢰성 있게 실행할 수 없는 구체적인 행동을 확정적으로 전달해서는 안 된다. 대신 감속하거나, 대기하거나, 명확화를 요청하거나, 제한된 운용 상태(Limited Operational State)를 표시할 수 있다. 주변 사람에게 복잡한 내부 확률 값을 전달하려는 것보다 보수적인 행동(Conservative Behavior)이 불확실성을 더욱 신뢰성 있게 표현하는 경우가 많다.

의사소통 채널(Communication Channel)의 고장은 예측 가능한 성능 저하(Predictable Degradation)로 이어져야 한다. 조명 고장, 가려진 디스플레이, 스피커 고장, 네트워크 지연 또는 소프트웨어 오류가 안전 운전에 필요한 보호 기능을 제거해서는 안 된다. 런타임 모니터링(Runtime Monitoring)은 의사소통 기능의 가용성과 명령된 로봇 행동과의 일관성을 검증할 수 있다. 중요한 인터페이스를 사용할 수 없게 되면 다른 양식으로 보완하거나, 안전 여유를 확대하거나, 속도를 낮추거나, 운전을 제한하거나, 더 안전한 상태로 전환할 수 있다.

다중 로봇(Multiple Robots) 환경은 추가적인 의사소통 문제를 발생시킨다. 여러 로봇의 조명, 소리 및 움직임이 동시에 나타나면 사람이 어떤 신호가 어느 로봇에서 발생한 것인지 판단하기 어려울 수 있다. 따라서 플릿 환경(Fleet Environment)은 신호의 위치성(Localization), 일관성, 우선순위 및 조정(Coordination)을 고려해야 한다. 특히 교차로, 공유 작업장, 충전 구역 및 좁은 이동 통로에서는 과도한 시각적 또는 청각적 혼잡을 발생시키지 않으면서 개별 로봇의 의도를 구별할 수 있도록 해야 한다.

평가(Evaluation)는 단순히 표시 장치가 기술적으로 활성화되는지를 확인하는 것이 아니라 인간이 신호를 어떻게 해석하는지를 측정해야 한다. 사용자는 로봇이 다음에 무엇을 할 가능성이 있는지 판단할 수 있어야 하며, 신호를 이해하는 데 걸리는 시간과 환경 조건에 따른 해석 변화도 평가해야 한다. 익숙하지 않은 사용자, 주의 분산, 소음, 낮은 가시성, 여러 로봇, 계획 변경, 모호한 궤적 및 의사소통 장애를 시험하여 의도된 의미가 잘못 해석되는 조건을 식별해야 한다.

안전 평가(Safety Evaluation)는 전달된 의도와 실제 행동 사이의 충돌도 검토해야 한다. 중요한 시나리오에는 지연된 표시, 잘못된 방향 신호, 갑작스러운 계획 변경, 오래된 디스플레이 정보(Stale Display), 누락된 경고 및 전달된 의도와 모순되는 로봇 움직임이 포함된다. 의사소통이 불완전하더라도 시스템은 물리적으로 안전한 상태를 유지해야 한다. 이러한 원칙은 인간 인터페이스가 안전 아키텍처에서 독립적으로 강제되는 제약을 대신하는 수단이 되는 것을 방지한다.

런타임 보증(Runtime Assurance)은 전달된 의도와 계획 및 실행되는 로봇 행동을 지속적으로 비교할 수 있다. 로봇이 양보한다고 표시하면서 명령된 궤적(Commanded Trajectory)은 계속 사람에게 접근하고 있다면 이러한 불일치는 단순한 인터페이스 문제가 아니라 시스템 결함(System Fault)으로 탐지되어야 한다. 이러한 관계를 모니터링하면 의사소통이 로봇의 운용 상태와 단기 행동을 진실하게 외부에 표현하는 수단으로 유지되도록 할 수 있다.

로봇 의도 전달(Robot Intent Communication)은 궁극적으로 자율 시스템과 인간 사이에 공유되는 상호작용 언어(Shared Interaction Language)를 형성한다. 인간 인식(Human Awareness)은 로봇이 사람이 무엇을 인지하고 어떻게 행동할 가능성이 있는지를 추정하도록 하며, 의도 전달은 사람이 로봇의 행동을 미리 예상할 수 있도록 한다. 움직임 단서, 시각 표시, 소리, 디스플레이 및 공간적 신호는 미래 행동을 더욱 이해 가능하게 만들지만 물리적 안전 메커니즘은 항상 최종적인 권한을 유지해야 한다. 의도 인식(Intent Recognition), 근접 관리(Proximity Management), 속도 및 분리 모니터링과 통합된 의도 전달은 더욱 안전하고 명확하며 예측 가능한 인간-로봇 공존(Human--Robot Coexistence)을 가능하게 한다.

## 05.07. Visual Auditory and Haptic Warnings

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

시각, 청각 및 햅틱 경고(Visual, Auditory, and Haptic Warnings)는 물리 AI 시스템(Physical AI System)과 사람 사이에서 안전 관련 정보(Safety-Relevant Information)를 전달하기 위한 상호보완적인 채널을 제공한다. 그 목적은 단순히 사건이 발생했음을 알리는 것이 아니라 사람의 주의를 유도하고, 긴급성을 전달하며, 위험의 원인이나 특성을 나타내고, 적절한 인간 대응(Human Response)을 지원하는 것이다. 효과적인 경고 설계는 실제 운용 조건에서도 이해 가능한 신호를 통해 로봇 상태, 환경 위험, 인간 인식(Human Awareness), 필요한 행동을 연결한다.

시각 경고(Visual Warnings)는 조명, 색상, 아이콘, 디스플레이, 투영 패턴(Projected Patterns), 발광 표면 또는 기타 관찰 가능한 표시를 통해 안전 정보를 전달한다. 시각 경고는 환경에 추가적인 소음을 발생시키지 않으면서 지속적인 상태 정보를 제공해야 하는 경우 특히 유용하다. 주의, 제한된 움직임, 보호 정지(Protective Stopping), 성능이 저하된 자율성(Degraded Autonomy), 접근하는 로봇 등을 표시할 수 있지만 그 의미는 단순하고 일관되며 일반적인 운용 정보와 명확하게 구별되어야 한다.

가시성(Visibility)은 단순히 표시기의 밝기만으로 결정되지 않는다. 인간의 방향, 관찰 거리, 조명, 눈부심, 가림(Occlusion), 로봇 형상, 보호 장비 및 경쟁하는 시각 정보가 신호의 실제 인지 여부를 결정할 수 있다. 따라서 표시기는 예상되는 인간의 관찰 위치와 상호작용 영역을 고려하여 배치해야 한다. 이동 로봇(Mobile Robot)은 플랫폼이 방향을 변경하는 동안 사람이 전방, 측면 또는 후방에서 접근할 수 있으므로 여러 방향에서의 가시성이 필요할 수 있다.

색상(Color)은 시각적 상태를 빠르게 구별하는 데 활용할 수 있지만 중요한 의미를 색상 하나에만 의존해서는 안 된다. 조명 조건, 색각 차이(Color-Vision Differences), 디스플레이 특성 및 지역적 관례에 따라 해석이 달라질 수 있다. 색상을 형태, 위치, 아이콘, 텍스트 또는 시간 패턴(Temporal Patterns)과 결합하면 중복성(Redundancy)을 확보할 수 있다. 목적은 하나의 시각적 특성을 인식하기 어려운 상황에서도 중요한 경고 상태를 구별하면서 지나치게 복잡한 조합으로 인지 부하(Cognitive Workload)를 증가시키지 않는 것이다.

점멸 또는 애니메이션 시각 신호(Animated Visual Signals)는 정적인 표시보다 효과적으로 주의를 끌 수 있지만 과도하게 사용하면 그 가치가 감소할 수 있다. 많은 상태에서 빠른 점멸을 사용하면 사용자가 긴급성을 구별하기 어렵거나 신호에 둔감해질 수 있다. 따라서 시간 패턴은 위험의 심각성이나 필요한 대응의 차이를 의미 있게 표현해야 한다. 높은 현저성(High Salience)을 가진 패턴은 일상적인 로봇 활동보다 즉각적인 주의가 필요한 조건에 제한적으로 사용하는 것이 효과적이다.

청각 경고(Auditory Warnings)는 사람이 로봇을 바라보고 있지 않거나 신속하게 주의를 유도해야 할 때 유용하다. 음향 신호, 비프음, 경보, 음성 메시지 및 방향성 오디오(Directional Audio)는 접근, 후진, 비정상 상태, 요청 또는 긴급 위험을 전달할 수 있다. 소리는 직접적인 시야(Line of Sight) 밖의 사람에게도 도달할 수 있지만 주변 소음, 거리, 청력 보호 장비, 음향 반사, 경쟁하는 기계 소음 및 다른 시스템의 동시 경고에 따라 효과가 달라질 수 있다.

청각 경고 설계(Auditory Warning Design)는 불필요한 경보를 발생시키지 않으면서 긴급성을 인식할 수 있도록 해야 한다. 주파수, 리듬, 반복, 지속 시간 및 음량을 이용하여 정보성 신호와 점차 심각해지는 경고를 구별할 수 있다. 그러나 모든 경고의 음량을 높이는 것만으로 더 좋은 안전 인터페이스(Safety Interface)가 만들어지는 것은 아니다. 과도한 소리는 스트레스와 의사소통 방해 및 경보 피로(Alarm Fatigue)를 발생시키며, 결국 지나치게 자주 발생하거나 의미 있는 결과와 연결되지 않는 신호를 사람이 무시하도록 만들 수 있다.

음성 경고(Spoken Warnings)는 단순한 음향 신호보다 더 상세한 의미 정보를 전달할 수 있다. 로봇은 후진 중임을 알리거나, 통로 확보를 요청하거나, 진행할 수 없는 상태 또는 제한 운전에 진입했음을 전달할 수 있다. 음성은 감독된 환경에서 유용하지만 언어, 억양, 청취 조건, 메시지 길이 및 처리 시간을 고려해야 한다. 특히 다국어 또는 소음이 많은 환경에서는 안전 필수 의미(Safety-Critical Meaning)가 복잡한 음성 문장을 이해하는 것에만 의존해서는 안 된다.

방향성 청각 단서(Directional Auditory Cues)는 어떤 로봇이나 영역에 주의를 기울여야 하는지를 사람이 식별하도록 도울 수 있다. 이는 여러 자율 기계가 동시에 운용되는 플릿 환경(Fleet Environment)에서 더욱 중요하다. 주의를 끌기는 하지만 경고의 발생 위치를 알려주지 않는 신호는 혼란을 일으키거나 사람이 잘못된 기계 방향으로 대응하게 만들 수 있다. 따라서 가능한 경우 공간화 또는 위치화된 신호(Localized Signaling)를 통해 경고와 관련된 물리적 위험을 신속하게 연결할 수 있도록 해야 한다.

햅틱 경고(Haptic Warnings)는 촉각을 통해 정보를 전달하며 시각 및 청각적 주의가 다른 곳에 사용되고 있을 때 특히 유용하다. 웨어러블 장치(Wearable Device), 제어기, 좌석, 손잡이, 조이스틱 또는 운영자 인터페이스의 진동을 이용하여 근접성, 위험 방향, 제어 한계 또는 개입 필요성을 전달할 수 있다. 햅틱 의사소통(Haptic Communication)은 소음이 많은 환경에서도 효과적일 수 있으며 주변 작업 공간에 시각적 또는 음향적 혼잡을 증가시키지 않고 특정 운영자에게 개별 정보를 제공할 수 있다.

햅틱 피드백(Haptic Feedback)의 위치와 패턴은 그 해석에 영향을 미친다. 서로 다른 진동 위치, 강도, 지속 시간 또는 펄스 패턴(Pulse Patterns)을 이용하여 방향, 긴급성 또는 이벤트 유형을 표현할 수 있다. 예를 들어 방향성 진동은 위험이 접근하는 방향을 나타낼 수 있다. 그러나 복잡한 진동 패턴은 육체 작업, 차량 움직임 또는 다른 기계적 진동이 존재하는 상황에서 구별하기 어려울 수 있으므로 햅틱 신호 체계(Haptic Vocabulary)는 제한적이고 학습하기 쉬워야 한다.

다중 양식 경고(Multi-Modal Warnings)는 시각, 청각 및 햅틱 채널을 결합하여 중요한 정보가 인지될 가능성을 높인다. 중요한 근접 이벤트(Proximity Event)는 시각 표시를 활성화하면서 청각 신호를 발생시키고 운영자에게 햅틱 피드백을 제공할 수 있다. 하나의 양식 성능이 저하된 경우 중복성이 유용하지만 각 신호는 일관된 의미를 전달해야 한다. 서로 다른 양식에서 상충되는 긴급성 수준이나 관련 없는 메시지를 전달하면 안전을 향상시키기보다 혼란을 증가시킬 수 있다.

적절한 양식의 조합은 위험과 상황(Context)에 따라 달라진다. 일상적인 상황 인식에는 현저성이 낮은 시각 표시만 필요할 수 있지만 근접 위험이 증가하면 더욱 눈에 띄는 시각 또는 청각 경고가 필요할 수 있다. 긴급한 개입 요청에는 여러 양식을 동시에 사용할 수 있다. 이러한 단계적 경고 전략(Graduated Warning Strategy)은 의사소통 강도를 위험 수준과 일치시켜 사용자가 정보성 상태, 주의가 필요한 상태 및 실제로 시간에 민감한 위험을 구별하도록 한다.

가능한 경우 경고는 구체적으로 기대되는 인간 대응(Expected Human Response)과 연결되어야 한다. 사람이 상황을 계속 주시해야 하는지, 멀어져야 하는지, 특정 영역에 진입하지 않아야 하는지, 요청을 확인해야 하는지 또는 제어권을 인수해야 하는지를 이해할 수 있을 때 신호는 더욱 유용하다. 따라서 경고 설계는 탐지 가능성뿐 아니라 행동 가능성(Actionability)도 고려해야 한다. 주의를 끌기는 하지만 무엇을 해야 하는지 판단할 수 없는 신호는 반응 시간이 중요한 상황에서 망설임을 발생시킬 수 있다.

인간 인식(Human Awareness)은 경고 양식 선택에 영향을 주어야 한다. 로봇이 주변 사람이 이미 자신의 움직임을 관찰하고 안전한 분리 거리를 유지하고 있다고 판단한다면 지나치게 강한 경보가 필요하지 않을 수 있다. 반대로 사람이 주의가 분산되어 있거나, 다른 방향을 보고 있거나, 시각 신호를 인지하기 어려울 가능성이 있다면 청각 경고 또는 더욱 강한 다중 양식 경고가 적절할 수 있다. 이러한 적응은 의사소통 효율을 향상시킬 수 있지만 물리적 안전은 경고가 인지되었다는 가정에 의존해서는 안 된다.

여러 조건이 동시에 발생하는 경우 경고 우선순위(Warning Priority)가 중요해진다. 로봇은 동시에 배터리 부족, 위치추정 성능 저하(Localization Degradation), 경로 차단, 인간 근접, 안전 결함(Safety Fault)을 경험할 수 있다. 모든 경고를 동일한 중요도로 표시하면 사용자가 정보 과부하에 빠질 수 있다. 경고 관리 아키텍처(Warning-Management Architecture)는 긴급성, 심각성, 필요한 대응 시간 및 현재 인간 역할과의 관련성에 따라 정보를 우선순위화하여 안전 필수 상태가 가장 높은 우선순위를 유지하도록 해야 한다.

경보 피로(Alarm Fatigue)는 중요한 인간공학적 문제(Human-Factors Concern)이다. 빈번한 거짓 경보(False Alarms), 지나치게 보수적인 임계값, 반복되는 낮은 가치의 알림 또는 실제 행동을 요구하지 않는 경고는 사람을 둔감하게 만들 수 있다. 사용자가 경고가 실제 의미 있는 위험과 거의 연결되지 않는다고 학습하면 반응 시간이 증가할 수 있다. 따라서 경고 시스템은 불필요한 활성화를 최소화하면서 지속적인 인간의 주의에 의존하지 않고 독립적인 물리적 안전 메커니즘(Independent Physical Safety Mechanisms)을 통해 보수적인 보호 수준을 유지해야 한다.

경고는 일반적인 로봇 의도 전달(Robot Intent Communication)과 명확하게 구별되면서도 전체적으로 일관성을 유지해야 한다. 예정된 회전을 나타내는 방향 표시등이 즉각적인 회피를 요구하는 위험 표시와 쉽게 혼동되어서는 안 된다. 의도 신호(Intent Signals)는 로봇이 무엇을 하려고 하는지를 설명하는 반면, 경고는 인간의 주의나 대응이 더욱 필요한 조건을 강조한다. 두 기능 사이의 명확한 의미적 분리(Semantic Separation)는 일상적인 의사소통이 안전 경고의 긴급성을 약화시키는 것을 방지한다.

안전 영역(Safety Zones)과 근접 관리(Proximity Management)는 경고를 단계적으로 강화하기 위한 구조화된 트리거(Structured Triggers)를 제공할 수 있다. 외곽 모니터링 영역(Outer Monitoring Region)에 진입하면 약한 정보성 신호를 제공하고, 주의 영역(Caution Region)으로 이동하면 더 강한 시각 또는 청각 신호를 활성화할 수 있다. 더 가까이 접근하면 감속과 함께 다중 양식 경고를 발생시키고, 보호 영역(Protective Region)에 진입하면 정지를 실행할 수 있다. 이를 통해 경고 강도가 임의적인 인터페이스 상태가 아니라 측정 가능한 물리적 위험 변화와 연결된다.

속도 및 분리 모니터링(Speed and Separation Monitoring)은 경고 시간이 충분한지도 판단해야 한다. 너무 늦게 발생한 경고는 사람이 정확하게 인지하더라도 대응할 시간이 충분하지 않을 수 있다. 종단 간 타이밍(End-to-End Timing)은 센싱, 위험 추정, 경고 생성, 신호 전달, 인간의 인지, 의사결정 시간 및 물리적 대응을 포함해야 한다. 따라서 빠르게 움직이는 로봇이나 빠르게 접근하는 사람의 경우 인간이 더 빨리 반응하기를 기대하기보다 더 이른 경고 임계값 또는 더욱 강력한 자율 보호 행동(Autonomous Protective Actions)이 필요하다.

의사소통 하드웨어가 고장난 경우에도 경고 시스템은 안전하게 성능이 저하되어야 한다. 고장난 조명, 가려진 디스플레이, 스피커 고장, 연결이 끊어진 웨어러블 장치, 손상된 진동 모터 또는 네트워크 지연은 경고 가용성(Warning Availability)을 감소시킬 수 있다. 런타임 모니터링(Runtime Monitoring)은 중요한 채널의 고장을 탐지하고 다른 양식이 충분한지를 판단해야 한다. 위험 수준에 따라 로봇은 안전 여유를 확대하고, 속도를 낮추고, 운전을 제한하고, 유지보수를 요청하거나, 더욱 안전한 운용 상태로 전환할 수 있다.

접근성(Accessibility)은 배치 이후에 추가하는 기능이 아니라 설계 초기부터 고려해야 한다. 사람은 시각 능력이 저하되어 있거나, 청각적 차이가 있거나, 이동 능력이 제한되어 있거나, 언어 장벽을 가지고 있거나, 보호 장비와 환경 조건 때문에 일시적인 제약을 받을 수 있다. 다중 양식 신호(Multi-Modal Signaling)는 하나 이상의 감각 경로를 통해 정보를 전달할 수 있으므로 포용적인 안전(Inclusive Safety)을 위한 중요한 기반을 제공한다. 중요한 경고는 하나의 인간 감각 능력에 불필요하게 의존하지 않아야 한다.

플릿 환경(Fleet Environments)에서는 조정된 경고 행동(Coordinated Warning Behavior)이 필요하다. 여러 로봇이 독립적으로 유사한 경보를 발생시키면 시각적 및 음향적 혼잡으로 인해 개별 경고를 해석하기 어려워질 수 있다. 신호는 어떤 로봇이 관련되어 있는지, 위험이 어디에 존재하는지, 즉각적인 행동이 필요한지를 사람이 판단하도록 해야 한다. 플릿 수준 조정(Fleet-Level Coordination)은 중복 경고를 감소시키면서 즉각적인 물리적 위험이 탐지된 경우 개별 로봇이 긴급 경고를 발생시킬 수 있는 로컬 권한(Local Authority)을 유지해야 한다.

평가(Evaluation)는 단순히 경고 하드웨어가 활성화되는지를 검증하는 것이 아니라 사람이 경고를 인지하고, 이해하고, 적절하게 대응하는지를 시험해야 한다. 시나리오에는 밝고 어두운 환경, 높은 배경 소음, 청력 보호 장비, 시각적 가림, 주의 분산, 여러 로봇, 익숙하지 않은 사용자 및 동시 경고가 포함되어야 한다. 반응 시간(Response Time), 해석 정확도, 누락된 경고(Missed Warnings), 잘못된 반응(False Reactions), 주관적 작업 부하(Subjective Workload)는 인터페이스가 안전 행동을 지원하는지를 평가하는 유용한 지표가 된다.

실패 중심 시험(Failure-Oriented Testing)은 지연된 경고, 잘못된 양식 선택, 서로 모순되는 신호, 사용할 수 없는 채널, 과도한 경보 및 실제 로봇 행동과 일치하지 않는 경고를 포함해야 한다. 의사소통이 잘못 이해되거나 완전히 인지되지 않더라도 물리 AI 시스템은 안전한 상태를 유지해야 한다. 독립적인 안전 영역, 움직임 제약(Motion Constraints), 보호 정지 및 비상 메커니즘(Emergency Mechanisms)은 경고가 인간 행동을 지원할 수는 있지만 이를 보장할 수 없기 때문에 항상 최종적인 권한을 유지해야 한다.

시각, 청각 및 햅틱 경고(Visual, Auditory, and Haptic Warnings)는 궁극적으로 로봇 행동 주변에 계층화된 주의 및 의사소통 시스템(Layered Attention and Communication System)을 형성한다. 시각 채널은 지속적이고 공간적인 정보를 제공하고, 청각 채널은 직접적인 시야 밖에서도 주의를 유도하며, 햅틱 채널은 연결된 사용자에게 즉각적인 촉각 단서를 전달한다. 인간 인식, 로봇 의도 전달, 근접 관리 및 독립적 보호(Independent Protection)와 통합된 이러한 양식은 물리 AI 시스템이 증가하는 위험을 명확하게 전달하면서 예측 가능하고 안전한 인간-로봇 상호작용(Human--Robot Interaction)을 유지하도록 한다.

## 05.08. Natural Language Safety Interaction

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

자연어 안전 상호작용(Natural Language Safety Interaction)은 사람이 일상적인 음성 또는 문자 언어를 통해 안전과 관련된 의도, 우려, 명령 및 질문을 물리 AI 시스템(Physical AI System)에 전달할 수 있도록 한다. 모든 사용자가 전문적인 제어 인터페이스를 이해하도록 요구하는 대신, 로봇은 정지, 감속, 대기, 거리 유지, 특정 영역 회피 또는 자신의 행동 설명과 같은 요청을 해석할 수 있다. 이를 통해 인간의 판단(Human Judgment)과 로봇 안전 행동(Robot Safety Behavior) 사이에 직관적인 의사소통 계층이 형성된다.

자연어(Natural Language)는 사람이 로봇의 센서나 계획 시스템에 아직 표현되지 않은 상황적 위험(Contextual Risks)을 인식하는 경우가 많기 때문에 유용하다. 작업자는 바닥이 미끄럽거나, 통로를 비워 두어야 하거나, 기계가 유지보수 중이거나, 다른 사람이 곧 작업 공간에 진입할 것이라는 사실을 알고 있을 수 있다. 언어는 복잡한 프로그래밍이나 인터페이스 조작 없이 이러한 상황적 지식을 로봇의 상황 이해(Situational Understanding)에 직접 추가할 수 있는 수단을 제공한다.

안전 관련 언어(Safety-Related Language)는 일반적인 작업 지시(Task Instructions)와 구별되어야 한다. "이 상자를 3번 스테이션으로 가져가라"와 같은 명령은 주로 작업을 지정하지만, "정지하라", "이 영역에 들어가지 마라", "나에게서 떨어져 있어라"와 같은 표현은 즉각적이거나 지속적인 안전 제약(Safety Constraint)을 나타낸다. 상호작용 아키텍처는 이러한 차이를 인식하여 안전 관련 언어에 적절한 우선순위를 부여하고, 생산성 목표나 이전 작업 명령에 의해 조용히 무시되지 않도록 해야 한다.

음성 인식(Speech Recognition)은 음성 기반 안전 상호작용의 첫 번째 단계이지만 단순한 음성 전사(Transcription)만으로는 충분하지 않다. 시스템은 발화가 로봇을 대상으로 하는지를 판단하고, 관련 대상과 행동을 식별하며, 의도된 제약을 추론하고, 이를 현재의 물리적 상황과 연결해야 한다. 주변 대화, 기계 소음, 여러 명의 화자, 불완전한 문장, 억양 및 중첩된 음성은 불확실성을 발생시킬 수 있으며, 이러한 불확실성을 숨기지 않고 명시적으로 표현해야 한다.

언어 이해(Language Understanding)는 인간의 표현을 실제 운용 가능한 의미(Operational Meaning)로 변환해야 한다. "저 문에서 떨어져 있어라"라는 표현은 해당 문을 식별하고 적절한 공간적 제약(Spatial Constraint)을 결정해야 하며, "사람 근처에서는 천천히 움직여라"는 표현은 인간 탐지와 근접성에 연결되는 행동 규칙을 의미한다. 따라서 자연어가 물리적 행동에 안전하게 영향을 주기 위해서는 로봇의 월드 모델(World Model), 의미 지도(Semantic Map), 인식된 물체, 추적된 인간, 작업 상태 및 사용 가능한 행동에 근거하여 의미가 연결되어야 한다.

동적 환경에서는 참조 해석(Reference Resolution)이 특히 중요하다. "여기", "저기", "저 기계", "내 뒤", "왼쪽에 있는 사람"과 같은 표현은 공간적 및 대화적 맥락(Conversational Context)에 따라 의미가 달라진다. 로봇은 참조 대상이나 영역이 모호한 상태에서 중요한 행동을 실행하지 않아야 한다. 대신 명확화를 요청하거나, 자신이 이해한 내용을 표시하거나, 충분한 근거가 확보될 때까지 일시적으로 보수적인 행동(Conservative Behavior)을 선택할 수 있다.

안전 명령(Safety Commands)은 명확한 우선순위 구조(Priority Structure)를 따라야 한다. 즉각적인 정지 요청, 비상 지시, 보호 제약(Protective Constraints), 임박한 위험에 대한 경고는 일반적인 대화 요청보다 빠르게 처리되어야 할 수 있다. 시스템은 신뢰도가 높은 긴급 안전 명령을 인식한 시점부터 해당 보호 대응(Protective Response)을 시작하기까지 불필요한 추론 단계를 최소화해야 한다. 신속한 물리적 개입이 필요한 경우 복잡한 언어 해석이 불필요한 지연의 원인이 되어서는 안 된다.

동시에 모든 안전 관련 표현이 자동으로 가장 제한적인 대응을 발생시켜야 하는 것은 아니다. "적재 구역 근처에서는 조심해라"라는 표현은 "적재 구역에 들어가지 마라"보다 명확성이 낮다. 시스템은 명령, 경고, 선호, 관찰, 질문 및 불확실한 표현을 구별해야 한다. 적절한 대응은 정보를 확인하고 모니터링을 강화하는 것부터 계획 수정, 감속, 임시 출입 금지 영역(Temporary Exclusion Zone) 생성 또는 완전 정지까지 다양할 수 있다.

명령이 중요한 결과를 발생시키지만 즉각적으로 긴급하지 않은 경우 확인(Confirmation)을 통해 오해를 줄일 수 있다. 로봇은 지정된 통로를 회피하거나 작업자와 더 큰 거리를 유지하는 것과 같이 자신이 해석한 제약을 다시 표현할 수 있다. 이를 통해 실행 전에 사람이 잘못된 해석을 수정할 기회를 제공한다. 그러나 명백한 비상 명령의 경우 확인 절차가 대응을 지연해서는 안 된다. 따라서 상호작용 설계는 검증(Verification)과 물리적 상황에서 요구되는 대응 시간 사이의 균형을 유지해야 한다.

언어에 모호성, 모순 또는 누락된 정보가 존재할 때는 명확화(Clarification)가 특히 중요하다. 사람이 명확하게 식별할 수 있는 영역을 지정하지 않고 "저쪽으로 가지 마라"라고 말한다면 로봇이 임의로 경계를 만들어서는 안 된다. 어느 영역을 의미하는지 질문하거나 현재의 해석을 제시할 수 있다. 명확화 과정에서도 계속 움직이는 것이 위험을 발생시킬 가능성이 있다면 보수적인 움직임이 적절할 수 있다. 이를 통해 불확실성을 근거 없는 자율적 가정이 아니라 명시적인 상호작용으로 전환한다.

자연어는 사람이 로봇의 안전 상태(Safety State)를 질문할 수 있도록 할 수도 있다. 로봇이 주변 사람을 탐지했는지, 왜 정지했는지, 어떤 경로를 사용할 예정인지 또는 특정 영역에 진입해도 안전한지를 질문하면 상황 이해를 향상시킬 수 있다. 응답은 간결하고 현재 이용 가능한 정보에 근거해야 한다. 로봇은 자신이 확실하게 알고 있는 것, 추정하고 있는 것, 불확실한 것을 구별해야 하며 추론된 안전 상태를 보장된 사실처럼 표현해서는 안 된다.

설명(Explanations)은 로봇 행동의 관찰 가능한 원인을 전달할 때 신뢰를 향상시킬 수 있다. 로봇은 사람이 모니터링 영역(Monitored Region)에 진입했기 때문에 감속했거나, 필요한 분리 거리(Required Separation)를 유지할 수 없어 정지했거나, 제한 영역(Restricted Zone)이 설정되어 경로를 변경했다고 설명할 수 있다. 이러한 설명은 자연어 상호작용을 안전 영역(Safety Zones), 근접 관리(Proximity Management), 속도 및 분리 모니터링(Speed and Separation Monitoring), 의도 전달(Intent Communication)과 연결하여 불필요한 내부 복잡성을 노출하지 않으면서 자율 행동을 이해하기 쉽게 만든다.

자연어는 전용 경고 채널(Dedicated Warning Channels)을 대체하는 것이 아니라 보완해야 한다. 음성 메시지는 로봇이 정지하는 이유를 설명할 수 있지만 즉각적인 시각, 청각 또는 햅틱 경고(Visual, Auditory, or Haptic Warnings)가 긴급성을 더욱 신뢰성 있게 전달할 수 있다. 마찬가지로 위험한 움직임을 방지하기 위해 사람이 문법적으로 완전한 문장을 말하도록 요구해서는 안 된다. 응용 분야와 위험 수준에서 요구되는 경우 전용 비상 제어, 보호 정지(Protective Stop), 안전 등급 센싱(Safety-Rated Sensing), 물리적 제약이 계속 필요하다.

다중 양식 상호작용(Multi-Modal Interaction)은 언어를 제스처, 시선, 가리키기, 터치 인터페이스 또는 공간적 맥락과 결합하여 그라운딩(Grounding)을 향상시킬 수 있다. 작업자가 출입구를 가리키면서 "저기로 들어가지 마라"라고 말하면 음성만 사용하는 것보다 강한 근거를 제공한다. 시스템은 언어적 정보와 지각 정보를 결합하여 의도된 영역을 식별할 수 있다. 서로 다른 양식의 정보가 충돌한다면 충분한 근거 없이 하나의 해석을 확정하기보다 불확실성을 높이고 명확화를 우선해야 한다.

여러 사람이 동일한 로봇과 상호작용하는 경우 화자 인식(Speaker Awareness)이 중요할 수 있다. 시스템은 누가 명령을 내렸는지, 해당 사람이 실제로 로봇을 대상으로 말하고 있는지, 동시에 발생한 요청을 어떻게 처리할지를 판단해야 할 수 있다. 그러나 즉각적인 안전 보호가 특정 사람의 신원을 식별하는 데 불필요하게 의존해서는 안 된다. 임박한 위험에 대한 신뢰할 수 있는 경고라면 화자의 신원이나 권한을 확실하게 판단할 수 없는 경우에도 보호 행동이 필요할 수 있다.

지속적이거나 운용상 중요한 명령에서는 권한 부여(Authorization)가 더욱 중요하다. 권한을 가진 운영자(Authorized Operator)는 운용 모드를 변경하거나 장기간의 제한을 설정할 수 있는 반면, 주변 사람은 즉각적인 정지나 거리 확보를 요청할 수 있는 권한만 필요할 수 있다. 따라서 안전 상호작용은 보호를 위해 누구에게나 허용되어야 하는 행동과 적절한 권한이 필요한 행동을 구별하여 편리한 자연어 인터페이스가 통제되지 않은 시스템 설정 채널이 되는 것을 방지해야 한다.

상충하는 지시(Conflicting Instructions)는 명시적으로 해결되어야 한다. 한 사람은 로봇에게 계속 진행하라고 지시하고 다른 사람은 정지를 요청할 수 있으며, 작업 명령이 기존 안전 제한과 충돌할 수도 있다. 안전 제약은 일반적인 작업 목표보다 우선해야 하며 해결되지 않은 인간 간의 의견 충돌이 공격적인 로봇 움직임으로 이어져서는 안 된다. 로봇은 어떤 지시를 무시할 것인지 임의로 추론하기보다 정지하거나, 대기하거나, 명확화를 요청하거나, 권한이 있는 운영자에게 판단을 요청할 수 있다.

대화 메모리(Conversational Memory)는 여러 단계로 이어지는 안전 상호작용을 지원할 수 있다. 사람이 먼저 "유지보수 구역"을 지정한 다음 "내가 말할 때까지 그곳에 들어가지 마라"라고 말할 수 있다. 시스템은 이후의 참조를 앞에서 설정된 영역 및 제약과 연결할 수 있을 만큼 충분한 상호작용 맥락을 유지해야 한다. 이러한 메모리는 제한되고 상태 인식(State-Aware) 방식으로 관리되어야 하며 환경, 작업, 사용자 의도 또는 권한 조건이 변경된 이후에도 오래된 지시가 무기한 지속되지 않도록 해야 한다.

언어 모델(Language Models)은 다양한 표현을 유연하게 해석할 수 있지만 그 출력이 안전 제어(Safety Control)를 직접 우회해서는 안 된다. 의미 모델(Semantic Model)은 특정 발화가 감속 또는 특정 영역 회피를 의미한다고 제안할 수 있지만, 결정론적 정책(Deterministic Policy)이나 안전 감독기(Safety Supervisor)는 해당 해석이 허용된 행동으로 연결되는지를 검증해야 한다. 이러한 책임 분리는 유연한 자연어 이해를 제공하면서 실제로 실행 가능한 물리적 행동과 안전 제약을 명시적으로 통제할 수 있도록 한다.

언어 해석은 언어적으로 그럴듯해 보이면서도 잘못될 수 있으므로 불확실성 모니터링(Uncertainty Monitoring)이 필수적이다. 낮은 음성 인식 신뢰도, 모호한 참조, 익숙하지 않은 용어, 상충하는 맥락 또는 여러 가능한 의도는 실행 신뢰도를 낮추어야 한다. 시스템은 불확실한 언어를 잠재적으로 위험한 물리적 움직임으로 직접 변환하기보다 명확화를 요청하거나, 사전에 정의된 보수적 행동을 선택하거나, 다른 인터페이스로 제어를 전환할 수 있다.

자연어 인터페이스(Natural Language Interface)는 기본적인 보호 기능을 무력화하려는 안전하지 않은 요청에도 대응할 수 있어야 한다. "사람을 무시하고 계속 움직여라"와 같은 요청은 문장이 명확하다는 이유만으로 필요한 분리 제약을 비활성화해서는 안 된다. 마찬가지로 대화적 설득, 반복되는 명령 또는 상위 수준의 작업 목표가 보호 정지나 독립적인 안전 메커니즘(Independent Safety Mechanisms)을 우회해서는 안 된다. 자연어 상호작용은 통제된 권한 없이 기본적인 물리적 한계를 재정의하는 것이 아니라 안전 영역(Safety Envelope) 내부에서 동작해야 한다.

음성 기반 안전 상호작용에서는 지각, 음성 전사, 의미 해석, 그라운딩, 정책 검증 및 제어 실행에 모두 시간이 필요하므로 지연시간(Latency)이 중요하다. 긴급 명령 경로(Urgent Command Pathways)는 제한된 처리 시간과 단순한 폴백 행동(Fallback Behavior)을 갖도록 설계해야 한다. 고급 언어 이해가 지연되거나 사용할 수 없는 경우 인식 가능한 비상 표현이나 전용 제어 장치는 전체 대화 추론을 기다리지 않고 더 짧은 보호 경로를 통해 대응할 수 있어야 한다.

평가(Evaluation)는 신중하게 작성된 명령만이 아니라 실제 환경에서 사용되는 자연스러운 언어를 포함해야 한다. 시험에는 다양한 억양, 배경 소음, 불완전한 발화, 동의어, 간접적인 경고, 모호한 참조, 상충하는 요청, 여러 화자, 빠르게 변화하는 상황 및 비정형적인 표현이 포함되어야 한다. 목표는 단순히 언어 정확도를 측정하는 것이 아니라 해석 오류, 불확실성 및 의사소통 실패가 발생했을 때 로봇이 적절하게 보수적인 행동을 수행하는지를 판단하는 것이다.

실패 시험(Failure Testing)은 누락된 명령, 잘못된 음성 전사, 존재하지 않는 참조의 생성(Hallucinated References), 오래된 대화 맥락(Stale Conversational Context), 지연된 응답, 권한 없는 지시 및 언어 인터페이스와 물리적 안전 시스템 사이의 충돌을 검토해야 한다. 자연어 인터페이스가 완전히 실패하더라도 로봇은 검증된 안전 한계(Validated Safety Limits) 안에 머물러야 한다. 이를 통해 자연어를 강력한 상호작용 수단으로 활용하면서도 인간-로봇 보호의 단일 실패 지점(Single Point of Failure)이 되지 않도록 한다.

자연어 안전 상호작용(Natural Language Safety Interaction)은 궁극적으로 인간의 이해(Human Understanding)와 기계의 안전 메커니즘(Machine Safety Mechanisms) 사이에 의미적 연결(Semantic Bridge)을 형성한다. 사람은 익숙한 언어를 이용하여 위험, 제약, 질문 및 의도를 표현하고, 로봇은 이러한 표현을 자신의 월드 모델에 그라운딩하여 검증된 의미를 통제된 행동으로 변환한다. 인간 인식(Human Awareness), 경고(Warnings), 근접 관리(Proximity Management), 독립적 보호(Independent Protection)와 통합된 이러한 역량은 물리적 안전의 기반을 약화시키지 않으면서 물리 AI 시스템이 사람과 더욱 자연스럽게 상호작용할 수 있도록 한다.

## 05.09. Human Command Confirmation and Override

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

인간 명령 확인(Human Command Confirmation)과 오버라이드(Override)는 인간의 권한(Human Authority)과 자율 로봇 행동(Autonomous Robot Behavior) 사이에 통제된 인터페이스를 제공한다. 물리 AI 시스템(Physical AI System)은 인간의 지시를 언제 즉시 실행할 수 있는지, 언제 그 해석을 확인해야 하는지, 그리고 언제 자율 행동이 권한을 가진 인간의 개입에 제어권을 넘겨야 하는지를 판단해야 한다. 목적은 모호하거나 우발적이거나 권한이 없거나 안전하지 않은 명령이 기본적인 안전 제약을 우회하지 못하도록 하면서 의미 있는 인간 제어(Meaningful Human Control)를 유지하는 것이다.

확인(Confirmation)은 명령이 중대한 물리적 결과를 초래하지만 즉각적인 비상 대응을 요구하지 않는 경우 특히 중요하다. 경로 변경, 제한 영역 진입, 무거운 물체 조작 또는 운용 모드 변경 전에 로봇은 해석한 지시를 다시 표현하고 사용자의 확인을 요청할 수 있다. 이러한 폐루프 상호작용(Closed-Loop Interaction)은 자율 시스템의 해석이 물리적 행동으로 전환되기 전에 사용자가 잘못된 이해를 발견할 수 있도록 한다.

확인은 단순히 원래의 명령을 반복하는 것이 아니라 로봇이 해석한 의미(Interpreted Meaning)를 전달해야 한다. 사람이 "저 팔레트를 저쪽으로 옮겨라"라고 말하면 시스템은 승인을 요청하기 전에 대상 팔레트, 목적지, 움직임 및 관련 제약을 식별해야 한다. 유용한 확인 과정에서는 선택된 물체와 목적지를 명확하게 표현할 수 있다. 이를 통해 의미적 그라운딩(Semantic Grounding)을 검증하고 언어적으로는 합의되었지만 실제 물리적 해석은 잘못된 상황의 가능성을 줄인다.

모든 명령에 확인이 필요한 것은 아니다. 일상적인 지시마다 승인을 요구하면 작업 부하가 증가하고 운용이 지연되며 사용자가 로봇의 해석을 실제로 검토하지 않고 자동적으로 확인하게 만들 수 있다. 따라서 확인 정책(Confirmation Policy)은 명령의 중요도, 모호성, 가역성(Reversibility), 불확실성, 사람과의 근접성, 잠재적 결과 및 권한 수준을 고려해야 한다. 위험이 낮은 행동은 해석 신뢰도와 운용 조건이 검증된 한계 안에 있을 경우 직접 수행할 수 있다.

긴급한 보호 명령(Urgent Protective Commands)은 다른 처리 경로가 필요하다. 정지, 중단, 동결 또는 즉각적인 위험으로부터 벗어나라는 명확한 요청은 지연이 위험을 증가시킬 수 있는 경우 긴 확인 대화를 기다려서는 안 된다. 시스템은 먼저 보수적인 보호 대응(Protective Response)을 시작하고 이후 세부 사항을 명확하게 할 수 있다. 즉, 중대한 비긴급 행동은 실행 전에 확인할 수 있지만 신뢰할 수 있는 비상 개입은 신속한 위험 감소를 우선해야 한다는 비대칭적 원칙(Asymmetric Principle)이 적용된다.

명령 신뢰도(Command Confidence)는 확인 행동에 영향을 주어야 한다. 음성 인식 품질, 참조 해석(Reference Resolution), 환경적 맥락, 화자 식별 및 의미 해석은 모두 불확실성에 영향을 미친다. 여러 가지 가능한 의미가 남아 있는 경우 로봇은 가장 편리한 해석을 임의로 선택해서는 안 된다. 대신 구체적인 명확화 질문을 하거나, 가능한 선택지를 제시하거나, 일시적으로 현재 위치를 유지할 수 있다. 따라서 확인은 불확실한 기계 추론을 명시적인 공유 이해(Shared Understanding)로 변환하는 메커니즘으로 기능한다.

인간 오버라이드(Human Override)는 자율 행동이 부적절하거나 예상과 다르거나 안전하지 않은 경우 권한을 가진 사람이 개입할 수 있도록 한다. 오버라이드는 정지, 일시정지, 제어권 양도, 경로 변경, 작업 취소 또는 통제된 수동 모드(Controlled Manual Mode)로의 진입을 요청할 수 있다. 인터페이스는 자율 운전에서 요청된 상태로 예측 가능한 전환을 제공하여 운영자가 자신이 어떤 권한을 인수하고 있으며 어떤 자율 기능이 계속 활성화되어 있는지를 이해할 수 있도록 해야 한다.

오버라이드 메커니즘(Override Mechanisms)은 긴급성과 결과에 따라 계층화되어야 한다. 일반적인 운용 오버라이드는 감독 인터페이스(Supervisory Interface)를 통해 작업이나 궤적을 변경할 수 있으며, 안전 관련 오버라이드는 움직임을 즉시 제한할 수 있다. 필요한 경우 비상 정지(Emergency Stop)는 별도의 보호 메커니즘으로 유지된다. 모든 개입을 동일한 종류의 오버라이드로 취급하면 작업 감독, 자율성 해제(Autonomy Disengagement), 보호 정지(Protective Stopping), 비상 행동 사이의 중요한 차이가 불명확해질 수 있다.

권한(Authority)은 명시적으로 정의되어야 한다. 주변 사람에게는 즉각적인 정지 또는 분리 거리 확대를 요청할 수 있는 보편적인 권한이 필요할 수 있지만, 안전 구성, 운용 모드 또는 지속적인 제약을 변경하려면 권한을 가진 운영자(Authorized Operator)가 필요할 수 있다. 유지보수 담당자는 생산 감독자 또는 일반 사용자와 서로 다른 권한을 가질 수 있다. 역할 기반 권한(Role-Based Authority)은 즉각적인 보호에 대한 접근성을 유지하면서 안전 관련 시스템 행동을 제한 없이 변경하는 것을 방지한다.

권한 검증(Authorization)은 명백한 보호 개입을 방해해서는 안 된다. 사람이 임박한 위험에 노출된 경우 화자의 신원을 충분히 빠르게 인증할 수 없다는 이유로 로봇이 위험한 움직임을 계속해서는 안 된다. 보호 요청은 보수적으로 처리하면서 장기적인 시스템 운용에 영향을 미치는 구성 변경에는 더 엄격한 권한을 요구할 수 있다. 이를 통해 즉각적인 안전을 요청할 권리와 장기간 시스템 동작 방식을 변경할 권한을 구분할 수 있다.

서로 충돌하는 인간 명령(Conflicting Human Commands)은 결정론적인 방식으로 해결해야 한다. 한 사람은 계속 움직이라고 요청하고 다른 사람은 정지를 요청할 수 있으며, 운영자의 명령이 기존 안전 제한과 충돌할 수도 있다. 안전 관련 제약은 생산성 목표보다 우선해야 하며 해결되지 않은 충돌은 일반적으로 로봇을 보수적인 상태(Conservative State)로 이동시켜야 한다. 시스템은 작업 완료에 유리한 지시를 임의로 선택하기보다 일시정지하고, 분리 거리를 유지하고, 명확화를 요청하거나, 상위 권한으로 판단을 에스컬레이션(Escalation)할 수 있다.

인간 명령은 자율 시스템의 안전 판단(Autonomous Safety Decisions)과 충돌할 수도 있다. 운영자는 속도 및 분리 모니터링(Speed and Separation Monitoring)이 감속이나 정지를 요구하는 상황에서도 로봇에게 계속 움직이라고 요청할 수 있다. 인간의 권한이 독립적으로 강제되는 보호 한계(Protective Limits)를 자동으로 무효화해서는 안 된다. 명령 인터페이스는 허용된 안전 영역(Safety Envelope) 내부에서 목표를 수정할 수 있지만 감독 권한이 검증된 물리적 제약을 위반할 수 있는 무제한적인 허가로 변환되어서는 안 된다.

시스템은 오버라이드를 받아들일 수 없는 경우 그 이유를 전달해야 한다. 인간의 명령을 단순히 무시하면 자율 행동이 예측 불가능하거나 반응하지 않는 것처럼 보일 수 있다. 로봇은 요청이 활성화된 보호 영역(Protective Zone), 불충분한 분리 거리, 장비 결함 또는 권한 제한과 충돌한다고 알릴 수 있다. 명확한 거부 설명(Refusal Explanation)은 사용자가 시스템 고장과 의도적인 안전 강제(Safety Enforcement)를 구별하도록 하며 적절한 수정 행동을 지원한다.

오버라이드 전환(Override Transition)은 제어권 이전 과정에서 누가 움직임을 책임지는지에 대한 일시적인 모호성이 발생할 수 있으므로 신중하게 제어해야 한다. 자율 모드에서 수동 또는 감독 운전으로 전환할 때 로봇은 알려진 움직임 상태(Known Motion State)를 확립하고 현재 활성화된 제어 모드를 명확하게 표시해야 한다. 자율 플래너(Autonomous Planner)에 이미 대기 중인 명령은 취소하거나 억제하여 인간이 제어권을 인수한 직후 예상하지 못한 움직임이 발생하지 않도록 해야 한다.

자율 제어로 다시 복귀하는 과정 역시 동일한 수준의 규율이 필요하다. 오버라이드가 종료되었다는 이유만으로 로봇이 오래된 궤적(Outdated Trajectory)을 다시 실행해서는 안 된다. 자율 움직임을 재개하기 전에 인간 위치, 안전 영역, 환경 변화, 작업 상태, 위치추정 품질(Localization Quality), 기존 제한을 다시 평가해야 한다. 응용 분야에 따라 명시적인 인간 확인(Human Acknowledgment)이 필요할 수도 있다. 따라서 자율성 재진입(Re-Entry)은 단순히 중단된 행동을 계속하는 것이 아니라 검증된 상태 전환(Validated State Transition)으로 처리해야 한다.

명령 지속성(Command Persistence)도 명확하게 정의되어야 한다. 일부 지시는 다음 행동에만 적용되는 반면 다른 지시는 일시적 또는 장기간의 제약을 설정한다. "정지하라"는 즉각적인 움직임 중단을 요구할 수 있지만 "유지보수가 끝날 때까지 이 통로를 사용하지 마라"는 지속적인 공간 제한(Persistent Spatial Restriction)을 생성한다. 시스템은 명령의 범위, 지속 시간, 소유권 및 종료 조건을 표현하여 제약이 너무 일찍 사라지거나 더 이상 유효하지 않은 이후에도 계속 유지되지 않도록 해야 한다.

피드백(Feedback)은 명령 루프(Command Loop)를 완성한다. 지시를 받은 후 로봇은 요청된 행동을 이해했는지, 수락했는지, 거부했는지 또는 완료했는지를 전달해야 한다. 안전 관련 명령의 경우 피드백은 단순히 메시지가 성공적으로 수신되었다는 사실이 아니라 실제 시스템 상태와 대응해야 한다. 로봇이 정지했다고 알리는 것은 검증된 움직임 상태(Verified Motion State)와 연결되어야 하며, 인터페이스의 응답이 실제 물리적 실행 완료로 잘못 이해되는 것을 방지해야 한다.

다중 양식 확인(Multi-Modal Confirmation)은 복잡한 환경에서 모호성을 줄일 수 있다. 음성 명령은 가리키기, 터치스크린, 지도, 강조된 물체, 물리적 제어 장치 또는 시각 표시와 결합될 수 있다. 로봇은 음성으로 확인을 요청하면서 선택된 목적지나 출입 제한 영역(Exclusion Region)을 시각적으로 표시할 수 있다. 언어와 공간 표현(Spatial Representation)을 결합하면 사용자가 로봇의 해석이 움직임에 영향을 주기 전에 그 의미를 검증할 수 있다.

고급 자연어 상호작용(Natural Language Interaction)을 사용할 수 있더라도 물리적 오버라이드 제어(Physical Override Controls)는 여전히 중요하다. 버튼, 스위치, 활성화 장치(Enabling Devices), 원격 제어 장치 또는 전용 정지 인터페이스는 특정 개입에 대해 더욱 단순하고 결정론적인 경로를 제공할 수 있다. 자연어는 유연성과 풍부한 맥락을 제공하지만 안전 필수 제어(Safety-Critical Control)가 음성 인식, 의미 추론, 네트워크 가용성 또는 범용 언어 모델에만 의존해서는 안 된다.

런타임 보증(Runtime Assurance)은 수신된 명령, 해석된 의도, 권한, 안전 제약, 명령된 움직임(Commanded Motion), 실제 로봇 행동 사이의 관계를 지속적으로 모니터링해야 한다. 수락된 정지 명령이 예상되는 움직임 대응을 발생시키지 않는다면 이러한 불일치는 안전 관련 결함(Safety-Relevant Fault)으로 처리해야 한다. 마찬가지로 인터페이스가 인간에게 제어권이 설정되었다고 계속 표시하는 동안 오버라이드가 조용히 실패해서는 안 된다.

명령 로그(Command Logs)는 추적 가능성(Traceability)과 사후 사건 분석(Post-Event Analysis)을 지원할 수 있다. 관련 기록에는 수신된 지시, 해석된 의미, 신뢰도, 확인, 권한 상태, 오버라이드 전환, 안전 제약 및 그 결과 발생한 로봇 행동이 포함될 수 있다. 이러한 기록은 사건이 인간의 지시, 해석 오류, 자율 계획, 제어 실패 또는 잘못된 권한 처리 중 무엇에서 발생했는지를 판단하는 데 도움을 준다. 로그는 개인정보 보호(Privacy), 보안 및 운용 요구사항에 적합하게 관리되어야 한다.

사이버보안(Cybersecurity)은 물리적 움직임에 영향을 줄 수 있는 인터페이스가 잠재적인 공격 표면(Attack Surface)을 형성하기 때문에 명령 및 오버라이드 설계와 밀접하게 연결된다. 배치 환경에 따라 인증(Authentication), 권한 부여, 보안 통신(Secure Communication), 명령 무결성(Command Integrity), 재전송 또는 위조 공격(Replay or Spoofing)에 대한 보호가 필요할 수 있다. 원격 오버라이드는 움직임 시스템으로 접근하는 통제되지 않은 경로가 되어서는 안 되지만 보안 메커니즘은 안전 필수 상황에서 정당한 개입이 충분히 빠르게 이루어질 수 있도록 해야 한다.

평가(Evaluation)는 모호한 명령, 우발적인 발화, 반복된 지시, 서로 충돌하는 사용자, 권한 없는 요청, 지연된 확인, 비상 정지, 수동 제어권 인수, 자율성 재진입 및 물리적 안전 제약과 충돌하는 명령을 포함해야 한다. 시험은 단순히 명령이 인식되는지를 측정하는 것이 아니라 현실적인 시간 및 환경 조건에서 전체 상호작용이 예측 가능하고 적절하게 보수적인 물리적 행동을 발생시키는지를 평가해야 한다.

실패 중심 시험(Failure-Oriented Testing)은 손실된 확인 응답, 오래된 명령(Stale Commands), 잘못된 참조 해석, 인증 실패, 통신 중단, 지연된 오버라이드 실행, 모드 혼동(Mode Confusion), 표시된 제어 상태와 실제 제어 상태 사이의 불일치를 검토해야 한다. 명령 인터페이스의 신뢰성이 저하될 경우 로봇은 안전한 상태를 유지하거나 더욱 안전한 상태로 전환해야 한다. 인간 오버라이드는 제어 가능성(Controllability)을 향상시켜야 하지만 또 다른 단일 실패 지점(Single Point of Failure)이 되어서는 안 된다.

인간 명령 확인(Human Command Confirmation)과 오버라이드(Override)는 궁극적으로 자율 지능(Autonomous Intelligence)과 인간 권한(Human Authority) 사이에 구조화된 경계(Structured Boundary)를 형성한다. 확인은 중대한 행동이 인간과 로봇 사이의 공유된 이해에 기반하도록 보장하고, 오버라이드는 자율 시스템이 더 이상 제어권을 유지해서는 안 되는 상황에서 인간이 개입할 수 있는 수단을 제공한다. 권한 부여, 런타임 보증, 자연어 상호작용, 근접 관리 및 독립적 보호(Independent Protection)와 통합된 이러한 메커니즘은 기본적인 물리적 안전 제약의 최종 권한을 유지하면서 의미 있는 인간 제어를 보존한다.

## 05.10. Shared Control and Supervisory Control

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

공유 제어(Shared Control)와 감독 제어(Supervisory Control)는 로봇 운용 과정에서 인간의 권한(Human Authority)과 자율 지능(Autonomous Intelligence)이 어떻게 협력하는지를 정의한다. 제어를 완전 자율성과 직접 원격조작(Teleoperation) 사이의 이분법적인 선택으로 취급하는 대신, 물리 AI 시스템(Physical AI System)은 작업 복잡성, 환경 불확실성, 위험 및 역량에 따라 인간과 기계 사이에 의사결정을 분배할 수 있다. 목적은 예측 가능한 권한 경계(Authority Boundaries)를 유지하면서 인간의 판단과 자율 지각, 계획 및 제어를 결합하는 것이다.

공유 제어(Shared Control)는 인간과 자율 시스템의 명령이 동시에 또는 긴밀하게 결합된 제어 루프(Control Loops) 안에서 로봇 행동에 영향을 미치는 방식으로 작동한다. 사람은 방향, 속도, 목표 또는 작업 의도를 지정하고, 로봇은 안정화, 장애물 회피, 충돌 방지, 궤적 개선 또는 조작 제약을 지원할 수 있다. 결과적으로 생성되는 움직임은 인간이나 자율 시스템 어느 한쪽에 의해서만 생성되는 것이 아니라 인간의 의도와 자율 지원(Autonomous Assistance)을 함께 반영한다.

감독 제어(Supervisory Control)는 인간을 더 높은 의사결정 수준에 배치한다. 감독자는 모든 움직임을 지속적으로 명령하는 대신 목표를 할당하고, 계획을 승인하고, 제약을 설정하고, 진행 상황을 모니터링하며, 필요한 경우 개입한다. 자율 시스템은 하위 수준의 지각, 계획, 내비게이션, 조작 및 제어를 수행한다. 이러한 구조를 통해 한 사람이 지속적인 저수준 제어를 수행하지 않고도 복잡한 로봇 또는 여러 자율 시스템을 감독할 수 있다.

적절한 제어 할당(Control Allocation)은 작업과 운용 상황에 따라 달라진다. 잘 매핑된 환경에서의 일상적인 내비게이션은 인간의 개입이 거의 필요하지 않을 수 있지만, 사람 주변에서의 조작이나 불확실한 환경에서의 운용에는 더 강한 감독이 유용할 수 있다. 따라서 제어 권한(Control Authority)은 전체 임무 동안 고정될 필요 없이 동적으로 변화할 수 있다. 이러한 적응은 사용자가 자율 시스템이 언제 지원하고, 제한하며, 제어권을 양보하는지 이해할 수 있도록 명시적인 규칙을 따라야 한다.

인간 입력(Human Input)은 서로 다른 추상화 수준(Levels of Abstraction)을 나타낼 수 있다. 낮은 수준에서는 운영자가 속도나 매니퓰레이터 움직임을 직접 명령할 수 있다. 중간 수준에서는 웨이포인트(Waypoint), 물체, 파지 목표(Grasp Target) 또는 선호 경로를 선택할 수 있다. 높은 수준에서는 특정 영역을 검사하거나 자재를 전달하는 것과 같은 목표를 지정할 수 있다. 추상화 수준이 높아질수록 더 많은 실행 책임이 자율 지능으로 이전되지만 임무 의도에 대한 인간의 권한은 유지된다.

자율 지원(Autonomous Assistance)은 인간의 의도를 예상하지 못한 방식으로 변형하지 않으면서 이를 지원해야 한다. 운영자가 전진을 명령한 경우 장애물 회피 기능은 가능한 한 의도된 방향을 유지하면서 경로를 조정할 수 있다. 지나친 보정은 로봇이 운영자의 의도에 저항하는 느낌을 줄 수 있으며, 지원이 부족하면 안전하지 않은 행동을 허용할 수 있다. 따라서 공유 제어는 인간 입력, 자율 수정(Autonomous Modification), 결과적인 로봇 움직임 사이에 이해 가능한 관계가 필요하다.

제어 중재(Control Arbitration)는 서로 경쟁하는 인간 명령과 자율 명령을 어떻게 결합할지를 결정한다. 중재에는 고정 우선순위, 가중 결합(Weighted Blending), 제약 기반 최적화(Constraint-Based Optimization), 상태 의존적 권한(State-Dependent Authority) 또는 이산 모드 전환(Discrete Mode Switching)을 사용할 수 있다. 어떤 중재 방식을 사용하더라도 안전 필수 제약(Safety-Critical Constraints)이 우선해야 한다. 인간 명령은 허용된 운용 영역 안에서 움직임에 영향을 줄 수 있지만 안전한 자율 대응과 안전하지 않은 인간 명령을 단순 평균하여 위험한 절충안을 만들어서는 안 된다.

위험이 증가할수록 제어 권한은 더욱 보수적으로 변화해야 한다. 정상적인 조건에서는 시스템이 폭넓은 인간의 지시나 자율적 행동을 허용할 수 있다. 사람, 장애물, 제한 영역 또는 불안정한 조건에 가까워질수록 움직임 제약(Motion Constraints)을 강화할 수 있다. 필요한 안전 여유를 유지할 수 없는 경우 현재 선택된 제어 모드와 관계없이 보호 메커니즘(Protective Mechanisms)이 움직임을 제한하거나 정지시킬 수 있다. 이를 통해 수동, 공유, 감독 및 자율 운전 전반에서 일관된 안전 경계(Safety Boundary)를 유지한다.

사용자는 현재 로봇 행동의 어떤 부분을 누가 제어하고 있는지 이해해야 하므로 모드 인식(Mode Awareness)이 필수적이다. 인터페이스는 로봇이 직접 제어, 공유 제어, 감독 자율성(Supervisory Autonomy), 일시적 자율 지원 또는 보호 개입(Protective Intervention) 중 어느 상태에 있는지를 명확하게 표시해야 한다. 숨겨지거나 모호한 모드 전환은 운영자가 자율 시스템에 책임이 있다고 생각하지만 시스템은 인간의 제어를 기대하거나 그 반대의 상황이 발생하는 모드 혼동(Mode Confusion)을 초래할 수 있다.

따라서 제어 모드 사이의 전환은 명시적이고 예측 가능해야 한다. 자율 운전에서 공유 제어로 전환할 때는 안정화, 대기 중인 행동의 취소 및 운영자 준비 상태 확인이 필요할 수 있다. 자율 운전으로 복귀할 때는 환경, 작업 상태, 인간 위치 및 활성화된 제한을 다시 평가해야 한다. 제어권 이전(Control Transfer)은 단순히 명령 출처를 순간적으로 변경하는 것이 아니라 정의된 진입 및 종료 조건을 가진 상태 전환(State Transition)으로 처리해야 한다.

자율 행동이 부적절하거나 예상과 다른 경우 인간 오버라이드(Human Override)를 사용할 수 있어야 한다. 감독자는 임무를 일시정지하거나, 목표를 수정하거나, 계획된 행동을 거부하거나, 수동 제어를 요청하거나, 새로운 제약을 설정할 수 있다. 그러나 오버라이드 권한은 독립적으로 강제되는 물리적 안전 한계 안에 있어야 한다. 인간의 개입은 로봇의 목표나 자율성 할당 방식을 변경할 수 있지만 필요한 보호 메커니즘을 자동으로 비활성화해서는 안 된다.

감독 인터페이스(Supervisory Interface)는 운영자에게 과도한 정보를 제공하지 않으면서 의미 있는 개입에 필요한 충분한 정보를 제공해야 한다. 관련 정보에는 로봇 위치, 작업 진행 상황, 계획된 궤적, 주변 사람, 탐지된 위험, 신뢰도, 활성 제약, 결함 및 지원 요청이 포함될 수 있다. 여러 로봇이나 작업을 동시에 감독하는 경우에도 안전 필수 조건이 명확하게 보이도록 운용상의 중요성에 따라 정보의 우선순위를 설정해야 한다.

신뢰도(Confidence)와 불확실성(Uncertainty)은 자율 시스템이 언제 인간의 지원을 요청해야 하는지를 결정하는 데 활용할 수 있다. 지각, 위치추정, 계획 및 작업 실행이 검증된 신뢰 범위 안에 있는 동안 로봇은 독립적으로 운용될 수 있다. 불확실성이 증가하면 감속하거나, 확인을 요청하거나, 대안 계획을 제시하거나, 감독 개입(Supervisory Intervention)을 요청할 수 있다. 이를 통해 자율 시스템이 안정적으로 처리할 수 있는 행동을 사람이 계속 감시하는 대신 어려운 상황에 인간의 주의를 집중시킬 수 있다.

감독 제어를 설계할 때는 인간 작업 부하(Human Workload)를 고려해야 한다. 이론적으로 자율적인 플릿(Fleet)이라도 로봇이 빈번하게 승인이나 지원을 요청한다면 실제 운용에서는 인간에게 크게 의존할 수 있다. 지나친 알림, 반복적인 확인 또는 동시다발적인 개입 요청은 감독자에게 과부하를 발생시키고 대응 시간을 증가시킬 수 있다. 따라서 시스템은 인간의 주의를 제한된 자원(Limited Resource)으로 관리하고 인간의 판단이 실제로 필요한 정보만 에스컬레이션해야 한다.

다중 로봇 감독(Multi-Robot Supervision)은 한 명의 운영자가 서로 다른 작업, 위치 및 위험 상태를 가진 여러 로봇을 감독할 수 있기 때문에 이러한 문제를 더욱 확장한다. 인터페이스는 어떤 로봇에 주의가 필요하며 그 이유가 무엇인지를 우선순위에 따라 보여주어야 한다. 일상적인 자율 활동은 요약해서 표시하고 이상 상황, 안전 이벤트, 차단된 작업 또는 불확실한 판단은 더욱 강조할 수 있다. 플릿 수준 조정(Fleet-Level Coordination)은 불필요한 개입을 줄이면서 필요할 때 개별 로봇의 제어권을 인수할 수 있는 능력을 유지해야 한다.

이동 로봇(Mobile Robot)의 공유 제어는 인간의 방향 의도와 자율 내비게이션 제약(Autonomous Navigation Constraints)을 결합할 수 있다. 운영자는 목적지 방향으로 조향하고 로봇은 장애물과의 간격을 유지하며, 제한 영역을 준수하고, 속도를 조절하며, 사람과의 위험한 근접을 회피할 수 있다. 운영자가 자신의 입력이 어떻게 수정될지를 예상할 수 있도록 지원은 부드럽고 예측 가능해야 한다. 갑작스러운 자율 보정은 그 자체로 혼란과 불안정한 인간 제어 행동을 발생시킬 수 있다.

매니퓰레이터(Manipulator)의 경우 공유 제어는 정렬, 충돌 회피, 힘 제한(Force Limits), 파지 제약 또는 허용된 작업 공간 내의 움직임을 지원할 수 있다. 사람이 엔드 이펙터(End Effector)를 안내하는 동안 자율 시스템은 방향을 유지하거나 위험 영역 진입을 방지할 수 있다. 이러한 역할 분담은 인간의 공간 판단과 숙련성을 기계의 정밀성과 결합한다. 제어 인터페이스는 활성화된 제약을 운영자가 인식할 수 있도록 하여 특정 움직임이 제한되는 이유를 이해하도록 해야 한다.

원격 감독 제어(Remote Supervisory Control)는 통신 지연, 대역폭 제한 및 네트워크 중단 가능성을 발생시킨다. 피드백이 지연되면 직접 원격조작이 어려워질 수 있지만, 로봇이 로컬에서 움직임을 자율적으로 실행한다면 상위 수준의 감독 명령은 여전히 실용적일 수 있다. 따라서 가능한 경우 안전 필수 지각(Safety-Critical Perception)과 보호 기능은 로컬에 유지하여 원격 통신의 성능이 저하되거나 사용할 수 없는 경우에도 로봇이 안전 행동을 유지하도록 해야 한다.

통신 손실(Loss of Communication)은 사전에 정의된 제어 대응으로 이어져야 한다. 응용 분야에 따라 로봇은 안전한 로컬 행동을 완료하거나, 현재 위치를 유지하거나, 감속하거나, 알려진 영역으로 후퇴하거나, 최소 위험 상태(Minimum-Risk Condition)로 전환할 수 있다. 사용할 수 없는 인간 감독을 전제로 한 상태에서 무기한 운전을 계속해서는 안 된다. 따라서 통신 상태(Communication Health)는 어떤 자율성과 제어 모드를 계속 허용할 수 있는지를 결정하는 런타임 상태(Runtime State)의 일부가 된다.

공유 제어는 인간 명령 확인(Human Command Confirmation)과 자연스럽게 통합되어야 한다. 중요한 감독 명령은 참조 대상, 목표 또는 제약이 모호한 경우 확인이 필요할 수 있으며, 즉각적인 보호 명령은 더 빠른 경로를 사용할 수 있다. 또한 로봇은 명령이 수락되었는지, 자율 제약에 의해 수정되었는지, 거부되었는지 또는 완료되었는지를 보여주는 피드백을 제공해야 한다. 이를 통해 제어 루프를 완성하고 인간이 시스템 행동에 대한 정확한 정신 모델(Mental Model)을 유지하도록 한다.

자연어(Natural Language)는 상위 수준의 감독 채널(High-Level Supervisory Channel)을 제공할 수 있다. 운영자는 로봇에게 다른 영역을 검사하거나, 작업자를 기다리거나, 특정 통로를 피하거나, 진행이 중단된 이유를 설명하도록 요청할 수 있다. 이러한 지시는 물리적 행동에 영향을 주기 전에 월드 모델(World Model)에 그라운딩되고 검증되어야 한다. 언어는 감독 상호작용을 단순화할 수 있지만 결정론적 안전 정책(Deterministic Safety Policies)과 물리적 보호 기능은 대화적 해석보다 최종적인 권한을 유지해야 한다.

런타임 보증(Runtime Assurance)은 인간과 자율 시스템 사이의 전체 제어 관계를 지속적으로 모니터링해야 한다. 관련 변수에는 활성 제어 모드, 명령 출처(Command Source), 권한, 통신 상태, 인간 입력, 자율 수정, 안전 제약, 계획된 움직임 및 실제 실행이 포함된다. 이러한 요소 사이에서 예상하지 못한 불일치가 발생하면 모드 혼동, 소프트웨어 결함, 오래된 명령(Stale Commands) 또는 제어권 이전 실패를 의미할 수 있으며 적절한 보수적 대응을 발생시켜야 한다.

공유된 의사결정에서는 책임 관계를 사후에 재구성하기 어려울 수 있으므로 로깅 및 추적 가능성(Logging and Traceability)이 특히 중요하다. 기록은 인간이 무엇을 요청했는지, 자율 시스템이 그 요청을 어떻게 수정했는지, 어떤 제약이 활성화되어 있었는지, 누가 제어 권한을 가지고 있었는지, 최종적으로 어떤 움직임이 실행되었는지를 식별할 수 있다. 이러한 정보는 디버깅, 검증, 사고 분석, 운영자 교육 및 향후 인간-로봇 협업 개선을 지원한다.

평가(Evaluation)는 정상적인 작업 성능만을 포함해서는 안 된다. 시험은 제어권 이전, 충돌하는 입력, 불확실한 자율성, 운영자의 주의 분산, 지연된 대응, 통신 손실, 여러 로봇의 동시 운용, 보호 개입 및 자율성 복귀를 포함해야 한다. 평가 지표에는 작업 성공률, 개입 빈도, 대응 시간, 모드 인식, 작업 부하, 안전 여유(Safety Margin), 인간 관점에서의 자율 지원 예측 가능성이 포함될 수 있다.

실패 중심 시험(Failure-Oriented Testing)은 오래된 명령, 잘못된 모드 표시, 지연된 제어권 이전, 네트워크 중단, 서로 충돌하는 인간과 자율 시스템의 목표 및 사용할 수 없는 감독 인터페이스를 의도적으로 발생시켜야 한다. 인간과 자율 시스템 사이의 협력이 악화되더라도 로봇은 검증된 안전 제약(Validated Safety Constraints) 안에 머물러야 한다. 협력 메커니즘의 실패가 기본적인 보호 기능을 제거하지 않을 때에만 공유 제어가 안전한 유연성을 제공할 수 있으므로 안전한 성능 저하(Safe Degradation)가 필수적이다.

공유 제어(Shared Control)와 감독 제어(Supervisory Control)는 궁극적으로 인간의 판단(Human Judgment)과 자율 물리 AI(Autonomous Physical AI) 사이에 확장 가능한 협력 관계(Scalable Partnership)를 구축한다. 인간은 목표, 상황적 이해, 예외 처리 및 권한을 제공하고, 자율 시스템은 지속적인 지각, 계획, 안정화 및 실행을 담당한다. 명확한 제어 할당, 예측 가능한 전환, 런타임 보증 및 독립적인 안전 제약을 통해 시스템은 명확성을 잃지 않으면서 책임을 전환할 수 있으며, 개별 로봇에서 조정된 플릿에 이르기까지 효과적인 인간 감독(Human Oversight)을 가능하게 한다.

## 05.11. Teleoperation and Remote Safety

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

원격조작(Teleoperation)과 원격 안전(Remote Safety)은 인간 운영자가 로봇과 물리적으로 떨어진 위치에서 물리 AI 시스템(Physical AI System)을 제어하거나 지원하는 조건을 다룬다. 원격 운용은 인간의 판단을 멀리 떨어져 있거나, 위험하거나, 접근하기 어렵거나, 운용상 복잡한 환경까지 확장할 수 있지만 통신 지연, 제한된 상황 인식(Situational Awareness), 네트워크 장애 및 제어 불확실성을 발생시키므로 이를 안전 아키텍처(Safety Architecture)의 명시적인 구성 요소로 관리해야 한다.

원격조작은 직접적인 저수준 움직임 제어(Low-Level Motion Control)부터 상위 수준의 원격 감독(Remote Supervision)까지 다양한 형태로 구성될 수 있다. 운영자가 조향, 속도, 매니퓰레이터 관절 또는 엔드 이펙터(End-Effector)의 움직임을 지속적으로 명령할 수도 있으며, 더 높은 자율성을 가진 시스템에서는 웨이포인트(Waypoint), 작업 목표 또는 제약을 전달하고 로봇이 이를 로컬에서 실행할 수 있다. 적절한 수준은 통신 품질, 작업 정밀도, 환경 복잡성, 로봇 역량 및 지연되거나 잘못된 인간 개입의 결과에 따라 결정된다.

원격 제어(Remote Control)를 사용한다고 해서 로컬 자율성(Local Autonomy)과 보호 기능이 불필요해지는 것은 아니다. 원격조작되는 로봇은 적절한 경우 장애물 탐지, 속도 제한, 충돌 회피, 보호 정지(Protective Stopping), 제한 영역 준수와 같은 독립적인 메커니즘을 유지해야 한다. 이러한 로컬 기능은 인간 명령 주변에 안전 경계(Safety Boundary)를 형성하여 직접 제어 권한이 부여되었다는 이유만으로 원격 운영자가 의도하지 않게 로봇을 검증된 물리적 제약 밖으로 움직이지 못하도록 한다.

상황 인식(Situational Awareness)은 운영자가 직접적인 물리적 현장 경험이 아니라 센서를 통해 환경을 인식하기 때문에 핵심적인 문제이다. 카메라, 깊이 센서(Depth Sensor), 라이다(LiDAR), 지도, 로봇 상태, 근접 정보, 오디오 및 작업 맥락을 원격 환경 표현에 활용할 수 있다. 인터페이스는 제한된 인간의 주의를 놓고 경쟁하는 과도한 원시 센서 스트림(Raw Sensor Streams)을 제공하지 않으면서 위험과 움직임의 결과를 이해할 수 있을 만큼 충분한 정보를 제공해야 한다.

카메라 배치(Camera Placement)는 원격 주행과 조작 성능에 큰 영향을 미친다. 전방 카메라는 내비게이션을 지원할 수 있지만 측면 간격, 후방 장애물, 매니퓰레이터 자세 또는 주변 사람을 보여주지 못할 수 있다. 여러 시점(Multiple Viewpoints)이나 동적으로 선택되는 시점을 이용하면 사각 영역을 줄일 수 있으며 공간 표현(Spatial Representation)을 통해 추가적인 맥락을 제공할 수 있다. 중요한 영역을 관찰할 수 없는 경우 운영자에게 이를 알려야 하며, 화면에 보이지 않는 것이 위험이 존재하지 않는다는 의미로 받아들여지지 않도록 해야 한다.

지연시간(Latency)은 제어 가능성(Controllability)에 직접적인 영향을 미친다. 운영자의 입력과 로봇 반응 사이에 지연이 발생하면 운영자가 오래된 로봇 상태를 기반으로 행동하기 때문에 오버슈트(Overshoot), 진동, 반복 명령 또는 부적절한 보정이 발생할 수 있다. 반대 방향의 지연도 중요하다. 센서 피드백은 로봇이 가장 최근의 명령을 실행하기 이전의 상황을 보여줄 수 있기 때문이다. 따라서 원격조작 설계에서는 네트워크 지연만이 아니라 전체 명령 및 피드백 루프(Command-and-Feedback Loop)를 고려해야 한다.

가변 지연시간(Variable Latency)은 일정하고 알려진 지연보다 관리하기 어려울 수 있다. 통신 타이밍이 예측할 수 없게 변하면 운영자는 로봇이 얼마나 빠르게 반응할지에 대한 안정적인 기대를 형성할 수 없다. 인터페이스는 통신 품질과 지연 상태를 표시할 수 있으며, 지연이 증가함에 따라 제어 시스템은 허용 속도를 낮추거나 자율 지원(Autonomous Assistance)을 강화할 수 있다. 심각한 성능 저하가 발생하면 직접 원격조작에서 감독 명령(Supervisory Commands) 또는 사전에 정의된 안전 상태로 전환해야 할 수 있다.

대역폭 제한(Bandwidth Limitations)은 원격 지각(Remote Perception)의 품질이나 갱신 속도를 감소시킬 수 있다. 비디오 압축, 해상도 저하, 낮은 프레임 속도, 지연된 지도 또는 누락된 센서 채널은 안전 운용에 중요한 정보를 숨길 수 있다. 시스템은 모든 데이터를 동일하게 취급하기보다 운용상의 중요도에 따라 정보 전송을 조정해야 한다. 안전 관련 상태, 제어 확인(Control Acknowledgments), 중요 경고는 필수적이지 않은 시각화 또는 진단 정보보다 높은 전송 우선순위를 가질 수 있다.

패킷 손실(Packet Loss)과 통신 중단(Communication Interruption)은 발생하지 않는 예외 상황이 아니라 예상 가능한 조건으로 취급해야 한다. 로봇은 원격 명령이 얼마 동안 유효한지와 새로운 명령이 더 이상 도착하지 않을 때 어떤 행동을 수행할지를 정의해야 한다. 마지막 속도 명령을 무기한 계속 실행하는 것은 심각한 위험을 발생시킬 수 있다. 응용 분야에 따라 통신 손실은 제어된 감속, 위치 유지, 로컬에서 안전한 동작의 완료, 후퇴 또는 최소 위험 상태(Minimum-Risk Condition)로의 전환을 발생시킬 수 있다.

따라서 명령 최신성(Command Freshness)은 중요한 안전 속성이다. 원격 명령에는 타임스탬프(Timestamp), 순서 정보, 유효 기간 또는 오래된 지시를 탐지하기 위한 다른 메커니즘을 포함할 수 있다. 이전 물리적 상황을 기준으로 생성된 명령은 통신이 복구된 이후 로봇이나 환경이 크게 변경되었다면 실행되어서는 안 된다. 로컬 제어 시스템은 현재 상태 또는 검증된 실행 시간 범위(Validated Execution Window)와 더 이상 호환되지 않는 명령을 거부해야 한다.

확인 응답(Acknowledgment)은 원격 명령 루프를 완성한다. 운영자는 명령이 전송된 상태, 수신된 상태, 수락된 상태, 로컬 안전 제약에 의해 수정된 상태 및 실제 물리적으로 실행된 상태를 구별할 수 있어야 한다. 이러한 구별이 없으면 원격 인터페이스가 의도한 행동이 이미 수행되었다는 잘못된 확신을 만들 수 있다. 따라서 안전 관련 피드백은 단순히 네트워크 전송에 성공했다는 사실이 아니라 검증된 로봇 상태(Verified Robot State)와 연결되어야 한다.

직접 원격조작 중에는 로컬 충돌 보호(Local Collision Protection)가 특히 중요하다. 인간 운영자는 거리를 잘못 판단하거나, 장애물을 놓치거나, 화면 지연을 경험하거나, 급격한 명령을 내릴 수 있다. 로봇은 속도를 제한하고, 최소 간격을 유지하고, 지오펜스(Geofence)를 강제하고, 매니퓰레이터 힘을 제한하거나, 탐지된 위험 방향으로의 움직임을 거부할 수 있다. 이러한 지원은 운영자가 요청한 움직임이 언제 그리고 왜 수정되는지를 이해할 수 있도록 예측 가능해야 한다.

속도(Speed)는 물리적 위험뿐만 아니라 통신 조건도 반영해야 한다. 고속 원격 운용에는 충분한 지각 범위, 갱신 주기, 제어 응답성 및 정지 능력이 필요하다. 네트워크 지연이 증가하거나 센서 품질이 저하되면 물리적 환경 자체가 변하지 않았더라도 허용 속도를 낮춰야 할 수 있다. 이를 통해 원격 통신 상태(Remote Communication Health)가 로봇의 동적 안전 영역(Dynamic Safety Envelope)과 직접 연결된다.

원격 조작(Remote Manipulation)은 작은 제어 오류도 접촉력이나 충돌을 발생시킬 수 있기 때문에 추가적인 문제를 가진다. 운영자는 제한된 깊이 인식(Depth Perception)으로 인해 관절 구성이나 주변 형상을 완전히 이해하지 못할 수 있다. 공유 제어(Shared Control) 기능은 정렬, 충돌 회피, 힘 제한, 작업 공간 제약 및 파지 안정화(Grasp Stabilization)를 지원할 수 있다. 적절한 경우 햅틱 피드백(Haptic Feedback)을 통해 추가적인 정보를 제공할 수 있지만 힘 피드백 루프를 구성할 때는 통신 지연을 고려해야 한다.

인간 탐지 및 추적(Human Detection and Tracking)은 원격조작 중에도 로컬에서 계속 활성화되어야 한다. 원격 운영자는 현재 카메라 시야 밖에서 사람이 진입하는 것을 발견하지 못하거나 네트워크 지연 때문에 너무 늦게 대응할 수 있다. 로컬 지각(Local Perception)은 사람의 근접을 탐지하고 원격 명령과 관계없이 자동으로 움직임을 제한할 수 있다. 따라서 원격 제어 권한은 자율 운전에서 사용되는 것과 동일한 기본적인 인간 보호 영역(Human-Protection Envelope) 안에서 동작한다.

안전 영역(Safety Zones)과 속도 및 분리 모니터링(Speed and Separation Monitoring)은 원격 제어 모드에서도 최종적인 권한을 유지할 수 있다. 사람이 로봇에 접근하면 운영자가 계속 높은 속도를 요청하더라도 허용되는 움직임을 단계적으로 감소시킬 수 있다. 보호 영역(Protective Region)에 진입하면 원격 운영자의 의도와 독립적으로 정지를 실행할 수 있다. 자율, 공유 및 원격조작 운전 전반에서 일관된 보호 기능을 유지하면 모드 변경으로 인해 물리적 안전에 공백이 발생하는 것을 방지할 수 있다.

원격 비상 개입(Remote Emergency Intervention)에는 신중하게 설계된 경로가 필요하다. 운영자는 신속한 정지나 안전 상태로의 전환을 명확하게 요청할 수 있는 방법을 가져야 하지만 사고가 발생하는 순간 통신 자체가 사용할 수 없는 상태일 수도 있다. 따라서 원격 비상 명령만을 유일한 보호 메커니즘으로 사용해서는 안 된다. 로컬 비상 및 보호 기능(Local Emergency and Protective Functions)은 원격 운영자나 지속적으로 사용 가능한 네트워크 연결에 의존하지 않고도 작동할 수 있어야 한다.

운영자는 자신의 명령이 실제로 로봇을 제어하고 있는지를 알아야 하므로 제어 모드 인식(Control Mode Awareness)이 중요하다. 시스템은 직접 원격조작, 공유 제어, 감독 운용, 자율 실행, 통신 손실 대응 또는 보호 개입 상태를 명확하게 표시해야 한다. 로컬 안전 로직(Local Safety Logic)이 일시적으로 명령을 거부하거나 수정하는 경우 인터페이스에 이를 표시해야 한다. 그렇지 않으면 운영자는 제어 권한을 잘못 이해한 상태에서 계속 보정 명령을 내릴 수 있다.

원격조작으로 전환할 때는 로봇을 알려지고 안정된 상태(Known and Stable Robot State)로 만들어야 한다. 원격 제어가 활성화되기 전에 자율 궤적이나 대기 중인 행동을 중지해야 할 수 있다. 움직임을 시작하기 전에 운영자의 준비 상태, 통신 품질, 센서 가용성 및 제어 권한을 검증할 수 있다. 이를 통해 제어권 이전 과정에서 자율 명령과 원격 명령이 예상하지 못한 방식으로 중첩되는 것을 방지한다.

자율 운전으로 복귀하는 과정에도 유사한 검증이 필요하다. 원격 운용 중 발생한 환경 변화를 다시 고려하지 않고 이전에 계획했던 궤적을 재개해서는 안 된다. 인간 위치, 장애물, 위치추정 품질(Localization Quality), 작업 상태, 활성 제한 및 로봇 구성을 다시 평가해야 한다. 따라서 자율 운전의 재개는 중단되었던 자율 명령 시퀀스를 단순히 계속하는 것이 아니라 새롭게 검증된 의사결정(Validated Decision)으로 처리해야 한다.

원격 운영자 작업 부하(Remote Operator Workload)는 특히 한 사람이 여러 로봇을 감독하는 경우 안전 제약이 될 수 있다. 빈번한 개입 요청, 여러 비디오 피드, 경보, 통신 문제 및 동시다발적인 작업 실패는 인간의 주의 능력을 초과할 수 있다. 플릿 수준 시스템(Fleet-Level System)은 위험과 긴급성에 따라 요청의 우선순위를 설정하여 일상적인 로봇은 자율 운전을 유지하고 인간의 판단이 실제로 필요한 상황에 운영자의 주의를 집중시켜야 한다.

원격 운영자 사이의 인계(Handover)에서도 제어의 명확성을 유지해야 한다. 교대 근무, 전문가에게 에스컬레이션 또는 로컬과 원격 인력 사이의 제어권 이전은 현재 누가 권한을 가지고 있는지에 대한 불확실성을 발생시킬 수 있다. 시스템은 제어권 소유(Control Ownership)를 명시적으로 관리하고 성공적인 인계를 확인하며 여러 운영자의 명령이 중복되지 않도록 해야 한다. 권한이 명확하지 않은 동안에는 알려진 안전 상태(Known Safe State)를 유지하는 것이 적절할 수 있다.

사이버보안(Cybersecurity)은 원격조작이 통신 네트워크를 통해 물리적 제어를 노출하기 때문에 원격 안전과 분리할 수 없다. 인증(Authentication), 권한 부여(Authorization), 암호화된 통신, 명령 무결성(Command Integrity), 세션 관리 및 위조나 재전송 공격(Spoofing or Replay)에 대한 보호가 필요할 수 있다. 보안 제어는 권한 없는 움직임을 방지하면서 정당한 개입이 적시에 이루어질 수 있도록 해야 한다. 침해된 원격 인터페이스가 안전 필수 로봇 기능에 무제한적으로 접근할 수 있어서는 안 된다.

런타임 보증(Runtime Assurance)은 통신 품질, 명령 최신성, 활성 운영자, 제어 모드, 로컬 안전 제약, 계획된 움직임 및 실제 실행을 지속적으로 모니터링해야 한다. 이러한 상태 사이에서 예상하지 못한 불일치가 발생하면 지연된 명령, 제어권 이전 실패, 네트워크 결함 또는 소프트웨어 오류를 의미할 수 있다. 시스템은 감속, 명령 거부, 자율 보호 강화, 위치 유지 또는 최소 위험 상태로의 전환을 통해 대응할 수 있다.

로깅(Logging)은 원격 제어 이벤트를 사후에 재구성할 수 있도록 지원한다. 관련 기록에는 운영자 신원, 제어 모드, 명령 타이밍, 네트워크 상태, 로봇 대응, 로컬 안전 개입, 센서 가용성 및 모드 전환이 포함될 수 있다. 이러한 기록은 운영자 오류와 통신 실패, 자율 수정, 지각 실패 또는 제어 시스템 결함을 구별하는 데 도움을 주며 검증, 교육, 사이버보안 분석 및 지속적인 개선을 지원한다.

평가(Evaluation)는 이상적인 네트워크 조건만 시험하는 것이 아니라 실제 원격 운용에서 발생할 수 있는 성능 저하를 재현해야 한다. 시나리오에는 고정 및 가변 지연, 대역폭 감소, 패킷 손실, 센서 중단, 카메라 가림, 지연된 명령, 통신 중단, 운영자 주의 분산, 제어권 인계 및 예상하지 못한 인간의 진입이 포함되어야 한다. 통신 품질이 저하될수록 결합된 인간-기계 시스템(Human-Machine System)이 예측 가능하고 안전한 상태를 유지하는지를 평가해야 한다.

실패 중심 시험(Failure-Oriented Testing)은 의도적으로 통신을 차단하고, 오래된 명령(Stale Commands)을 전달하고, 피드백을 지연시키고, 불완전한 지각 정보를 제공하고, 서로 충돌하는 제어 출처를 생성하며, 원격조작 중 로컬 보호 개입(Local Protective Intervention)을 발생시켜야 한다. 운영자가 로봇을 효과적으로 관찰하거나 제어할 수 없는 경우에도 로봇은 검증된 안전 한계(Validated Safety Limits)를 유지해야 한다. 또한 재연결 이후 오래된 명령이나 안전하지 않은 움직임이 자동으로 다시 활성화되지 않도록 복구 과정도 시험해야 한다.

원격조작(Teleoperation)과 원격 안전(Remote Safety)은 궁극적으로 제어 권한(Control Authority)과 기본적인 보호 기능(Fundamental Protection)을 분리해야 한다. 원격 인간 운영자는 판단, 상황적 추론, 숙련된 조작 및 예외 처리를 제공할 수 있으며, 로봇은 로컬 지각, 움직임 제약, 보호 대응 및 안전한 성능 저하(Safe Degradation)를 유지한다. 원격 감독과 로컬 안전 권한(Local Safety Authority)을 결합함으로써 물리 AI 시스템은 네트워크 연결이나 원격 지각을 단일 실패 지점(Single Point of Failure)으로 만들지 않으면서 인간의 능력을 먼 거리까지 확장할 수 있다.

## 05.12. Emergency Intervention Interfaces

![](images/image13.png){width="7.268055555555556in" height="7.268055555555556in"}

비상 개입 인터페이스(Emergency Intervention Interfaces)는 정상적인 자율 또는 감독 프로세스만으로 더 이상 안전을 유지하기 어려운 상황에서 인간이 로봇의 행동을 직접적이고 예측 가능한 방식으로 중단, 제한 또는 종료할 수 있는 메커니즘을 제공한다. 물리 AI 시스템(Physical AI System)에서 이러한 인터페이스는 예상하지 못한 행동, 지각 실패, 제어 결함, 통신 손실 또는 빠르게 전개되는 위험 상황에서도 이해하기 쉽고 접근 가능해야 하는 독립적인 보호 계층(Protection Layer)을 형성한다.

비상 개입(Emergency Intervention)은 일상적인 인간 명령이나 감독 오버라이드(Supervisory Override)와 구별된다. 그 주된 목적이 작업 최적화나 정상적인 제어권 이전이 아니라 즉각적인 위험 감소(Immediate Risk Reduction)이기 때문이다. 감독자는 일반적으로 임무를 일시정지하거나 궤적을 수정할 수 있지만, 비상 개입은 계획, 언어 해석 또는 상위 수준 추론을 기다리지 않고 위험한 움직임을 억제해야 할 수 있다. 이러한 차이는 전체 시스템 아키텍처에서 명확하게 유지되어야 한다.

비상 인터페이스(Emergency Interface)는 인간의 행동과 로봇의 대응 사이에 명확한 관계를 제공해야 한다. 사람이 비상 메커니즘을 작동시켰을 때 결과 상태는 사람이 로봇의 다음 행동을 예상할 수 있을 만큼 결정론적(Deterministic)이어야 한다. 위험과 기계 설계에 따라 움직임 정지, 필요한 경우 액추에이터 전원 차단, 새로운 명령 억제, 안전한 유지 상태(Safe Holding State) 유지 또는 사전에 정의된 다른 보호 대응(Protective Response)을 실행할 수 있다.

물리적 비상 정지 장치(Physical Emergency-Stop Devices)는 즉각적인 행동을 요청할 수 있는 직접적이고 쉽게 인식 가능한 수단을 제공하므로 중요한 개입 메커니즘으로 유지된다. 장치의 배치는 단순히 장비 패키징의 편의성을 기준으로 하는 것이 아니라 실제 운용 중 인간이 접근할 수 있는 위치를 고려해야 한다. 사람은 비상 개입을 활성화하기 위해 추가적인 위험 영역으로 들어갈 필요 없이 예상되는 작업 위치에서 관련 제어 장치를 신속하게 식별하고 접근할 수 있어야 한다.

비상 제어(Emergency Controls)는 일반적인 운용 제어와 시각적·기능적으로 명확하게 구별되어야 한다. 스트레스를 받는 사용자가 보호 기능을 요청하기 전에 복잡한 메뉴를 탐색하거나, 모호한 아이콘을 해석하거나, 현재 어떤 소프트웨어 모드가 활성화되어 있는지를 판단해야 해서는 안 된다. 인터페이스 설계는 비상 상황을 인식한 시점부터 의도된 보호 대응을 시작하기까지 필요한 인지적 및 물리적 단계(Cognitive and Physical Steps)를 최소화해야 한다.

접근성(Accessibility)은 인간과 이동 로봇 사이의 지속적으로 변화하는 물리적 관계를 고려해야 한다. 고정된 산업 기계와 달리 자율 이동 로봇(Autonomous Mobile Robot)은 넓은 공간을 이동하고 다양한 방향에서 사람에게 접근할 수 있다. 따라서 비상 개입에는 로봇 여러 위치에 분산된 제어 장치, 접근 가능한 운영자 스테이션, 원격 장치 또는 환경에 적합한 다른 메커니즘이 필요할 수 있다. 실제 운용 시나리오를 검토하지 않은 상태에서 하나의 인터페이스 위치만으로 충분하다고 가정해서는 안 된다.

가능한 경우 비상 개입은 상위 수준 자율 추론(High-Level Autonomous Reasoning)과 독립적으로 유지되어야 한다. 안전 필수 정지 요청(Safety-Critical Stop Request)이 언어 모델이 문장을 정확하게 해석하거나, 임무 플래너가 새로운 목표를 수락하거나, 클라우드 서비스가 정상적으로 유지되는 것에 의존해서는 안 된다. 고급 인터페이스는 비상 메커니즘을 보완할 수 있지만 상위 수준 지능이 사용할 수 없거나 예상과 다르게 동작하는 경우에도 가장 짧고 신뢰할 수 있는 보호 경로(Protective Pathway)를 사용할 수 있어야 한다.

원격 운용(Remote Operation)이나 플릿 감독(Fleet Supervision)을 사용하는 경우 로컬 개입(Local Intervention)이 특히 중요하다. 원격 운영자가 비상 대응을 요청할 수 있지만 네트워크 지연이나 통신 장애로 인해 명령이 제시간에 도착하지 않을 수 있다. 따라서 로봇 주변에 실제로 존재하는 사람은 로컬에서 접근 가능한 보호 메커니즘을 사용할 수 있어야 하며, 로봇 자체도 원격 연결 없이 작동할 수 있는 자율 보호 기능(Autonomous Protective Functions)을 유지해야 한다.

원격 비상 개입(Remote Emergency Intervention)은 운영자가 먼 거리에서 로봇을 감독하는 경우 추가적인 보호 계층을 제공할 수 있다. 인터페이스는 비상 요청이 전송되었는지, 수신되었는지, 수락되었는지, 그리고 실제 물리적 대응이 완료되었는지를 명확하게 구별해야 한다. 원격 화면에서 버튼을 성공적으로 눌렀다는 사실만으로 로봇이 정지했다고 판단해서는 안 되며, 검증된 로봇 상태(Verified Robot State)가 예상된 대응을 확인해야 한다.

통신 상태(Communication Health)는 원격 비상 인터페이스의 신뢰성에 영향을 미친다. 네트워크 지연, 패킷 손실, 연결 중단 또는 혼잡은 신속한 대응이 필요한 바로 그 순간에 원격 개입을 불확실하게 만들 수 있다. 따라서 원격 비상 제어는 로컬 안전 기능을 대체하는 것이 아니라 보완해야 한다. 지속적인 원격 감독이 운용의 필수 조건이라면 통신 채널 손실 자체가 사전에 정의된 안전한 성능 저하(Safe Degradation)를 발생시켜야 한다.

비상 개입은 인간 탐지(Human Detection), 안전 영역(Safety Zones), 충돌 회피(Collision Avoidance), 속도 및 분리 모니터링(Speed and Separation Monitoring)과 같은 자율 보호 행동과 함께 작동해야 한다. 이러한 메커니즘은 사람이 개입하기로 결정하기 전에 작동하여 발생 중인 위험이 비상 상황으로 확대되는 것을 방지할 수 있다. 인간 비상 인터페이스는 자동화된 보호 기능이 불충분하거나, 불확실하거나, 사용할 수 없거나, 사람이 로봇이 알지 못하는 상황 정보를 가지고 있을 때 추가적인 대응 경로를 제공한다.

시스템은 비상 개입 이후 어떤 동작이 계속 활성화될 수 있는지를 정의해야 한다. 하나의 움직임을 정지시켰지만 다른 서브시스템이 예상하지 못하게 계속 작동한다면 2차 위험(Secondary Hazards)이 발생할 수 있다. 이동 베이스, 매니퓰레이터, 도구, 페이로드 메커니즘, 컨베이어 또는 기타 구동 구성요소를 함께 고려해야 할 수 있다. 따라서 비상 대응은 주 구동 메커니즘만 정지하면 항상 안전하다고 가정하는 대신 전체 물리 시스템(Complete Physical System)을 고려해야 한다.

저장 에너지(Stored Energy)는 명령된 움직임이 중단되더라도 물리적 위험이 반드시 제거되는 것은 아니므로 특별히 고려해야 한다. 중력, 매달린 하중, 스프링, 유압 또는 공압, 회전 부품, 열에너지 및 전기적으로 활성화된 메커니즘은 제어 명령이 제거된 이후에도 위험할 수 있다. 비상 인터페이스의 동작은 개입 과정에서 저장 에너지가 의도하지 않게 방출되거나 시스템이 불안정해지지 않도록 기계의 물리적 안전 설계(Physical Safety Design)와 연계되어야 한다.

보호 정지(Protective Stop)와 비상 정지(Emergency Stop)를 동일한 개념으로 취급해서는 안 된다. 보호 정지는 정상적인 운용 중 안전 조건이 위반될 때 자동으로 발생할 수 있는 반면, 비상 개입은 인간의 행동이 필요한 비정상적이거나 위험한 상황을 대상으로 한다. 구체적인 구현 방식은 기계와 응용 분야에 따라 달라지지만 개념적인 구분을 유지하면 일상적인 보호 이벤트가 비상 메커니즘의 중요성을 약화시키는 것을 방지할 수 있다.

리셋 동작(Reset Behavior)은 활성화 동작만큼 중요하다. 비상 인터페이스를 해제하거나 리셋했다고 해서 로봇 움직임이 자동으로 다시 시작되어서는 안 된다. 리셋은 개입 메커니즘이 다시 사용할 준비 상태로 복원되었다는 의미이며 반드시 움직임에 대한 허가가 부여되었다는 의미는 아니다. 시스템은 능동 운용으로 복귀하기 전에 적절한 검증 또는 별도의 의도적인 재시작 동작(Deliberate Restart Action)을 요구해야 한다.

재시작 전에 로봇은 비상 개입을 발생시킨 조건을 다시 평가해야 한다. 인간 위치, 장애물, 안전 영역, 액추에이터 상태, 위치추정 품질(Localization Quality), 페이로드 상태, 활성 결함, 통신 상태 및 작업 맥락이 비상 상황 동안 변경되었을 수 있다. 이러한 재평가 없이 이전 궤적을 다시 실행하면 기존 위험을 재현하거나 새로운 위험을 발생시킬 수 있다. 따라서 복구(Recovery)는 새로운 안전 관련 상태 전환(Safety-Relevant State Transition)으로 처리해야 한다.

비상 개입 이후의 제어 권한(Control Authority)은 명확해야 한다. 시스템은 누가 개입을 리셋할 수 있는지, 누가 재시작을 승인할 수 있는지, 추가 검사 또는 유지보수가 필요한지를 정의해야 한다. 일부 환경에서는 비상 제어를 활성화한 사람이 운용 재개를 승인할 권한을 가진 사람이 아닐 수 있다. 명확한 권한 체계는 빠른 생산 복구에 대한 압박으로 인해 필요한 안전 점검이 우회되는 것을 방지한다.

로봇은 이해하기 쉬운 시각, 청각 또는 기타 적절한 신호를 통해 비상 상태(Emergency State)를 전달해야 한다. 주변 사람과 원격 운영자는 비상 개입이 활성화되어 있으며 정상적인 자율 실행이 억제되어 있다는 사실을 확인할 수 있어야 한다. 상태 전달(Status Communication)은 또한 활성 비상 상태를 정상 일시정지, 보호 정지, 통신 손실 또는 유지보수 상태와 구별하여 모드 혼동(Mode Confusion)을 감소시켜야 한다.

자연어(Natural Language)는 비상 상호작용을 지원할 수 있지만 중요한 개입을 위한 유일한 경로가 되어서는 안 된다. "정지(Stop)"와 같은 짧은 표현은 물리적 제어 장치에 즉시 접근하기 어려운 경우 유용한 보조 제어 수단을 제공할 수 있다. 그러나 음성 인식은 소음, 억양, 여러 화자, 마이크 고장 또는 의미적 불확실성의 영향을 받을 수 있다. 즉각적이고 신뢰성 있는 개입이 필요한 경우 전용 보호 메커니즘(Dedicated Protective Mechanisms)이 최종적인 권한을 유지해야 한다.

공유 제어(Shared Control)와 원격조작(Teleoperation) 인터페이스는 비상 권한(Emergency Authority)을 준수해야 한다. 인간의 조향 명령, 자율 플래너 출력, 대기 중인 궤적, 원격 명령 및 작업 지시는 활성 비상 상태와 충돌하는 경우 억제되어야 한다. 비상 개입은 정상적인 제어 중재(Control Arbitration)보다 상위에 위치하여 보호 조건이 활성화된 동안 낮은 우선순위의 명령 출처가 위험한 움직임을 우발적으로 복원하지 못하도록 해야 한다.

소프트웨어 인터페이스(Software Interfaces)를 통해 비상 기능을 제공할 수 있지만 복잡한 소프트웨어 경로에 의존하면 추가적인 실패 가능성이 발생한다. 화면 정지, 애플리케이션 충돌, 사용할 수 없는 터치스크린, 운영체제 결함 또는 네트워크 장애는 소프트웨어 제어의 작동을 방해할 수 있다. 위험 수준이 높은 신뢰성의 개입을 요구하는 경우 시스템은 범용 사용자 인터페이스(General-Purpose User Interface)에만 의존하지 않고 충분히 독립적인 보호 경로를 제공해야 한다.

런타임 보증(Runtime Assurance)은 비상 개입이 예상된 물리적 대응을 실제로 발생시키는지를 모니터링해야 한다. 시스템은 인터페이스 활성화, 명령된 액추에이터 상태, 측정 속도, 브레이크 상태, 전원 상태 및 기타 관련 피드백을 비교할 수 있다. 움직임을 정지시켜야 하는 개입 이후에도 로봇이 계속 움직인다면 이러한 불일치는 단순한 인터페이스 오류가 아니라 에스컬레이션이 필요한 중대한 결함(Critical Fault)으로 처리해야 한다.

진단(Diagnostics)은 비상 인터페이스가 활성화된 것과 의도된 안전 대응이 성공적으로 완료된 것을 구별해야 한다. 버튼 회로는 활성화를 나타내더라도 기계적 또는 제어 결함으로 인해 완전한 정지가 이루어지지 않을 수 있다. 명령 신호에만 의존하는 것보다 실제 물리 상태(Actual Physical State)를 모니터링하는 것이 더 강력한 보증을 제공한다. 이러한 구분은 대형 로봇, 높은 관성을 가진 플랫폼, 매니퓰레이터 또는 무거운 페이로드를 운반하는 시스템에서 특히 중요하다.

비상 이벤트(Emergency Events)는 추적 가능성과 시스템 개선을 위해 기록되어야 한다. 관련 정보에는 개입 출처, 활성화 시간, 로봇 상태, 활성 작업, 주변 위험, 제어 모드, 통신 상태, 안전 시스템 대응, 정지 행동, 결함, 리셋 및 재시작 권한이 포함될 수 있다. 이러한 기록은 사고 분석, 검증, 유지보수, 운영자 교육 및 자동화된 안전 메커니즘을 통해 더 일찍 예방해야 하는 반복적인 위험 조건의 식별을 지원한다.

사이버보안(Cybersecurity)은 특히 원격 또는 네트워크에 연결된 비상 제어의 경우 비상 인터페이스에도 적용된다. 권한이 없는 사용자가 반복적으로 개입을 발생시켜 운용을 방해하거나 비상 상태를 거짓으로 해제할 수 있어서는 안 된다. 동시에 보안 절차가 정당한 보호 행동에 과도한 지연을 발생시켜서도 안 된다. 아키텍처는 신속한 비상 활성화와 더욱 엄격한 인증이 필요한 리셋, 구성 변경 및 재시작 권한을 구분해야 한다.

평가(Evaluation)는 실제 인간 위치와 현실적인 운용 조건에서 개입을 시험해야 한다. 시나리오에는 움직이는 로봇, 접근이 방해된 환경, 낮은 가시성, 높은 소음, 운영자의 주의 분산, 여러 로봇, 원격 운용, 통신 성능 저하 및 예상하지 못한 자율 행동이 포함되어야 한다. 평가 지표에는 위험 탐지에서 행동까지의 시간(Detection-to-Action Time), 인터페이스 접근성, 정지 대응, 상태 명확성, 재시작 규율(Restart Discipline), 사용자가 결과적인 로봇 상태를 정확하게 이해하는지가 포함될 수 있다.

실패 중심 시험(Failure-Oriented Testing)은 접근할 수 없는 제어 장치, 고장난 스위치, 통신 장애, 지연된 소프트웨어 대응, 잘못된 상태 표시, 불완전한 액추에이터 정지, 오래된 명령(Stale Commands), 예상하지 못한 재시작 시도 및 동시다발적인 결함을 검토해야 한다. 목표는 정상 운용 중 비상 버튼이 작동한다는 것만 입증하는 것이 아니라 다른 시스템 구성요소가 이미 성능 저하 상태에 있는 경우에도 전체 개입 아키텍처가 효과적으로 작동하는지를 검증하는 것이다.

비상 개입 인터페이스(Emergency Intervention Interfaces)는 궁극적으로 자율적인 물리적 행동 주변에 인간이 접근할 수 있는 안전 경계(Human-Accessible Safety Boundary)를 형성한다. 자동화된 지능, 정상적인 감독 또는 상황 이해가 충분하지 않은 경우 사람이 로봇을 신속하게 제한할 수 있도록 하며, 인간의 개입이 지연되거나 불가능한 경우에는 로컬 보호 메커니즘(Local Protective Mechanisms)이 안전을 유지한다. 결정론적 정지, 명확한 상태 전달, 통제된 복구, 런타임 보증 및 독립적 보호(Independent Protection)와 통합함으로써 비상 개입 인터페이스는 인간-로봇 안전의 핵심적인 최종 보호 계층(Final Protection Layer)을 형성한다.

## 05.13. Trust Transparency and Predictability

![](images/image14.png){width="7.268055555555556in" height="7.268055555555556in"}

인간-로봇 상호작용(Human--Robot Interaction)에서 신뢰(Trust)는 지능형 로봇이 신뢰할 수 있다는 일반적인 믿음이 아니라 보정된 운용 관계(Calibrated Operational Relationship)로 다루어져야 한다. 신뢰할 수 있는 물리 AI 시스템(Physical AI System)은 자신이 무엇을 할 수 있는지, 어떤 한계가 존재하는지, 변화하는 조건에서 어떻게 행동할지를 사람이 이해할 수 있도록 해야 한다. 효과적인 안전은 인간의 기대를 실제 시스템 역량과 일치시켜 과도한 신뢰와 불필요한 불신이 의사결정을 왜곡하지 않도록 하는 데 달려 있다.

신뢰 보정(Trust Calibration)은 고도화된 로봇이 실제 역량보다 더 뛰어나 보일 수 있기 때문에 특히 중요하다. 유창한 언어, 부드러운 내비게이션, 인간과 유사한 설명 또는 성공적인 시연은 사용자가 한 영역에서 확인된 능력을 다른 영역까지 일반화하도록 만들 수 있다. 따라서 인터페이스는 역량 경계(Capability Boundaries)와 불확실성을 전달하여 익숙한 상황에서의 인상적인 행동이 익숙하지 않거나 안전 필수적인 상황에서 근거 없는 신뢰로 이어지지 않도록 해야 한다.

과소 신뢰(Undertrust) 역시 운용상의 문제를 발생시킬 수 있다. 사용자가 로봇이 왜 감속하고, 정지하고, 경로를 변경하거나, 지원을 요청하는지 이해하지 못하면 올바른 보호 행동을 낮은 성능으로 잘못 해석할 수 있다. 그 결과 자율 시스템을 반복적으로 오버라이드하거나 유용한 기능을 사용하지 않거나 비효율적인 수동 절차를 도입할 수 있다. 따라서 투명성(Transparency)은 의도적인 보호 행동과 오작동 또는 불충분한 역량을 구별할 수 있을 만큼 시스템의 추론과 안전 상태를 보여주어야 한다.

투명성은 모든 내부 계산을 공개하는 것을 의미하지 않는다. 현대의 물리 AI 시스템에는 지각 모델(Perception Models), 월드 모델(World Models), 플래너(Planners), 파운데이션 모델(Foundation Models), 안전 모니터(Safety Monitors), 제어 시스템(Control Systems)이 포함될 수 있으며, 이들의 전체 내부 상태는 대부분의 사용자에게 과도한 정보를 제공할 수 있다. 유용한 투명성은 로봇이 현재 상황을 어떻게 이해하는지, 무엇을 하려고 하는지, 어떤 제약이 활성화되어 있는지, 얼마나 확신하는지, 언제 인간의 개입이 필요한지와 같이 행동에 도움이 되는 정보를 제시한다.

예측 가능성(Predictability)은 인간이 로봇의 행동이 발생하기 전에 그 행동에 대한 신뢰할 수 있는 기대를 형성할 수 있는지를 의미한다. 예측 가능한 로봇이 모든 상황에서 동일한 행동을 수행해야 하는 것은 아니다. 대신 유사한 상황에서는 이해 가능한 정책과 제약에 일관된 행동이 나타나야 한다. 위험, 불확실성, 권한 또는 환경 조건의 변화로 행동이 달라지는 경우에도 그 변화의 이유는 주변 사람과 운영자가 충분히 이해할 수 있어야 한다.

움직임(Motion) 자체도 중요한 의사소통 채널이다. 부드러운 가속, 조기 감속, 안정적인 궤적, 명확한 정지 행동 및 의도적인 양보는 로봇의 의도를 사람이 쉽게 예상하도록 할 수 있다. 갑작스러운 방향 전환, 설명되지 않는 일시정지, 진동하는 궤적 또는 늦은 장애물 회피는 충돌을 피했더라도 신뢰를 낮출 수 있다. 따라서 물리적 행동은 동역학적 실행 가능성(Dynamic Feasibility)뿐만 아니라 같은 환경을 공유하는 인간이 쉽게 이해할 수 있는 가독성(Legibility)을 고려하여 설계해야 한다.

로봇 의도 전달(Robot Intent Communication)은 움직임이 시작되기 전에 예측 가능성을 향상시킬 수 있다. 시각 표시, 투영된 경로(Projected Paths), 디스플레이, 청각 신호, 제스처 또는 기타 신호를 이용하여 로봇이 진행, 정지, 양보, 후진, 물체 조작 또는 대기 중 무엇을 수행하려는지를 전달할 수 있다. 이러한 신호는 실제 제어 상태와 밀접하게 일치해야 한다. 플래너가 여전히 불확실한 상황에서 인터페이스가 "진행해도 안전함"을 표시한다면 아무런 신호를 제공하지 않는 것보다 더 큰 위험을 발생시킬 수 있다.

인터페이스 간 일관성(Consistency Across Interfaces)도 중요하다. 상태 표시등, 원격 대시보드, 음성 설명, 모바일 애플리케이션 및 실제 로봇 행동이 동일한 상태에 대해 서로 충돌하는 해석을 제공해서는 안 된다. 보호 영역(Protective Zone)에 사람이 있기 때문에 로봇이 정지했다면 로컬 인터페이스와 원격 인터페이스는 서로 일치하는 정보를 전달해야 한다. 일관된 의미 체계(Consistent Semantics)는 모드 혼동(Mode Confusion)을 줄이고 사용자가 시스템에 대한 안정적인 정신 모델(Mental Model)을 형성하도록 한다.

설명(Explanations)은 간결하고 관련성이 높으며 관찰 가능한 행동과 연결되어야 한다. 로봇이 정지한 경우 단순히 오류가 발생했다고 표시하는 것보다 "보호 영역에서 사람 탐지", "경로 차단", "위치추정 신뢰도 부족"과 같은 설명이 더 유용하다. 설명은 시스템이 실제로 가진 것보다 더 높은 확실성을 암시하지 않으면서 행동에 영향을 미치는 조건을 명확하게 식별해야 한다.

불확실성(Uncertainty)은 사용자와 작업에 적합한 형태로 전달되어야 한다. 엔지니어는 정량적인 신뢰도 값(Quantitative Confidence Values)을 활용할 수 있지만 운영자는 정상, 성능 저하, 불확실, 개입 필요와 같은 범주가 필요할 수 있다. 주변의 일반 사용자는 단순한 행동 신호만 필요할 수도 있다. 목적은 불확실성 자체를 보여주는 것이 아니라 각 사용자가 로봇이 안전하게 계속 운용될 수 있는지, 감독이 필요한지 또는 접근을 피해야 하는지를 판단하도록 지원하는 것이다.

투명성은 현재 상태뿐만 아니라 한계(Limitations)도 포함해야 한다. 사용자는 관련 센싱 사각지대(Sensing Blind Spots), 운용 경계, 페이로드 제약, 환경적 제한, 통신 의존성 및 지원되지 않는 작업을 이해해야 한다. 실패가 발생한 이후에야 드러나는 한계는 위험한 기대를 형성할 수 있다. 자신이 안정적으로 수행할 수 없는 것을 명확하게 전달하는 시스템은 모든 작업을 수행할 수 있는 것처럼 보이지만 예측할 수 없게 실패하는 시스템보다 더 높은 정당한 신뢰(Justified Trust)를 형성할 수 있다.

예측 가능한 실패 행동(Predictable Failure Behavior)은 특히 중요하다. 지각 신뢰도가 낮아지거나, 통신이 손실되거나, 위치추정 성능이 저하되거나, 계획이 불확실해질 경우 로봇은 설명할 수 없는 행동을 계속하는 대신 알려진 성능 저하 모드(Degraded Modes)로 전환해야 한다. 감속, 위치 유지, 지원 요청, 후퇴 또는 최소 위험 상태(Minimum-Risk Condition)로의 전환은 불확실성에 대한 이해 가능한 대응을 제공하며 정상적인 자율 기능을 사용할 수 없을 때 사람이 다음 행동을 예상하도록 한다.

모드 인식(Mode Awareness)은 투명성과 예측 가능성을 모두 지원한다. 사용자는 로봇이 자율 운전 중인지, 공유 제어(Shared Control) 상태인지, 원격조작(Teleoperation) 중인지, 확인을 기다리고 있는지, 보호 정지(Protective Stop)를 수행 중인지 또는 성능 저하 모드에서 동작하는지를 알아야 한다. 숨겨진 모드 변경은 책임과 향후 행동에 대한 잘못된 가정을 발생시킬 수 있다. 특히 자율 시스템과 인간 운영자 사이에서 권한이 이전될 때 명확한 모드 표시가 중요하다.

인간 명령(Human Commands)은 시각적 또는 다른 방식으로 이해 가능한 확인 응답(Acknowledgment)을 발생시켜야 한다. 사용자는 명령이 수신되었는지, 해석되었는지, 수락되었는지, 안전 제약에 의해 수정되었는지, 거부되었는지 또는 완료되었는지를 알 수 있어야 한다. 이러한 피드백이 없으면 사람은 명령을 반복하거나 실제로 수행되지 않은 행동이 완료되었다고 가정할 수 있다. 상호작용 루프(Interaction Loop)를 완성하면 로봇의 대응을 더욱 예측 가능하게 만들고 자율성과 인간 제어 인터페이스에 대한 적절한 신뢰를 지원한다.

신뢰는 설득력 있는 언어(Persuasive Language)에 의존해서는 안 된다. 로봇은 자연어 설명을 제공할 수 있지만 신뢰는 대화의 유창성이 아니라 일관된 행동, 검증된 역량, 투명한 상태 및 신뢰할 수 있는 보호 기능에서 형성되어야 한다. 물리 AI 시스템은 불확실한 추론을 확정된 사실처럼 제시하거나 사용자가 적절한 검증 없이 의사결정을 받아들이도록 유도하는 권위적인 표현을 사용해서는 안 된다.

설명은 자율 의사결정(Autonomous Decisions)과 안전 강제 제약(Safety-Enforced Constraints)도 구별해야 한다. 플래너는 혼잡을 예측하여 더 긴 경로를 선택할 수 있지만, 안전 시스템은 보호 영역이 활성화되어 더 짧은 경로를 금지할 수 있다. 이들은 서로 다른 형태의 시스템 행동이다. 행동이 최적화, 불확실성 관리, 인간 지시 또는 의무적인 안전 강제 중 무엇에 의해 발생했는지를 보여주면 사용자는 어떤 요소를 변경할 수 있고 어떤 요소가 최종적인 권한을 유지하는지를 이해할 수 있다.

신뢰는 반복적인 상호작용을 통해 시간에 따라 변화한다. 성공적인 운용은 신뢰를 높일 수 있지만 설명되지 않은 실패는 신뢰를 빠르게 낮출 수 있다. 따라서 시스템은 여러 임무와 소프트웨어 업데이트 전반에서 행동 일관성(Behavioral Consistency)을 유지해야 한다. 내비게이션 방식, 경고 행동, 제어 권한 또는 개입 임계값이 크게 변경되는 경우 이전에 학습된 인간의 기대가 업데이트된 로봇과 더 이상 일치하지 않을 수 있으므로 이러한 변경을 전달하고 검증해야 한다.

다중 로봇 환경(Multi-Robot Environments)에서는 서로 다른 역량이나 구성을 가진 로봇과 사람이 상호작용할 수 있으므로 추가적인 일관성이 필요하다. 양보 행동, 경고 신호, 상태 표시, 안전 영역 및 개입 인터페이스에 공통 규칙(Shared Conventions)을 적용하면 각 로봇을 개별적으로 학습해야 하는 필요성을 줄일 수 있다. 로봇들의 행동이 서로 다른 경우 표면적으로 동일한 인터페이스 뒤에 그 차이를 숨기기보다 명확하게 전달해야 한다.

플릿 감독(Fleet Supervision)에는 여러 수준의 투명성이 필요하다. 운영자는 정상적인 플릿 운용에 대한 간결한 개요를 확인하면서 이상이 발생하면 개별 로봇을 자세히 검사할 수 있어야 한다. 인터페이스는 지각 성능 저하, 차단된 작업, 통신 문제, 안전 개입 또는 지원 요청이 발생한 로봇의 우선순위를 높일 수 있다. 투명성은 모든 자율 행동을 지속적으로 관찰하도록 강요하는 대신 의미 있는 예외 상황에 인간의 주의를 집중시켜야 한다.

런타임 보증(Runtime Assurance)은 로봇이 전달하는 상태와 실제 물리적 행동이 일치하는지를 확인함으로써 신뢰 형성에 기여한다. 인터페이스가 로봇이 정지했다고 표시한다면 측정된 움직임이 해당 상태를 확인해야 한다. 로봇이 장애물이 제거되었다고 판단한다면 지각 및 안전 모니터링이 다시 움직이기 위한 상태 전환을 뒷받침해야 한다. 보고된 상태와 실제 상태 사이의 불일치를 탐지함으로써 투명성 메커니즘이 단순한 외형적 기능에 그치는 것을 방지한다.

로깅 및 추적 가능성(Logging and Traceability)은 사건 이후 더욱 심층적인 투명성을 제공한다. 기록에는 지각 상태, 계획된 행동, 안전 제약, 인간 명령, 제어 모드, 경고, 개입 및 결과적인 움직임이 포함될 수 있다. 이러한 기록을 통해 엔지니어와 운영자는 특정 행동이 왜 발생했는지를 재구성하고 그 원인이 환경적 불확실성, 자율 계획, 인간 입력, 통신 실패 또는 시스템 결함 중 무엇인지를 판단할 수 있다.

개인정보 보호(Privacy)와 보안(Security)은 투명성의 범위를 적절하게 제한해야 한다. 유용한 설명을 제공한다는 것이 민감한 센서 데이터, 개인정보, 독점 모델, 인증 정보 또는 보안상 중요한 구현 세부사항을 공개한다는 의미는 아니다. 서로 다른 이해관계자(Stakeholders)는 서로 다른 접근 수준을 필요로 할 수 있다. 투명성은 개인정보 보호, 사이버보안 및 운용 기밀성을 존중하면서 안전한 이해와 책임성(Accountability)에 필요한 충분한 정보를 제공해야 한다.

신뢰 평가(Trust Evaluation)는 사용자에게 단순히 로봇을 좋아하거나 신뢰하는지를 질문하는 것이 아니라 신뢰 보정 정도를 측정해야 한다. 사용자는 시스템이 충분한 역량을 가지고 있을 때 적절하게 의존하고 감독이나 개입이 필요한 상황을 정확하게 인식해야 한다. 실험에서는 사용자가 인식하는 역량과 실제 역량을 비교하고, 불확실성에 대한 대응을 조사하며, 설명이 단순히 주관적인 신뢰를 높이는 것이 아니라 로봇 행동을 정확하게 예측하는 능력을 향상시키는지를 평가할 수 있다.

예측 가능성 시험(Predictability Testing)은 사용자가 정상 운용, 성능 저하 조건, 안전 개입, 모호한 상황 및 복구 과정을 경험하도록 해야 한다. 연구자는 사용자가 정지, 양보, 경로 변경, 지원 요청 또는 최소 위험 상태 진입을 올바르게 예상하는지를 측정할 수 있다. 예상하지 못한 행동은 단순히 제어 문제로만 분석해서는 안 되며, 기술적으로 올바른 행동이라도 인간이 이해하기 어렵다면 상호작용 문제(Interaction Problem)로도 분석해야 한다.

실패 중심 평가(Failure-Oriented Evaluation)는 오해를 유발하는 표시, 지연된 상태 갱신, 일관되지 않은 설명, 잘못된 신뢰도 추정, 숨겨진 모드 변경, 서로 모순되는 인터페이스 및 이전에 형성된 기대를 위반하는 행동을 검토해야 한다. 목적은 시스템이 불확실하거나 성능이 저하된 상황에서도 투명성이 신뢰성을 유지하도록 하는 것이다. 비정상적인 조건에서 잘못된 확신(Misleading Confidence)을 제공하는 것은 제한된 역량을 명확하게 전달하는 것보다 더 위험할 수 있다.

신뢰(Trust), 투명성(Transparency), 예측 가능성(Predictability)은 궁극적으로 인간의 이해(Human Understanding)와 로봇 행동(Robot Behavior) 사이에 피드백 관계(Feedback Relationship)를 형성한다. 투명성은 관련 상태, 의도, 불확실성 및 한계를 보여주고, 예측 가능한 행동은 인간이 정확한 기대를 형성하도록 하며, 전달된 정보와 실제 관찰된 행동이 반복적으로 일치함으로써 보정된 신뢰(Calibrated Trust)가 형성된다. 안전 모니터링, 명확한 권한, 통제된 성능 저하(Controlled Degradation), 검증 가능한 물리적 대응과 통합된 이러한 원칙은 인간이 맹목적인 신뢰나 지속적인 의심에 의존하지 않고 물리 AI와 안전하게 협력할 수 있도록 한다.

## 05.14. Human Robot Interface Safety Evaluation

![](images/image15.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image16.png){width="7.268055555555556in" height="7.268055555555556in"}

인간-로봇 인터페이스 안전 평가(Human--Robot Interface Safety Evaluation)는 사람과 물리 AI 시스템(Physical AI System)을 연결하는 메커니즘이 정상, 성능 저하 및 비상 조건 전반에서 안전하고 이해 가능하며 예측 가능한 상호작용을 지원하는지를 판단한다. 평가는 단순한 인터페이스 사용성(Interface Usability)을 넘어 지각, 의사소통, 명령, 경고, 제어 전환, 인간 개입 및 로봇 대응이 전체 상호작용 수명주기(Interaction Lifecycle)에 걸쳐 안전을 유지하는지를 검증해야 한다.

평가는 인터페이스가 운용될 상호작용 맥락(Interaction Context)을 정의하는 것에서 시작한다. 관련 요소에는 로봇 유형, 작업 공간, 예상 사용자, 주변의 비운영자, 작업 복잡성, 자율성 수준, 환경 조건, 운용 속도, 페이로드 및 잠재적 위험이 포함된다. 감독되는 실험실 로봇에 충분한 인터페이스가 동적인 산업 환경에서 작업자 주변을 운용하는 이동 플랫폼에는 충분하지 않을 수 있다.

평가에서는 인간과 로봇 사이의 모든 안전 관련 상호작용 경로(Safety-Relevant Interaction Pathways)를 식별해야 한다. 여기에는 인간 탐지 및 추적, 근접 모니터링, 로봇 의도 전달, 경고, 자연어 명령, 명령 확인, 공유 제어, 원격조작, 감독 제어, 오버라이드 및 비상 개입이 포함된다. 각 경로는 독립적으로 평가하는 동시에 통합 시스템의 일부로도 평가해야 한다. 개별적으로 정상적인 구성요소 사이의 상호작용에서도 실패가 발생할 수 있기 때문이다.

인간 탐지 성능(Human Detection Performance)은 통제된 장면만이 아니라 실제 운용 조건에서 평가해야 한다. 시험에는 다양한 신체 방향, 의복, 부분적 가림, 조명 조건, 군중 밀도, 움직임 패턴, 센서 사각지대 및 환경적 혼잡이 포함되어야 한다. 목적은 단순히 탐지 정확도를 측정하는 것이 아니라 누락되거나 지연되거나 불확실한 탐지가 발생했을 때 로봇이 충분히 보수적인 행동(Conservative Behavior)을 수행하는지를 판단하는 것이다.

추적 평가(Tracking Evaluation)는 사람들이 로봇 주변을 움직이는 동안 시스템이 신뢰할 수 있는 인간 상태 추정(Human State Estimates)을 유지하는지를 검토해야 한다. 신원 전환(Identity Switches), 일시적인 가림, 센서 전환, 갑작스러운 움직임 및 여러 명의 주변 사람은 추적 품질을 저하시킬 수 있다. 안전 로직은 이러한 불확실성을 고려하여 추적 대상이 사라졌다는 이유만으로 실제 물리 환경에서 사람이 사라졌다고 판단하거나 기존의 분리 제약을 자동으로 제거해서는 안 된다.

안전 영역(Safety Zones)과 근접 관리(Proximity Management)는 로봇의 전체 운용 영역(Operating Envelope)에 걸쳐 시험해야 한다. 평가에서는 영역 경계가 실제 센싱 및 정지 능력과 일치하는지, 영역 사이의 전환이 의도된 대응을 발생시키는지, 동적 영역(Dynamic Zones)이 속도와 환경 조건에 따라 올바르게 조정되는지를 검증해야 한다. 예상하지 못한 방향에서 사람이 접근하거나 모니터링 영역으로 빠르게 진입하는 상황도 시험에 포함해야 한다.

속도 및 분리 모니터링(Speed and Separation Monitoring)은 전체 지각-정지 체인(Perception-to-Stop Chain)에 대한 평가가 필요하다. 인간 위치 추정, 로봇 속도, 상대 운동, 시스템 지연, 제동 성능, 정지 거리 및 불확실성 여유가 충분한 분리 거리를 유지할 수 있는지에 모두 영향을 미친다. 따라서 소프트웨어 계산의 정확성만 평가해서는 안 되며 실제 물리적 결과를 검증해야 한다. 특히 속도, 지연 및 탐지 불확실성이 최악의 조건으로 결합되는 상황을 중요하게 평가해야 한다.

로봇 의도 전달(Robot Intent Communication)은 사람이 향후 로봇 행동을 올바르게 이해할 수 있는지를 기준으로 평가해야 한다. 시각 표시, 투영 경로(Projected Paths), 청각 신호, 디스플레이, 제스처 및 움직임 단서를 대표 사용자와 함께 시험해야 한다. 중요한 평가 기준은 단순히 신호가 보이거나 들리는지가 아니라 사용자가 이를 올바르게 해석하고 로봇이 진행, 정지, 양보, 후진 또는 다른 관련 행동을 수행할지를 예측할 수 있는지이다.

경고(Warnings)는 탐지 가능성, 긴급성, 의미 및 타이밍을 기준으로 평가해야 한다. 시각 경고는 가시성이 낮거나 사용자가 다른 방향을 보고 있을 때 실패할 수 있으며, 청각 경고는 산업 현장의 소음에 묻힐 수 있다. 햅틱 경고(Haptic Warnings)는 인터페이스와 적절한 물리적 접촉이 필요하다. 다중 양식 경고(Multi-Modal Warnings)는 강건성을 향상시킬 수 있지만 각 경고의 의미는 일관되어야 한다. 또한 가치가 낮은 경고가 지나치게 자주 발생하면 경보 피로(Alarm Fatigue)가 발생할 수 있으므로 이를 평가해야 한다.

자연어 안전 상호작용(Natural-Language Safety Interaction)은 일반적인 음성 인식 정확도 이상의 평가가 필요하다. 시험에는 소음, 억양, 불완전한 표현, 모호한 참조, 간접적인 경고, 여러 화자, 서로 모순되는 명령 및 익숙하지 않은 표현이 포함되어야 한다. 불확실한 언어가 근거 없는 물리적 행동으로 이어지지 않고 명확화(Clarification) 또는 보수적인 행동을 발생시키는지를 평가해야 한다. 긴급 안전 표현의 인식 및 대응 지연시간도 함께 평가해야 한다.

명령 확인(Command Confirmation)은 위험한 오해를 감소시키면서 불필요한 상호작용 부담을 발생시키지 않는지를 시험해야 한다. 중대한 결과를 발생시키지만 긴급하지 않은 명령에는 명시적인 확인이 유용할 수 있지만 즉각적인 보호 명령은 긴 대화로 인해 지연되어서는 안 된다. 또한 로봇이 사용자의 원래 표현을 단순히 반복하는 것이 아니라 대상 물체나 목적지와 같이 자신이 해석한 물리적 의미(Interpreted Physical Meaning)를 확인하는지를 평가해야 한다.

인간 오버라이드(Human Override) 평가는 권한을 가진 인간의 개입이 로봇 행동에 예측 가능한 변화를 발생시키는지를 검증해야 한다. 시험에는 일시정지, 작업 취소, 경로 수정, 수동 제어권 인수 및 기타 지원되는 전환이 포함되어야 한다. 또한 인간 오버라이드가 독립적으로 강제되는 안전 제약(Independently Enforced Safety Constraints)을 조용히 우회할 수 없는지도 확인해야 한다. 오버라이드가 거부되거나 수정될 경우 인터페이스는 요청된 행동을 그대로 수행할 수 없는 이유를 명확하게 전달해야 한다.

공유 제어(Shared Control)는 인간 명령과 자율 명령이 어떻게 상호작용하는지를 검토하여 평가해야 한다. 자율 지원(Autonomous Assistance)은 로봇을 예측 불가능하게 만들거나 정당한 운영자 의도에 저항한다는 느낌을 주지 않으면서 안전을 향상시켜야 한다. 시험에서는 장애물, 근접 제약, 충돌하는 입력 및 급격한 인간 명령을 도입할 수 있다. 인간과 자율 시스템의 목표가 서로 다르더라도 결과적인 움직임은 안정적이고 이해 가능하며 검증된 안전 경계 안에 있어야 한다.

감독 제어(Supervisory Control) 평가는 인간 작업 부하(Human Workload)와 주의 관리(Attention Management)를 포함해야 한다. 하나의 로봇에서는 정상적으로 작동하는 인터페이스라도 한 명의 운영자가 여러 시스템을 동시에 감독하면 안전하지 않을 수 있다. 시험에서는 알림 빈도, 개입 요청, 경보 우선순위, 정보 밀도 및 대응 시간을 검토해야 한다. 목표는 상황이 심각해지기 전에 감독자가 어떤 로봇에 주의가 필요한지와 그 이유를 식별할 수 있는지를 판단하는 것이다.

원격조작 안전 평가(Teleoperation Safety Evaluation)는 현실적인 통신 성능 저하를 재현해야 한다. 고정 지연, 가변 지연, 패킷 손실, 대역폭 감소, 지연된 영상, 센서 중단 및 완전한 연결 단절은 제어 가능성을 크게 변화시킬 수 있다. 통신 품질이 저하될수록 로봇은 원격 명령에 대한 의존성을 낮추고 로컬 보호 기능(Local Protective Functions)을 유지해야 한다. 재연결 시험에서는 물리적 상황이 변경된 이후 오래된 명령(Stale Commands)이 자동으로 실행되지 않는지를 검증해야 한다.

원격조작 중 상황 인식(Situational Awareness)은 대표적인 카메라 배치, 센서 시야, 지도 및 상태 정보를 이용하여 평가해야 한다. 운영자가 사람, 장애물, 여유 공간, 로봇 방향, 매니퓰레이터 구성 및 사각 영역을 식별할 수 있는지를 시험해야 한다. 특히 보이지 않는 영역을 안전하다고 확인된 영역으로 잘못 판단하는 것과 같이 인터페이스의 한계가 잘못된 가정을 유발하는지를 평가해야 한다.

비상 개입 인터페이스(Emergency Intervention Interfaces)는 인간이 접근할 수 있는 최종 보호 계층(Final Human-Accessible Protection Layer)을 나타내므로 별도의 평가가 필요하다. 물리적 및 원격 제어 장치는 접근성, 인식 가능성, 활성화 시간, 결과적인 로봇 대응 및 상태 표시를 기준으로 시험해야 한다. 계획된 시연뿐만 아니라 스트레스가 높고 비정상적인 조건에서도 평가해야 한다. 다른 구성요소가 이미 성능 저하 상태에 있더라도 시스템은 예측 가능한 보호 대응(Protective Response)을 제공해야 한다.

비상 정지 시험(Emergency Stopping Tests)은 개입 이후 실제 물리적 행동을 검토해야 한다. 측정된 속도, 정지 거리, 브레이크 상태, 액추에이터 행동, 페이로드 안정성 및 저장 에너지(Stored Energy)가 모두 관련될 수 있다. 비상 명령이 활성화되었다고 해서 로봇이 예상과 다르게 계속 움직이거나 다른 서브시스템이 위험한 상태로 남아 있다면 위험 감소가 성공적으로 이루어진 것은 아니다. 따라서 검증은 인터페이스 활성화부터 의도된 물리적 대응이 완료될 때까지 이어져야 한다.

복구 및 재시작 행동(Recovery and Restart Behavior)은 정지와 동일한 수준으로 신중하게 평가해야 한다. 개입을 리셋했다고 해서 움직임이 자동으로 다시 시작되어서는 안 된다. 시험에서는 운용을 재개하기 전에 인간 위치, 장애물, 위치추정, 활성 결함, 안전 영역, 통신 상태 및 작업 맥락을 다시 평가하는지를 검증해야 한다. 또한 이전에 대기 중이던 행동이나 오래된 행동이 복구 과정에서 예상하지 못하게 다시 활성화되지 않도록 해야 한다.

신뢰, 투명성 및 예측 가능성(Trust, Transparency, and Predictability)은 단순한 주관적 선호가 아니라 인간의 이해를 통해 평가해야 한다. 사용자에게 정상, 불확실, 성능 저하 및 보호 조건에서 로봇의 행동을 예측하도록 할 수 있다. 평가에서는 표시된 상태, 설명, 경고 및 물리적 행동이 정확한 정신 모델(Mental Model)을 형성하는지를 판단해야 한다. 과도한 신뢰(Overtrust)와 과소 신뢰(Undertrust)가 실제 시스템 역량과 일치하지 않는다면 모두 신뢰 보정(Trust Calibration)의 실패를 의미한다.

모드 인식(Mode Awareness)은 자율, 공유 제어, 원격조작, 감독, 보호 정지 및 성능 저하 상태 전반에서 시험해야 한다. 사용자는 현재 로봇의 움직임을 누가 또는 무엇이 제어하고 있으며 어떤 안전 메커니즘이 계속 활성화되어 있는지를 일관되게 식별할 수 있어야 한다. 숨겨지거나 모호한 전환은 모드 혼동(Mode Confusion)을 발생시켜 운영자가 불필요하게 개입하거나 인간 제어가 필요한 상황에서 개입하지 못할 수 있으므로 안전 문제로 다루어야 한다.

인터페이스 일관성(Interface Consistency)은 물리적 표시 장치, 디스플레이, 원격 대시보드, 음성 메시지, 모바일 인터페이스 및 실제 로봇 행동 전반에서 검토해야 한다. 동일한 시스템 상태가 서로 다른 채널에서 다르게 표현되어서는 안 된다. 시험에서는 의도적으로 상태 전환과 결함을 발생시켜 모든 관련 인터페이스가 동기화된 상태를 유지하는지를 검증해야 한다. 서로 모순되는 상태 정보는 상황 인식과 안전 메커니즘에 대한 신뢰를 모두 약화시킬 수 있다.

인간 요소 평가(Human Factors Evaluation)는 개발자나 전문 운영자에게만 의존하지 않고 대표적인 사용자를 포함해야 한다. 경험, 교육 수준, 신체 능력, 언어 친숙도, 주의력, 스트레스, 피로 및 보호 장비는 상호작용에 영향을 미칠 수 있다. 중요한 제어 장치, 경고, 설명 및 로봇 행동이 시스템 설계에 이미 익숙한 사람에게만 이해되는 것이 아니라 현실적인 작업 조건에서도 이해 가능한지를 평가해야 한다.

시나리오 기반 평가(Scenario-Based Evaluation)는 현실적인 작업 안에서 여러 인터페이스 기능을 결합해야 한다. 로봇이 원격조작되는 동안 사람이 안전 영역에 진입하고, 동시에 통신 지연이 증가하며, 운영자가 오버라이드를 요청하고, 경고가 발생할 수 있다. 이러한 통합 시나리오는 개별 구성요소 시험만으로 발견할 수 없는 상호작용 실패를 드러낸다. 따라서 안전 평가는 구성요소 검증에서 시작하여 완전한 인간-로봇 운용 시나리오로 점진적으로 확장되어야 한다.

실패 중심 시험(Failure-Oriented Testing)은 탐지 누락, 모호한 명령, 잘못된 추적, 지연된 경고, 오래된 제어 입력, 통신 손실, 모드 혼동, 확인 실패, 사용할 수 없는 디스플레이 및 충돌하는 명령을 의도적으로 발생시켜야 한다. 목적은 개별 인터페이스의 실패가 즉각적으로 위험한 물리적 행동으로 이어지지 않는지를 검증하는 것이다. 통신 또는 상호작용 메커니즘의 신뢰성이 저하되면 시스템은 보수적으로 성능을 저하시키고 독립적인 보호 기능(Independent Protection)을 유지해야 한다.

평가 지표(Evaluation Metrics)는 인터페이스 성능을 실제 물리적 안전 결과와 연결해야 한다. 관련 지표에는 탐지에서 대응까지의 시간(Detection-to-Response Time), 경고 인식, 명령 해석 정확도, 개입 지연시간, 정지 거리, 최소 분리 거리, 운영자 작업 부하, 모드 인식, 행동 예측 정확도, 오경보(False Alarms), 미탐지 경보(Missed Alarms) 및 성공적인 복구가 포함될 수 있다. 안전한 상호작용은 인간, 인터페이스, 자율 시스템 및 물리 제어의 결합된 성능에서 발생하므로 하나의 지표만으로 충분하지 않다.

추적 가능성(Traceability)은 평가 결과를 위험, 안전 요구사항, 인터페이스 기능, 시험 시나리오 및 관찰된 결과와 연결해야 한다. 실패가 발견되었을 때 엔지니어는 어떤 요구사항이 위반되었으며 어떤 설계 요소를 개선해야 하는지를 판단할 수 있어야 한다. 로봇 상태, 인간 명령, 지각 출력, 제어 모드, 경고, 개입 및 물리적 대응에 대한 로그는 검증(Validation)과 시험 후 분석(Post-Test Analysis)을 위한 증거를 제공할 수 있다.

인간-로봇 인터페이스 안전 평가(Human--Robot Interface Safety Evaluation)는 궁극적으로 조건이 완벽하지 않은 상황에서도 인간과 자율 물리 AI(Autonomous Physical AI)가 조정된 상태를 유지할 수 있는지를 검증한다. 안전한 인터페이스는 사람이 로봇 상태를 인식하고, 의도를 이해하고, 명령을 전달하고 확인하며, 필요한 경우 개입하고, 실패와 복구 과정에서 어떤 일이 발생할지를 예상할 수 있도록 해야 한다. 인간 요소, 물리적 시험, 불확실성, 실패 주입(Failure Injection), 런타임 증거(Runtime Evidence) 및 통합 시나리오를 결합함으로써 평가는 전체 상호작용 시스템이 의미 있는 인간 제어(Meaningful Human Control)와 신뢰할 수 있는 물리적 보호(Dependable Physical Protection)를 유지하는지를 입증한다.
