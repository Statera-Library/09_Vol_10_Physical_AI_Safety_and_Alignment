**Volume 10. Physical AI Safety and Alignment**


# Chapter 07. Monitoring and Runtime Assurance

##  

## 07.01. Runtime Assurance Fundamentals

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Runtime assurance provides a safety layer that supervises an autonomous Physical AI system while it is operating. Instead of assuming that perception, planning, learned policies, or world models will always behave correctly, runtime assurance continuously evaluates whether the current system state and proposed behavior remain compatible with defined safety requirements and operational constraints.

The central motivation for runtime assurance is that many Physical AI components cannot be completely verified before deployment. Learned models may encounter unfamiliar environments, distribution shifts, sensor degradation, ambiguous human behavior, or combinations of conditions absent from training. Runtime assurance therefore complements design-time verification by detecting unsafe conditions during actual operation.

A runtime assurance architecture generally separates performance-oriented intelligence from safety-oriented supervision. The primary controller may use neural networks, reinforcement learning, VLA policies, world models, or sophisticated optimization to achieve mission objectives. A more constrained assurance mechanism independently determines whether proposed actions remain inside an acceptable region of behavior.

This separation is especially important because high-performance AI and safety mechanisms have different objectives. The primary AI seeks efficient, adaptive, and capable behavior, whereas the assurance layer prioritizes constraint satisfaction and risk reduction. Independence prevents a failure inside the primary decision process from automatically disabling the mechanism responsible for detecting that failure.

Runtime assurance operates by observing relevant states, actions, trajectories, environmental conditions, and system health indicators. These observations can include robot velocity, distance to humans, localization confidence, predicted collision probability, actuator status, compute latency, battery state, model uncertainty, and sensor consistency. Their combination provides evidence about whether operation remains trustworthy.

Safety constraints transform this evidence into enforceable operational boundaries. Constraints may define maximum velocity, minimum separation distance, permitted workspace regions, stability conditions, actuator limits, timing deadlines, or acceptable uncertainty. The assurance mechanism evaluates current and predicted behavior against these boundaries before hazardous conditions become irreversible.

Monitoring must consider both the present state and the consequences of future actions. A robot may currently satisfy every safety constraint while following a trajectory that will violate one several seconds later. Runtime assurance therefore benefits from predictive evaluation using trajectory forecasting, reachable-state analysis, collision prediction, or conservative estimates of future system evolution.

When a potential violation is detected, the assurance system can intervene at different levels of severity. Minor risk may result in speed reduction or trajectory modification, while greater risk can trigger a backup controller, degraded operating mode, protective stop, minimum-risk maneuver, or mission abort. Intervention should occur early enough that the robot retains sufficient physical authority to reach a safe condition.

Runtime assurance should also account for uncertainty rather than treating every estimated state as exact. Perception confidence, localization covariance, model disagreement, out-of-distribution indicators, and prediction uncertainty can reveal that the system\'s understanding of the environment is becoming unreliable. Increasing uncertainty can progressively tighten safety margins or restrict the set of permitted actions.

An important design principle is that the assurance mechanism itself should be simpler and more auditable than the intelligence it supervises. It does not necessarily need to understand every internal representation of a foundation model or learned policy. Instead, it can monitor externally meaningful properties such as state bounds, action validity, trajectory safety, timing behavior, and physical constraints.

Runtime assurance also connects directly with fail-safe and fallback design. Monitoring identifies when normal operation is no longer sufficiently trustworthy, while fallback mechanisms define what the system should do after that determination. Effective safety therefore requires coordinated detection, decision, transition, and recovery logic rather than an isolated alarm that merely reports abnormal behavior.

The assurance boundary extends beyond AI inference because failures can originate throughout the physical computing stack. Sensor loss, stale messages, excessive latency, thermal throttling, actuator faults, communication interruption, or resource exhaustion may invalidate otherwise correct AI decisions. Runtime supervision must therefore combine AI health monitoring with conventional system and hardware diagnostics.

For adaptive robots, runtime assurance provides a practical boundary between learning capability and operational permission. A system may generate novel strategies or adapt its behavior, but adaptation does not automatically authorize every resulting action. The assurance layer preserves invariant safety requirements even when the internal policy, environmental context, or learned representation changes during deployment.

Logging and traceability are also fundamental because assurance decisions become evidence for later investigation and improvement. Records of monitored variables, detected violations, intervention triggers, controller transitions, uncertainty levels, and resulting robot behavior help reconstruct incidents. These traces support debugging, validation, safety-case development, and refinement of operational limits.

At fleet scale, runtime assurance can combine local protection with higher-level supervision. Individual robots must retain immediate safety mechanisms that do not depend on network connectivity, while fleet systems can detect shared hazards, correlated degradation, abnormal behavior patterns, or unsafe interactions among multiple agents. Local autonomy and collective monitoring therefore provide complementary layers of protection.

Ultimately, runtime assurance should be understood as continuous operational evidence that a Physical AI system remains within an acceptable safety envelope. It does not eliminate uncertainty or guarantee that complex AI will never fail. Instead, it limits the physical consequences of uncertain intelligence by continuously monitoring behavior, enforcing constraints, and transferring control toward safer modes whenever confidence in normal autonomous operation becomes insufficient.

런타임 보증(Runtime Assurance)은 자율 물리 인공지능(Physical AI) 시스템이 실제로 작동하는 동안 이를 감독하는 안전 계층(Safety Layer)을 제공한다. 인식(Perception), 계획(Planning), 학습 정책(Learned Policy), 월드 모델(World Model)이 항상 올바르게 동작한다고 가정하는 대신, 런타임 보증(Runtime Assurance)은 현재 시스템 상태와 제안된 행동이 정의된 안전 요구사항(Safety Requirements) 및 운영 제약조건(Operational Constraints)에 계속 부합하는지를 지속적으로 평가한다.

런타임 보증(Runtime Assurance)이 필요한 핵심 이유는 많은 물리 인공지능(Physical AI) 구성요소를 배포 전에 완전하게 검증할 수 없기 때문이다. 학습 모델(Learned Model)은 익숙하지 않은 환경, 분포 변화(Distribution Shift), 센서 성능 저하(Sensor Degradation), 모호한 인간 행동(Ambiguous Human Behavior), 또는 학습 과정에서 경험하지 못한 조건의 조합을 만날 수 있다. 따라서 런타임 보증(Runtime Assurance)은 실제 운용 중 위험한 상태를 탐지함으로써 설계 단계 검증(Design-Time Verification)을 보완한다.

런타임 보증 아키텍처(Runtime Assurance Architecture)는 일반적으로 성능 중심 지능(Performance-Oriented Intelligence)과 안전 중심 감독(Safety-Oriented Supervision)을 분리한다. 주 제어기(Primary Controller)는 임무 목표를 달성하기 위해 신경망(Neural Network), 강화학습(Reinforcement Learning), 시각-언어-행동 정책(VLA Policy), 월드 모델(World Model), 또는 정교한 최적화(Optimization)를 사용할 수 있다. 이와 별도로 보다 제한적인 보증 메커니즘(Assurance Mechanism)이 제안된 행동이 허용 가능한 행동 영역 내부에 유지되는지를 독립적으로 판단한다.

이러한 분리는 고성능 인공지능(High-Performance AI)과 안전 메커니즘(Safety Mechanism)이 서로 다른 목적을 가지기 때문에 특히 중요하다. 주 인공지능(Primary AI)은 효율적이고 적응적이며 높은 성능을 갖는 행동을 추구하지만, 보증 계층(Assurance Layer)은 제약조건 충족(Constraint Satisfaction)과 위험 감소(Risk Reduction)를 우선한다. 이러한 독립성(Independence)은 주 의사결정 과정(Primary Decision Process)의 고장이 해당 고장을 탐지해야 하는 메커니즘까지 동시에 무력화하는 것을 방지한다.

런타임 보증(Runtime Assurance)은 관련 상태(State), 행동(Action), 궤적(Trajectory), 환경 조건(Environmental Conditions), 시스템 건전성 지표(System Health Indicators)를 관찰함으로써 작동한다. 여기에는 로봇 속도(Robot Velocity), 인간과의 거리(Distance to Humans), 위치추정 신뢰도(Localization Confidence), 예측 충돌 확률(Predicted Collision Probability), 액추에이터 상태(Actuator Status), 연산 지연시간(Compute Latency), 배터리 상태(Battery State), 모델 불확실성(Model Uncertainty), 센서 일관성(Sensor Consistency) 등이 포함될 수 있다. 이러한 정보의 조합은 시스템 운용을 계속 신뢰할 수 있는지를 판단하는 근거가 된다.

안전 제약조건(Safety Constraints)은 이러한 관측 정보를 강제 가능한 운영 경계(Operational Boundaries)로 변환한다. 제약조건에는 최대 속도(Maximum Velocity), 최소 이격 거리(Minimum Separation Distance), 허용 작업공간 영역(Permitted Workspace Regions), 안정성 조건(Stability Conditions), 액추에이터 한계(Actuator Limits), 시간 마감 조건(Timing Deadlines), 허용 가능한 불확실성(Acceptable Uncertainty) 등이 정의될 수 있다. 보증 메커니즘(Assurance Mechanism)은 위험한 상태가 되돌릴 수 없는 상황으로 발전하기 전에 현재 및 예측 행동을 이러한 경계와 비교하여 평가한다.

모니터링(Monitoring)은 현재 상태뿐만 아니라 미래 행동의 결과까지 고려해야 한다. 로봇이 현재 모든 안전 제약조건(Safety Constraints)을 만족하더라도 몇 초 후 제약조건을 위반하게 되는 궤적(Trajectory)을 따라갈 수 있다. 따라서 런타임 보증(Runtime Assurance)은 궤적 예측(Trajectory Forecasting), 도달 가능 상태 분석(Reachable-State Analysis), 충돌 예측(Collision Prediction), 또는 미래 시스템 변화에 대한 보수적 추정(Conservative Estimation)을 이용한 예측 평가(Predictive Evaluation)를 통해 더욱 효과적으로 구현될 수 있다.

잠재적인 위반 가능성이 탐지되면 보증 시스템(Assurance System)은 위험의 심각도에 따라 서로 다른 수준으로 개입할 수 있다. 경미한 위험은 속도 감소(Speed Reduction)나 궤적 수정(Trajectory Modification)으로 대응할 수 있으며, 더 큰 위험은 백업 제어기(Backup Controller), 성능 저하 운전 모드(Degraded Operating Mode), 보호 정지(Protective Stop), 최소 위험 기동(Minimum-Risk Maneuver), 또는 임무 중단(Mission Abort)을 실행할 수 있다. 개입은 로봇이 안전한 상태에 도달할 수 있는 충분한 물리적 제어 능력(Physical Authority)을 유지하고 있을 때 이루어져야 한다.

런타임 보증(Runtime Assurance)은 모든 추정 상태를 정확한 값으로 간주하기보다는 불확실성(Uncertainty)도 고려해야 한다. 인식 신뢰도(Perception Confidence), 위치추정 공분산(Localization Covariance), 모델 간 불일치(Model Disagreement), 분포 외 데이터 지표(Out-of-Distribution Indicators), 예측 불확실성(Prediction Uncertainty)은 시스템의 환경 이해가 신뢰성을 잃어가고 있음을 나타낼 수 있다. 불확실성이 증가하면 안전 여유(Safety Margins)를 점진적으로 확대하거나 허용 가능한 행동 집합(Permitted Action Set)을 제한할 수 있다.

중요한 설계 원칙(Design Principle)은 보증 메커니즘(Assurance Mechanism) 자체가 감독 대상인 지능 시스템보다 단순하고 감사 가능(Auditable)해야 한다는 것이다. 보증 메커니즘이 파운데이션 모델(Foundation Model)이나 학습 정책(Learned Policy)의 모든 내부 표현(Internal Representation)을 이해할 필요는 없다. 대신 상태 경계(State Bounds), 행동 유효성(Action Validity), 궤적 안전성(Trajectory Safety), 시간 동작(Timing Behavior), 물리적 제약조건(Physical Constraints)과 같이 외부에서 의미 있게 확인할 수 있는 속성을 모니터링할 수 있다.

런타임 보증(Runtime Assurance)은 페일세이프 및 폴백 설계(Fail-Safe and Fallback Design)와도 직접적으로 연결된다. 모니터링(Monitoring)은 정상 운용을 더 이상 충분히 신뢰할 수 없는 시점을 식별하며, 폴백 메커니즘(Fallback Mechanism)은 이러한 판단 이후 시스템이 무엇을 수행해야 하는지를 정의한다. 따라서 효과적인 안전성(Safety)은 단순히 비정상 행동을 알리는 독립적인 경보가 아니라 탐지(Detection), 판단(Decision), 전환(Transition), 복구(Recovery) 로직이 서로 조정된 형태로 구현되어야 한다.

보증 경계(Assurance Boundary)는 인공지능 추론(AI Inference)을 넘어 확장되어야 한다. 고장은 물리적 컴퓨팅 스택(Physical Computing Stack)의 다양한 부분에서 발생할 수 있기 때문이다. 센서 손실(Sensor Loss), 오래된 메시지(Stale Messages), 과도한 지연시간(Excessive Latency), 열 스로틀링(Thermal Throttling), 액추에이터 고장(Actuator Faults), 통신 중단(Communication Interruption), 자원 고갈(Resource Exhaustion)은 인공지능의 판단 자체가 올바르더라도 그 판단을 무효화할 수 있다. 따라서 런타임 감독(Runtime Supervision)은 인공지능 건전성 모니터링(AI Health Monitoring)과 기존 시스템 및 하드웨어 진단(System and Hardware Diagnostics)을 결합해야 한다.

적응형 로봇(Adaptive Robot)에서 런타임 보증(Runtime Assurance)은 학습 능력(Learning Capability)과 실제 운용 허가(Operational Permission) 사이의 실질적인 경계를 제공한다. 시스템은 새로운 전략을 생성하거나 행동을 적응시킬 수 있지만, 적응 자체가 그 결과로 생성되는 모든 행동을 자동으로 허용하는 것은 아니다. 보증 계층(Assurance Layer)은 내부 정책(Internal Policy), 환경 상황(Environmental Context), 학습 표현(Learned Representation)이 배포 중 변화하더라도 불변의 안전 요구사항(Invariant Safety Requirements)을 유지한다.

로깅 및 추적성(Logging and Traceability) 역시 런타임 보증(Runtime Assurance)의 핵심 요소이다. 보증 과정에서 이루어진 판단은 이후 조사와 시스템 개선을 위한 증거가 되기 때문이다. 모니터링 변수(Monitored Variables), 탐지된 위반(Detected Violations), 개입 트리거(Intervention Triggers), 제어기 전환(Controller Transitions), 불확실성 수준(Uncertainty Levels), 그리고 그 결과로 나타난 로봇 행동(Robot Behavior)을 기록하면 사고를 재구성할 수 있다. 이러한 기록은 디버깅(Debugging), 검증(Validation), 안전 사례(Safety Case) 개발, 운영 한계(Operational Limits) 개선을 지원한다.

플릿 규모(Fleet Scale)에서 런타임 보증(Runtime Assurance)은 로컬 보호(Local Protection)와 상위 수준 감독(Higher-Level Supervision)을 결합할 수 있다. 개별 로봇은 네트워크 연결에 의존하지 않는 즉각적인 안전 메커니즘(Immediate Safety Mechanisms)을 유지해야 하며, 플릿 시스템(Fleet System)은 공유 위험(Shared Hazards), 상관된 성능 저하(Correlated Degradation), 비정상 행동 패턴(Abnormal Behavior Patterns), 다중 에이전트(Multiple Agents) 사이의 위험한 상호작용을 탐지할 수 있다. 따라서 로컬 자율성(Local Autonomy)과 집단 모니터링(Collective Monitoring)은 상호 보완적인 보호 계층을 제공한다.

궁극적으로 런타임 보증(Runtime Assurance)은 물리 인공지능(Physical AI) 시스템이 허용 가능한 안전 영역(Safety Envelope) 내부에 계속 존재한다는 것을 운용 중 지속적으로 확인하는 과정으로 이해할 수 있다. 런타임 보증은 불확실성(Uncertainty)을 제거하거나 복잡한 인공지능이 절대로 실패하지 않는다고 보장하지 않는다. 대신 행동을 지속적으로 모니터링하고, 제약조건을 강제하며, 정상 자율 운용(Normal Autonomous Operation)에 대한 신뢰가 충분하지 않을 때 더 안전한 모드(Safer Modes)로 제어권을 전환함으로써 불확실한 지능이 초래할 수 있는 물리적 결과를 제한한다.

##  

## 07.02. Independent Safety Monitor Architecture

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

An independent safety monitor is a dedicated supervisory mechanism that evaluates whether a Physical AI system remains within predefined safety conditions while the primary autonomy stack performs perception, reasoning, planning, and control. Its defining characteristic is independence: the monitor should not rely entirely on the same models, assumptions, data paths, or failure-prone components that it is intended to supervise.

The architecture separates mission-oriented intelligence from safety-oriented authority. A primary AI controller may optimize navigation efficiency, manipulation performance, task completion, or adaptive behavior, while the independent monitor evaluates whether the resulting states, actions, and trajectories remain acceptable. This separation allows advanced autonomy to operate freely inside an explicitly defined safety envelope without granting it unrestricted control.

Independence can be established at several architectural levels. The monitor may execute as a separate software process, on an isolated operating-system partition, within a safety-certified controller, or on physically independent computing hardware. Greater separation reduces the probability that a common software crash, resource exhaustion event, corrupted memory region, or AI inference failure simultaneously disables both primary control and safety supervision.

The monitor requires trustworthy observations of the physical system and its environment. Inputs may include velocity, position, acceleration, actuator state, human proximity, localization confidence, obstacle distance, battery condition, communication status, timing information, and AI uncertainty. Safety-critical signals may be obtained directly from sensors or independent interfaces rather than solely through representations generated by the primary AI pipeline.

Monitoring logic converts these observations into explicit safety judgments. Instead of reproducing the full intelligence of the primary controller, the monitor evaluates a smaller set of safety-relevant properties such as speed limits, separation distances, workspace boundaries, stability margins, collision risk, actuator limits, communication freshness, or execution deadlines. This narrower responsibility makes its behavior easier to understand, verify, test, and certify.

A key architectural principle is diversity between the primary system and its monitor. If both components use identical neural networks, sensor-processing pipelines, algorithms, or training datasets, the same systematic error can affect them simultaneously. Diverse sensing, simpler algorithms, independent state estimation, analytical checks, geometric constraints, or deterministic rules can reduce common-cause failures and strengthen confidence in supervisory decisions.

The independent monitor must evaluate proposed behavior early enough to prevent unsafe physical consequences. Monitoring only the robot\'s current state may detect danger too late because momentum, actuator dynamics, braking distance, and environmental motion constrain future recovery. The architecture can therefore inspect planned trajectories and predict whether future states will cross safety boundaries before execution reaches an unrecoverable condition.

Safety decisions can be organized around explicit operating states. When monitored conditions are normal, the primary controller retains authority. As risk increases, the monitor may impose speed restrictions, constrain trajectories, reject particular actions, or request replanning. When safety limits are violated or confidence becomes insufficient, authority can be transferred to a backup controller or another mechanism capable of reaching a defined safe state.

Control authority is therefore one of the most important interfaces in the architecture. A monitor that can detect danger but cannot influence execution provides limited protection. The supervisory path must be capable of overriding, filtering, inhibiting, or replacing commands from the primary controller when necessary. Safety intervention should remain available even when the primary AI becomes unresponsive, unstable, computationally overloaded, or logically inconsistent.

The backup path should generally be simpler and more conservative than normal autonomous control. It may perform controlled deceleration, hold position, retreat to a known safe region, maintain stability, execute a minimum-risk maneuver, or initiate a protective stop. The objective is not to preserve maximum mission performance but to prevent unacceptable physical outcomes while maintaining enough control authority for safe recovery.

Timing independence is equally important because Physical AI safety depends on decisions arriving before physical deadlines. The monitor can supervise control-cycle execution time, sensor freshness, communication latency, inference delay, and watchdog signals. If the primary autonomy stack misses critical deadlines, the absence of a valid command must itself be interpreted as a potentially unsafe condition rather than allowing outdated control information to continue indefinitely.

Resource isolation further protects the monitor from failures in computationally demanding AI workloads. Large perception networks, world models, VLA systems, or planning algorithms may consume excessive CPU, GPU, memory, power, or thermal capacity. A safety monitor should retain sufficient protected resources to continue evaluating essential conditions and initiating fallback actions even when the performance-oriented computing environment becomes degraded.

The architecture should also address uncertainty and degraded observability. Loss of a camera, inconsistent LiDAR measurements, declining localization confidence, or disagreement among perception models may prevent the monitor from proving that operation remains safe. In such cases, absence of confirmed danger should not automatically be interpreted as evidence of safety. Operational permissions can instead become progressively more conservative as trustworthy information decreases.

Communication between the primary controller and safety monitor should use clearly defined, minimal interfaces. The monitor may receive current state estimates, candidate actions, trajectories, confidence measures, health indicators, and timing information while returning permission, restriction, override, or fallback commands. Keeping this interface explicit reduces unnecessary coupling and makes safety responsibilities easier to analyze and validate independently.

Every monitoring and intervention event should be traceable. Logs can record observed conditions, violated constraints, uncertainty levels, rejected commands, controller transitions, fallback activation, and recovery results. Such records allow engineers to determine whether the monitor responded correctly, identify recurring failure patterns, refine thresholds, and provide operational evidence for verification, validation, incident analysis, and safety assurance.

At fleet scale, the same principle can be extended without eliminating local independence. Each robot should retain a local safety monitor capable of immediate intervention without relying on remote infrastructure, while fleet-level supervision identifies interactions and hazards that cannot be observed by one robot alone. This creates layered assurance in which local monitors protect individual platforms and higher-level monitoring addresses collective behavior.

An independent safety monitor architecture ultimately creates a controlled boundary around complex and potentially unpredictable Physical AI. The primary AI can pursue increasingly capable perception, reasoning, learning, and action, while a separate supervisory mechanism determines whether those capabilities may continue controlling the physical system. Independence, simplicity, diversity, protected authority, and conservative intervention together transform runtime monitoring into an active safety architecture.

독립 안전 모니터(Independent Safety Monitor)는 주 자율 시스템(Primary Autonomy Stack)이 인식(Perception), 추론(Reasoning), 계획(Planning), 제어(Control)를 수행하는 동안 물리 인공지능(Physical AI) 시스템이 사전에 정의된 안전 조건(Safety Conditions) 내에 유지되는지를 평가하는 전용 감독 메커니즘(Supervisory Mechanism)이다. 핵심적인 특징은 독립성(Independence)으로, 모니터는 자신이 감독해야 하는 동일한 모델, 가정, 데이터 경로 또는 고장 가능성이 있는 구성요소에 전적으로 의존해서는 안 된다.

이 아키텍처(Architecture)는 임무 중심 지능(Mission-Oriented Intelligence)과 안전 중심 권한(Safety-Oriented Authority)을 분리한다. 주 인공지능 제어기(Primary AI Controller)는 내비게이션 효율성, 조작 성능, 작업 완료 또는 적응형 행동을 최적화할 수 있으며, 독립 안전 모니터(Independent Safety Monitor)는 그 결과로 생성되는 상태(State), 행동(Action), 궤적(Trajectory)이 허용 가능한지를 평가한다. 이러한 분리를 통해 고도화된 자율 시스템은 무제한적인 제어 권한을 갖지 않으면서 명시적으로 정의된 안전 영역(Safety Envelope) 내부에서 자유롭게 작동할 수 있다.

독립성(Independence)은 여러 아키텍처 계층(Architectural Levels)에서 구현될 수 있다. 모니터는 별도의 소프트웨어 프로세스(Software Process), 격리된 운영체제 파티션(Operating-System Partition), 안전 인증 제어기(Safety-Certified Controller), 또는 물리적으로 독립된 컴퓨팅 하드웨어(Computing Hardware)에서 실행될 수 있다. 분리 수준이 높아질수록 공통 소프트웨어 충돌, 자원 고갈(Resource Exhaustion), 메모리 손상(Corrupted Memory), 인공지능 추론 실패(AI Inference Failure)가 주 제어와 안전 감독을 동시에 무력화할 가능성을 줄일 수 있다.

모니터는 물리 시스템(Physical System)과 환경(Environment)에 대한 신뢰할 수 있는 관측 정보(Observations)를 필요로 한다. 입력에는 속도(Velocity), 위치(Position), 가속도(Acceleration), 액추에이터 상태(Actuator State), 인간과의 근접도(Human Proximity), 위치추정 신뢰도(Localization Confidence), 장애물 거리(Obstacle Distance), 배터리 상태(Battery Condition), 통신 상태(Communication Status), 타이밍 정보(Timing Information), 인공지능 불확실성(AI Uncertainty) 등이 포함될 수 있다. 안전 핵심 신호(Safety-Critical Signals)는 주 인공지능 파이프라인이 생성한 표현에만 의존하지 않고 센서나 독립 인터페이스(Independent Interfaces)로부터 직접 획득할 수 있다.

모니터링 로직(Monitoring Logic)은 이러한 관측 정보를 명시적인 안전 판단(Safety Judgments)으로 변환한다. 모니터는 주 제어기의 전체 지능을 그대로 재현하는 대신 속도 제한(Speed Limits), 이격 거리(Separation Distances), 작업공간 경계(Workspace Boundaries), 안정성 여유(Stability Margins), 충돌 위험(Collision Risk), 액추에이터 한계(Actuator Limits), 통신 최신성(Communication Freshness), 실행 마감시간(Execution Deadlines)과 같은 제한된 안전 관련 속성을 평가한다. 이러한 좁은 책임 범위는 모니터의 동작을 보다 쉽게 이해하고 검증하며 시험하고 인증할 수 있도록 한다.

핵심적인 아키텍처 원칙(Architectural Principle)은 주 시스템(Primary System)과 모니터 사이의 다양성(Diversity)이다. 두 구성요소가 동일한 신경망(Neural Networks), 센서 처리 파이프라인(Sensor-Processing Pipelines), 알고리즘 또는 학습 데이터셋(Training Datasets)을 사용한다면 동일한 체계적 오류(Systematic Error)가 동시에 영향을 줄 수 있다. 다양한 센싱(Diverse Sensing), 단순한 알고리즘, 독립 상태 추정(Independent State Estimation), 분석적 검사(Analytical Checks), 기하학적 제약조건(Geometric Constraints), 결정론적 규칙(Deterministic Rules)은 공통 원인 고장(Common-Cause Failures)을 줄이고 감독 판단에 대한 신뢰도를 높일 수 있다.

독립 안전 모니터(Independent Safety Monitor)는 위험한 물리적 결과를 방지할 수 있을 만큼 충분히 이른 시점에 제안된 행동(Proposed Behavior)을 평가해야 한다. 로봇의 현재 상태만 모니터링하면 운동량(Momentum), 액추에이터 동역학(Actuator Dynamics), 제동 거리(Braking Distance), 환경의 움직임(Environmental Motion)이 미래의 복구 가능성을 제한하기 때문에 위험 탐지가 너무 늦어질 수 있다. 따라서 아키텍처는 계획된 궤적(Planned Trajectory)을 검사하고 실행이 복구 불가능한 상태에 도달하기 전에 미래 상태가 안전 경계를 넘어설 것인지를 예측할 수 있다.

안전 판단(Safety Decisions)은 명시적인 운영 상태(Operating States)를 중심으로 구성할 수 있다. 모니터링된 조건이 정상인 경우 주 제어기(Primary Controller)가 제어 권한을 유지한다. 위험이 증가하면 모니터는 속도 제한(Speed Restrictions)을 적용하거나, 궤적을 제한하고, 특정 행동을 거부하거나, 재계획(Replanning)을 요청할 수 있다. 안전 한계가 위반되거나 신뢰도가 충분하지 않은 경우 제어 권한을 백업 제어기(Backup Controller) 또는 정의된 안전 상태(Safe State)에 도달할 수 있는 다른 메커니즘으로 전환할 수 있다.

따라서 제어 권한(Control Authority)은 이 아키텍처에서 가장 중요한 인터페이스 가운데 하나이다. 위험을 탐지할 수 있지만 실행에 영향을 줄 수 없는 모니터는 제한적인 보호만 제공한다. 감독 경로(Supervisory Path)는 필요한 경우 주 제어기의 명령을 재정의(Override), 필터링(Filtering), 억제(Inhibiting) 또는 대체할 수 있어야 한다. 주 인공지능이 응답하지 않거나 불안정해지고, 연산 과부하(Computational Overload)가 발생하거나 논리적으로 일관되지 않더라도 안전 개입(Safety Intervention)은 계속 사용 가능해야 한다.

백업 경로(Backup Path)는 일반적으로 정상 자율 제어보다 단순하고 보수적으로 설계되어야 한다. 제어된 감속(Controlled Deceleration), 위치 유지(Hold Position), 알려진 안전 영역으로의 후퇴(Retreat), 안정성 유지(Maintain Stability), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop) 등을 수행할 수 있다. 목적은 최대 임무 성능을 유지하는 것이 아니라 안전한 복구에 필요한 충분한 제어 권한을 유지하면서 허용할 수 없는 물리적 결과를 방지하는 것이다.

시간 독립성(Timing Independence)도 중요하다. 물리 인공지능(Physical AI)의 안전성은 물리적 마감시간(Physical Deadlines) 이전에 판단이 이루어지는지에 의존하기 때문이다. 모니터는 제어 주기 실행시간(Control-Cycle Execution Time), 센서 정보의 최신성(Sensor Freshness), 통신 지연시간(Communication Latency), 추론 지연(Inference Delay), 감시 타이머 신호(Watchdog Signals)를 감독할 수 있다. 주 자율 시스템이 중요한 시간 제한을 놓치는 경우 유효한 명령이 존재하지 않는다는 사실 자체를 잠재적인 위험 상태로 해석해야 하며, 오래된 제어 정보를 무기한 계속 사용해서는 안 된다.

자원 격리(Resource Isolation)는 연산 요구량이 높은 인공지능 작업에서 발생하는 고장으로부터 모니터를 추가적으로 보호한다. 대규모 인식 네트워크(Large Perception Networks), 월드 모델(World Models), 시각-언어-행동 시스템(VLA Systems), 계획 알고리즘(Planning Algorithms)은 과도한 CPU, GPU, 메모리, 전력 또는 열 용량을 사용할 수 있다. 안전 모니터는 성능 중심 컴퓨팅 환경이 저하되더라도 필수 조건을 계속 평가하고 폴백 행동(Fallback Actions)을 시작할 수 있도록 충분한 보호 자원(Protected Resources)을 확보해야 한다.

아키텍처는 불확실성(Uncertainty)과 관측 가능성 저하(Degraded Observability)도 처리해야 한다. 카메라 손실(Camera Loss), 일관되지 않은 라이다 측정(LiDAR Measurements), 위치추정 신뢰도 감소, 인식 모델 간 불일치(Disagreement among Perception Models)는 모니터가 운용의 안전성을 확인하지 못하게 할 수 있다. 이러한 상황에서는 위험이 확인되지 않았다는 사실을 자동으로 안전의 증거로 해석해서는 안 된다. 대신 신뢰할 수 있는 정보가 감소함에 따라 운영 허용 범위(Operational Permissions)를 점진적으로 더욱 보수적으로 제한할 수 있다.

주 제어기(Primary Controller)와 안전 모니터(Safety Monitor) 사이의 통신은 명확하게 정의된 최소 인터페이스(Minimal Interfaces)를 사용해야 한다. 모니터는 현재 상태 추정(Current State Estimates), 후보 행동(Candidate Actions), 궤적(Trajectories), 신뢰도 척도(Confidence Measures), 건전성 지표(Health Indicators), 타이밍 정보(Timing Information)를 전달받고, 허용(Permission), 제한(Restriction), 재정의(Override), 폴백 명령(Fallback Commands)을 반환할 수 있다. 인터페이스를 명시적으로 유지하면 불필요한 결합(Coupling)을 줄이고 안전 책임을 독립적으로 분석하고 검증하기 쉬워진다.

모든 모니터링 및 개입 이벤트(Monitoring and Intervention Events)는 추적 가능(Traceable)해야 한다. 로그(Log)는 관측된 조건, 위반된 제약조건, 불확실성 수준, 거부된 명령, 제어기 전환(Controller Transitions), 폴백 활성화(Fallback Activation), 복구 결과(Recovery Results)를 기록할 수 있다. 이러한 기록을 통해 엔지니어는 모니터가 올바르게 대응했는지를 판단하고, 반복되는 고장 패턴을 식별하며, 임계값(Thresholds)을 개선하고, 검증(Verification), 유효성 확인(Validation), 사고 분석(Incident Analysis), 안전 보증(Safety Assurance)을 위한 운용 증거를 확보할 수 있다.

플릿 규모(Fleet Scale)에서도 동일한 원칙을 적용할 수 있으며 로컬 독립성(Local Independence)은 유지되어야 한다. 각 로봇은 원격 인프라(Remote Infrastructure)에 의존하지 않고 즉각적으로 개입할 수 있는 로컬 안전 모니터(Local Safety Monitor)를 유지해야 하며, 플릿 수준 감독(Fleet-Level Supervision)은 하나의 로봇만으로 관측할 수 없는 상호작용과 위험을 식별한다. 이를 통해 로컬 모니터가 개별 플랫폼을 보호하고 상위 수준 모니터링이 집단 행동(Collective Behavior)을 감독하는 계층형 보증(Layered Assurance)이 형성된다.

독립 안전 모니터 아키텍처(Independent Safety Monitor Architecture)는 궁극적으로 복잡하고 잠재적으로 예측하기 어려운 물리 인공지능(Physical AI)을 둘러싸는 통제된 안전 경계(Controlled Safety Boundary)를 형성한다. 주 인공지능(Primary AI)은 더욱 발전된 인식, 추론, 학습 및 행동 능력을 추구할 수 있으며, 별도의 감독 메커니즘(Supervisory Mechanism)은 이러한 능력이 물리 시스템을 계속 제어하도록 허용할 것인지를 판단한다. 독립성(Independence), 단순성(Simplicity), 다양성(Diversity), 보호된 제어 권한(Protected Authority), 보수적 개입(Conservative Intervention)이 결합될 때 런타임 모니터링(Runtime Monitoring)은 능동적인 안전 아키텍처(Active Safety Architecture)로 전환된다.

##  

## 07.03. Runtime Constraint Enforcement

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Runtime constraint enforcement is the mechanism that converts safety requirements into continuously enforceable limits on the behavior of a Physical AI system. While runtime monitoring determines what the robot is doing and whether risk is increasing, constraint enforcement actively determines which states, actions, commands, and trajectories are permitted to reach the physical system during operation.

The need for runtime enforcement arises because autonomous behavior cannot always be completely constrained during training or design. Learned policies, VLA systems, world-model planners, and adaptive controllers may generate actions that are reasonable according to their learned objectives yet violate physical or operational safety requirements. Runtime constraints therefore establish an authoritative boundary that remains valid regardless of how an action was generated.

Constraints can represent physical, geometric, temporal, operational, or behavioral requirements. Examples include maximum velocity and acceleration, minimum human separation, actuator force limits, permitted workspace regions, stability conditions, collision-clearance margins, battery thresholds, communication deadlines, and prohibited actions. Together, these constraints define a dynamically enforceable safety envelope around autonomous behavior.

A useful distinction exists between state constraints and action constraints. State constraints specify conditions that the system should never enter, such as excessive tilt, unsafe proximity, or operation outside an authorized region. Action constraints determine which commands may be executed from the current state. Runtime enforcement connects these concepts by preventing actions whose predicted consequences could drive the system toward prohibited states.

Constraint enforcement should therefore consider future evolution rather than examining commands independently. A velocity command may appear valid at the present instant but become unsafe when braking distance, robot momentum, actuator delay, human motion, or environmental geometry are considered. Predictive enforcement evaluates candidate trajectories or reachable states and rejects behavior that cannot preserve sufficient future safety margins.

The enforcement mechanism is typically positioned between high-level autonomous decision making and physical execution. A primary controller proposes an action, trajectory, or control command, while a safety gate, command filter, runtime shield, or supervisory controller evaluates it before actuation. Commands satisfying all required constraints pass through, whereas unsafe commands can be modified, delayed, rejected, or replaced by safer alternatives.

Hard constraints represent requirements that must not be intentionally violated during normal operation. Collision avoidance boundaries, mechanical limits, emergency exclusion zones, or stability requirements may belong to this category. Soft constraints represent preferences or margins that can be relaxed under controlled conditions. Separating them prevents performance optimization from trading away requirements that are essential to physical safety.

Runtime constraints may also change according to operating context. A mobile robot can safely travel faster in an empty corridor than near workers, while a manipulator may use different force limits depending on whether it is operating inside an isolated cell or collaborating with a person. Context-dependent enforcement therefore adjusts permissible behavior using environment state, mission mode, human proximity, and system health.

Uncertainty should directly influence constraint boundaries. When perception confidence decreases, localization uncertainty grows, or an out-of-distribution condition is detected, a fixed safety boundary may no longer provide adequate protection. The enforcement layer can enlarge separation margins, reduce speed, restrict available trajectories, or prohibit complex maneuvers as uncertainty increases, producing progressively more conservative operation.

Constraint conflicts require explicit resolution because several safety and operational requirements may become active simultaneously. A robot may need to avoid a person while remaining inside a permitted region and preserving vehicle stability. The enforcement architecture should prioritize non-negotiable safety requirements and search for behavior satisfying all feasible constraints rather than allowing mission objectives to override higher-priority protection.

When a proposed action violates constraints but a safe alternative exists, modification is often preferable to immediate shutdown. A command filter can reduce velocity, limit acceleration, clip actuator output, alter steering, or project an unsafe action into a permitted action set. This preserves useful autonomy while ensuring that the physical command delivered to the robot remains inside the allowable safety envelope.

Some situations cannot be resolved through command modification. The feasible safe action set may become empty because of sensor failure, localization loss, rapidly approaching obstacles, mechanical faults, or contradictory environmental conditions. In such cases, enforcement must escalate from filtering to fallback behavior, transferring authority to a backup controller, minimum-risk maneuver, protective stop, or other predefined safe-state strategy.

Timing is fundamental because a mathematically correct constraint decision is ineffective if it arrives after the command has already produced physical motion. Enforcement must operate within bounded latency relative to the dynamics of the robot. Watchdogs, real-time scheduling, deterministic safety processes, and independent compute resources can help ensure that safety checks complete before the physical system passes a point from which safe recovery is impossible.

Runtime enforcement should remain sufficiently independent from the primary AI controller. If the same learned model both proposes an action and determines whether that action is safe, systematic errors may defeat both functions simultaneously. Independent constraints, simpler algorithms, direct safety sensors, deterministic checks, and separate execution paths can provide diversity and reduce common-cause failures within the control architecture.

For adaptive or learning-enabled systems, constraint enforcement establishes a stable boundary around changing intelligence. Online learning may update policies, world models, or decision strategies, but those updates do not automatically modify fundamental safety permissions. New behavior can therefore be explored or deployed within a controlled region while invariant safety requirements remain externally enforced by the runtime assurance architecture.

Every enforcement decision should be observable and traceable. The system can record evaluated constraints, measured values, predicted violations, rejected or modified commands, activated margins, controller transitions, and resulting physical behavior. These records provide evidence for debugging, incident reconstruction, threshold refinement, verification, validation, and demonstration that safety requirements were actively enforced during operation.

At fleet level, constraint enforcement expands from individual robot limits to shared operational constraints. Robots may need to maintain mutual separation, respect traffic priorities, avoid conflicting reservations, limit congestion, or respond to shared hazards. Fleet supervision can coordinate these constraints, but each robot should retain local enforcement capable of protecting itself when communication or centralized coordination becomes unavailable.

Runtime constraint enforcement ultimately forms the executable boundary between autonomous intelligence and physical authority. The AI system may generate sophisticated plans, predictions, and adaptive actions, but only behavior satisfying the active safety constraints should reach actuators. By combining predictive evaluation, contextual limits, uncertainty-aware margins, command filtering, independent authority, and fallback escalation, runtime assurance turns abstract safety requirements into continuously enforced physical protection.

런타임 제약조건 강제(Runtime Constraint Enforcement)는 안전 요구사항(Safety Requirements)을 물리 인공지능(Physical AI) 시스템의 행동에 대해 지속적으로 강제할 수 있는 제한으로 변환하는 메커니즘이다. 런타임 모니터링(Runtime Monitoring)이 로봇이 무엇을 수행하고 있으며 위험이 증가하고 있는지를 판단한다면, 제약조건 강제(Constraint Enforcement)는 운용 중 어떤 상태(State), 행동(Action), 명령(Command), 궤적(Trajectory)이 실제 물리 시스템에 전달될 수 있는지를 능동적으로 결정한다.

런타임 강제(Runtime Enforcement)가 필요한 이유는 자율 행동(Autonomous Behavior)을 학습이나 설계 단계에서 항상 완전하게 제한할 수 없기 때문이다. 학습 정책(Learned Policy), 시각-언어-행동 시스템(VLA System), 월드 모델 계획기(World-Model Planner), 적응형 제어기(Adaptive Controller)는 학습된 목표 관점에서는 합리적이지만 물리적 또는 운영상의 안전 요구사항을 위반하는 행동을 생성할 수 있다. 따라서 런타임 제약조건(Runtime Constraints)은 행동이 어떤 방식으로 생성되었는지와 관계없이 유지되는 권한 있는 경계(Authoritative Boundary)를 설정한다.

제약조건(Constraints)은 물리적(Physical), 기하학적(Geometric), 시간적(Temporal), 운영적(Operational), 행동적(Behavioral) 요구사항을 나타낼 수 있다. 대표적으로 최대 속도 및 가속도(Maximum Velocity and Acceleration), 최소 인간 이격 거리(Minimum Human Separation), 액추에이터 힘 제한(Actuator Force Limits), 허용 작업공간 영역(Permitted Workspace Regions), 안정성 조건(Stability Conditions), 충돌 여유 거리(Collision-Clearance Margins), 배터리 임계값(Battery Thresholds), 통신 마감시간(Communication Deadlines), 금지 행동(Prohibited Actions) 등이 있다. 이러한 제약조건은 자율 행동을 둘러싸는 동적으로 강제 가능한 안전 영역(Safety Envelope)을 정의한다.

상태 제약조건(State Constraints)과 행동 제약조건(Action Constraints)은 구분해서 이해하는 것이 유용하다. 상태 제약조건은 과도한 기울기, 위험한 근접 상태, 허가된 영역 밖에서의 운용과 같이 시스템이 절대로 진입해서는 안 되는 조건을 정의한다. 행동 제약조건은 현재 상태에서 어떤 명령을 실행할 수 있는지를 결정한다. 런타임 강제(Runtime Enforcement)는 예측된 결과가 시스템을 금지 상태(Prohibited States)로 이동시킬 수 있는 행동을 차단함으로써 이 두 개념을 연결한다.

따라서 제약조건 강제(Constraint Enforcement)는 개별 명령만 검사하는 것이 아니라 미래의 시스템 변화(Future Evolution)를 고려해야 한다. 현재 순간에는 속도 명령(Velocity Command)이 유효해 보일 수 있지만 제동 거리(Braking Distance), 로봇 운동량(Robot Momentum), 액추에이터 지연(Actuator Delay), 인간 움직임(Human Motion), 환경 기하구조(Environmental Geometry)를 고려하면 위험해질 수 있다. 예측 기반 강제(Predictive Enforcement)는 후보 궤적(Candidate Trajectories) 또는 도달 가능 상태(Reachable States)를 평가하고 충분한 미래 안전 여유(Future Safety Margins)를 유지할 수 없는 행동을 거부한다.

강제 메커니즘(Enforcement Mechanism)은 일반적으로 상위 수준 자율 의사결정(High-Level Autonomous Decision Making)과 물리적 실행(Physical Execution) 사이에 배치된다. 주 제어기(Primary Controller)가 행동, 궤적 또는 제어 명령을 제안하면 안전 게이트(Safety Gate), 명령 필터(Command Filter), 런타임 실드(Runtime Shield), 감독 제어기(Supervisory Controller)가 작동 전에 이를 평가한다. 모든 필수 제약조건을 만족하는 명령은 통과하지만, 위험한 명령은 수정, 지연, 거부되거나 더 안전한 대안으로 대체될 수 있다.

하드 제약조건(Hard Constraints)은 정상 운용 중 의도적으로 위반해서는 안 되는 요구사항을 의미한다. 충돌 방지 경계(Collision Avoidance Boundaries), 기계적 한계(Mechanical Limits), 비상 제외 구역(Emergency Exclusion Zones), 안정성 요구사항(Stability Requirements) 등이 여기에 포함될 수 있다. 소프트 제약조건(Soft Constraints)은 통제된 조건에서 완화할 수 있는 선호사항이나 여유 범위를 의미한다. 이 둘을 구분하면 성능 최적화(Performance Optimization)가 물리적 안전에 필수적인 요구사항을 희생하는 것을 방지할 수 있다.

런타임 제약조건(Runtime Constraints)은 운영 상황(Operating Context)에 따라 변화할 수도 있다. 이동 로봇(Mobile Robot)은 작업자가 없는 빈 복도에서는 더 빠르게 이동할 수 있지만 사람 근처에서는 속도를 낮춰야 하며, 매니퓰레이터(Manipulator)는 격리된 셀(Isolated Cell)에서 작동하는 경우와 사람과 협업하는 경우 서로 다른 힘 제한을 사용할 수 있다. 따라서 상황 의존적 강제(Context-Dependent Enforcement)는 환경 상태, 임무 모드(Mission Mode), 인간 근접도(Human Proximity), 시스템 건전성(System Health)을 이용해 허용 가능한 행동 범위를 조정한다.

불확실성(Uncertainty)은 제약조건의 경계에 직접 영향을 주어야 한다. 인식 신뢰도(Perception Confidence)가 감소하거나 위치추정 불확실성(Localization Uncertainty)이 증가하고, 분포 외 상태(Out-of-Distribution Condition)가 탐지되면 고정된 안전 경계만으로 충분한 보호를 제공하지 못할 수 있다. 강제 계층(Enforcement Layer)은 불확실성이 증가함에 따라 이격 여유(Separation Margins)를 확대하고, 속도를 낮추며, 사용 가능한 궤적을 제한하거나 복잡한 기동을 금지함으로써 점진적으로 더 보수적인 운용을 수행할 수 있다.

여러 안전 및 운영 요구사항이 동시에 활성화될 수 있으므로 제약조건 충돌(Constraint Conflicts)은 명시적으로 해결해야 한다. 로봇은 사람을 회피하면서 동시에 허용된 영역 내부에 머물고 차량 안정성(Vehicle Stability)을 유지해야 할 수 있다. 강제 아키텍처(Enforcement Architecture)는 임무 목표가 더 높은 우선순위의 보호 요구사항을 무시하도록 허용하는 대신, 타협할 수 없는 안전 요구사항을 우선하고 가능한 모든 제약조건을 만족하는 행동을 탐색해야 한다.

제안된 행동이 제약조건을 위반하더라도 안전한 대안이 존재한다면 즉각적인 정지보다 행동 수정(Action Modification)이 더 적절한 경우가 많다. 명령 필터(Command Filter)는 속도를 줄이고, 가속도를 제한하며, 액추에이터 출력을 제한하고, 조향을 수정하거나 위험한 행동을 허용된 행동 집합(Permitted Action Set) 내부로 투영할 수 있다. 이를 통해 유용한 자율성(Useful Autonomy)을 유지하면서 실제 로봇으로 전달되는 물리적 명령이 허용 가능한 안전 영역 내부에 있도록 보장한다.

일부 상황은 명령 수정만으로 해결할 수 없다. 센서 고장(Sensor Failure), 위치추정 상실(Localization Loss), 빠르게 접근하는 장애물, 기계적 고장(Mechanical Faults), 상충되는 환경 조건으로 인해 실행 가능한 안전 행동 집합(Feasible Safe Action Set)이 비어 있을 수 있다. 이러한 경우 강제 시스템은 필터링에서 폴백 행동(Fallback Behavior)으로 대응 수준을 높이고 제어 권한을 백업 제어기(Backup Controller), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop), 또는 사전에 정의된 안전 상태 전략(Safe-State Strategy)으로 전환해야 한다.

시간성(Timing)은 핵심 요소이다. 수학적으로 올바른 제약조건 판단이라도 명령이 이미 물리적 움직임을 발생시킨 이후에 도착한다면 효과가 없기 때문이다. 강제 시스템은 로봇의 동역학(Dynamics)에 대응할 수 있도록 제한된 지연시간(Bounded Latency) 내에서 동작해야 한다. 감시 타이머(Watchdog), 실시간 스케줄링(Real-Time Scheduling), 결정론적 안전 프로세스(Deterministic Safety Processes), 독립 연산 자원(Independent Compute Resources)은 물리 시스템이 안전하게 복구할 수 없는 지점을 지나기 전에 안전 검사가 완료되도록 지원한다.

런타임 강제(Runtime Enforcement)는 주 인공지능 제어기(Primary AI Controller)로부터 충분한 독립성(Independence)을 유지해야 한다. 동일한 학습 모델이 행동을 제안하는 동시에 그 행동이 안전한지를 판단한다면 체계적 오류(Systematic Errors)가 두 기능을 동시에 무력화할 수 있다. 독립적인 제약조건(Independent Constraints), 단순한 알고리즘, 직접 안전 센서(Direct Safety Sensors), 결정론적 검사(Deterministic Checks), 별도의 실행 경로(Separate Execution Paths)는 다양성(Diversity)을 제공하고 제어 아키텍처 내부의 공통 원인 고장(Common-Cause Failures)을 줄일 수 있다.

적응형 또는 학습 가능 시스템(Adaptive or Learning-Enabled Systems)에서 제약조건 강제(Constraint Enforcement)는 변화하는 지능 주변에 안정적인 경계를 형성한다. 온라인 학습(Online Learning)은 정책, 월드 모델, 의사결정 전략을 갱신할 수 있지만 이러한 갱신이 기본적인 안전 허가(Fundamental Safety Permissions)를 자동으로 변경하지는 않는다. 따라서 새로운 행동은 통제된 영역 내부에서 탐색하거나 배포할 수 있으며, 불변 안전 요구사항(Invariant Safety Requirements)은 런타임 보증 아키텍처(Runtime Assurance Architecture)에 의해 외부에서 계속 강제된다.

모든 강제 판단(Enforcement Decision)은 관찰 가능하고 추적 가능(Traceable)해야 한다. 시스템은 평가된 제약조건, 측정값, 예측된 위반, 거부되거나 수정된 명령, 활성화된 안전 여유(Activated Margins), 제어기 전환(Controller Transitions), 결과적인 물리 행동을 기록할 수 있다. 이러한 기록은 디버깅(Debugging), 사고 재구성(Incident Reconstruction), 임계값 개선(Threshold Refinement), 검증(Verification), 유효성 확인(Validation), 그리고 운용 중 안전 요구사항이 실제로 강제되었다는 것을 입증하는 데 필요한 증거를 제공한다.

플릿 수준(Fleet Level)에서 제약조건 강제(Constraint Enforcement)는 개별 로봇의 제한을 넘어 공유 운영 제약조건(Shared Operational Constraints)으로 확장된다. 로봇들은 상호 이격 거리(Mutual Separation)를 유지하고, 교통 우선순위(Traffic Priorities)를 준수하며, 충돌하는 예약(Conflicting Reservations)을 피하고, 혼잡을 제한하거나 공유 위험(Shared Hazards)에 대응해야 할 수 있다. 플릿 감독(Fleet Supervision)은 이러한 제약조건을 조정할 수 있지만 통신이나 중앙 집중식 조정이 사용할 수 없게 되더라도 각 로봇은 자신을 보호할 수 있는 로컬 강제(Local Enforcement) 기능을 유지해야 한다.

궁극적으로 런타임 제약조건 강제(Runtime Constraint Enforcement)는 자율 지능(Autonomous Intelligence)과 물리적 제어 권한(Physical Authority) 사이의 실행 가능한 경계(Executable Boundary)를 형성한다. 인공지능 시스템은 정교한 계획, 예측, 적응형 행동을 생성할 수 있지만 활성화된 안전 제약조건(Active Safety Constraints)을 만족하는 행동만 액추에이터(Actuators)에 전달되어야 한다. 예측 평가(Predictive Evaluation), 상황별 제한(Contextual Limits), 불확실성 인식 안전 여유(Uncertainty-Aware Margins), 명령 필터링(Command Filtering), 독립적 제어 권한(Independent Authority), 폴백 단계 전환(Fallback Escalation)을 결합함으로써 런타임 보증(Runtime Assurance)은 추상적인 안전 요구사항을 지속적으로 강제되는 물리적 보호(Physical Protection)로 변환한다.

##  

## 07.04. Safety Envelope and Operational Boundaries

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

A safety envelope defines the set of physical states and behaviors within which a Physical AI system can operate while maintaining specified safety conditions. Operational boundaries translate this abstract safe region into concrete limits on motion, location, interaction, resources, and environmental conditions. Together, they establish where autonomy is permitted and where safety intervention becomes necessary.

Unlike a single fixed threshold, a safety envelope is typically multidimensional. It may simultaneously constrain velocity, acceleration, position, orientation, separation distance, actuator force, stability, battery state, localization confidence, communication quality, and environmental conditions. A robot is considered inside the envelope only when the combination of relevant variables remains within an acceptable region.

The envelope provides an important connection between hazard analysis and runtime assurance. Design-time safety analysis identifies hazardous states, unsafe interactions, and required risk reductions, while the runtime architecture converts these findings into observable boundaries. Monitoring and enforcement mechanisms can then determine whether actual or predicted robot behavior is approaching conditions identified as unacceptable during system development.

Operational boundaries can be physical or logical. Physical boundaries include restricted zones, workspace limits, minimum obstacle clearance, maximum slope, water-depth limits, manipulator reach restrictions, or permitted flight volumes. Logical boundaries may specify allowable operating modes, authorized missions, communication requirements, minimum sensor availability, or conditions under which particular autonomous capabilities may be activated.

Safety envelopes should account for robot dynamics rather than describing only static geometry. A boundary that is safe for a stationary robot may be insufficient for a platform traveling at high speed because stopping distance and maneuverability change with velocity, payload, surface friction, actuator condition, and control latency. Dynamic envelopes therefore incorporate the system\'s ability to avoid or recover from hazardous states.

Human proximity creates another important form of dynamic boundary. As a robot approaches workers, pedestrians, passengers, or collaborators, the permissible velocity, acceleration, force, or trajectory may need to become progressively more restrictive. The safety envelope can consequently contract around the robot as human exposure increases and expand again when sufficient separation and environmental confidence are restored.

Uncertainty should also modify the shape and size of the safety envelope. Increasing localization covariance, reduced perception confidence, sensor disagreement, or out-of-distribution observations mean that the estimated state may differ from the physical state. Runtime assurance can compensate by enlarging obstacle margins, reducing speed limits, restricting maneuver choices, or excluding regions that cannot be observed with sufficient confidence.

The operational design domain defines another boundary around autonomy. Environmental conditions such as lighting, temperature, weather, terrain, visibility, electromagnetic interference, traffic characteristics, or infrastructure availability may determine where a system has been validated to operate. When conditions move outside this validated domain, continued full-performance autonomy should not automatically be assumed safe.

Safety envelopes can therefore be organized hierarchically. Component-level envelopes protect motors, batteries, sensors, and compute hardware; robot-level envelopes constrain motion and stability; task-level boundaries restrict manipulation or navigation behavior; and site-level boundaries define permitted operating regions. Fleet-level boundaries can additionally regulate interactions among multiple robots sharing space, infrastructure, or operational resources.

A runtime monitor continuously estimates the system\'s position relative to these boundaries. Instead of waiting until a constraint has already been violated, it can calculate remaining safety margin and identify trends toward the edge of the envelope. Approaching a boundary may trigger warnings, reduced performance, trajectory replanning, increased separation, or tighter control limits before direct intervention becomes unavoidable.

Prediction extends this concept from current-state assurance to future-state assurance. Planned trajectories, reachable sets, human-motion forecasts, world-model predictions, or conservative dynamic models can estimate whether the robot is likely to leave the safe region. An action may therefore be rejected even when the present state is safe if its predicted evolution cannot remain inside the required envelope.

Different boundaries can have different levels of strictness. A hard boundary represents a condition that autonomous operation must not intentionally cross, such as a collision region, mechanical limit, or prohibited workspace. A softer operational boundary may indicate a preferred margin where performance should be reduced. This layered structure supports gradual intervention instead of treating every boundary approach as an emergency.

Envelope management must also consider conflicts among constraints. Avoiding an obstacle may require steering toward a workspace boundary, while maintaining stability may limit the acceleration available for collision avoidance. Runtime assurance should evaluate the combined feasible region created by all active constraints and determine whether a safe trajectory still exists rather than considering each boundary independently.

If the feasible safe region becomes very small, the system should become increasingly conservative. Reduced speed, restricted actions, simplified planning, degraded operating modes, or requests for human supervision may preserve safety while maintaining limited functionality. If no safe action remains, the runtime assurance architecture should transition toward a minimum-risk condition, protective stop, or predefined fallback state.

Operational boundaries should be explicitly represented and version controlled because they form part of the system\'s safety configuration. Changes to maximum speed, permitted regions, sensor requirements, uncertainty thresholds, or environmental limits can materially alter risk. Such changes should therefore be traceable to engineering justification, verification evidence, system configuration, and appropriate authorization.

Logging the robot\'s relationship to its safety envelope provides valuable operational evidence. Records can include current safety margins, boundary approaches, constraint activations, predicted violations, intervention events, environmental conditions, and recovery behavior. Analysis of these records can reveal whether boundaries are excessively permissive, unnecessarily restrictive, or systematically challenged by real-world operating conditions.

For fleets, safety envelopes must account for moving boundaries created by other agents. Reserved paths, intersection priorities, shared workspaces, temporary exclusion zones, congestion, and communication failures can continuously alter the feasible region for each robot. Fleet coordination can provide global information, while each platform retains local boundaries capable of protecting it independently when centralized information becomes unavailable.

Safety envelopes and operational boundaries ultimately provide a geometric, physical, and logical representation of permissible autonomy. They convert broad safety goals into regions that can be monitored, predicted, and enforced at runtime. By adapting boundaries to dynamics, uncertainty, human proximity, system health, and environmental context, Physical AI can pursue useful behavior while maintaining explicit limits on where autonomous authority is allowed.

안전 영역(Safety Envelope)은 물리 인공지능(Physical AI) 시스템이 지정된 안전 조건(Safety Conditions)을 유지하면서 작동할 수 있는 물리적 상태와 행동의 집합을 정의한다. 운영 경계(Operational Boundaries)는 이러한 추상적인 안전 영역을 움직임, 위치, 상호작용, 자원 및 환경 조건에 대한 구체적인 제한으로 변환한다. 이 두 개념은 자율성(Autonomy)이 허용되는 범위와 안전 개입(Safety Intervention)이 필요한 경계를 함께 설정한다.

단일한 고정 임계값(Fixed Threshold)과 달리 안전 영역(Safety Envelope)은 일반적으로 다차원적(Multidimensional)이다. 안전 영역은 속도(Velocity), 가속도(Acceleration), 위치(Position), 방향(Orientation), 이격 거리(Separation Distance), 액추에이터 힘(Actuator Force), 안정성(Stability), 배터리 상태(Battery State), 위치추정 신뢰도(Localization Confidence), 통신 품질(Communication Quality), 환경 조건(Environmental Conditions)을 동시에 제한할 수 있다. 관련 변수들의 조합이 허용 가능한 영역 내부에 유지될 때만 로봇이 안전 영역 내부에 있다고 판단한다.

안전 영역(Safety Envelope)은 위험 분석(Hazard Analysis)과 런타임 보증(Runtime Assurance)을 연결하는 중요한 역할을 한다. 설계 단계 안전 분석(Design-Time Safety Analysis)은 위험 상태, 안전하지 않은 상호작용, 필요한 위험 감소 조치를 식별하고, 런타임 아키텍처(Runtime Architecture)는 이러한 결과를 관찰 가능한 경계(Observable Boundaries)로 변환한다. 이후 모니터링 및 강제 메커니즘(Monitoring and Enforcement Mechanisms)은 실제 또는 예측된 로봇 행동이 시스템 개발 과정에서 허용할 수 없는 것으로 정의된 조건에 접근하고 있는지를 판단할 수 있다.

운영 경계(Operational Boundaries)는 물리적(Physical) 또는 논리적(Logical) 형태가 될 수 있다. 물리적 경계에는 제한 구역(Restricted Zones), 작업공간 한계(Workspace Limits), 최소 장애물 여유 거리(Minimum Obstacle Clearance), 최대 경사(Maximum Slope), 수심 제한(Water-Depth Limits), 매니퓰레이터 도달 범위 제한(Manipulator Reach Restrictions), 허용 비행 공간(Permitted Flight Volumes) 등이 포함된다. 논리적 경계에는 허용 가능한 운용 모드(Operating Modes), 승인된 임무(Authorized Missions), 통신 요구사항(Communication Requirements), 최소 센서 가용성(Minimum Sensor Availability), 특정 자율 기능을 활성화할 수 있는 조건 등이 포함될 수 있다.

안전 영역(Safety Envelope)은 정적인 기하구조(Static Geometry)만을 표현하는 것이 아니라 로봇 동역학(Robot Dynamics)을 고려해야 한다. 정지한 로봇에서는 안전한 경계가 고속으로 이동하는 플랫폼에서는 충분하지 않을 수 있는데, 속도, 페이로드(Payload), 노면 마찰(Surface Friction), 액추에이터 상태(Actuator Condition), 제어 지연(Control Latency)에 따라 정지 거리(Stopping Distance)와 기동성(Maneuverability)이 달라지기 때문이다. 따라서 동적 안전 영역(Dynamic Envelope)은 위험 상태를 회피하거나 그 상태에서 복구할 수 있는 시스템의 능력을 반영한다.

인간 근접도(Human Proximity)는 또 다른 중요한 동적 경계(Dynamic Boundary)를 형성한다. 로봇이 작업자, 보행자, 승객 또는 협업자에게 접근할수록 허용 가능한 속도, 가속도, 힘 또는 궤적(Trajectory)은 점진적으로 더욱 제한될 필요가 있다. 따라서 인간의 위험 노출(Human Exposure)이 증가하면 로봇 주변의 안전 영역(Safety Envelope)이 축소되고, 충분한 이격 거리와 환경 신뢰도(Environmental Confidence)가 회복되면 다시 확장될 수 있다.

불확실성(Uncertainty) 또한 안전 영역(Safety Envelope)의 형태와 크기를 변화시켜야 한다. 위치추정 공분산(Localization Covariance)이 증가하거나 인식 신뢰도(Perception Confidence)가 감소하고, 센서 간 불일치(Sensor Disagreement) 또는 분포 외 관측(Out-of-Distribution Observations)이 발생하면 추정 상태가 실제 물리 상태와 달라질 수 있다. 런타임 보증(Runtime Assurance)은 장애물 여유 거리(Obstacle Margins)를 확대하고, 속도 제한을 낮추며, 기동 선택지를 제한하거나 충분한 신뢰도로 관측할 수 없는 영역을 제외함으로써 이를 보상할 수 있다.

운영 설계 영역(Operational Design Domain)은 자율성을 둘러싸는 또 다른 경계를 정의한다. 조명(Lighting), 온도(Temperature), 날씨(Weather), 지형(Terrain), 가시성(Visibility), 전자기 간섭(Electromagnetic Interference), 교통 특성(Traffic Characteristics), 인프라 가용성(Infrastructure Availability)과 같은 환경 조건은 시스템이 검증된 운용 범위를 결정할 수 있다. 환경 조건이 이러한 검증 영역을 벗어나는 경우에도 완전한 성능의 자율 운용(Full-Performance Autonomy)이 계속 안전하다고 자동으로 가정해서는 안 된다.

따라서 안전 영역(Safety Envelope)은 계층적(Hierarchical)으로 구성할 수 있다. 구성요소 수준 안전 영역(Component-Level Envelopes)은 모터, 배터리, 센서, 연산 하드웨어를 보호하고, 로봇 수준 안전 영역(Robot-Level Envelopes)은 움직임과 안정성을 제한한다. 작업 수준 경계(Task-Level Boundaries)는 조작 또는 내비게이션 행동을 제한하며, 사이트 수준 경계(Site-Level Boundaries)는 허용된 운용 영역을 정의한다. 플릿 수준 경계(Fleet-Level Boundaries)는 동일한 공간, 인프라 또는 운영 자원을 공유하는 여러 로봇 간의 상호작용까지 추가적으로 규제할 수 있다.

런타임 모니터(Runtime Monitor)는 이러한 경계에 대한 시스템의 상대적인 위치를 지속적으로 추정한다. 제약조건이 이미 위반될 때까지 기다리는 대신 남아 있는 안전 여유(Safety Margin)를 계산하고 안전 영역의 가장자리로 향하는 추세를 식별할 수 있다. 경계에 접근하면 직접적인 안전 개입이 불가피해지기 전에 경고(Warning), 성능 감소(Reduced Performance), 궤적 재계획(Trajectory Replanning), 이격 거리 증가 또는 더 엄격한 제어 제한을 적용할 수 있다.

예측(Prediction)은 이러한 개념을 현재 상태 보증(Current-State Assurance)에서 미래 상태 보증(Future-State Assurance)으로 확장한다. 계획된 궤적(Planned Trajectories), 도달 가능 집합(Reachable Sets), 인간 움직임 예측(Human-Motion Forecasts), 월드 모델 예측(World-Model Predictions), 보수적인 동역학 모델(Conservative Dynamic Models)을 이용해 로봇이 안전 영역을 벗어날 가능성을 추정할 수 있다. 따라서 현재 상태가 안전하더라도 예측된 변화가 필요한 안전 영역 내부에 유지될 수 없다면 해당 행동을 거부할 수 있다.

서로 다른 경계는 서로 다른 수준의 엄격성(Strictness)을 가질 수 있다. 하드 경계(Hard Boundary)는 충돌 영역(Collision Region), 기계적 한계(Mechanical Limit), 금지 작업공간(Prohibited Workspace)과 같이 자율 운용 중 의도적으로 넘어서는 안 되는 조건을 의미한다. 보다 완화된 운영 경계(Soft Operational Boundary)는 성능을 낮춰야 하는 선호 안전 여유(Preferred Margin)를 나타낼 수 있다. 이러한 계층적 구조(Layered Structure)는 모든 경계 접근을 비상 상황으로 처리하지 않고 점진적인 개입(Gradual Intervention)을 가능하게 한다.

안전 영역 관리(Envelope Management)는 제약조건 사이의 충돌(Constraint Conflicts)도 고려해야 한다. 장애물을 회피하기 위해 작업공간 경계 쪽으로 이동해야 할 수 있으며, 안정성 유지가 충돌 회피에 사용할 수 있는 가속도를 제한할 수도 있다. 런타임 보증(Runtime Assurance)은 각 경계를 독립적으로 판단하는 대신 활성화된 모든 제약조건이 형성하는 결합 실행 가능 영역(Combined Feasible Region)을 평가하고 안전한 궤적이 여전히 존재하는지를 판단해야 한다.

실행 가능한 안전 영역(Feasible Safe Region)이 매우 작아지면 시스템은 점진적으로 더욱 보수적으로 동작해야 한다. 속도 감소(Reduced Speed), 행동 제한(Restricted Actions), 단순화된 계획(Simplified Planning), 성능 저하 운전 모드(Degraded Operating Modes), 인간 감독 요청(Human Supervision Requests)을 통해 제한적인 기능을 유지하면서 안전을 보존할 수 있다. 안전한 행동이 더 이상 존재하지 않는다면 런타임 보증 아키텍처(Runtime Assurance Architecture)는 최소 위험 상태(Minimum-Risk Condition), 보호 정지(Protective Stop), 또는 사전에 정의된 폴백 상태(Fallback State)로 전환해야 한다.

운영 경계(Operational Boundaries)는 시스템 안전 구성(Safety Configuration)의 일부를 형성하므로 명시적으로 표현되고 버전 관리(Version Control)되어야 한다. 최대 속도, 허용 영역, 센서 요구사항, 불확실성 임계값(Uncertainty Thresholds), 환경 한계(Environmental Limits)의 변경은 위험 수준을 실질적으로 변화시킬 수 있다. 따라서 이러한 변경은 공학적 근거(Engineering Justification), 검증 증거(Verification Evidence), 시스템 구성(System Configuration), 적절한 승인(Authorization)과 추적 가능하게 연결되어야 한다.

로봇과 안전 영역(Safety Envelope)의 관계를 로깅(Logging)하면 중요한 운용 증거(Operational Evidence)를 확보할 수 있다. 기록에는 현재 안전 여유(Current Safety Margins), 경계 접근(Boundary Approaches), 제약조건 활성화(Constraint Activations), 예측된 위반(Predicted Violations), 개입 이벤트(Intervention Events), 환경 조건(Environmental Conditions), 복구 행동(Recovery Behavior) 등이 포함될 수 있다. 이러한 기록을 분석하면 경계가 지나치게 허용적인지, 불필요하게 제한적인지 또는 실제 운용 조건에서 반복적으로 위협받고 있는지를 파악할 수 있다.

플릿(Fleet)에서는 안전 영역(Safety Envelope)이 다른 에이전트(Agents)에 의해 생성되는 이동 경계(Moving Boundaries)까지 고려해야 한다. 예약된 경로(Reserved Paths), 교차로 우선순위(Intersection Priorities), 공유 작업공간(Shared Workspaces), 임시 제외 구역(Temporary Exclusion Zones), 혼잡(Congestion), 통신 장애(Communication Failures)는 각 로봇의 실행 가능 영역(Feasible Region)을 지속적으로 변화시킬 수 있다. 플릿 조정(Fleet Coordination)은 전역 정보를 제공할 수 있지만 중앙 정보가 사용할 수 없게 되는 경우에도 각 플랫폼은 독립적으로 자신을 보호할 수 있는 로컬 경계(Local Boundaries)를 유지해야 한다.

안전 영역 및 운영 경계(Safety Envelopes and Operational Boundaries)는 궁극적으로 허용 가능한 자율성(Permissible Autonomy)을 기하학적(Geometric), 물리적(Physical), 논리적(Logical) 형태로 표현한다. 이는 광범위한 안전 목표(Safety Goals)를 런타임에서 모니터링하고 예측하며 강제할 수 있는 영역으로 변환한다. 동역학(Dynamics), 불확실성(Uncertainty), 인간 근접도(Human Proximity), 시스템 건전성(System Health), 환경 상황(Environmental Context)에 따라 경계를 적응시킴으로써 물리 인공지능(Physical AI)은 자율적 권한이 허용되는 범위를 명확하게 제한하면서 유용한 행동을 수행할 수 있다.

##  

## 07.05. Runtime Perception Health Monitoring

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Runtime perception health monitoring evaluates whether the sensing and perception pipeline of a Physical AI system remains sufficiently reliable for safe autonomous operation. It does not ask only what objects, people, surfaces, or obstacles have been detected. It also asks whether the information used to create those detections is trustworthy enough for planning, control, and runtime safety decisions.

Perception health differs from ordinary perception performance because it focuses on operational validity rather than recognition accuracy alone. A camera may continue producing images while its lens is obscured, a LiDAR may return points despite contamination, and a neural detector may generate confident outputs under unfamiliar conditions. Health monitoring therefore evaluates the quality and credibility of the complete perception process.

Monitoring begins with the physical condition and availability of sensors. Cameras, LiDAR, radar, ultrasonic sensors, depth sensors, IMUs, GNSS receivers, encoders, and other devices can experience disconnection, overheating, vibration, contamination, saturation, timing faults, or calibration changes. Detecting these conditions early prevents apparently valid but degraded measurements from silently entering the autonomy pipeline.

Signal-level quality provides another important source of evidence. Image brightness, blur, contrast, exposure, occlusion, dropped frames, LiDAR point density, radar return quality, IMU noise, GNSS satellite availability, and depth completeness can indicate whether sensor information remains usable. These metrics allow degradation to be detected before it produces an obvious failure in downstream perception outputs.

Temporal health monitoring determines whether perception data arrives with the required timing characteristics. Autonomous systems depend not only on accurate observations but also on observations representing the current physical world. Excessive latency, timestamp errors, frame loss, synchronization drift, or stale messages can cause planning to operate on outdated conditions, creating hazards even when individual measurements are technically correct.

Calibration health is especially important in multimodal Physical AI systems. Changes in camera intrinsics, sensor extrinsics, LiDAR-camera alignment, IMU orientation, or coordinate transformations can systematically distort the reconstructed environment. Runtime consistency checks can identify growing disagreement between sensor geometry and expected relationships, indicating that recalibration, degradation, or restricted operation may be required.

Perception health monitoring should extend beyond raw sensors to intermediate representations. Object detections, semantic segmentation, occupancy maps, depth estimates, traversability maps, human tracking, free-space estimates, and scene representations may become unstable even when the sensors themselves appear healthy. Monitoring these representations helps identify failures introduced by preprocessing, inference, fusion, or post-processing stages.

Cross-sensor consistency provides powerful evidence because different sensing modalities observe the same physical environment through different mechanisms. A pedestrian detected by a camera may be compared with LiDAR geometry or radar returns, while estimated ego-motion can be checked against wheel odometry and IMU measurements. Persistent disagreement can reveal sensor faults, calibration errors, perception failures, or unusual environmental conditions.

Redundancy alone, however, does not guarantee trustworthy perception. Multiple sensors can fail together because of rain, fog, dust, glare, darkness, vibration, electromagnetic interference, or shared compute failures. Runtime monitoring should therefore distinguish independent disagreement from correlated degradation and evaluate whether the remaining sensing diversity is sufficient to support the safety requirements of the current operating mode.

Model confidence can contribute to perception health but should not be treated as definitive evidence. Neural perception systems may produce high confidence for incorrect predictions, particularly under distribution shift or unfamiliar scenes. Confidence scores should therefore be combined with calibration information, sensor quality, temporal consistency, model disagreement, environmental context, and out-of-distribution indicators.

Temporal consistency can reveal perception instability that is difficult to detect from a single frame. Objects should normally evolve according to physically plausible motion, occupancy should not change arbitrarily, and tracked entities should maintain reasonable continuity. Sudden label changes, impossible jumps, flickering detections, inconsistent depth, or rapidly changing confidence can indicate that the perception pipeline is becoming unreliable.

Environmental conditions should be included because perception capability depends strongly on operating context. Heavy rain may reduce camera and LiDAR quality, low illumination can degrade vision, reflective surfaces can disturb ranging, and dust or snow can generate misleading returns. Health monitoring can compare current conditions with validated perception capabilities and determine whether safety margins or operating modes should change.

A useful perception health architecture aggregates multiple indicators into a health state rather than relying on a single pass-or-fail signal. The system may classify perception as normal, degraded, severely degraded, or unavailable. Each state can correspond to specific operational permissions, allowing autonomy to continue with controlled restrictions when sufficient perception remains instead of immediately treating every degradation as total failure.

When perception health deteriorates, runtime assurance should modify the safety envelope accordingly. Reduced confidence may require lower velocity, greater obstacle clearance, increased human separation, shorter planning horizons, restricted routes, or simpler maneuvers. The important principle is that the robot\'s allowed behavior should become more conservative as its ability to observe the physical environment becomes less trustworthy.

Sensor fallback can preserve limited autonomy when suitable redundancy exists. If one camera fails, another viewpoint may provide partial coverage; GNSS degradation may be compensated by LiDAR or visual localization; and a failed perception model may be replaced by a simpler backup detector. The fallback capability must nevertheless be evaluated against the actual safety requirements rather than assumed equivalent to normal perception.

If perception becomes insufficient to establish safe operation, the system should not continue merely because no hazard has been detected. Failure to observe a person or obstacle is fundamentally different from proving that none exists. Runtime assurance should therefore transition toward degraded operation, human assistance, minimum-risk behavior, or protective stopping when environmental observability falls below the required threshold.

Perception health monitoring must also consider computational dependencies. GPU overload, memory pressure, thermal throttling, inference timeout, corrupted model state, middleware congestion, or process failure can degrade perception without producing a physical sensor fault. Monitoring execution rate, processing latency, resource availability, queue depth, and inference completion provides visibility into this computational dimension of perception reliability.

Logging supports diagnosis and continuous improvement of perception assurance. Sensor-health indicators, quality metrics, confidence values, disagreement events, environmental conditions, timing faults, fallback transitions, and safety interventions can be recorded together. These traces help engineers reconstruct incidents, identify recurring degradation patterns, refine thresholds, improve models, and establish operational evidence for safety validation.

Runtime perception health monitoring ultimately determines whether the Physical AI system can trust its own observation of the world sufficiently to exercise autonomous authority. By combining sensor diagnostics, signal quality, timing, calibration, cross-modal consistency, model behavior, uncertainty, environmental context, and compute health, the system can adapt its behavior before degraded perception becomes unsafe physical action.

런타임 인식 건전성 모니터링(Runtime Perception Health Monitoring)은 물리 인공지능(Physical AI) 시스템의 센싱 및 인식 파이프라인(Sensing and Perception Pipeline)이 안전한 자율 운용을 수행하기에 충분한 신뢰성을 유지하고 있는지를 평가한다. 이는 단순히 어떤 객체, 사람, 표면 또는 장애물이 탐지되었는지만 확인하는 것이 아니다. 이러한 탐지를 생성하는 데 사용된 정보가 계획(Planning), 제어(Control), 런타임 안전 판단(Runtime Safety Decisions)에 사용할 만큼 신뢰할 수 있는지도 함께 판단한다.

인식 건전성(Perception Health)은 단순한 인식 성능(Perception Performance)과 다르다. 인식 정확도만이 아니라 운용상의 유효성(Operational Validity)에 초점을 맞추기 때문이다. 카메라는 렌즈가 가려져 있어도 영상을 계속 생성할 수 있고, 라이다(LiDAR)는 오염된 상태에서도 포인트를 반환할 수 있으며, 신경망 탐지기(Neural Detector)는 익숙하지 않은 조건에서도 높은 신뢰도의 결과를 생성할 수 있다. 따라서 건전성 모니터링(Health Monitoring)은 전체 인식 과정의 품질과 신뢰성을 평가한다.

모니터링은 센서의 물리적 상태와 가용성(Availability)을 확인하는 것에서 시작한다. 카메라, 라이다(LiDAR), 레이더(Radar), 초음파 센서(Ultrasonic Sensor), 깊이 센서(Depth Sensor), 관성 측정 장치(IMU), 위성항법시스템 수신기(GNSS Receiver), 엔코더(Encoder) 등의 장치는 연결 해제, 과열, 진동, 오염, 포화(Saturation), 타이밍 오류(Timing Fault), 캘리브레이션 변화(Calibration Change)를 경험할 수 있다. 이러한 상태를 조기에 탐지하면 겉보기에는 정상적이지만 성능이 저하된 측정값이 자율 시스템 파이프라인에 조용히 유입되는 것을 방지할 수 있다.

신호 수준 품질(Signal-Level Quality)은 또 다른 중요한 판단 근거를 제공한다. 영상 밝기(Image Brightness), 흐림(Blur), 대비(Contrast), 노출(Exposure), 가림(Occlusion), 프레임 손실(Dropped Frames), 라이다 포인트 밀도(LiDAR Point Density), 레이더 반사 품질(Radar Return Quality), 관성 측정 장치 노이즈(IMU Noise), 위성항법시스템 위성 가용성(GNSS Satellite Availability), 깊이 정보 완전성(Depth Completeness)은 센서 정보가 계속 사용 가능한지를 나타낼 수 있다. 이러한 지표를 이용하면 하위 인식 결과에서 명확한 고장이 발생하기 전에 성능 저하를 탐지할 수 있다.

시간적 건전성 모니터링(Temporal Health Monitoring)은 인식 데이터가 요구되는 시간 특성(Timing Characteristics)에 맞게 도착하는지를 판단한다. 자율 시스템은 정확한 관측뿐만 아니라 현재의 물리적 세계를 반영하는 관측에도 의존한다. 과도한 지연시간(Excessive Latency), 타임스탬프 오류(Timestamp Errors), 프레임 손실(Frame Loss), 동기화 드리프트(Synchronization Drift), 오래된 메시지(Stale Messages)는 개별 측정값 자체가 정확하더라도 계획 시스템이 과거의 환경 상태를 기반으로 동작하게 만들어 위험을 발생시킬 수 있다.

캘리브레이션 건전성(Calibration Health)은 다중모달 물리 인공지능(Multimodal Physical AI) 시스템에서 특히 중요하다. 카메라 내부 파라미터(Camera Intrinsics), 센서 외부 파라미터(Sensor Extrinsics), 라이다-카메라 정렬(LiDAR-Camera Alignment), 관성 측정 장치 방향(IMU Orientation), 좌표 변환(Coordinate Transformations)의 변화는 재구성된 환경을 체계적으로 왜곡할 수 있다. 런타임 일관성 검사(Runtime Consistency Checks)는 센서 기하구조와 예상 관계 사이에서 증가하는 불일치를 식별하여 재캘리브레이션(Recalibration), 성능 저하 또는 제한된 운용이 필요한지를 판단할 수 있다.

인식 건전성 모니터링(Perception Health Monitoring)은 원시 센서(Raw Sensors)를 넘어 중간 표현(Intermediate Representations)까지 확장되어야 한다. 객체 탐지(Object Detection), 의미론적 분할(Semantic Segmentation), 점유 지도(Occupancy Maps), 깊이 추정(Depth Estimation), 주행 가능성 지도(Traversability Maps), 인간 추적(Human Tracking), 자유 공간 추정(Free-Space Estimation), 장면 표현(Scene Representations)은 센서 자체가 정상적으로 보이더라도 불안정해질 수 있다. 이러한 표현을 모니터링하면 전처리, 추론, 융합 또는 후처리 단계에서 발생하는 고장을 식별할 수 있다.

센서 간 일관성(Cross-Sensor Consistency)은 서로 다른 센싱 모달리티(Sensing Modalities)가 서로 다른 원리를 통해 동일한 물리적 환경을 관측하기 때문에 강력한 판단 근거를 제공한다. 카메라가 탐지한 보행자를 라이다 기하정보 또는 레이더 반사와 비교할 수 있으며, 추정된 자체 움직임(Ego-Motion)은 휠 오도메트리(Wheel Odometry) 및 관성 측정 장치 데이터와 비교할 수 있다. 지속적인 불일치는 센서 고장, 캘리브레이션 오류, 인식 실패 또는 비정상적인 환경 조건을 나타낼 수 있다.

그러나 중복성(Redundancy)만으로 신뢰할 수 있는 인식을 보장할 수 있는 것은 아니다. 여러 센서가 비, 안개, 먼지, 눈부심, 어둠, 진동, 전자기 간섭(Electromagnetic Interference), 공유 연산 장애(Shared Compute Failures) 때문에 동시에 성능이 저하될 수 있다. 따라서 런타임 모니터링은 독립적인 불일치(Independent Disagreement)와 상관된 성능 저하(Correlated Degradation)를 구분하고, 남아 있는 센싱 다양성(Sensing Diversity)이 현재 운용 모드의 안전 요구사항을 지원하기에 충분한지를 평가해야 한다.

모델 신뢰도(Model Confidence)는 인식 건전성 판단에 활용될 수 있지만 결정적인 증거로 취급해서는 안 된다. 신경망 기반 인식 시스템(Neural Perception Systems)은 특히 분포 변화(Distribution Shift)나 익숙하지 않은 장면에서 잘못된 예측에 대해서도 높은 신뢰도를 출력할 수 있다. 따라서 신뢰도 점수(Confidence Scores)는 캘리브레이션 정보, 센서 품질, 시간적 일관성, 모델 간 불일치(Model Disagreement), 환경 상황(Environmental Context), 분포 외 지표(Out-of-Distribution Indicators)와 함께 사용해야 한다.

시간적 일관성(Temporal Consistency)은 단일 프레임만으로 탐지하기 어려운 인식 불안정성을 드러낼 수 있다. 객체는 일반적으로 물리적으로 타당한 움직임에 따라 변화해야 하고, 점유 상태(Occupancy)는 임의로 변화해서는 안 되며, 추적 대상은 합리적인 연속성을 유지해야 한다. 갑작스러운 라벨 변화, 불가능한 위치 도약, 깜박이는 탐지(Flickering Detections), 일관되지 않은 깊이, 급격하게 변화하는 신뢰도는 인식 파이프라인의 신뢰성이 저하되고 있음을 나타낼 수 있다.

환경 조건(Environmental Conditions)은 인식 능력이 운용 상황에 크게 의존하기 때문에 반드시 고려되어야 한다. 폭우는 카메라와 라이다 품질을 저하시킬 수 있고, 낮은 조도(Low Illumination)는 비전 성능을 떨어뜨리며, 반사 표면(Reflective Surfaces)은 거리 측정을 방해하고, 먼지나 눈은 오해를 유발하는 센서 반사값을 생성할 수 있다. 건전성 모니터링은 현재 환경 조건을 검증된 인식 능력(Validated Perception Capabilities)과 비교하여 안전 여유(Safety Margins) 또는 운용 모드(Operating Modes)를 변경해야 하는지를 판단할 수 있다.

유용한 인식 건전성 아키텍처(Perception Health Architecture)는 단일한 통과 또는 실패(Pass-or-Fail) 신호에 의존하지 않고 여러 지표를 통합하여 건전성 상태(Health State)를 구성한다. 시스템은 인식 상태를 정상(Normal), 성능 저하(Degraded), 심각한 성능 저하(Severely Degraded), 사용 불가(Unavailable) 등으로 분류할 수 있다. 각 상태를 특정 운영 권한(Operational Permissions)과 연결하면 모든 성능 저하를 즉시 전체 고장으로 처리하지 않고 충분한 인식 능력이 남아 있는 경우 제한된 조건에서 자율성을 유지할 수 있다.

인식 건전성(Perception Health)이 저하되면 런타임 보증(Runtime Assurance)은 이에 따라 안전 영역(Safety Envelope)을 변경해야 한다. 신뢰도 감소는 더 낮은 속도, 더 큰 장애물 여유 거리, 증가된 인간 이격 거리, 짧은 계획 범위(Planning Horizon), 제한된 경로 또는 단순한 기동을 요구할 수 있다. 핵심 원칙은 물리적 환경을 관측하는 능력에 대한 신뢰도가 낮아질수록 로봇에게 허용되는 행동도 더욱 보수적으로 제한되어야 한다는 것이다.

적절한 중복성(Redundancy)이 존재한다면 센서 폴백(Sensor Fallback)을 통해 제한적인 자율성을 유지할 수 있다. 하나의 카메라가 고장 나면 다른 시점의 카메라가 부분적인 관측 범위를 제공할 수 있고, 위성항법시스템 성능이 저하되면 라이다 또는 비전 위치추정(Visual Localization)으로 보완할 수 있으며, 인식 모델이 고장 나면 더 단순한 백업 탐지기(Backup Detector)로 대체할 수 있다. 그러나 폴백 능력이 정상 인식과 동등하다고 가정해서는 안 되며 실제 안전 요구사항을 기준으로 평가해야 한다.

인식 능력이 안전한 운용을 입증하기에 불충분해지면 단순히 위험이 탐지되지 않았다는 이유로 시스템이 계속 작동해서는 안 된다. 사람이나 장애물을 관측하지 못한 것은 그것이 존재하지 않는다는 사실을 입증하는 것과 근본적으로 다르다. 따라서 환경 관측 가능성(Environmental Observability)이 요구되는 임계값 아래로 떨어지면 런타임 보증은 성능 저하 운용(Degraded Operation), 인간 지원(Human Assistance), 최소 위험 행동(Minimum-Risk Behavior), 또는 보호 정지(Protective Stop)로 전환해야 한다.

인식 건전성 모니터링(Perception Health Monitoring)은 연산 의존성(Computational Dependencies)도 고려해야 한다. GPU 과부하, 메모리 압박(Memory Pressure), 열 스로틀링(Thermal Throttling), 추론 시간 초과(Inference Timeout), 손상된 모델 상태(Corrupted Model State), 미들웨어 혼잡(Middleware Congestion), 프로세스 고장(Process Failure)은 물리적 센서 고장 없이도 인식 성능을 저하시킬 수 있다. 실행 주기(Execution Rate), 처리 지연시간(Processing Latency), 자원 가용성(Resource Availability), 큐 깊이(Queue Depth), 추론 완료 상태(Inference Completion)를 모니터링하면 인식 신뢰성의 연산적 측면을 파악할 수 있다.

로깅(Logging)은 인식 보증(Perception Assurance)의 진단과 지속적인 개선을 지원한다. 센서 건전성 지표(Sensor-Health Indicators), 품질 지표(Quality Metrics), 신뢰도 값, 불일치 이벤트(Disagreement Events), 환경 조건, 타이밍 오류, 폴백 전환(Fallback Transitions), 안전 개입(Safety Interventions)을 함께 기록할 수 있다. 이러한 추적 정보는 엔지니어가 사고를 재구성하고, 반복되는 성능 저하 패턴을 식별하며, 임계값을 개선하고, 모델을 향상시키며, 안전 검증(Safety Validation)을 위한 운용 증거를 구축하는 데 도움을 준다.

궁극적으로 런타임 인식 건전성 모니터링(Runtime Perception Health Monitoring)은 물리 인공지능(Physical AI) 시스템이 자율적 권한(Autonomous Authority)을 행사할 수 있을 만큼 자신의 세계 관측을 신뢰할 수 있는지를 판단한다. 센서 진단(Sensor Diagnostics), 신호 품질(Signal Quality), 타이밍(Timing), 캘리브레이션(Calibration), 교차 모달 일관성(Cross-Modal Consistency), 모델 행동(Model Behavior), 불확실성(Uncertainty), 환경 상황(Environmental Context), 연산 건전성(Compute Health)을 결합함으로써 시스템은 성능이 저하된 인식이 위험한 물리적 행동으로 이어지기 전에 자신의 행동을 적응시킬 수 있다.

##  

## 07.06. Runtime AI Model Health Monitoring

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Runtime AI model health monitoring determines whether the learned models inside a Physical AI system remain sufficiently reliable for continued autonomous operation. Unlike conventional software, AI models can continue producing syntactically valid outputs while their predictions become unreliable. Runtime assurance must therefore evaluate not only whether inference executes, but whether model behavior remains trustworthy in the current operating context.

Model health is broader than conventional process health. A neural network may be loaded correctly, consume inputs, and return outputs within its timing deadline while still making systematically incorrect predictions. Distribution shift, unfamiliar objects, environmental changes, corrupted inputs, calibration errors, or unexpected interactions can degrade decision quality without producing an explicit software exception or hardware fault.

The first monitoring dimension is inference execution health. Runtime supervision can observe model availability, inference completion, execution latency, throughput, memory consumption, GPU utilization, thermal conditions, queue depth, and timeout events. These indicators reveal whether the computational environment can continue supporting the model at the frequency and responsiveness required by perception, prediction, planning, or control.

Input validity provides another essential health signal because model reliability depends on receiving data similar to what the model can meaningfully process. Missing modalities, malformed tensors, stale observations, abnormal value ranges, sensor degradation, synchronization errors, or preprocessing failures can invalidate inference. Model monitoring should therefore verify that incoming data satisfies expected structural, temporal, and statistical conditions.

Distribution shift monitoring evaluates whether runtime inputs remain sufficiently close to the conditions represented during training and validation. Changes in weather, terrain, lighting, object appearance, human behavior, robot configuration, payload, or site characteristics can move observations outside familiar regions. Detecting such shifts provides evidence that nominal validation results may no longer represent current model performance.

Out-of-distribution detection provides a related but more explicit warning that the model may be encountering conditions outside its supported knowledge. Embedding distance, feature statistics, density estimates, reconstruction signals, ensemble disagreement, or specialized detectors can contribute to this judgment. No individual indicator is universally reliable, so multiple forms of evidence should be combined when safety depends on the result.

Confidence monitoring examines whether model outputs contain useful evidence about prediction reliability. Classification probabilities, detection confidence, predictive distributions, uncertainty estimates, or policy scores can reveal weakening certainty. However, neural models may be confidently wrong, so raw confidence should not be interpreted as safety evidence without calibration, consistency checks, environmental context, and independent observations.

Calibration monitoring evaluates whether confidence remains statistically meaningful. A well-calibrated model should exhibit a reasonable relationship between predicted confidence and observed correctness. Runtime conditions may gradually invalidate calibration established during validation. Tracking confidence distributions, prediction outcomes where observable, and disagreement patterns can indicate when model certainty is becoming systematically misleading.

Model disagreement is especially valuable when multiple models or ensemble members provide partially independent estimates. If several models that normally agree begin producing substantially different classifications, trajectories, occupancy predictions, or action recommendations, the disagreement may indicate ambiguity or unfamiliar conditions. Increased disagreement can therefore serve as a practical signal for reducing autonomous authority.

Temporal consistency provides another dimension of model health. Predictions concerning objects, motion, occupancy, intent, or future states should generally evolve according to plausible physical continuity. Sudden oscillations, unstable classifications, rapidly switching plans, impossible state transitions, or large output changes caused by small input variations can indicate model instability even when individual predictions appear reasonable.

For world models, runtime health monitoring should evaluate prediction quality over time rather than treating generated future states as inherently trustworthy. Short-horizon predictions can be compared with subsequent observations to measure prediction error, drift, occupancy consistency, motion accuracy, and state-transition plausibility. Growing prediction error may indicate that the internal model is losing alignment with the actual physical environment.

Policy and VLA health monitoring focuses on the actions proposed by learned decision models. Generated commands can be examined for constraint violations, unusual action distributions, excessive oscillation, inconsistency with task context, or divergence from verified behavior patterns. A language-conditioned command that is semantically plausible must still be checked against the robot\'s physical state, operational permissions, and safety envelope.

Health monitoring should distinguish model uncertainty from environmental uncertainty and system faults. Poor predictions may originate from an unfamiliar scene, damaged sensor, incorrect calibration, compute overload, corrupted model state, or genuinely ambiguous environment. Combining model-level indicators with perception health, sensor diagnostics, system health, and contextual information helps prevent incorrect diagnosis and supports more appropriate fallback decisions.

A useful architecture aggregates these signals into an explicit model health state. Rather than declaring the model simply healthy or failed, the runtime system can classify it as normal, degraded, severely degraded, or unavailable. Each health state can correspond to predefined limits on autonomous authority, allowing the system to preserve useful capability while progressively reducing dependence on models whose reliability is becoming uncertain.

When model health degrades, the safety envelope should become more conservative. The system may reduce speed, increase separation margins, restrict routes, shorten planning horizons, simplify tasks, disable uncertain capabilities, or require confirmation from another model or deterministic mechanism. This establishes a direct relationship between confidence in learned intelligence and the amount of physical authority granted to that intelligence.

Fallback strategies may include switching to a validated backup model, deterministic controller, simpler perception algorithm, conservative planner, remote supervision, or minimum-risk behavior. A backup should not merely reproduce the same architecture and failure modes as the primary model. Diversity in algorithms, training data, sensing dependencies, and computational paths can reduce the probability of common-cause failure.

Runtime model monitoring is particularly important for systems that adapt after deployment. Online learning, parameter-efficient fine-tuning, policy updates, memory augmentation, or site-specific adaptation can alter behavior after initial validation. Model identity, version, configuration, adaptation history, and active parameters should therefore remain traceable so that runtime behavior can be associated with the exact intelligence configuration controlling the robot.

Logging transforms model health monitoring into evidence for continuous assurance. Input statistics, uncertainty measures, confidence distributions, disagreement events, inference latency, prediction errors, detected shifts, model versions, fallback transitions, and safety interventions can be recorded together. These traces support incident reconstruction, threshold refinement, model improvement, regression analysis, and future verification activities.

Runtime AI model health monitoring ultimately answers whether learned intelligence remains trustworthy enough to retain its current level of autonomous authority. By combining execution health, input validity, distribution awareness, uncertainty, calibration, disagreement, temporal consistency, predictive accuracy, behavioral checks, and traceability, Physical AI can reduce or transfer control before deteriorating model reliability becomes unsafe physical behavior.

런타임 인공지능 모델 건전성 모니터링(Runtime AI Model Health Monitoring)은 물리 인공지능(Physical AI) 시스템 내부의 학습 모델(Learned Model)이 지속적인 자율 운용(Autonomous Operation)을 수행하기에 충분한 신뢰성을 유지하고 있는지를 판단한다. 기존 소프트웨어와 달리 인공지능 모델은 예측이 신뢰할 수 없는 상태가 되더라도 문법적으로 유효한 출력을 계속 생성할 수 있다. 따라서 런타임 보증(Runtime Assurance)은 추론(Inference)이 실행되는지만 확인하는 것이 아니라 현재 운용 상황에서 모델의 행동이 계속 신뢰할 수 있는지도 평가해야 한다.

모델 건전성(Model Health)은 일반적인 프로세스 건전성(Process Health)보다 넓은 개념이다. 신경망(Neural Network)은 정상적으로 로드되고 입력을 처리하며 정해진 시간 내에 출력을 반환하면서도 체계적으로 잘못된 예측을 생성할 수 있다. 분포 변화(Distribution Shift), 익숙하지 않은 객체, 환경 변화, 손상된 입력(Corrupted Inputs), 캘리브레이션 오류(Calibration Errors), 예상하지 못한 상호작용은 명시적인 소프트웨어 예외나 하드웨어 고장을 발생시키지 않으면서 의사결정 품질을 저하시킬 수 있다.

첫 번째 모니터링 차원은 추론 실행 건전성(Inference Execution Health)이다. 런타임 감독(Runtime Supervision)은 모델 가용성(Model Availability), 추론 완료(Inference Completion), 실행 지연시간(Execution Latency), 처리량(Throughput), 메모리 사용량, GPU 사용률, 열 상태(Thermal Conditions), 큐 깊이(Queue Depth), 시간 초과 이벤트(Timeout Events)를 관찰할 수 있다. 이러한 지표는 연산 환경이 인식, 예측, 계획 또는 제어에 필요한 주기와 응답성으로 모델을 계속 지원할 수 있는지를 보여준다.

입력 유효성(Input Validity)은 모델 신뢰성이 모델이 의미 있게 처리할 수 있는 데이터를 입력받는 것에 의존하기 때문에 또 다른 핵심 건전성 신호가 된다. 누락된 모달리티(Missing Modalities), 잘못 형성된 텐서(Malformed Tensors), 오래된 관측(Stale Observations), 비정상적인 값 범위, 센서 성능 저하, 동기화 오류, 전처리 실패(Preprocessing Failures)는 추론을 무효화할 수 있다. 따라서 모델 모니터링은 입력 데이터가 예상되는 구조적, 시간적, 통계적 조건을 만족하는지 검증해야 한다.

분포 변화 모니터링(Distribution Shift Monitoring)은 런타임 입력이 학습 및 검증 과정에서 표현된 조건과 충분히 가까운지를 평가한다. 날씨, 지형, 조명, 객체 외형, 인간 행동, 로봇 구성, 페이로드(Payload), 사이트 특성의 변화는 관측 데이터를 익숙한 영역 밖으로 이동시킬 수 있다. 이러한 변화를 탐지하면 기존의 검증 결과가 현재 모델 성능을 더 이상 적절하게 대표하지 못할 가능성을 판단할 수 있다.

분포 외 탐지(Out-of-Distribution Detection)는 모델이 지원되는 지식 범위를 벗어난 조건을 경험하고 있을 가능성을 보다 명시적으로 경고한다. 임베딩 거리(Embedding Distance), 특징 통계(Feature Statistics), 밀도 추정(Density Estimates), 재구성 신호(Reconstruction Signals), 앙상블 불일치(Ensemble Disagreement), 전용 탐지기(Specialized Detectors) 등을 이러한 판단에 활용할 수 있다. 어떤 단일 지표도 모든 상황에서 신뢰할 수 있는 것은 아니므로 안전이 판단 결과에 의존하는 경우 여러 형태의 증거를 결합해야 한다.

신뢰도 모니터링(Confidence Monitoring)은 모델 출력에 예측 신뢰성을 판단하는 데 유용한 정보가 포함되어 있는지를 평가한다. 분류 확률(Classification Probabilities), 탐지 신뢰도(Detection Confidence), 예측 분포(Predictive Distributions), 불확실성 추정(Uncertainty Estimates), 정책 점수(Policy Scores)는 확신이 약화되고 있음을 나타낼 수 있다. 그러나 신경망 모델은 틀린 결과에 대해서도 높은 확신을 보일 수 있으므로 원시 신뢰도(Raw Confidence)를 캘리브레이션, 일관성 검사, 환경 상황, 독립적인 관측 없이 안전성의 증거로 해석해서는 안 된다.

캘리브레이션 모니터링(Calibration Monitoring)은 신뢰도가 통계적으로 의미 있는 상태를 유지하는지를 평가한다. 적절하게 캘리브레이션된 모델(Well-Calibrated Model)은 예측된 신뢰도와 실제 정확성 사이에 합리적인 관계를 보여야 한다. 런타임 조건은 검증 과정에서 설정된 캘리브레이션을 점진적으로 무효화할 수 있다. 신뢰도 분포, 관측 가능한 경우의 예측 결과, 불일치 패턴을 추적하면 모델의 확신이 체계적으로 잘못된 방향으로 변하고 있는지를 식별할 수 있다.

여러 모델 또는 앙상블 구성요소(Ensemble Members)가 부분적으로 독립된 추정값을 제공하는 경우 모델 불일치(Model Disagreement)는 특히 중요한 정보를 제공한다. 일반적으로 서로 일치하던 여러 모델이 분류, 궤적, 점유 예측(Occupancy Predictions), 행동 권고(Action Recommendations)에서 크게 다른 결과를 생성하기 시작한다면 이는 모호성 또는 익숙하지 않은 조건을 의미할 수 있다. 따라서 불일치 증가는 자율 권한(Autonomous Authority)을 축소하기 위한 실용적인 신호로 활용될 수 있다.

시간적 일관성(Temporal Consistency)은 모델 건전성의 또 다른 중요한 차원이다. 객체, 움직임, 점유 상태, 의도 또는 미래 상태에 관한 예측은 일반적으로 물리적으로 타당한 연속성에 따라 변화해야 한다. 갑작스러운 진동(Oscillations), 불안정한 분류, 빠르게 전환되는 계획, 불가능한 상태 전이(Impossible State Transitions), 작은 입력 변화에 의해 발생하는 큰 출력 변화는 개별 예측이 합리적으로 보이는 경우에도 모델 불안정성(Model Instability)을 나타낼 수 있다.

월드 모델(World Model)의 경우 런타임 건전성 모니터링은 생성된 미래 상태를 본질적으로 신뢰할 수 있다고 간주하지 않고 시간에 따른 예측 품질을 평가해야 한다. 단기 예측(Short-Horizon Predictions)을 이후의 실제 관측과 비교하여 예측 오류(Prediction Error), 드리프트(Drift), 점유 일관성(Occupancy Consistency), 움직임 정확도(Motion Accuracy), 상태 전이 타당성(State-Transition Plausibility)을 측정할 수 있다. 예측 오류가 증가하면 내부 모델이 실제 물리 환경과의 정합성(Alignment)을 잃고 있음을 나타낼 수 있다.

정책 및 시각-언어-행동 모델 건전성(Policy and VLA Health Monitoring)은 학습 기반 의사결정 모델이 제안하는 행동에 초점을 맞춘다. 생성된 명령은 제약조건 위반(Constraint Violations), 비정상적인 행동 분포(Unusual Action Distributions), 과도한 진동, 작업 상황과의 불일치, 검증된 행동 패턴으로부터의 이탈 여부를 검사할 수 있다. 언어 조건 기반 명령(Language-Conditioned Command)이 의미론적으로 타당하더라도 로봇의 물리적 상태, 운영 권한(Operational Permissions), 안전 영역(Safety Envelope)에 대해 반드시 추가 검증되어야 한다.

건전성 모니터링은 모델 불확실성(Model Uncertainty), 환경 불확실성(Environmental Uncertainty), 시스템 고장(System Faults)을 구분해야 한다. 부정확한 예측은 익숙하지 않은 장면, 손상된 센서, 잘못된 캘리브레이션, 연산 과부하, 손상된 모델 상태 또는 실제로 모호한 환경으로 인해 발생할 수 있다. 모델 수준 지표를 인식 건전성(Perception Health), 센서 진단(Sensor Diagnostics), 시스템 건전성(System Health), 상황 정보(Contextual Information)와 결합하면 잘못된 진단을 방지하고 더욱 적절한 폴백 판단(Fallback Decisions)을 지원할 수 있다.

유용한 아키텍처는 이러한 신호를 통합하여 명시적인 모델 건전성 상태(Model Health State)를 생성한다. 런타임 시스템은 모델을 단순히 정상 또는 고장으로 판단하는 대신 정상(Normal), 성능 저하(Degraded), 심각한 성능 저하(Severely Degraded), 사용 불가(Unavailable)로 분류할 수 있다. 각각의 건전성 상태를 사전에 정의된 자율 권한의 제한과 연결하면 모델 신뢰성이 불확실해질수록 의존도를 점진적으로 낮추면서 유용한 기능은 가능한 범위에서 유지할 수 있다.

모델 건전성(Model Health)이 저하되면 안전 영역(Safety Envelope)은 더욱 보수적으로 변경되어야 한다. 시스템은 속도를 줄이고, 이격 여유(Separation Margins)를 확대하며, 경로를 제한하고, 계획 범위(Planning Horizons)를 단축하며, 작업을 단순화하고, 불확실한 기능을 비활성화하거나 다른 모델 또는 결정론적 메커니즘(Deterministic Mechanism)의 확인을 요구할 수 있다. 이를 통해 학습 지능에 대한 신뢰도와 해당 지능에 부여되는 물리적 권한 사이에 직접적인 관계가 형성된다.

폴백 전략(Fallback Strategies)에는 검증된 백업 모델(Validated Backup Model), 결정론적 제어기(Deterministic Controller), 보다 단순한 인식 알고리즘, 보수적 계획기(Conservative Planner), 원격 감독(Remote Supervision), 최소 위험 행동(Minimum-Risk Behavior)으로의 전환이 포함될 수 있다. 백업 시스템은 주 모델과 동일한 아키텍처 및 고장 형태를 단순히 복제해서는 안 된다. 알고리즘, 학습 데이터, 센싱 의존성, 연산 경로의 다양성(Diversity)을 확보하면 공통 원인 고장(Common-Cause Failure)의 가능성을 줄일 수 있다.

런타임 모델 모니터링(Runtime Model Monitoring)은 배포 이후에도 적응하는 시스템에서 특히 중요하다. 온라인 학습(Online Learning), 파라미터 효율적 미세조정(Parameter-Efficient Fine-Tuning), 정책 업데이트(Policy Updates), 메모리 증강(Memory Augmentation), 사이트 특화 적응(Site-Specific Adaptation)은 초기 검증 이후 시스템 행동을 변화시킬 수 있다. 따라서 모델 식별 정보(Model Identity), 버전, 구성(Configuration), 적응 이력(Adaptation History), 활성 파라미터(Active Parameters)를 추적 가능하게 유지하여 런타임 행동을 실제 로봇을 제어하고 있는 정확한 지능 구성(Intelligence Configuration)과 연결할 수 있어야 한다.

로깅(Logging)은 모델 건전성 모니터링을 지속적인 보증(Continuous Assurance)을 위한 증거로 전환한다. 입력 통계(Input Statistics), 불확실성 척도(Uncertainty Measures), 신뢰도 분포(Confidence Distributions), 불일치 이벤트, 추론 지연시간, 예측 오류, 탐지된 분포 변화, 모델 버전, 폴백 전환, 안전 개입(Safety Interventions)을 함께 기록할 수 있다. 이러한 추적 정보는 사고 재구성(Incident Reconstruction), 임계값 개선(Threshold Refinement), 모델 개선, 회귀 분석(Regression Analysis), 향후 검증 활동을 지원한다.

궁극적으로 런타임 인공지능 모델 건전성 모니터링(Runtime AI Model Health Monitoring)은 학습된 지능(Learned Intelligence)이 현재 수준의 자율 권한(Autonomous Authority)을 계속 유지할 만큼 충분히 신뢰할 수 있는지를 판단한다. 실행 건전성(Execution Health), 입력 유효성(Input Validity), 분포 인식(Distribution Awareness), 불확실성(Uncertainty), 캘리브레이션(Calibration), 불일치(Disagreement), 시간적 일관성(Temporal Consistency), 예측 정확도(Predictive Accuracy), 행동 검사(Behavioral Checks), 추적성(Traceability)을 결합함으로써 물리 인공지능은 모델 신뢰성 저하가 위험한 물리적 행동으로 이어지기 전에 제어 권한을 축소하거나 다른 시스템으로 전환할 수 있다.

##  

## 07.07. Uncertainty and OOD Monitoring

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Uncertainty monitoring determines how confidently a Physical AI system can rely on its perception, prediction, world modeling, planning, and decision outputs during operation. Because autonomous systems act in open and changing environments, uncertainty cannot be eliminated completely. Runtime assurance must therefore estimate when uncertainty is increasing and determine whether the remaining confidence is sufficient for continued autonomous authority.

Uncertainty can originate from several fundamentally different sources. Aleatoric uncertainty reflects ambiguity or noise inherent in observations, such as occlusion, sensor noise, uncertain human motion, or poor visibility. Epistemic uncertainty reflects limitations in the model\'s knowledge, often caused by insufficient training coverage or unfamiliar situations. Distinguishing these sources helps determine whether additional sensing, conservative behavior, or model fallback is appropriate.

Out-of-distribution monitoring focuses on situations that differ significantly from the data or conditions under which an AI model was trained and validated. A robot may encounter unfamiliar objects, unusual terrain, new facility layouts, unexpected weather, novel human behavior, or modified hardware configurations. The model may still produce apparently reasonable outputs, making explicit OOD monitoring important for detecting hidden loss of reliability.

Distribution shift does not always mean that an observation is completely novel. Gradual changes in lighting, sensor characteristics, traffic patterns, payload, surface conditions, or operating procedures can move runtime data away from the original training distribution. Monitoring statistical changes over time helps detect this drift before accumulated differences significantly undermine the assumptions used during model validation.

OOD detection can operate at input, feature, and output levels. Input statistics can reveal unusual sensor distributions, while latent embeddings may show that current observations lie far from known training representations. Output entropy, confidence patterns, reconstruction error, density estimates, energy scores, or specialized OOD detectors can provide additional evidence that the system is operating outside familiar conditions.

No single uncertainty or OOD metric should normally be treated as definitive safety evidence. Neural networks may remain highly confident on unfamiliar inputs, while conservative detectors may generate false alarms for harmless variations. Runtime assurance should therefore combine multiple indicators, including model confidence, embedding distance, ensemble disagreement, sensor quality, temporal consistency, environmental context, and prediction error.

Model ensembles provide a practical method for estimating epistemic uncertainty. Several independently trained models, differently initialized networks, or alternative prediction mechanisms can process the same observations. Strong agreement can increase confidence, whereas substantial disagreement suggests ambiguity or insufficient knowledge. The value of this approach depends on meaningful diversity rather than merely duplicating identical failure modes.

Temporal evidence is important because isolated uncertainty spikes may not justify major intervention. Runtime monitoring can examine whether uncertainty is persistent, increasing, oscillating, or associated with particular environmental changes. A sustained rise in disagreement, prediction error, or OOD score can provide stronger evidence of degraded reliability than a single abnormal observation caused by temporary noise.

World models provide another opportunity for uncertainty monitoring by comparing predicted future states with subsequent observations. If predicted occupancy, object motion, scene evolution, or robot state repeatedly diverges from reality, the model may be operating outside its reliable predictive region. Prediction residuals can therefore serve as runtime evidence that the internal representation of the world is becoming inaccurate.

Uncertainty monitoring should also examine planning and policy outputs. A planner may produce several alternatives with nearly equal value, or a learned policy may rapidly switch between actions when small changes occur in its input. Such behavior can indicate decision uncertainty even when perception appears confident. Monitoring action stability and sensitivity helps identify uncertainty propagating from internal representations into physical control.

Context is essential when interpreting uncertainty. The same numerical confidence level may have different safety implications at low speed in an empty area and at high speed near people. Runtime assurance should therefore combine uncertainty with exposure, stopping distance, mission criticality, environmental complexity, and available fallback options rather than using one universal threshold for every operating condition.

Uncertainty should directly influence the safety envelope. As confidence decreases or OOD evidence increases, permissible velocity can be reduced, obstacle margins enlarged, human separation increased, routes restricted, and planning horizons shortened. This creates an uncertainty-aware operating boundary in which physical authority decreases progressively as the system becomes less certain about its understanding of the environment.

A graded response is generally more useful than a binary normal-or-failed decision. Low uncertainty may permit full autonomy, moderate uncertainty may trigger additional monitoring or reduced performance, and high uncertainty may require restricted capabilities or confirmation from independent systems. Extreme uncertainty can cause transition to a backup controller, human supervision, minimum-risk maneuver, or protective stop.

Recovery is equally important because uncertainty can decrease when conditions improve. A robot leaving a dusty area, reacquiring localization, restoring sensor visibility, or returning to a familiar environment may regain sufficient confidence for broader autonomy. Recovery should nevertheless use defined hysteresis, persistence requirements, or validation checks so that authority does not repeatedly switch between modes because of noisy threshold crossings.

OOD events should be recorded as valuable operational evidence rather than treated only as temporary runtime anomalies. Inputs associated with high uncertainty, unfamiliar embeddings, disagreement, prediction failures, interventions, and environmental context can reveal gaps in training and validation coverage. These records can support dataset expansion, scenario generation, retraining, threshold refinement, and future safety verification.

Monitoring itself must be validated because uncertainty estimates can also fail. Calibration may deteriorate under distribution shift, OOD detectors may be insensitive to certain novelty types, and ensemble members may share common biases. Runtime assurance should therefore avoid assuming that an uncertainty estimator is infallible and should combine model-based signals with independent sensor, system, environmental, and behavioral evidence.

At fleet scale, uncertainty monitoring can reveal patterns that are difficult to identify from a single robot. Multiple robots reporting increased OOD scores or similar prediction errors in the same location may indicate a site-level environmental change or previously unseen condition. Shared evidence can improve collective awareness, while each robot should retain local authority to react immediately to its own uncertainty.

Uncertainty and OOD monitoring ultimately provide a mechanism for recognizing the limits of what a Physical AI system currently knows. Instead of treating every AI output as equally trustworthy, runtime assurance continuously evaluates confidence, novelty, disagreement, prediction accuracy, and contextual risk. Autonomous authority can then contract before uncertain intelligence produces unsafe physical consequences and expand again only when sufficient evidence of reliability returns.

불확실성 모니터링(Uncertainty Monitoring)은 물리 인공지능(Physical AI) 시스템이 운용 중 인식(Perception), 예측(Prediction), 월드 모델링(World Modeling), 계획(Planning), 의사결정(Decision)의 출력을 어느 정도 신뢰할 수 있는지를 판단한다. 자율 시스템은 개방적이고 지속적으로 변화하는 환경에서 작동하므로 불확실성(Uncertainty)을 완전히 제거할 수 없다. 따라서 런타임 보증(Runtime Assurance)은 불확실성이 증가하는 시점을 추정하고 남아 있는 신뢰 수준이 현재의 자율 권한(Autonomous Authority)을 계속 유지하기에 충분한지를 판단해야 한다.

불확실성(Uncertainty)은 근본적으로 서로 다른 여러 원인에서 발생할 수 있다. 우연적 불확실성(Aleatoric Uncertainty)은 가림(Occlusion), 센서 노이즈(Sensor Noise), 불확실한 인간 움직임, 낮은 가시성(Poor Visibility)처럼 관측 자체에 내재된 모호성이나 노이즈를 의미한다. 인식론적 불확실성(Epistemic Uncertainty)은 학습 범위 부족이나 익숙하지 않은 상황 등 모델 지식의 한계에서 발생한다. 이러한 원인을 구분하면 추가 센싱(Additional Sensing), 보수적 행동(Conservative Behavior), 모델 폴백(Model Fallback) 중 어떤 대응이 적절한지 판단하는 데 도움이 된다.

분포 외 모니터링(Out-of-Distribution Monitoring)은 인공지능 모델이 학습 및 검증된 데이터나 조건과 크게 다른 상황에 초점을 맞춘다. 로봇은 익숙하지 않은 객체, 비정상적인 지형, 새로운 시설 배치, 예상하지 못한 날씨, 새로운 인간 행동 또는 변경된 하드웨어 구성을 만날 수 있다. 이러한 상황에서도 모델은 겉보기에는 합리적인 출력을 생성할 수 있기 때문에 숨겨진 신뢰성 저하를 탐지하기 위한 명시적인 분포 외 모니터링(OOD Monitoring)이 중요하다.

분포 변화(Distribution Shift)가 항상 관측 데이터가 완전히 새로운 것임을 의미하는 것은 아니다. 조명, 센서 특성, 교통 패턴, 페이로드(Payload), 노면 상태 또는 운영 절차의 점진적인 변화도 런타임 데이터를 원래의 학습 분포에서 벗어나게 할 수 있다. 시간에 따른 통계적 변화를 모니터링하면 누적된 차이가 모델 검증 과정에서 사용한 가정을 심각하게 약화시키기 전에 이러한 드리프트(Drift)를 탐지할 수 있다.

분포 외 탐지(OOD Detection)는 입력(Input), 특징(Feature), 출력(Output) 수준에서 수행할 수 있다. 입력 통계(Input Statistics)는 비정상적인 센서 분포를 나타낼 수 있으며, 잠재 임베딩(Latent Embeddings)은 현재 관측이 알려진 학습 표현으로부터 얼마나 멀리 떨어져 있는지를 보여줄 수 있다. 출력 엔트로피(Output Entropy), 신뢰도 패턴(Confidence Patterns), 재구성 오류(Reconstruction Error), 밀도 추정(Density Estimates), 에너지 점수(Energy Scores), 전용 분포 외 탐지기(Specialized OOD Detectors)도 시스템이 익숙한 조건을 벗어나고 있다는 추가적인 증거를 제공할 수 있다.

어떠한 단일 불확실성 또는 분포 외 지표도 일반적으로 결정적인 안전 증거로 간주해서는 안 된다. 신경망(Neural Network)은 익숙하지 않은 입력에서도 높은 신뢰도를 유지할 수 있으며, 지나치게 보수적인 탐지기는 무해한 변화에도 잘못된 경보(False Alarm)를 발생시킬 수 있다. 따라서 런타임 보증(Runtime Assurance)은 모델 신뢰도(Model Confidence), 임베딩 거리(Embedding Distance), 앙상블 불일치(Ensemble Disagreement), 센서 품질(Sensor Quality), 시간적 일관성(Temporal Consistency), 환경 상황(Environmental Context), 예측 오류(Prediction Error) 등 여러 지표를 결합해야 한다.

모델 앙상블(Model Ensembles)은 인식론적 불확실성(Epistemic Uncertainty)을 추정하기 위한 실용적인 방법을 제공한다. 서로 독립적으로 학습된 여러 모델, 서로 다른 초기값을 사용하는 신경망 또는 대안적인 예측 메커니즘이 동일한 관측을 처리할 수 있다. 강한 일치(Strong Agreement)는 신뢰도를 높일 수 있지만 상당한 불일치는 모호성 또는 지식 부족을 의미한다. 이 접근법의 가치는 단순히 동일한 고장 형태를 복제하는 것이 아니라 의미 있는 다양성(Diversity)을 확보하는 데 달려 있다.

시간적 증거(Temporal Evidence)도 중요하다. 일시적인 불확실성 상승만으로는 큰 규모의 개입을 정당화하기 어려울 수 있기 때문이다. 런타임 모니터링(Runtime Monitoring)은 불확실성이 지속되는지, 증가하는지, 진동하는지 또는 특정 환경 변화와 연관되어 있는지를 확인할 수 있다. 불일치, 예측 오류 또는 분포 외 점수(OOD Score)가 지속적으로 증가한다면 일시적인 노이즈로 인한 단일 비정상 관측보다 신뢰성 저하에 대한 더 강한 증거가 될 수 있다.

월드 모델(World Model)은 예측된 미래 상태를 이후의 실제 관측과 비교함으로써 불확실성을 모니터링할 수 있는 또 다른 기회를 제공한다. 예측된 점유 상태(Occupancy), 객체 움직임(Object Motion), 장면 변화(Scene Evolution), 로봇 상태가 실제 상황과 반복적으로 벗어난다면 모델이 신뢰할 수 있는 예측 영역을 벗어나고 있을 수 있다. 따라서 예측 잔차(Prediction Residuals)는 내부 세계 표현이 부정확해지고 있음을 나타내는 런타임 증거로 활용할 수 있다.

불확실성 모니터링(Uncertainty Monitoring)은 계획 및 정책 출력(Planning and Policy Outputs)도 검사해야 한다. 계획기(Planner)가 거의 동일한 가치의 여러 대안을 생성하거나 학습 정책(Learned Policy)이 작은 입력 변화에도 행동을 빠르게 전환한다면 인식 결과의 신뢰도가 높더라도 의사결정 불확실성(Decision Uncertainty)이 존재할 수 있다. 행동 안정성(Action Stability)과 민감도(Sensitivity)를 모니터링하면 내부 표현에서 발생한 불확실성이 물리적 제어로 전파되는 과정을 식별하는 데 도움이 된다.

불확실성을 해석할 때 상황(Context)은 필수적이다. 동일한 수치의 신뢰 수준이라도 사람이 없는 공간에서 저속으로 이동하는 경우와 사람 근처에서 고속으로 이동하는 경우에는 안전에 미치는 의미가 다르다. 따라서 런타임 보증(Runtime Assurance)은 모든 운용 조건에 하나의 보편적인 임계값을 적용하는 대신 불확실성을 위험 노출(Exposure), 정지 거리(Stopping Distance), 임무 중요도(Mission Criticality), 환경 복잡성(Environmental Complexity), 사용 가능한 폴백 옵션(Fallback Options)과 결합해야 한다.

불확실성(Uncertainty)은 안전 영역(Safety Envelope)에 직접 영향을 주어야 한다. 신뢰도가 감소하거나 분포 외 증거(OOD Evidence)가 증가하면 허용 속도를 낮추고, 장애물 여유 거리(Obstacle Margins)를 확대하며, 인간과의 이격 거리를 증가시키고, 경로를 제한하며, 계획 범위(Planning Horizons)를 단축할 수 있다. 이를 통해 시스템의 환경 이해에 대한 확신이 감소할수록 물리적 권한(Physical Authority)이 점진적으로 축소되는 불확실성 인식 운영 경계(Uncertainty-Aware Operating Boundary)를 형성할 수 있다.

정상 또는 고장이라는 이진 판단(Binary Decision)보다 단계적인 대응(Graded Response)이 일반적으로 더 유용하다. 낮은 불확실성은 완전 자율 운용(Full Autonomy)을 허용할 수 있고, 중간 수준의 불확실성은 추가 모니터링이나 성능 감소(Reduced Performance)를 유발할 수 있다. 높은 불확실성에서는 기능 제한 또는 독립 시스템의 확인이 필요할 수 있으며, 극단적인 불확실성은 백업 제어기(Backup Controller), 인간 감독(Human Supervision), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop)로의 전환을 요구할 수 있다.

환경 조건이 개선되면 불확실성이 감소할 수 있기 때문에 복구(Recovery) 역시 중요하다. 로봇이 먼지가 많은 영역을 벗어나거나, 위치추정(Localization)을 다시 확보하거나, 센서 가시성을 회복하거나, 익숙한 환경으로 돌아오면 더 넓은 자율성을 허용할 만큼 충분한 신뢰도를 회복할 수 있다. 그러나 노이즈가 있는 임계값 교차 때문에 권한이 반복적으로 전환되는 것을 방지하기 위해 복구 과정에는 정의된 히스테리시스(Hysteresis), 지속성 요구조건(Persistence Requirements), 검증 검사(Validation Checks)를 적용해야 한다.

분포 외 이벤트(OOD Events)는 단순한 일시적 런타임 이상(Runtime Anomalies)으로 처리하지 않고 중요한 운용 증거(Operational Evidence)로 기록해야 한다. 높은 불확실성과 연관된 입력, 익숙하지 않은 임베딩, 모델 불일치, 예측 실패, 개입 이벤트, 환경 상황을 분석하면 학습 및 검증 범위의 공백을 발견할 수 있다. 이러한 기록은 데이터셋 확장(Dataset Expansion), 시나리오 생성(Scenario Generation), 재학습(Retraining), 임계값 개선(Threshold Refinement), 향후 안전 검증(Safety Verification)을 지원할 수 있다.

불확실성 추정 자체도 실패할 수 있으므로 모니터링 메커니즘 역시 검증되어야 한다. 분포 변화 환경에서는 캘리브레이션(Calibration)이 저하될 수 있고, 분포 외 탐지기가 특정 유형의 새로운 상황을 탐지하지 못할 수 있으며, 앙상블 구성요소가 공통된 편향(Common Biases)을 가질 수도 있다. 따라서 런타임 보증(Runtime Assurance)은 불확실성 추정기가 완전하다고 가정하지 않고 모델 기반 신호를 독립적인 센서, 시스템, 환경 및 행동 증거와 결합해야 한다.

플릿 규모(Fleet Scale)에서 불확실성 모니터링(Uncertainty Monitoring)은 하나의 로봇만으로는 식별하기 어려운 패턴을 발견할 수 있다. 여러 로봇이 동일한 위치에서 증가된 분포 외 점수나 유사한 예측 오류를 보고한다면 사이트 수준의 환경 변화 또는 이전에 경험하지 못한 조건이 존재할 수 있다. 공유된 증거(Shared Evidence)는 집단 인식(Collective Awareness)을 향상시킬 수 있지만 각 로봇은 자신의 불확실성에 즉각 대응할 수 있는 로컬 권한(Local Authority)을 유지해야 한다.

궁극적으로 불확실성 및 분포 외 모니터링(Uncertainty and OOD Monitoring)은 물리 인공지능(Physical AI) 시스템이 현재 무엇을 알고 있으며 무엇을 충분히 알지 못하는지를 인식하기 위한 메커니즘을 제공한다. 모든 인공지능 출력을 동일하게 신뢰하는 대신 런타임 보증(Runtime Assurance)은 신뢰도(Confidence), 새로움(Novelty), 불일치(Disagreement), 예측 정확도(Prediction Accuracy), 상황적 위험(Contextual Risk)을 지속적으로 평가한다. 이를 통해 불확실한 지능이 위험한 물리적 결과를 발생시키기 전에 자율 권한을 축소하고, 충분한 신뢰성 증거가 회복된 이후에만 다시 확대할 수 있다.

##  

## 07.08. State Action and Trajectory Monitoring

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

State, action, and trajectory monitoring provides runtime assurance by continuously checking what a Physical AI system is, what it intends to do, and where its behavior is likely to lead. These three monitoring perspectives connect the current physical condition of the robot with immediate control decisions and future motion, allowing unsafe behavior to be detected before it develops into an irreversible physical consequence.

State monitoring evaluates whether the robot and its environment remain within permitted operating conditions. Relevant states may include position, orientation, velocity, acceleration, joint configuration, actuator load, battery condition, localization confidence, human proximity, obstacle distance, terrain condition, and system health. The monitored state therefore combines physical configuration, environmental context, and operational readiness.

State validity must include uncertainty because runtime state estimates are rarely exact. Localization covariance, perception confidence, sensor disagreement, delayed measurements, or incomplete observations can make the estimated state differ from reality. Runtime assurance should therefore evaluate both the nominal state and its uncertainty bounds, using larger safety margins whenever the physical condition of the system cannot be determined with sufficient confidence.

Action monitoring evaluates commands before or while they are executed. Actions can include steering, acceleration, braking, manipulator motion, force commands, navigation decisions, task transitions, or learned policy outputs. A proposed action should be checked against actuator limits, collision constraints, stability requirements, authorized behaviors, human-safety rules, and the current operational mode before it receives physical authority.

An action cannot be judged safely without considering the state from which it is executed. The same acceleration command may be acceptable in an open area but unsafe near a person, on a slippery surface, or when localization confidence is poor. State-action monitoring therefore evaluates whether a particular action is permissible under the current combination of physical conditions, environmental context, uncertainty, and system health.

Trajectory monitoring extends assurance beyond individual actions by evaluating sequences of future states and controls. A trajectory may satisfy immediate constraints while gradually approaching an obstacle, unstable configuration, restricted region, or situation from which braking is impossible. Monitoring the complete planned path allows the system to identify risks that are invisible when commands are examined only one control cycle at a time.

Prediction is central to trajectory monitoring. Robot dynamics, reachable-state analysis, motion forecasting, world models, or conservative simulation can estimate how the system will evolve under candidate actions. Predicted position, velocity, separation, stability, and collision risk can then be compared with safety constraints. Behavior can be rejected before execution if future states are expected to leave the permitted safety envelope.

Trajectory monitoring should include other moving agents because the future environment is not static. Humans, vehicles, robots, manipulators, and moving equipment can change the safety of an otherwise valid path. Predicted trajectories should therefore consider possible motion of relevant agents and incorporate uncertainty margins when their future behavior cannot be estimated reliably.

Time-to-collision, stopping distance, time-to-boundary, and remaining recovery time are useful predictive indicators. They describe not only whether a hazard exists but how much time remains before intervention becomes ineffective. Runtime assurance can use these quantities to escalate responses progressively, allowing replanning or speed reduction when sufficient margin exists and stronger intervention when recovery time becomes critically short.

Consistency between state, action, and trajectory information should also be monitored. A planned trajectory may assume a velocity that differs from the measured robot state, or actuator commands may fail to produce the expected motion. Persistent differences between commanded, predicted, and observed behavior can indicate control faults, model mismatch, wheel slip, actuator degradation, external disturbance, or inaccurate state estimation.

Execution monitoring closes the loop by comparing planned behavior with actual physical behavior. The system can measure tracking error, path deviation, velocity error, actuator response, timing deviation, and unexpected state transitions. If the robot cannot follow the trajectory within validated tolerances, continuing to issue the original commands may become unsafe even if the trajectory itself was initially considered valid.

Monitoring thresholds should depend on context rather than remaining universally fixed. Higher velocity, heavier payload, poor surface conditions, reduced visibility, human proximity, or degraded localization may require tighter action limits and larger trajectory margins. Context-sensitive thresholds allow the runtime assurance system to preserve useful performance when conditions are favorable while becoming more conservative as operational risk increases.

Uncertainty should propagate from state estimation into action and trajectory evaluation. If the robot\'s location, obstacle position, human motion, or dynamic parameters are uncertain, future trajectories should not be represented as exact lines. Reachable regions, confidence bounds, probabilistic occupancy, or conservative margins can represent possible evolution and determine whether all sufficiently plausible outcomes remain acceptably safe.

When monitoring detects a developing violation, intervention can occur at several levels. The system may reject an action, reduce speed, modify acceleration, constrain steering, replan the trajectory, increase separation, or select another route. Early intervention preserves more feasible alternatives, whereas delayed detection may leave only emergency braking, minimum-risk maneuver, protective stopping, or transfer to a backup controller.

A critical concept is the feasible safe action set: the collection of actions that can be executed from the current state without causing unacceptable future risk. Runtime assurance can continuously estimate this set and restrict the primary controller to actions inside it. As hazards or uncertainty increase, the safe set contracts; when conditions improve, it may expand and restore greater autonomous freedom.

If the feasible safe action set becomes empty, normal autonomous operation should no longer continue. This condition indicates that no available command can confidently preserve the required safety constraints under the current assumptions. The runtime architecture should then transition toward a predefined fallback strategy, minimum-risk condition, protective stop, or another state designed to minimize physical consequences.

Monitoring should remain sufficiently independent from the planning and control functions being supervised. A planner should not be the sole judge of whether its own trajectory is safe. Independent geometric checks, deterministic constraints, simplified dynamic models, safety sensors, or supervisory controllers can evaluate state-action-trajectory consistency and reduce the risk that a single modeling or reasoning error defeats both autonomy and assurance.

Logging provides evidence of how autonomous behavior evolved before and during safety interventions. State estimates, uncertainty bounds, proposed actions, planned trajectories, predicted violations, safety margins, rejected commands, tracking errors, and fallback transitions can be recorded together. These synchronized traces support incident reconstruction, verification, threshold refinement, model improvement, and safety-case development.

At fleet scale, state-action-trajectory monitoring must include interactions among multiple robots. Individual trajectories may be safe in isolation but incompatible when robots share intersections, corridors, workspaces, or resources. Fleet coordination can predict conflicts and reserve shared space, while each robot retains local monitoring and collision avoidance capable of protecting it if centralized coordination becomes delayed or unavailable.

State, action, and trajectory monitoring ultimately forms a continuous chain from observation to physical consequence. State monitoring establishes where the system is, action monitoring determines what it may do, and trajectory monitoring evaluates where those actions may lead. By linking these levels with uncertainty, prediction, execution feedback, and independent safety constraints, runtime assurance can intervene before unsafe intent becomes unsafe motion.

상태, 행동 및 궤적 모니터링(State, Action, and Trajectory Monitoring)은 물리 인공지능(Physical AI) 시스템이 현재 어떤 상태에 있는지, 무엇을 수행하려 하는지, 그리고 그 행동이 어디로 이어질 가능성이 있는지를 지속적으로 확인함으로써 런타임 보증(Runtime Assurance)을 제공한다. 이 세 가지 모니터링 관점은 로봇의 현재 물리적 상태를 즉각적인 제어 결정 및 미래 움직임과 연결하여, 안전하지 않은 행동이 되돌릴 수 없는 물리적 결과로 발전하기 전에 탐지할 수 있도록 한다.

상태 모니터링(State Monitoring)은 로봇과 환경이 허용된 운용 조건(Permitted Operating Conditions) 내부에 유지되고 있는지를 평가한다. 관련 상태에는 위치(Position), 방향(Orientation), 속도(Velocity), 가속도(Acceleration), 관절 구성(Joint Configuration), 액추에이터 부하(Actuator Load), 배터리 상태(Battery Condition), 위치추정 신뢰도(Localization Confidence), 인간 근접도(Human Proximity), 장애물 거리(Obstacle Distance), 지형 상태(Terrain Condition), 시스템 건전성(System Health) 등이 포함될 수 있다. 따라서 모니터링되는 상태는 물리적 구성, 환경 상황(Environmental Context), 운영 준비 상태(Operational Readiness)를 결합한다.

런타임 상태 추정(Runtime State Estimates)은 거의 항상 어느 정도의 오차를 포함하므로 상태 유효성(State Validity)은 불확실성(Uncertainty)을 포함해야 한다. 위치추정 공분산(Localization Covariance), 인식 신뢰도(Perception Confidence), 센서 불일치(Sensor Disagreement), 지연된 측정값, 불완전한 관측은 추정 상태와 실제 상태 사이에 차이를 발생시킬 수 있다. 따라서 런타임 보증(Runtime Assurance)은 명목 상태(Nominal State)와 불확실성 범위(Uncertainty Bounds)를 함께 평가하고, 시스템의 물리적 상태를 충분한 신뢰도로 판단할 수 없을 때 더 큰 안전 여유(Safety Margins)를 적용해야 한다.

행동 모니터링(Action Monitoring)은 명령이 실행되기 전 또는 실행되는 동안 이를 평가한다. 행동에는 조향(Steering), 가속, 제동, 매니퓰레이터 움직임(Manipulator Motion), 힘 명령(Force Commands), 내비게이션 결정, 작업 전환(Task Transitions), 학습 정책 출력(Learned Policy Outputs) 등이 포함될 수 있다. 제안된 행동은 물리적 제어 권한(Physical Authority)을 부여받기 전에 액추에이터 한계, 충돌 제약조건, 안정성 요구사항, 허가된 행동, 인간 안전 규칙, 현재 운용 모드와 비교하여 검사되어야 한다.

행동(Action)은 그것이 실행되는 상태(State)를 고려하지 않고서는 안전하게 판단할 수 없다. 동일한 가속 명령이라도 개방된 공간에서는 허용될 수 있지만 사람 근처, 미끄러운 표면, 또는 위치추정 신뢰도가 낮은 상황에서는 위험할 수 있다. 따라서 상태-행동 모니터링(State-Action Monitoring)은 현재의 물리적 조건, 환경 상황, 불확실성, 시스템 건전성의 조합에서 특정 행동이 허용 가능한지를 평가한다.

궤적 모니터링(Trajectory Monitoring)은 미래 상태와 제어의 연속적인 시퀀스(Sequence)를 평가함으로써 개별 행동을 넘어 보증 범위를 확장한다. 어떤 궤적은 즉각적인 제약조건을 만족하면서도 점진적으로 장애물, 불안정한 구성, 제한 구역 또는 제동이 불가능한 상황에 접근할 수 있다. 전체 계획 경로(Planned Path)를 모니터링하면 한 번의 제어 주기(Control Cycle) 단위로 명령을 검사할 때는 보이지 않는 위험을 식별할 수 있다.

예측(Prediction)은 궤적 모니터링(Trajectory Monitoring)의 핵심이다. 로봇 동역학(Robot Dynamics), 도달 가능 상태 분석(Reachable-State Analysis), 움직임 예측(Motion Forecasting), 월드 모델(World Models), 보수적 시뮬레이션(Conservative Simulation)을 이용하여 후보 행동에 따라 시스템이 어떻게 변화할지를 추정할 수 있다. 예측된 위치, 속도, 이격 거리, 안정성, 충돌 위험을 안전 제약조건과 비교하고 미래 상태가 허용된 안전 영역(Safety Envelope)을 벗어날 것으로 예상되면 실행 전에 해당 행동을 거부할 수 있다.

미래 환경은 정적이지 않으므로 궤적 모니터링(Trajectory Monitoring)은 다른 이동 에이전트(Moving Agents)도 포함해야 한다. 인간, 차량, 로봇, 매니퓰레이터, 이동 장비는 원래 유효했던 경로의 안전성을 변화시킬 수 있다. 따라서 예측 궤적(Predicted Trajectories)은 관련 에이전트의 가능한 움직임을 고려해야 하며, 그들의 미래 행동을 신뢰성 있게 추정할 수 없는 경우 불확실성 여유(Uncertainty Margins)를 포함해야 한다.

충돌까지의 시간(Time-to-Collision), 정지 거리(Stopping Distance), 경계까지의 시간(Time-to-Boundary), 남은 복구 시간(Remaining Recovery Time)은 유용한 예측 지표(Predictive Indicators)이다. 이러한 지표는 위험의 존재 여부뿐만 아니라 개입이 효과를 잃기까지 얼마나 많은 시간이 남아 있는지를 나타낸다. 런타임 보증(Runtime Assurance)은 충분한 여유가 있을 때 재계획이나 속도 감소를 수행하고, 복구 시간이 임계 수준으로 짧아지면 더 강력한 개입으로 단계적으로 전환할 수 있다.

상태, 행동, 궤적 정보 사이의 일관성(Consistency) 역시 모니터링해야 한다. 계획된 궤적이 실제 측정된 로봇 상태와 다른 속도를 가정할 수 있으며, 액추에이터 명령이 예상했던 움직임을 발생시키지 못할 수도 있다. 명령된 행동(Commanded Behavior), 예측 행동(Predicted Behavior), 관측된 행동(Observed Behavior) 사이의 지속적인 차이는 제어 고장(Control Faults), 모델 불일치(Model Mismatch), 휠 슬립(Wheel Slip), 액추에이터 성능 저하, 외부 교란(External Disturbance), 부정확한 상태 추정 등을 나타낼 수 있다.

실행 모니터링(Execution Monitoring)은 계획된 행동과 실제 물리적 행동을 비교함으로써 피드백 루프(Feedback Loop)를 완성한다. 시스템은 추종 오차(Tracking Error), 경로 편차(Path Deviation), 속도 오차(Velocity Error), 액추에이터 응답, 타이밍 편차(Timing Deviation), 예상하지 못한 상태 전이를 측정할 수 있다. 로봇이 검증된 허용오차(Validated Tolerances) 내에서 궤적을 따라갈 수 없다면 해당 궤적 자체가 처음에는 유효한 것으로 판단되었더라도 기존 명령을 계속 실행하는 것은 위험해질 수 있다.

모니터링 임계값(Monitoring Thresholds)은 항상 고정된 값으로 유지되기보다 상황(Context)에 따라 달라져야 한다. 높은 속도, 무거운 페이로드(Payload), 불량한 노면 상태, 낮은 가시성, 인간 근접도 증가, 위치추정 성능 저하는 더욱 엄격한 행동 제한과 더 큰 궤적 안전 여유를 요구할 수 있다. 상황 인식 임계값(Context-Sensitive Thresholds)은 조건이 양호할 때 유용한 성능을 유지하면서 운영 위험이 증가할수록 런타임 보증 시스템이 더욱 보수적으로 동작하도록 한다.

불확실성(Uncertainty)은 상태 추정에서 행동 및 궤적 평가까지 전파되어야 한다. 로봇 위치, 장애물 위치, 인간 움직임 또는 동역학 파라미터(Dynamic Parameters)가 불확실하다면 미래 궤적을 정확한 하나의 선으로 표현해서는 안 된다. 도달 가능 영역(Reachable Regions), 신뢰 범위(Confidence Bounds), 확률적 점유(Probabilistic Occupancy), 보수적 안전 여유(Conservative Margins)를 사용하여 가능한 시스템 변화를 표현하고 충분히 발생 가능한 모든 결과가 허용 가능한 안전 범위 내에 유지되는지를 판단할 수 있다.

모니터링에서 잠재적인 위반이 탐지되면 여러 수준에서 개입(Intervention)이 이루어질 수 있다. 시스템은 행동을 거부하고, 속도를 낮추며, 가속도를 수정하고, 조향을 제한하거나, 궤적을 재계획하고, 이격 거리를 확대하거나 다른 경로를 선택할 수 있다. 조기 개입(Early Intervention)은 더 많은 실행 가능한 대안을 유지하지만 탐지가 늦어질수록 비상 제동(Emergency Braking), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop), 백업 제어기(Backup Controller)로의 전환만 가능한 상황이 될 수 있다.

핵심적인 개념은 실행 가능한 안전 행동 집합(Feasible Safe Action Set)으로, 현재 상태에서 허용할 수 없는 미래 위험을 발생시키지 않고 실행할 수 있는 행동들의 집합을 의미한다. 런타임 보증(Runtime Assurance)은 이 집합을 지속적으로 추정하고 주 제어기(Primary Controller)가 그 내부의 행동만 선택하도록 제한할 수 있다. 위험이나 불확실성이 증가하면 안전 행동 집합은 축소되고, 조건이 개선되면 다시 확대되어 더 높은 수준의 자율적 자유(Autonomous Freedom)를 허용할 수 있다.

실행 가능한 안전 행동 집합(Feasible Safe Action Set)이 비어 있게 되면 정상적인 자율 운용(Normal Autonomous Operation)은 더 이상 계속되어서는 안 된다. 이는 현재의 가정과 조건에서 요구되는 안전 제약조건을 신뢰성 있게 유지할 수 있는 명령이 존재하지 않는다는 것을 의미한다. 이 경우 런타임 아키텍처(Runtime Architecture)는 사전에 정의된 폴백 전략(Fallback Strategy), 최소 위험 상태(Minimum-Risk Condition), 보호 정지(Protective Stop), 또는 물리적 결과를 최소화하도록 설계된 다른 상태로 전환해야 한다.

모니터링은 감독 대상인 계획 및 제어 기능으로부터 충분한 독립성(Independence)을 유지해야 한다. 계획기(Planner)가 자신이 생성한 궤적의 안전성을 판단하는 유일한 주체가 되어서는 안 된다. 독립적인 기하학적 검사(Independent Geometric Checks), 결정론적 제약조건(Deterministic Constraints), 단순화된 동역학 모델(Simplified Dynamic Models), 안전 센서(Safety Sensors), 감독 제어기(Supervisory Controllers)를 이용하여 상태-행동-궤적의 일관성을 평가하면 하나의 모델링 또는 추론 오류가 자율성과 보증 기능을 동시에 무력화할 위험을 줄일 수 있다.

로깅(Logging)은 안전 개입 이전과 개입 과정에서 자율 행동이 어떻게 변화했는지를 보여주는 증거를 제공한다. 상태 추정(State Estimates), 불확실성 범위, 제안된 행동, 계획된 궤적, 예측된 위반, 안전 여유, 거부된 명령, 추종 오차, 폴백 전환(Fallback Transitions)을 함께 기록할 수 있다. 이러한 동기화된 기록(Synchronized Traces)은 사고 재구성(Incident Reconstruction), 검증(Verification), 임계값 개선(Threshold Refinement), 모델 개선, 안전 사례(Safety Case) 개발을 지원한다.

플릿 규모(Fleet Scale)에서는 상태-행동-궤적 모니터링(State-Action-Trajectory Monitoring)이 여러 로봇 사이의 상호작용까지 포함해야 한다. 개별 궤적은 독립적으로 보면 안전할 수 있지만 여러 로봇이 교차로, 복도, 작업공간 또는 자원을 공유하면 서로 양립할 수 없게 될 수 있다. 플릿 조정(Fleet Coordination)은 충돌 가능성을 예측하고 공유 공간을 예약할 수 있으며, 각 로봇은 중앙 조정이 지연되거나 사용할 수 없을 때도 자신을 보호할 수 있는 로컬 모니터링(Local Monitoring)과 충돌 회피(Collision Avoidance) 기능을 유지해야 한다.

궁극적으로 상태, 행동 및 궤적 모니터링(State, Action, and Trajectory Monitoring)은 관측(Observation)에서 물리적 결과(Physical Consequence)까지 이어지는 연속적인 안전 사슬을 형성한다. 상태 모니터링(State Monitoring)은 시스템이 어디에 있는지를 확인하고, 행동 모니터링(Action Monitoring)은 무엇을 수행할 수 있는지를 결정하며, 궤적 모니터링(Trajectory Monitoring)은 그러한 행동이 어디로 이어질지를 평가한다. 이러한 수준을 불확실성(Uncertainty), 예측(Prediction), 실행 피드백(Execution Feedback), 독립 안전 제약조건(Independent Safety Constraints)과 연결함으로써 런타임 보증(Runtime Assurance)은 안전하지 않은 의도(Unsafe Intent)가 안전하지 않은 물리적 움직임(Unsafe Motion)으로 전환되기 전에 개입할 수 있다.

##  

## 07.09. World Model Prediction Consistency Monitoring

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

World model prediction consistency monitoring evaluates whether the future states predicted by a Physical AI system remain aligned with the physical world as it actually unfolds. A world model may predict object motion, occupancy, robot state, environmental change, and action consequences. Runtime assurance compares these predictions with subsequent observations to determine whether the internal predictive representation remains trustworthy.

The fundamental mechanism is a prediction-observation feedback loop. At time t, the world model receives the current estimated state and candidate actions and predicts future states at t+1, t+2, or longer horizons. When those future moments arrive, sensor observations and state estimates provide evidence of what actually occurred. Differences between prediction and observation become consistency signals for runtime monitoring.

Prediction consistency should be evaluated across multiple representations rather than through a single global error. Robot pose, velocity, object location, occupancy, depth, semantic state, traversability, contact, human motion, and environmental dynamics may each exhibit different failure characteristics. Representation-specific monitoring helps determine which part of the predicted world is becoming unreliable instead of treating every mismatch as complete model failure.

State-transition consistency examines whether predicted changes obey plausible physical and operational dynamics. Objects should not teleport between locations, robot motion should remain compatible with commanded actions and dynamics, and persistent structures should not disappear without explanation. Violations of these relationships can indicate model error, inaccurate state estimation, corrupted observations, unexpected disturbances, or conditions outside the model\'s learned experience.

Action-conditioned consistency is especially important because a useful world model must represent how the environment changes in response to robot behavior. The monitor can compare predicted consequences of steering, acceleration, manipulation, contact, or navigation actions with observed outcomes. If identical classes of actions repeatedly produce consequences different from those predicted, the model may no longer represent the current system or environment accurately.

Prediction error should be monitored as a temporal pattern rather than only as an instantaneous value. A single mismatch may result from measurement noise or an unusual transient event, while steadily increasing residuals can indicate systematic model drift. Moving statistics, cumulative errors, trend detection, and persistence tests help distinguish temporary prediction noise from sustained degradation of the world model.

Prediction horizons require separate treatment because uncertainty normally increases further into the future. A model may remain accurate for several hundred milliseconds while becoming unreliable over several seconds. Runtime monitoring should therefore characterize consistency as a function of prediction horizon and determine how far into the future the model currently provides sufficiently reliable information for planning and safety decisions.

Uncertainty must accompany prediction error because not every mismatch has the same meaning. A prediction that explicitly represents a wide uncertainty range may remain statistically consistent with the observation even when its nominal estimate is inaccurate. Conversely, a highly confident prediction that repeatedly contradicts reality provides stronger evidence of model failure. Consistency monitoring should therefore evaluate both error magnitude and predicted uncertainty.

Calibration determines whether the uncertainty predicted by the world model corresponds reasonably to observed errors. If actual outcomes repeatedly fall outside predicted confidence regions, the model may be overconfident. If uncertainty remains excessively large even under familiar conditions, the model may become operationally uninformative. Runtime calibration monitoring helps determine whether predictive confidence remains meaningful enough to support autonomous decisions.

Spatial consistency is important for world models that predict occupancy, geometry, or scene evolution. Predicted free space should correspond with subsequent sensor observations, obstacles should appear near expected locations, and persistent map structures should remain geometrically coherent. Growing spatial disagreement can reveal localization drift, perception degradation, environmental change, or failures in the world model\'s internal spatial representation.

Temporal consistency evaluates whether predicted sequences evolve smoothly and causally through time. Object motion, human trajectories, traffic flow, manipulation states, and robot dynamics should follow plausible transitions rather than unstable jumps or oscillations. Comparing successive predictions with both previous predictions and later observations can reveal instability that may not be visible when individual predicted frames are inspected independently.

Multi-modal consistency can strengthen monitoring by comparing predictions against independent sensing channels. A predicted obstacle trajectory may be checked against camera, LiDAR, radar, or occupancy observations, while predicted robot motion can be compared with encoders and IMU measurements. Agreement across diverse modalities increases confidence, whereas systematic disagreement can help distinguish model failure from failure of a single sensing source.

Unexpected environmental changes should not automatically be interpreted as world model faults. A person may suddenly change direction, an object may fall, a door may open, or another robot may behave unpredictably. Runtime monitoring should distinguish unavoidable environmental unpredictability from systematic predictive weakness by examining recurrence, context, uncertainty estimates, sensor evidence, and whether errors persist after the model receives updated observations.

Consistency degradation should influence planning authority. If short-horizon predictions remain reliable but long-horizon predictions deteriorate, the system can shorten its planning horizon and replan more frequently. Greater degradation may require lower speed, increased separation margins, simpler maneuvers, reduced dependence on model-based planning, or transition toward deterministic or reactive safety mechanisms that require fewer predictive assumptions.

Severe inconsistency can indicate that the model is operating outside its validated or learned domain. Persistent prediction residuals, abnormal latent states, high ensemble disagreement, and repeated confidence violations can be combined with out-of-distribution indicators. This relationship connects world model consistency monitoring with broader uncertainty and OOD monitoring, allowing predictive failure to become evidence for reducing autonomous authority.

Recovery should be evaluated explicitly because predictive consistency can improve after temporary degradation. Once perception recovers, environmental conditions stabilize, or the robot returns to familiar operating conditions, prediction errors may decrease. Runtime assurance should require sustained evidence of restored consistency before returning to longer planning horizons or higher autonomy, preventing unstable switching between degraded and normal operation.

Monitoring should remain sufficiently independent from the world model being evaluated. A model should not be the sole mechanism responsible for judging the correctness of its own predictions. Independent sensor observations, geometric checks, simplified dynamics, physical invariants, alternative models, or deterministic constraints provide external reference points and reduce the risk that one modeling error corrupts both prediction and assurance.

Logging prediction consistency creates valuable evidence for model improvement and safety validation. Predicted states, uncertainty ranges, actual observations, residual errors, prediction horizons, actions, environmental conditions, OOD indicators, interventions, and model versions can be recorded together. These traces reveal where prediction fails and support dataset expansion, retraining, calibration improvement, scenario testing, and regression analysis.

At fleet scale, prediction consistency can be evaluated collectively. If several robots experience similar prediction errors in the same area or operating condition, the cause may be a site-level change rather than an isolated model failure. Shared residual patterns can improve collective awareness and identify emerging conditions, while each robot retains local monitoring and immediate authority to reduce risk independently.

World model prediction consistency monitoring ultimately closes the loop between imagined futures and physical reality. A world model is valuable only while its predictions remain sufficiently aligned with what subsequently occurs. By continuously comparing prediction with observation across states, actions, horizons, uncertainty, space, and time, runtime assurance can detect predictive drift and reduce reliance on the model before inaccurate imagined futures produce unsafe physical decisions.

월드 모델 예측 일관성 모니터링(World Model Prediction Consistency Monitoring)은 물리 인공지능(Physical AI) 시스템이 예측한 미래 상태가 실제로 전개되는 물리적 세계와 지속적으로 일치하는지를 평가한다. 월드 모델(World Model)은 객체 움직임(Object Motion), 점유 상태(Occupancy), 로봇 상태(Robot State), 환경 변화(Environmental Change), 행동 결과(Action Consequences)를 예측할 수 있다. 런타임 보증(Runtime Assurance)은 이러한 예측을 이후의 실제 관측과 비교하여 내부 예측 표현(Internal Predictive Representation)이 계속 신뢰할 수 있는지를 판단한다.

기본적인 메커니즘은 예측-관측 피드백 루프(Prediction-Observation Feedback Loop)이다. 시간 t에서 월드 모델은 현재의 추정 상태(Estimated State)와 후보 행동(Candidate Actions)을 입력받아 t+1, t+2 또는 더 긴 시간 범위의 미래 상태를 예측한다. 해당 미래 시점에 도달하면 센서 관측(Sensor Observations)과 상태 추정(State Estimates)을 통해 실제로 발생한 상황을 확인할 수 있다. 예측과 관측 사이의 차이는 런타임 모니터링을 위한 일관성 신호(Consistency Signals)가 된다.

예측 일관성(Prediction Consistency)은 하나의 전역 오류(Global Error)만으로 판단하기보다 여러 표현(Representations)에 걸쳐 평가해야 한다. 로봇 자세(Robot Pose), 속도(Velocity), 객체 위치(Object Location), 점유 상태(Occupancy), 깊이(Depth), 의미론적 상태(Semantic State), 주행 가능성(Traversability), 접촉(Contact), 인간 움직임(Human Motion), 환경 동역학(Environmental Dynamics)은 각각 서로 다른 고장 특성을 나타낼 수 있다. 표현별 모니터링(Representation-Specific Monitoring)을 사용하면 모든 불일치를 전체 모델 고장으로 처리하는 대신 예측된 세계의 어떤 부분이 신뢰성을 잃고 있는지를 판단할 수 있다.

상태 전이 일관성(State-Transition Consistency)은 예측된 변화가 물리적으로 그리고 운영적으로 타당한 동역학을 따르는지를 검사한다. 객체가 한 위치에서 다른 위치로 순간 이동해서는 안 되고, 로봇 움직임은 명령된 행동과 동역학에 부합해야 하며, 지속적으로 존재해야 하는 구조물이 설명 없이 사라져서는 안 된다. 이러한 관계의 위반은 모델 오류(Model Error), 부정확한 상태 추정, 손상된 관측(Corrupted Observations), 예상하지 못한 외부 교란 또는 모델이 학습한 경험 범위를 벗어난 조건을 나타낼 수 있다.

행동 조건부 일관성(Action-Conditioned Consistency)은 유용한 월드 모델이 로봇 행동에 따라 환경이 어떻게 변화하는지를 표현해야 한다는 점에서 특히 중요하다. 모니터는 조향(Steering), 가속(Acceleration), 조작(Manipulation), 접촉(Contact), 내비게이션 행동(Navigation Actions)의 예측 결과를 실제 관측된 결과와 비교할 수 있다. 동일한 종류의 행동이 반복적으로 예측과 다른 결과를 발생시킨다면 모델이 현재의 시스템이나 환경을 더 이상 정확하게 표현하지 못하고 있을 가능성이 있다.

예측 오류(Prediction Error)는 순간적인 값만이 아니라 시간에 따른 패턴(Temporal Pattern)으로 모니터링해야 한다. 단일 불일치는 측정 노이즈(Measurement Noise) 또는 일시적인 비정상 사건으로 발생할 수 있지만, 지속적으로 증가하는 잔차(Residuals)는 체계적인 모델 드리프트(Model Drift)를 의미할 수 있다. 이동 통계(Moving Statistics), 누적 오류(Cumulative Errors), 추세 탐지(Trend Detection), 지속성 검사(Persistence Tests)를 활용하면 일시적인 예측 노이즈와 월드 모델의 지속적인 성능 저하를 구분할 수 있다.

예측 범위(Prediction Horizons)는 미래로 갈수록 불확실성이 일반적으로 증가하므로 개별적으로 다루어야 한다. 모델은 수백 밀리초의 단기 예측에서는 정확성을 유지하면서도 수 초 이후의 예측에서는 신뢰성을 잃을 수 있다. 따라서 런타임 모니터링은 예측 범위에 따른 일관성을 특성화하고, 현재 모델이 계획(Planning)과 안전 판단(Safety Decisions)에 충분히 신뢰할 수 있는 정보를 미래의 어느 시점까지 제공하는지를 판단해야 한다.

모든 불일치가 동일한 의미를 가지는 것은 아니므로 예측 오류에는 불확실성(Uncertainty)이 함께 고려되어야 한다. 넓은 불확실성 범위(Uncertainty Range)를 명시적으로 표현한 예측은 명목 추정값(Nominal Estimate)이 부정확하더라도 실제 관측이 해당 범위 안에 있다면 통계적으로 일관된 것으로 판단할 수 있다. 반대로 높은 확신을 가진 예측이 현실과 반복적으로 모순된다면 모델 고장에 대한 더 강력한 증거가 된다. 따라서 일관성 모니터링은 오류 크기(Error Magnitude)와 예측 불확실성(Predicted Uncertainty)을 함께 평가해야 한다.

캘리브레이션(Calibration)은 월드 모델이 예측한 불확실성이 실제 관측 오류와 합리적으로 대응하는지를 판단한다. 실제 결과가 예측된 신뢰 영역(Predicted Confidence Regions)을 반복적으로 벗어난다면 모델이 과도한 확신(Overconfidence)을 가지고 있을 수 있다. 반대로 익숙한 조건에서도 불확실성이 지나치게 크다면 모델의 예측이 운용에 유용한 정보를 제공하지 못할 수 있다. 런타임 캘리브레이션 모니터링(Runtime Calibration Monitoring)은 예측 신뢰도가 자율 의사결정을 지원할 만큼 의미 있는 상태를 유지하는지를 판단하는 데 도움을 준다.

공간적 일관성(Spatial Consistency)은 점유 상태, 기하구조(Geometry), 장면 변화(Scene Evolution)를 예측하는 월드 모델에서 중요하다. 예측된 자유 공간(Free Space)은 이후의 센서 관측과 일치해야 하고, 장애물은 예상된 위치 주변에 나타나야 하며, 지속적인 지도 구조(Persistent Map Structures)는 기하학적 일관성을 유지해야 한다. 공간적 불일치가 증가하면 위치추정 드리프트(Localization Drift), 인식 성능 저하(Perception Degradation), 환경 변화 또는 월드 모델 내부 공간 표현의 오류를 의미할 수 있다.

시간적 일관성(Temporal Consistency)은 예측 시퀀스(Predicted Sequences)가 시간에 따라 부드럽고 인과적으로 변화하는지를 평가한다. 객체 움직임, 인간 궤적(Human Trajectories), 교통 흐름(Traffic Flow), 조작 상태(Manipulation States), 로봇 동역학은 불안정한 도약이나 진동이 아니라 물리적으로 타당한 전이를 따라야 한다. 연속적인 예측을 이전 예측 및 이후 실제 관측과 함께 비교하면 개별 예측 프레임만 검사할 때는 발견하기 어려운 불안정성을 식별할 수 있다.

다중 모달 일관성(Multi-Modal Consistency)은 예측을 독립적인 센싱 채널(Independent Sensing Channels)과 비교함으로써 모니터링을 강화할 수 있다. 예측된 장애물 궤적은 카메라, 라이다(LiDAR), 레이더(Radar), 점유 관측(Occupancy Observations)과 비교할 수 있으며, 예측된 로봇 움직임은 엔코더(Encoder)와 관성 측정 장치(IMU) 측정값과 비교할 수 있다. 다양한 모달리티 사이의 일치는 신뢰도를 높이는 반면, 체계적인 불일치는 모델 고장과 단일 센싱 소스의 고장을 구분하는 데 도움을 줄 수 있다.

예상하지 못한 환경 변화(Unexpected Environmental Changes)를 자동으로 월드 모델 고장으로 판단해서는 안 된다. 사람이 갑자기 방향을 변경하거나, 물체가 떨어지거나, 문이 열리거나, 다른 로봇이 예측할 수 없는 행동을 수행할 수 있다. 런타임 모니터링은 오류의 반복성(Recurrence), 상황(Context), 불확실성 추정(Uncertainty Estimates), 센서 증거(Sensor Evidence), 갱신된 관측을 모델에 제공한 이후에도 오류가 지속되는지를 분석하여 피할 수 없는 환경적 예측 불가능성(Environmental Unpredictability)과 체계적인 예측 성능 저하를 구분해야 한다.

일관성 저하(Consistency Degradation)는 계획 권한(Planning Authority)에 직접 영향을 주어야 한다. 단기 예측은 신뢰할 수 있지만 장기 예측의 신뢰성이 떨어지는 경우 시스템은 계획 범위(Planning Horizon)를 단축하고 더 자주 재계획(Replanning)할 수 있다. 성능 저하가 더 심해지면 속도를 낮추고, 이격 여유(Separation Margins)를 확대하며, 기동을 단순화하고, 모델 기반 계획(Model-Based Planning)에 대한 의존도를 낮추거나, 더 적은 예측 가정을 요구하는 결정론적 또는 반응형 안전 메커니즘(Deterministic or Reactive Safety Mechanisms)으로 전환할 수 있다.

심각한 불일치(Severe Inconsistency)는 모델이 검증되거나 학습된 영역을 벗어나 작동하고 있음을 의미할 수 있다. 지속적인 예측 잔차(Persistent Prediction Residuals), 비정상적인 잠재 상태(Abnormal Latent States), 높은 앙상블 불일치(Ensemble Disagreement), 반복되는 신뢰도 위반(Confidence Violations)을 분포 외 지표(Out-of-Distribution Indicators)와 결합할 수 있다. 이러한 관계는 월드 모델 일관성 모니터링(World Model Consistency Monitoring)을 더 광범위한 불확실성 및 분포 외 모니터링(Uncertainty and OOD Monitoring)과 연결하여 예측 실패가 자율 권한을 축소하기 위한 증거로 사용될 수 있도록 한다.

일시적인 성능 저하 이후 예측 일관성이 다시 개선될 수 있으므로 복구(Recovery)도 명시적으로 평가해야 한다. 인식(Perception)이 회복되고, 환경 조건이 안정화되거나, 로봇이 익숙한 운용 조건으로 돌아오면 예측 오류가 감소할 수 있다. 런타임 보증(Runtime Assurance)은 더 긴 계획 범위나 더 높은 수준의 자율성으로 복귀하기 전에 일관성이 회복되었다는 지속적인 증거(Sustained Evidence)를 요구해야 하며, 이를 통해 성능 저하 운용과 정상 운용 사이에서 불안정하게 전환되는 것을 방지할 수 있다.

모니터링은 평가 대상인 월드 모델(World Model)로부터 충분한 독립성(Independence)을 유지해야 한다. 모델 자체가 자신의 예측 정확성을 판단하는 유일한 메커니즘이 되어서는 안 된다. 독립적인 센서 관측(Independent Sensor Observations), 기하학적 검사(Geometric Checks), 단순화된 동역학(Simplified Dynamics), 물리적 불변조건(Physical Invariants), 대안 모델(Alternative Models), 결정론적 제약조건(Deterministic Constraints)은 외부 기준점을 제공하며 하나의 모델링 오류가 예측과 안전 보증 기능을 동시에 손상시킬 위험을 줄인다.

예측 일관성 로깅(Prediction Consistency Logging)은 모델 개선과 안전 검증(Safety Validation)을 위한 중요한 증거를 생성한다. 예측 상태(Predicted States), 불확실성 범위, 실제 관측, 잔차 오류(Residual Errors), 예측 범위, 행동, 환경 조건, 분포 외 지표, 개입(Interventions), 모델 버전을 함께 기록할 수 있다. 이러한 기록은 예측이 실패하는 영역을 식별하고 데이터셋 확장(Dataset Expansion), 재학습(Retraining), 캘리브레이션 개선, 시나리오 시험(Scenario Testing), 회귀 분석(Regression Analysis)을 지원한다.

플릿 규모(Fleet Scale)에서는 예측 일관성(Prediction Consistency)을 집단적으로 평가할 수 있다. 여러 로봇이 동일한 장소 또는 운용 조건에서 유사한 예측 오류를 경험한다면 그 원인은 개별 모델의 고장보다 사이트 수준 변화(Site-Level Change)일 가능성이 있다. 공유된 잔차 패턴(Shared Residual Patterns)은 집단 인식(Collective Awareness)을 향상시키고 새롭게 발생하는 조건을 식별하는 데 도움을 줄 수 있으며, 각 로봇은 독립적으로 위험을 줄일 수 있는 로컬 모니터링(Local Monitoring)과 즉각적인 제어 권한을 유지해야 한다.

궁극적으로 월드 모델 예측 일관성 모니터링(World Model Prediction Consistency Monitoring)은 상상된 미래(Imagined Futures)와 물리적 현실(Physical Reality) 사이의 피드백 루프를 완성한다. 월드 모델은 자신의 예측이 이후 실제로 발생하는 상황과 충분히 일치하는 동안에만 가치가 있다. 상태(State), 행동(Action), 예측 범위(Horizons), 불확실성(Uncertainty), 공간(Space), 시간(Time)에 걸쳐 예측과 관측을 지속적으로 비교함으로써 런타임 보증(Runtime Assurance)은 예측 드리프트(Predictive Drift)를 탐지하고, 부정확하게 상상된 미래가 위험한 물리적 의사결정으로 이어지기 전에 월드 모델에 대한 의존도를 낮출 수 있다.

##  

## 07.10. System Resource and Timing Monitoring

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

System resource and timing monitoring ensures that a Physical AI system retains the computational capacity and temporal responsiveness required for safe autonomous operation. Perception, world modeling, planning, control, and runtime assurance all depend on computations completing with sufficient resources and within defined deadlines. Correct algorithms can still become unsafe when their outputs arrive too late or when critical resources become unavailable.

Physical AI workloads frequently combine cameras, LiDAR, radar, localization, neural inference, world models, VLA systems, motion planning, and control on shared computing platforms. These components compete for CPU, GPU, memory, storage, network bandwidth, and power. Runtime monitoring must therefore observe the complete resource environment rather than assuming that successful software execution guarantees sufficient computational health.

CPU monitoring evaluates utilization, scheduling delay, execution time, process availability, thread starvation, and real-time task behavior. High average utilization alone does not necessarily indicate failure, but sustained saturation can delay safety-critical tasks. Monitoring should therefore focus on whether essential processes receive predictable execution opportunities and whether their worst-case timing remains compatible with physical control requirements.

GPU monitoring is increasingly important because perception networks, foundation models, world models, and learned policies can consume substantial accelerator capacity. GPU utilization, memory allocation, inference queue depth, kernel execution delay, thermal state, and contention among models can reveal developing overload. Safety-critical inference should not silently miss deadlines because a lower-priority AI workload monopolizes accelerator resources.

Memory health includes more than total memory consumption. Runtime assurance should observe available capacity, allocation failures, memory pressure, swapping, fragmentation, buffer exhaustion, and abnormal growth that may indicate a leak. A system operating near its memory limit can experience sudden latency increases or process termination, transforming a gradual resource problem into an immediate loss of autonomous capability.

Storage and data-path health can also influence runtime safety. Logging, map access, model loading, local databases, and temporary sensor buffers may depend on persistent storage. Low capacity, excessive I/O latency, file-system faults, or corrupted data can interfere with system operation. Monitoring should distinguish noncritical logging degradation from storage failures that directly affect localization, models, configuration, or recovery functions.

Network resources become safety relevant when perception modules, controllers, sensors, or fleet services communicate across Ethernet, CAN, wireless networks, or other middleware. Bandwidth saturation, packet loss, congestion, retransmission, queue growth, and connection instability can delay or remove information required for decisions. Runtime assurance should monitor both communication availability and whether messages arrive within their useful temporal window.

Timing monitoring evaluates whether information and computations remain synchronized with the physical world. Sensor observations, perception outputs, state estimates, predictions, plans, and control commands each have a period during which they remain valid. A technically correct result can become dangerous when used after the environment has changed, making freshness and latency fundamental safety properties rather than merely performance metrics.

End-to-end latency should be considered across the complete autonomy pipeline. Sensor acquisition, preprocessing, inference, fusion, localization, prediction, planning, command generation, communication, and actuator response all contribute to the delay between observing the world and physically reacting to it. Monitoring only individual module execution times can miss accumulated latency that makes the complete control loop unsafe.

Deadline monitoring determines whether critical computations complete before defined temporal limits. Control cycles, obstacle detection, emergency response, localization updates, and safety checks may have different deadlines according to robot dynamics. A missed deadline should be treated explicitly because continuing with stale outputs can be more dangerous than recognizing that valid information is temporarily unavailable.

Jitter is another important timing property because predictable latency can often be accommodated while highly variable latency is difficult to manage safely. Occasional long inference times, scheduler interference, garbage collection, memory paging, network bursts, or thermal throttling can produce timing spikes. Monitoring latency distributions and worst-case behavior therefore provides more useful assurance than relying only on average execution time.

Sensor and computation synchronization must also be supervised. Multi-camera systems, LiDAR-camera fusion, IMU integration, and distributed perception require observations from compatible time references. Clock drift, timestamp errors, synchronization loss, or delayed queues can combine measurements representing different physical moments. The resulting fused state may appear plausible while describing a world configuration that never actually existed.

Watchdogs provide a simple but important layer of timing assurance. Processes, controllers, sensors, and communication channels can periodically demonstrate that they remain responsive. Missing heartbeat signals or execution acknowledgments can trigger escalation before prolonged silence creates uncontrolled behavior. Independent watchdogs are particularly valuable when they remain operational despite failure or overload of the primary computing environment.

Resource monitoring should account for temperature, power, and hardware throttling because computational capability depends on physical operating conditions. High temperature can reduce CPU or GPU frequency, while unstable power can reset devices or degrade accelerators and sensors. Monitoring thermal margin, power availability, clock frequency, and hardware health helps predict performance degradation before timing failures become visible at the software level.

Resource isolation protects safety-critical functions from performance-oriented AI workloads. Runtime monitors, emergency controllers, watchdogs, communication safety paths, and essential state estimation should retain reserved CPU time, memory, communication bandwidth, or independent computing resources. Without isolation, the same overload that disables primary autonomy may also prevent the safety architecture from recognizing and responding to the failure.

Monitoring should combine resource state with mission and physical context. A temporary increase in latency may be tolerable while a robot is stationary but unacceptable when traveling quickly near people. Resource thresholds should therefore reflect velocity, stopping distance, environmental complexity, current autonomy mode, and available fallback options. Computational health becomes meaningful when interpreted in relation to physical risk.

Degradation should produce graded operational responses rather than waiting for complete resource exhaustion. Rising latency or resource pressure may first trigger workload reduction, lower inference frequency, shorter planning horizons, disabled nonessential models, or reduced logging. Further degradation can reduce robot speed, simplify autonomy, increase safety margins, or transfer functions to predefined backup mechanisms.

When critical timing guarantees can no longer be maintained, the system should transition toward a safe operating condition. A stale trajectory, delayed perception result, or missing control update should not be reused indefinitely merely to preserve mission continuity. Depending on the platform, the appropriate response may include controlled deceleration, hold position, minimum-risk maneuver, protective stop, or transfer to an independent safety controller.

Recovery from resource degradation should be controlled rather than immediate. After temperature decreases, memory becomes available, network congestion clears, or compute load returns to normal, the system should verify that timing and resource margins remain stable for a defined period. Hysteresis and persistence criteria prevent rapid switching between normal and degraded modes when computational conditions fluctuate near thresholds.

Logging provides essential evidence for diagnosing resource and timing failures. CPU and GPU utilization, memory pressure, temperatures, queue depths, network delay, execution times, missed deadlines, watchdog events, process failures, degradation transitions, and physical operating context can be recorded together. Correlating these signals helps identify whether unsafe behavior originated from algorithms, resource contention, timing failure, or hardware degradation.

System resource and timing monitoring ultimately ensures that autonomous intelligence is not granted physical authority merely because its software remains logically functional. Safe Physical AI requires sufficient computation, fresh information, bounded latency, synchronized data, and protected safety resources. By detecting degradation early and adapting autonomy before deadlines are lost, runtime assurance preserves the connection between computational correctness and timely physical control.

시스템 자원 및 타이밍 모니터링(System Resource and Timing Monitoring)은 물리 인공지능(Physical AI) 시스템이 안전한 자율 운용에 필요한 연산 능력과 시간적 응답성(Temporal Responsiveness)을 유지하도록 보장한다. 인식(Perception), 월드 모델링(World Modeling), 계획(Planning), 제어(Control), 런타임 보증(Runtime Assurance)은 모두 충분한 자원을 이용하여 정의된 마감시간(Deadline) 내에 연산이 완료되는 것에 의존한다. 알고리즘 자체가 정확하더라도 결과가 너무 늦게 도착하거나 중요한 자원을 사용할 수 없게 되면 시스템은 위험해질 수 있다.

물리 인공지능(Physical AI)의 워크로드는 일반적으로 카메라, 라이다(LiDAR), 레이더(Radar), 위치추정(Localization), 신경망 추론(Neural Inference), 월드 모델(World Models), 시각-언어-행동 시스템(VLA Systems), 모션 계획(Motion Planning), 제어 기능을 공유 연산 플랫폼(Shared Computing Platforms)에서 함께 실행한다. 이러한 구성요소들은 CPU, GPU, 메모리, 저장장치, 네트워크 대역폭(Network Bandwidth), 전력(Power)을 서로 경쟁적으로 사용한다. 따라서 런타임 모니터링은 소프트웨어가 정상적으로 실행된다는 이유만으로 충분한 연산 건전성(Computational Health)이 보장된다고 가정하지 않고 전체 자원 환경(Resource Environment)을 관찰해야 한다.

CPU 모니터링(CPU Monitoring)은 사용률(Utilization), 스케줄링 지연(Scheduling Delay), 실행 시간(Execution Time), 프로세스 가용성(Process Availability), 스레드 기아(Thread Starvation), 실시간 작업 동작(Real-Time Task Behavior)을 평가한다. 높은 평균 사용률 자체가 반드시 고장을 의미하는 것은 아니지만 지속적인 포화(Sustained Saturation)는 안전 필수 작업(Safety-Critical Tasks)을 지연시킬 수 있다. 따라서 필수 프로세스가 예측 가능한 실행 기회를 확보하고 있는지와 최악 조건의 타이밍(Worst-Case Timing)이 물리적 제어 요구사항에 부합하는지를 중점적으로 모니터링해야 한다.

GPU 모니터링(GPU Monitoring)은 인식 네트워크(Perception Networks), 파운데이션 모델(Foundation Models), 월드 모델(World Models), 학습 정책(Learned Policies)이 상당한 가속기 자원(Accelerator Capacity)을 사용할 수 있기 때문에 점점 더 중요해지고 있다. GPU 사용률, 메모리 할당(Memory Allocation), 추론 큐 깊이(Inference Queue Depth), 커널 실행 지연(Kernel Execution Delay), 열 상태(Thermal State), 모델 간 자원 경합(Contention)을 통해 증가하는 과부하를 탐지할 수 있다. 우선순위가 낮은 인공지능 워크로드가 가속기 자원을 독점하여 안전 필수 추론(Safety-Critical Inference)이 마감시간을 조용히 초과하도록 허용해서는 안 된다.

메모리 건전성(Memory Health)은 단순한 전체 메모리 사용량 이상의 요소를 포함한다. 런타임 보증(Runtime Assurance)은 사용 가능한 용량, 할당 실패(Allocation Failures), 메모리 압박(Memory Pressure), 스와핑(Swapping), 단편화(Fragmentation), 버퍼 고갈(Buffer Exhaustion), 메모리 누수(Memory Leak)를 나타낼 수 있는 비정상적인 사용량 증가를 관찰해야 한다. 메모리 한계에 근접하여 동작하는 시스템은 갑작스러운 지연시간 증가나 프로세스 종료를 경험할 수 있으며, 점진적인 자원 문제가 즉각적인 자율 기능 상실로 전환될 수 있다.

저장장치 및 데이터 경로 건전성(Storage and Data-Path Health) 역시 런타임 안전에 영향을 줄 수 있다. 로깅(Logging), 지도 접근(Map Access), 모델 로딩(Model Loading), 로컬 데이터베이스(Local Databases), 임시 센서 버퍼(Temporary Sensor Buffers)는 영구 저장장치(Persistent Storage)에 의존할 수 있다. 저장 공간 부족, 과도한 입출력 지연(I/O Latency), 파일 시스템 오류(File-System Faults), 손상된 데이터(Corrupted Data)는 시스템 운용을 방해할 수 있다. 모니터링 시스템은 중요하지 않은 로깅 성능 저하와 위치추정, 모델, 구성(Configuration), 복구 기능(Recovery Functions)에 직접 영향을 주는 저장장치 고장을 구분해야 한다.

인식 모듈, 제어기, 센서 또는 플릿 서비스(Fleet Services)가 이더넷(Ethernet), CAN, 무선 네트워크 또는 기타 미들웨어(Middleware)를 통해 통신하는 경우 네트워크 자원(Network Resources)은 안전과 직접 관련된다. 대역폭 포화(Bandwidth Saturation), 패킷 손실(Packet Loss), 혼잡(Congestion), 재전송(Retransmission), 큐 증가(Queue Growth), 연결 불안정(Connection Instability)은 의사결정에 필요한 정보를 지연시키거나 손실시킬 수 있다. 런타임 보증은 통신 가능 여부뿐만 아니라 메시지가 유효한 시간 범위(Useful Temporal Window) 내에 도착하는지도 모니터링해야 한다.

타이밍 모니터링(Timing Monitoring)은 정보와 연산이 물리적 세계와 시간적으로 동기화된 상태를 유지하는지를 평가한다. 센서 관측(Sensor Observations), 인식 출력(Perception Outputs), 상태 추정(State Estimates), 예측(Predictions), 계획(Plans), 제어 명령(Control Commands)은 각각 유효성을 유지할 수 있는 시간 범위를 가진다. 기술적으로 정확한 결과도 환경이 변화한 이후 사용되면 위험해질 수 있으므로 데이터 최신성(Freshness)과 지연시간(Latency)은 단순한 성능 지표가 아니라 기본적인 안전 속성(Safety Properties)이 된다.

종단 간 지연시간(End-to-End Latency)은 전체 자율 시스템 파이프라인(Autonomy Pipeline)에 걸쳐 고려해야 한다. 센서 획득(Sensor Acquisition), 전처리(Preprocessing), 추론(Inference), 융합(Fusion), 위치추정(Localization), 예측(Prediction), 계획(Planning), 명령 생성(Command Generation), 통신(Communication), 액추에이터 응답(Actuator Response)은 모두 환경을 관측한 시점에서 실제 물리적으로 대응하기까지의 지연에 영향을 준다. 개별 모듈의 실행 시간만 모니터링하면 전체 제어 루프(Control Loop)를 위험하게 만드는 누적 지연(Accumulated Latency)을 발견하지 못할 수 있다.

마감시간 모니터링(Deadline Monitoring)은 중요 연산이 정의된 시간 제한 이전에 완료되는지를 판단한다. 제어 주기(Control Cycles), 장애물 탐지(Obstacle Detection), 비상 대응(Emergency Response), 위치추정 업데이트(Localization Updates), 안전 검사(Safety Checks)는 로봇 동역학(Robot Dynamics)에 따라 서로 다른 마감시간을 가질 수 있다. 유효한 정보를 일시적으로 사용할 수 없다는 사실을 인식하는 것보다 오래된 출력을 계속 사용하는 것이 더 위험할 수 있으므로 마감시간 초과(Missed Deadline)는 명시적인 이상 상태로 처리해야 한다.

지터(Jitter) 역시 중요한 타이밍 특성이다. 예측 가능한 지연시간은 시스템 설계에서 대응할 수 있는 경우가 많지만 크게 변화하는 지연시간은 안전하게 관리하기 어렵다. 간헐적으로 발생하는 긴 추론 시간, 스케줄러 간섭(Scheduler Interference), 가비지 컬렉션(Garbage Collection), 메모리 페이징(Memory Paging), 네트워크 버스트(Network Bursts), 열 스로틀링(Thermal Throttling)은 타이밍 급증(Timing Spikes)을 발생시킬 수 있다. 따라서 평균 실행 시간만 사용하는 것보다 지연시간 분포(Latency Distributions)와 최악 조건의 동작을 모니터링하는 것이 더 유용한 보증 정보를 제공한다.

센서와 연산 사이의 동기화(Synchronization) 역시 감독되어야 한다. 다중 카메라 시스템(Multi-Camera Systems), 라이다-카메라 융합(LiDAR-Camera Fusion), 관성 측정 장치 통합(IMU Integration), 분산 인식(Distributed Perception)은 서로 호환되는 시간 기준(Time References)의 관측 데이터를 필요로 한다. 클록 드리프트(Clock Drift), 타임스탬프 오류(Timestamp Errors), 동기화 손실(Synchronization Loss), 지연된 큐(Delayed Queues)는 서로 다른 물리적 시점을 나타내는 측정값을 결합하게 만들 수 있다. 이렇게 융합된 상태는 겉보기에는 타당하지만 실제로는 한 번도 존재하지 않았던 세계 상태를 표현할 수 있다.

워치독(Watchdog)은 단순하지만 중요한 타이밍 보증(Timing Assurance) 계층을 제공한다. 프로세스, 제어기, 센서, 통신 채널은 주기적으로 자신이 정상적으로 응답하고 있음을 확인할 수 있다. 하트비트 신호(Heartbeat Signals)나 실행 확인(Execution Acknowledgments)이 누락되면 장시간의 응답 중단이 통제되지 않은 행동으로 이어지기 전에 대응 수준을 높일 수 있다. 독립적인 워치독(Independent Watchdogs)은 주 연산 환경의 고장이나 과부하 상황에서도 계속 작동할 수 있다는 점에서 특히 중요하다.

연산 능력은 물리적인 운용 조건에도 의존하므로 자원 모니터링(Resource Monitoring)은 온도, 전력, 하드웨어 스로틀링(Hardware Throttling)을 고려해야 한다. 높은 온도는 CPU 또는 GPU의 동작 주파수를 낮출 수 있고, 불안정한 전력은 장치를 재시작하거나 가속기 및 센서의 성능을 저하시킬 수 있다. 열 여유(Thermal Margin), 전력 가용성(Power Availability), 클록 주파수(Clock Frequency), 하드웨어 건전성(Hardware Health)을 모니터링하면 소프트웨어 수준에서 타이밍 고장이 나타나기 전에 성능 저하를 예측할 수 있다.

자원 격리(Resource Isolation)는 안전 필수 기능을 성능 중심의 인공지능 워크로드로부터 보호한다. 런타임 모니터(Runtime Monitor), 비상 제어기(Emergency Controller), 워치독(Watchdog), 안전 통신 경로(Safety Communication Paths), 필수 상태 추정(Essential State Estimation)은 예약된 CPU 시간, 메모리, 통신 대역폭 또는 독립적인 연산 자원(Independent Computing Resources)을 유지해야 한다. 이러한 격리가 없다면 주 자율 시스템을 무력화시키는 동일한 과부하가 안전 아키텍처가 고장을 탐지하고 대응하는 것까지 방해할 수 있다.

모니터링은 자원 상태(Resource State)를 임무 및 물리적 상황(Mission and Physical Context)과 결합해야 한다. 로봇이 정지해 있는 동안에는 일시적인 지연시간 증가를 허용할 수 있지만 사람 근처에서 빠르게 이동하는 상황에서는 동일한 지연이 허용되지 않을 수 있다. 따라서 자원 임계값(Resource Thresholds)은 속도, 정지 거리(Stopping Distance), 환경 복잡성(Environmental Complexity), 현재 자율 운용 모드(Autonomy Mode), 사용 가능한 폴백 옵션(Fallback Options)을 반영해야 한다. 연산 건전성(Computational Health)은 물리적 위험과 연결하여 해석될 때 실질적인 의미를 가진다.

성능 저하(Degradation)는 자원이 완전히 고갈될 때까지 기다리는 대신 단계적인 운용 대응(Graded Operational Responses)을 발생시켜야 한다. 지연시간이나 자원 압박이 증가하면 먼저 워크로드 감소(Workload Reduction), 추론 주기 감소(Lower Inference Frequency), 계획 범위 단축(Shorter Planning Horizons), 비필수 모델 비활성화, 로깅 감소 등을 수행할 수 있다. 성능 저하가 더 진행되면 로봇 속도를 낮추고, 자율 기능을 단순화하며, 안전 여유를 확대하거나 사전에 정의된 백업 메커니즘(Backup Mechanisms)으로 기능을 이전할 수 있다.

중요한 타이밍 보장(Critical Timing Guarantees)을 더 이상 유지할 수 없다면 시스템은 안전한 운용 상태(Safe Operating Condition)로 전환해야 한다. 오래된 궤적(Stale Trajectory), 지연된 인식 결과(Delayed Perception Result), 누락된 제어 업데이트(Missing Control Update)를 단순히 임무 연속성을 유지하기 위해 무기한 재사용해서는 안 된다. 플랫폼의 특성에 따라 제어된 감속(Controlled Deceleration), 위치 유지(Hold Position), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop), 독립 안전 제어기(Independent Safety Controller)로의 전환이 적절한 대응이 될 수 있다.

자원 성능 저하로부터의 복구(Recovery)는 즉각적이기보다 통제된 방식으로 이루어져야 한다. 온도가 낮아지고, 메모리가 확보되며, 네트워크 혼잡이 해소되거나, 연산 부하가 정상으로 돌아온 이후에도 시스템은 타이밍 및 자원 여유(Timing and Resource Margins)가 일정 기간 안정적으로 유지되는지를 확인해야 한다. 히스테리시스(Hysteresis)와 지속성 기준(Persistence Criteria)을 적용하면 연산 조건이 임계값 주변에서 변동할 때 정상 모드와 성능 저하 모드 사이를 빠르게 반복 전환하는 현상을 방지할 수 있다.

로깅(Logging)은 자원 및 타이밍 고장을 진단하기 위한 핵심적인 증거를 제공한다. CPU 및 GPU 사용률, 메모리 압박, 온도, 큐 깊이, 네트워크 지연(Network Delay), 실행 시간, 마감시간 초과(Missed Deadlines), 워치독 이벤트(Watchdog Events), 프로세스 고장(Process Failures), 성능 저하 전환(Degradation Transitions), 물리적 운용 상황을 함께 기록할 수 있다. 이러한 신호의 상관관계를 분석하면 위험한 행동이 알고리즘, 자원 경합(Resource Contention), 타이밍 고장(Timing Failure), 하드웨어 성능 저하 중 어디에서 시작되었는지를 식별하는 데 도움이 된다.

궁극적으로 시스템 자원 및 타이밍 모니터링(System Resource and Timing Monitoring)은 소프트웨어가 논리적으로 계속 동작한다는 이유만으로 자율 지능(Autonomous Intelligence)에 물리적 제어 권한(Physical Authority)이 부여되지 않도록 보장한다. 안전한 물리 인공지능(Physical AI)은 충분한 연산 자원, 최신 정보(Fresh Information), 제한된 지연시간(Bounded Latency), 동기화된 데이터(Synchronized Data), 보호된 안전 자원(Protected Safety Resources)을 필요로 한다. 런타임 보증(Runtime Assurance)은 성능 저하를 조기에 탐지하고 마감시간을 상실하기 전에 자율성을 적절하게 조정함으로써 연산의 정확성(Computational Correctness)과 적시의 물리적 제어(Timely Physical Control) 사이의 연결을 유지한다.

##  

## 07.11. Drift and Performance Degradation Detection

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

Drift and performance degradation detection determines whether a Physical AI system is gradually moving away from the conditions and performance levels established during validation. Unlike abrupt faults, degradation may emerge slowly through changing environments, aging hardware, evolving data distributions, model adaptation, or accumulated calibration error. Runtime assurance must identify these trends before they become unsafe behavior.

Drift can occur at several layers of the autonomy stack. Sensor drift changes measurement characteristics, data drift changes the statistical properties of observations, model drift changes predictive behavior, and operational drift changes the environment or mission context. Performance degradation may therefore originate from perception, localization, world modeling, planning, control, compute resources, or interactions among multiple subsystems.

Sensor drift often develops gradually and can remain hidden behind apparently valid measurements. Camera exposure characteristics, LiDAR alignment, IMU bias, wheel encoder scale, GNSS accuracy, temperature sensitivity, or sensor mounting geometry may change over time. Runtime monitoring can track reference relationships, calibration parameters, noise statistics, cross-sensor consistency, and residual errors to identify slow deterioration.

Data distribution drift occurs when runtime observations increasingly differ from the data used for training and validation. Changes in lighting, weather, terrain, facility layout, object populations, human behavior, traffic patterns, payload, or operating procedures can alter the input distribution. Statistical monitoring can reveal whether these changes are temporary variations or persistent shifts that challenge validated assumptions.

Model performance can degrade even when the model parameters themselves have not changed. A perception network, world model, policy, or VLA system may encounter combinations of conditions that were poorly represented during training. Confidence calibration, prediction residuals, ensemble disagreement, temporal consistency, task success, and intervention frequency can provide indirect evidence that effective model reliability is declining.

Adaptive models introduce another form of drift because their parameters or internal memory may change after deployment. Online learning, parameter-efficient fine-tuning, memory augmentation, and site-specific adaptation can improve performance while also moving behavior away from the originally verified configuration. Runtime assurance should therefore track model identity, adaptation history, parameter versions, and behavioral changes associated with updates.

Performance degradation should be measured against explicit operational baselines. Relevant indicators may include perception accuracy proxies, localization residuals, world-model prediction error, planning success, trajectory tracking error, task completion time, intervention frequency, energy efficiency, inference latency, and safety-margin consumption. Baselines provide a reference for determining whether current behavior remains within validated expectations.

Single measurements are rarely sufficient for detecting gradual degradation. Runtime monitoring should analyze trends across appropriate temporal windows using moving averages, residual statistics, change-point detection, cumulative deviation, control charts, or other trend indicators. The objective is to distinguish normal variability from persistent movement toward poorer performance without reacting excessively to temporary noise.

Different degradation mechanisms evolve at different time scales. Thermal throttling may develop within minutes, localization drift within seconds or hours, sensor aging across months, and environmental distribution shift across seasons or deployments. Monitoring windows and thresholds should therefore match the expected dynamics of each failure mechanism rather than applying one universal temporal criterion.

Cross-layer correlation helps identify the origin of degradation. Increasing localization error combined with growing LiDAR-camera inconsistency may suggest calibration drift, while rising world-model prediction error with healthy sensors may indicate model-domain mismatch. Correlating perception, model, resource, timing, control, and environmental indicators provides stronger diagnostic evidence than monitoring each subsystem independently.

Performance degradation must also be interpreted relative to operational risk. A modest increase in tracking error may be acceptable at low speed in an open environment but unacceptable near people or narrow infrastructure. Runtime assurance should combine degradation severity with speed, payload, environmental complexity, human exposure, mission criticality, and available recovery options when determining the appropriate response.

Early detection allows gradual mitigation before emergency intervention becomes necessary. The system may reduce speed, increase safety margins, shorten planning horizons, increase monitoring frequency, disable uncertain capabilities, request recalibration, or shift toward simpler validated functions. This preserves useful autonomy while reducing dependence on components whose performance is trending toward unacceptable levels.

Degradation can also trigger maintenance-oriented responses rather than immediate mission termination. Persistent sensor bias, increasing actuator effort, abnormal thermal behavior, storage errors, or communication instability may indicate emerging hardware problems. Runtime monitoring can generate diagnostic evidence that supports inspection, calibration, component replacement, or scheduled maintenance before complete failure occurs.

Threshold design should include hysteresis and persistence requirements because measurements often fluctuate around boundaries. Entering a degraded mode may require sustained evidence that performance has crossed a limit, while returning to normal operation may require stronger evidence of recovery. This prevents repeated transitions between states and reduces instability caused by noise or short-lived disturbances.

Drift detection should distinguish reversible degradation from structural change. Temporary fog, network congestion, or thermal overload may disappear when conditions improve, whereas sensor misalignment, hardware aging, persistent environmental change, or model mismatch may require engineering intervention. The recovery strategy should therefore depend on whether the underlying cause can reasonably disappear during continued operation.

Fleet-level monitoring can make drift easier to detect by comparing behavior across robots operating under similar conditions. If one robot develops increasing localization residuals while others remain stable, the cause may be local hardware degradation. If many robots show similar prediction errors at the same location or time, the evidence may indicate site-level distribution shift or environmental change.

Shared fleet statistics can also establish dynamic reference populations for performance comparison. Robots with similar hardware, software, tasks, and operating conditions can provide peer baselines for latency, energy use, tracking accuracy, perception consistency, or intervention rates. Significant deviation from comparable peers can reveal degradation even when absolute thresholds have not yet been exceeded.

Logging and traceability are essential because drift is fundamentally a historical phenomenon. Sensor statistics, model versions, prediction residuals, task outcomes, timing metrics, environmental conditions, maintenance events, calibration changes, interventions, and safety margins should be recorded with consistent timestamps. Longitudinal traces allow engineers to reconstruct how degradation developed and identify its likely causes.

Detected drift should feed back into validation and lifecycle management. Repeated OOD events, recurring prediction errors, changing operational distributions, and newly observed failure patterns can identify gaps in datasets and test scenarios. These findings can guide retraining, recalibration, simulation campaigns, regression testing, maintenance policy, and updates to the validated operational envelope.

Drift monitoring itself must remain trustworthy. Baselines can become obsolete, thresholds can be poorly calibrated, and monitoring algorithms can confuse legitimate operational evolution with degradation. Reference models and limits should therefore be versioned, reviewed, and validated against representative scenarios so that the monitoring system evolves together with the Physical AI platform.

Drift and performance degradation detection ultimately provides an early-warning layer between normal operation and explicit failure. By observing long-term changes across sensors, data, models, computation, control, and environment, runtime assurance can recognize when previously validated performance is being lost. Autonomous authority can then be reduced, maintenance initiated, or validation updated before gradual deterioration becomes unsafe physical behavior.

드리프트 및 성능 저하 탐지(Drift and Performance Degradation Detection)는 물리 인공지능(Physical AI) 시스템이 검증(Validation) 과정에서 확립된 조건과 성능 수준으로부터 점진적으로 벗어나고 있는지를 판단한다. 갑작스러운 고장(Abrupt Faults)과 달리 성능 저하는 환경 변화, 하드웨어 노후화(Aging Hardware), 데이터 분포 변화, 모델 적응(Model Adaptation), 누적된 캘리브레이션 오류(Calibration Error)를 통해 서서히 나타날 수 있다. 런타임 보증(Runtime Assurance)은 이러한 추세가 위험한 행동으로 발전하기 전에 식별해야 한다.

드리프트(Drift)는 자율 시스템 스택(Autonomy Stack)의 여러 계층에서 발생할 수 있다. 센서 드리프트(Sensor Drift)는 측정 특성을 변화시키고, 데이터 드리프트(Data Drift)는 관측의 통계적 특성을 변화시키며, 모델 드리프트(Model Drift)는 예측 행동을 변화시키고, 운영 드리프트(Operational Drift)는 환경 또는 임무 상황을 변화시킨다. 따라서 성능 저하(Performance Degradation)는 인식(Perception), 위치추정(Localization), 월드 모델링(World Modeling), 계획(Planning), 제어(Control), 연산 자원(Compute Resources) 또는 여러 서브시스템 간의 상호작용에서 발생할 수 있다.

센서 드리프트(Sensor Drift)는 일반적으로 점진적으로 발생하며 겉보기에는 유효한 측정값 뒤에 숨겨질 수 있다. 카메라 노출 특성(Camera Exposure Characteristics), 라이다 정렬(LiDAR Alignment), 관성 측정 장치 바이어스(IMU Bias), 휠 엔코더 스케일(Wheel Encoder Scale), 위성항법시스템 정확도(GNSS Accuracy), 온도 민감도(Temperature Sensitivity), 센서 장착 기하구조(Sensor Mounting Geometry)는 시간이 지나면서 변화할 수 있다. 런타임 모니터링은 기준 관계(Reference Relationships), 캘리브레이션 파라미터, 노이즈 통계, 센서 간 일관성(Cross-Sensor Consistency), 잔차 오류(Residual Errors)를 추적하여 점진적인 성능 악화를 식별할 수 있다.

데이터 분포 드리프트(Data Distribution Drift)는 런타임 관측이 학습 및 검증에 사용된 데이터와 점점 달라질 때 발생한다. 조명, 날씨, 지형, 시설 배치, 객체 구성(Object Populations), 인간 행동, 교통 패턴, 페이로드(Payload), 운영 절차의 변화는 입력 분포(Input Distribution)를 변화시킬 수 있다. 통계적 모니터링(Statistical Monitoring)을 통해 이러한 변화가 일시적인 변동인지 또는 검증된 가정(Validated Assumptions)을 위협하는 지속적인 분포 변화인지 판단할 수 있다.

모델 파라미터 자체가 변경되지 않았더라도 모델 성능(Model Performance)은 저하될 수 있다. 인식 네트워크(Perception Network), 월드 모델(World Model), 정책(Policy), 시각-언어-행동 시스템(VLA System)은 학습 과정에서 충분히 표현되지 않았던 조건의 조합을 경험할 수 있다. 신뢰도 캘리브레이션(Confidence Calibration), 예측 잔차(Prediction Residuals), 앙상블 불일치(Ensemble Disagreement), 시간적 일관성(Temporal Consistency), 작업 성공률(Task Success), 개입 빈도(Intervention Frequency)는 실질적인 모델 신뢰성이 감소하고 있다는 간접적인 증거를 제공할 수 있다.

적응형 모델(Adaptive Models)은 배포 이후 파라미터 또는 내부 메모리가 변화할 수 있기 때문에 또 다른 형태의 드리프트를 발생시킨다. 온라인 학습(Online Learning), 파라미터 효율적 미세조정(Parameter-Efficient Fine-Tuning), 메모리 증강(Memory Augmentation), 사이트 특화 적응(Site-Specific Adaptation)은 성능을 향상시킬 수 있지만 동시에 시스템 행동을 원래 검증된 구성(Verified Configuration)으로부터 벗어나게 할 수 있다. 따라서 런타임 보증은 모델 식별 정보(Model Identity), 적응 이력(Adaptation History), 파라미터 버전(Parameter Versions), 업데이트에 따른 행동 변화를 추적해야 한다.

성능 저하(Performance Degradation)는 명시적인 운영 기준선(Operational Baselines)을 기준으로 측정되어야 한다. 관련 지표에는 인식 정확도 대리지표(Perception Accuracy Proxies), 위치추정 잔차(Localization Residuals), 월드 모델 예측 오류(World-Model Prediction Error), 계획 성공률(Planning Success), 궤적 추종 오차(Trajectory Tracking Error), 작업 완료 시간(Task Completion Time), 개입 빈도, 에너지 효율(Energy Efficiency), 추론 지연시간(Inference Latency), 안전 여유 소모(Safety-Margin Consumption) 등이 포함될 수 있다. 기준선은 현재 행동이 검증된 기대 범위 내에 유지되는지를 판단하기 위한 참조 기준을 제공한다.

점진적인 성능 저하를 탐지하기에는 단일 측정값만으로 충분하지 않은 경우가 많다. 런타임 모니터링은 적절한 시간 구간(Temporal Windows)에 걸쳐 이동 평균(Moving Averages), 잔차 통계(Residual Statistics), 변화점 탐지(Change-Point Detection), 누적 편차(Cumulative Deviation), 관리도(Control Charts) 또는 기타 추세 지표(Trend Indicators)를 이용하여 변화 추세를 분석해야 한다. 목적은 일시적인 노이즈에 과도하게 반응하지 않으면서 정상적인 변동과 지속적인 성능 악화 추세를 구분하는 것이다.

서로 다른 성능 저하 메커니즘은 서로 다른 시간 척도(Time Scales)에서 진행된다. 열 스로틀링(Thermal Throttling)은 수분 이내에 발생할 수 있고, 위치추정 드리프트(Localization Drift)는 수초에서 수시간 동안 진행될 수 있으며, 센서 노후화(Sensor Aging)는 수개월에 걸쳐 발생할 수 있다. 환경 분포 변화(Environmental Distribution Shift)는 계절 또는 배포 환경에 따라 나타날 수 있다. 따라서 하나의 보편적인 시간 기준을 적용하기보다 각 고장 메커니즘의 예상 동역학에 맞는 모니터링 구간과 임계값을 사용해야 한다.

계층 간 상관관계(Cross-Layer Correlation)는 성능 저하의 원인을 식별하는 데 도움을 준다. 위치추정 오류 증가와 라이다-카메라 불일치(LiDAR-Camera Inconsistency)가 함께 증가한다면 캘리브레이션 드리프트(Calibration Drift)를 의심할 수 있으며, 센서가 정상인 상태에서 월드 모델 예측 오류가 증가한다면 모델-도메인 불일치(Model-Domain Mismatch)를 의미할 수 있다. 인식, 모델, 자원, 타이밍, 제어, 환경 지표의 상관관계를 분석하면 각 서브시스템을 독립적으로 모니터링하는 것보다 강력한 진단 증거를 확보할 수 있다.

성능 저하(Performance Degradation)는 운영 위험(Operational Risk)과 관련하여 해석되어야 한다. 추종 오차가 약간 증가하는 것은 개방된 환경에서 저속으로 운행할 때는 허용될 수 있지만 사람이나 좁은 인프라 주변에서는 허용되지 않을 수 있다. 런타임 보증(Runtime Assurance)은 적절한 대응을 결정할 때 성능 저하의 심각도를 속도, 페이로드, 환경 복잡성(Environmental Complexity), 인간 노출(Human Exposure), 임무 중요도(Mission Criticality), 사용 가능한 복구 옵션(Recovery Options)과 결합해야 한다.

조기 탐지(Early Detection)는 비상 개입(Emergency Intervention)이 필요해지기 전에 점진적인 완화 조치(Mitigation)를 가능하게 한다. 시스템은 속도를 줄이고, 안전 여유(Safety Margins)를 확대하며, 계획 범위(Planning Horizons)를 단축하고, 모니터링 빈도를 증가시키며, 불확실한 기능을 비활성화하거나 재캘리브레이션(Recalibration)을 요청할 수 있다. 또한 보다 단순하고 검증된 기능으로 전환함으로써 허용할 수 없는 수준으로 성능이 저하되는 구성요소에 대한 의존도를 낮추면서 유용한 자율성을 유지할 수 있다.

성능 저하는 즉각적인 임무 종료가 아니라 유지보수 중심 대응(Maintenance-Oriented Responses)을 유발할 수도 있다. 지속적인 센서 바이어스(Sensor Bias), 증가하는 액추에이터 부하(Actuator Effort), 비정상적인 열 동작(Thermal Behavior), 저장장치 오류(Storage Errors), 통신 불안정(Communication Instability)은 발생 중인 하드웨어 문제를 나타낼 수 있다. 런타임 모니터링은 완전한 고장이 발생하기 전에 검사(Inspection), 캘리브레이션, 부품 교체(Component Replacement), 예정된 유지보수(Scheduled Maintenance)를 지원하는 진단 증거를 생성할 수 있다.

측정값은 일반적으로 경계 주변에서 변동하므로 임계값 설계(Threshold Design)에는 히스테리시스(Hysteresis)와 지속성 요구조건(Persistence Requirements)이 포함되어야 한다. 성능 저하 모드(Degraded Mode)로 진입하기 위해서는 성능이 제한값을 지속적으로 초과했다는 증거가 필요할 수 있으며, 정상 운용으로 복귀하기 위해서는 더 강력한 회복 증거를 요구할 수 있다. 이를 통해 상태 간 반복적인 전환을 방지하고 노이즈 또는 일시적인 교란으로 발생하는 불안정성을 줄일 수 있다.

드리프트 탐지(Drift Detection)는 복구 가능한 성능 저하(Reversible Degradation)와 구조적 변화(Structural Change)를 구분해야 한다. 일시적인 안개, 네트워크 혼잡(Network Congestion), 열 과부하(Thermal Overload)는 조건이 개선되면 사라질 수 있지만 센서 정렬 오류, 하드웨어 노후화, 지속적인 환경 변화, 모델 불일치는 공학적인 개입(Engineering Intervention)을 필요로 할 수 있다. 따라서 복구 전략(Recovery Strategy)은 근본적인 원인이 운용을 계속하는 동안 자연스럽게 사라질 수 있는지에 따라 달라져야 한다.

플릿 수준 모니터링(Fleet-Level Monitoring)은 유사한 조건에서 작동하는 여러 로봇의 행동을 비교함으로써 드리프트를 더 쉽게 탐지할 수 있다. 하나의 로봇에서만 위치추정 잔차가 지속적으로 증가하고 다른 로봇들은 안정적이라면 로컬 하드웨어 성능 저하(Local Hardware Degradation)가 원인일 수 있다. 반대로 여러 로봇이 동일한 위치나 시간에서 유사한 예측 오류를 나타낸다면 사이트 수준의 분포 변화(Site-Level Distribution Shift) 또는 환경 변화가 발생했다는 증거일 수 있다.

공유 플릿 통계(Shared Fleet Statistics)는 성능 비교를 위한 동적 참조 집단(Dynamic Reference Populations)을 구성할 수도 있다. 유사한 하드웨어, 소프트웨어, 작업 및 운용 조건을 가진 로봇들은 지연시간, 에너지 사용량, 추종 정확도, 인식 일관성(Perception Consistency), 개입 빈도에 대한 동료 기준선(Peer Baselines)을 제공할 수 있다. 비교 가능한 다른 로봇들과의 상당한 편차는 절대적인 임계값을 아직 초과하지 않은 경우에도 성능 저하를 발견하는 데 도움을 줄 수 있다.

드리프트는 본질적으로 시간에 따른 역사적 현상(Historical Phenomenon)이므로 로깅 및 추적성(Logging and Traceability)이 필수적이다. 센서 통계, 모델 버전(Model Versions), 예측 잔차, 작업 결과(Task Outcomes), 타이밍 지표(Timing Metrics), 환경 조건, 유지보수 이벤트(Maintenance Events), 캘리브레이션 변경, 개입, 안전 여유를 일관된 타임스탬프(Consistent Timestamps)와 함께 기록해야 한다. 장기 추적 기록(Longitudinal Traces)을 통해 엔지니어는 성능 저하가 어떻게 발전했는지를 재구성하고 가능한 원인을 식별할 수 있다.

탐지된 드리프트(Detected Drift)는 검증 및 수명주기 관리(Validation and Lifecycle Management)에 다시 반영되어야 한다. 반복적인 분포 외 이벤트(OOD Events), 반복되는 예측 오류, 변화하는 운영 분포(Operational Distributions), 새롭게 관측된 고장 패턴은 데이터셋 및 시험 시나리오의 공백을 식별할 수 있다. 이러한 결과는 재학습(Retraining), 재캘리브레이션(Recalibration), 시뮬레이션 캠페인(Simulation Campaigns), 회귀 시험(Regression Testing), 유지보수 정책(Maintenance Policy), 검증된 운영 영역(Validated Operational Envelope)의 업데이트를 안내할 수 있다.

드리프트 모니터링(Drift Monitoring) 자체도 신뢰할 수 있는 상태를 유지해야 한다. 기준선(Baselines)은 시간이 지나면서 오래될 수 있고, 임계값이 부적절하게 캘리브레이션될 수 있으며, 모니터링 알고리즘이 정당한 운영상의 변화와 실제 성능 저하를 혼동할 수 있다. 따라서 참조 모델(Reference Models)과 제한값(Limits)은 버전 관리되고 정기적으로 검토되어야 하며, 대표적인 시나리오를 통해 검증되어 모니터링 시스템 자체가 물리 인공지능 플랫폼과 함께 발전할 수 있도록 해야 한다.

궁극적으로 드리프트 및 성능 저하 탐지(Drift and Performance Degradation Detection)는 정상 운용(Normal Operation)과 명시적인 고장(Explicit Failure) 사이에 위치하는 조기 경보 계층(Early-Warning Layer)을 제공한다. 센서, 데이터, 모델, 연산, 제어, 환경 전반에서 장기적인 변화를 관찰함으로써 런타임 보증(Runtime Assurance)은 이전에 검증된 성능이 점차 상실되고 있는 시점을 인식할 수 있다. 이를 통해 점진적인 성능 악화가 위험한 물리적 행동으로 발전하기 전에 자율 권한(Autonomous Authority)을 축소하고, 유지보수를 시작하거나, 필요한 검증 체계를 업데이트할 수 있다.

##  

## 07.12. Anomaly and Novelty Detection

![](images/image13.png){width="7.268055555555556in" height="7.268055555555556in"}

Anomaly and novelty detection provides runtime assurance by identifying observations, behaviors, system states, or interactions that differ meaningfully from what a Physical AI system normally expects. Unlike monitoring that checks only predefined limits, anomaly detection searches for unusual patterns that may indicate faults, environmental changes, emerging hazards, or previously unseen situations requiring additional caution.

An anomaly is generally an observation or behavior that deviates from an established reference pattern, while novelty refers to a condition that is genuinely unfamiliar to the system. The distinction is important because unusual behavior may result from a known fault or temporary disturbance, whereas novelty may indicate that the robot has entered a situation poorly represented by its training, validation, or operational experience.

Detection can operate across multiple layers of the autonomy system. Sensor measurements, perception outputs, localization states, world-model representations, planned trajectories, control commands, actuator responses, computational resources, communication behavior, and mission execution can all contain anomalous patterns. Cross-layer monitoring provides broader coverage than relying on a single AI model or subsystem.

Sensor-level anomaly detection searches for unusual noise, bias, saturation, missing measurements, timing irregularities, calibration changes, or disagreement among redundant sensors. A camera may produce abnormal exposure patterns, an IMU may develop bias, or LiDAR returns may suddenly become sparse. These changes may remain within hardware limits while still reducing the reliability of downstream perception and state estimation.

Perception anomalies can appear as unexpected object configurations, unstable detections, inconsistent segmentation, abnormal depth estimates, or rapid semantic changes. Novel objects and unusual scenes may also produce latent representations far from familiar examples. Monitoring both output behavior and internal feature representations can reveal when perception is processing conditions that differ substantially from validated experience.

World models provide a powerful basis for anomaly detection because they encode expectations about how states should evolve. When subsequent observations differ strongly from predicted occupancy, object motion, robot state, interaction outcomes, or environmental dynamics, prediction residuals become anomaly signals. Persistent or structured residuals can indicate conditions that the internal model does not adequately explain.

Behavioral anomaly detection evaluates whether actions and trajectories remain consistent with normal operational patterns. Unexpected steering oscillation, repeated replanning, unusual acceleration, excessive corrective motion, unstable manipulation, or frequent policy switching may indicate problems even when individual commands remain within allowed limits. Behavioral monitoring therefore complements deterministic safety constraints by detecting abnormal patterns before explicit violations occur.

Novelty detection often uses learned representations of familiar operating conditions. Embedding distance, density estimation, reconstruction error, energy scores, clustering, nearest-neighbor relationships, or dedicated novelty models can estimate how different a new observation is from previously known data. These methods are useful when it is impossible to enumerate every abnormal condition before deployment.

Temporal context is essential because many anomalies cannot be identified from a single observation. A sensor value may be individually plausible but abnormal when considered as part of a sequence. Runtime monitoring can examine persistence, rate of change, periodicity, transition patterns, and temporal consistency to distinguish isolated noise from meaningful changes in system or environmental behavior.

Context also determines whether an anomaly is operationally important. An unusual object far from the robot may require only observation, while the same novelty directly inside the planned path may demand immediate intervention. Anomaly severity should therefore be interpreted using proximity, velocity, stopping distance, uncertainty, mission criticality, human exposure, and available recovery options.

Anomaly detection should not automatically classify every unusual event as a fault. A newly placed object, changed facility layout, unexpected human behavior, temporary weather condition, or legitimate mission variation may be unusual without indicating system malfunction. Runtime assurance should combine environmental evidence, model confidence, sensor health, temporal persistence, and operational context before selecting a response.

Cross-modal consistency provides useful evidence for separating real-world novelty from sensor or model faults. If camera, LiDAR, radar, and other sensors independently observe the same unusual object, the event is more likely to represent genuine environmental novelty. If only one sensing channel reports the anomaly while others remain consistent, sensor degradation or processing failure becomes a stronger hypothesis.

Anomaly scores should be calibrated against representative normal variability. A detector that is too sensitive may generate excessive false alarms and unnecessarily restrict autonomy, while an insensitive detector may miss emerging hazards. Thresholds can depend on operational context and may include multiple severity levels so that uncertainty increases gradually rather than forcing every abnormal event into a binary normal-or-failed classification.

Runtime responses should scale with anomaly severity and confidence. Low-level anomalies may increase monitoring or trigger additional sensor checks. Moderate anomalies may reduce speed, enlarge safety margins, shorten planning horizons, or request replanning. Severe or unexplained anomalies near critical safety boundaries may require degraded autonomy, independent verification, minimum-risk maneuver, or protective stopping.

Novel conditions can be treated as opportunities for information gathering when sufficient safety margin exists. The robot may slow down, change viewpoint, collect additional sensor observations, or select a conservative trajectory that improves understanding without increasing exposure. This active observation strategy allows the system to resolve ambiguity before committing to actions that depend strongly on uncertain interpretations.

Recovery requires evidence that the anomaly has disappeared or has become sufficiently understood. A transient abnormal measurement may clear quickly, while a persistent novel environment may require continued degraded operation. Hysteresis and persistence criteria can prevent rapid switching between normal and restricted modes, and re-entry into full autonomy should occur only after relevant confidence and consistency measures recover.

Anomaly events should be logged with the context needed for later analysis. Sensor data, latent features, anomaly scores, world-model predictions, actions, trajectories, environmental conditions, system resources, interventions, and model versions can be synchronized around each event. These records support root-cause analysis, detector tuning, scenario reconstruction, dataset expansion, retraining, and safety validation.

At fleet scale, anomaly detection becomes more powerful because observations can be compared across multiple robots. An event that appears novel to one robot may already have been encountered by another, while simultaneous anomalies across many robots may reveal a site-level environmental or infrastructure change. Shared evidence can transform isolated novelty into collective operational knowledge.

Fleet-level novelty management should still preserve local safety authority. Communication delay, centralized processing failure, or incomplete shared knowledge must not prevent an individual robot from reacting to an immediate anomaly. Local detectors should therefore support rapid protective decisions, while fleet or on-premise intelligence can aggregate events, identify patterns, distribute knowledge, and improve future recognition.

Detected anomalies and novelties should feed back into the system lifecycle. Recurrent unusual scenes, previously unseen objects, abnormal interactions, and new operational conditions can reveal gaps in datasets, simulation scenarios, validation coverage, and safety assumptions. Engineering teams can use these events to extend training data, refine world models, update detectors, and expand validated operating knowledge.

Anomaly and novelty detection ultimately gives Physical AI a mechanism for recognizing that reality is behaving differently from expectation. By combining sensor evidence, learned representations, prediction residuals, behavioral patterns, temporal consistency, context, and fleet knowledge, runtime assurance can detect the unexpected early. Autonomous authority can then adapt before an unfamiliar or abnormal condition develops into unsafe physical behavior.

이상 및 신규성 탐지(Anomaly and Novelty Detection)는 물리 인공지능(Physical AI) 시스템이 일반적으로 예상하는 것과 의미 있게 다른 관측, 행동, 시스템 상태 또는 상호작용을 식별함으로써 런타임 보증(Runtime Assurance)을 제공한다. 사전에 정의된 제한값만 검사하는 모니터링과 달리 이상 탐지(Anomaly Detection)는 고장, 환경 변화, 새롭게 발생하는 위험 또는 추가적인 주의가 필요한 이전에 경험하지 못한 상황을 나타낼 수 있는 비정상적인 패턴을 탐색한다.

이상(Anomaly)은 일반적으로 확립된 기준 패턴(Reference Pattern)에서 벗어난 관측이나 행동을 의미하며, 신규성(Novelty)은 시스템에 실질적으로 익숙하지 않은 조건을 의미한다. 이러한 구분은 중요하다. 비정상적인 행동은 알려진 고장이나 일시적인 교란에서 발생할 수 있지만, 신규성은 로봇이 학습(Training), 검증(Validation) 또는 운영 경험(Operational Experience)에서 충분히 표현되지 않았던 상황에 진입했음을 나타낼 수 있기 때문이다.

탐지(Detection)는 자율 시스템(Autonomy System)의 여러 계층에서 수행될 수 있다. 센서 측정값, 인식 출력(Perception Outputs), 위치추정 상태(Localization States), 월드 모델 표현(World-Model Representations), 계획된 궤적(Planned Trajectories), 제어 명령(Control Commands), 액추에이터 응답(Actuator Responses), 연산 자원(Computational Resources), 통신 동작(Communication Behavior), 임무 실행(Mission Execution) 모두에서 이상 패턴이 나타날 수 있다. 계층 간 모니터링(Cross-Layer Monitoring)은 하나의 인공지능 모델이나 서브시스템에만 의존하는 것보다 더 넓은 탐지 범위를 제공한다.

센서 수준 이상 탐지(Sensor-Level Anomaly Detection)는 비정상적인 노이즈, 바이어스(Bias), 포화(Saturation), 측정값 누락, 타이밍 불규칙성(Timing Irregularities), 캘리브레이션 변화(Calibration Changes), 중복 센서 간 불일치 등을 탐색한다. 카메라는 비정상적인 노출 패턴을 생성할 수 있고, 관성 측정 장치(IMU)는 바이어스를 발생시킬 수 있으며, 라이다(LiDAR) 반환값이 갑자기 희소해질 수도 있다. 이러한 변화는 하드웨어 한계 내에 있으면서도 후속 인식 및 상태 추정(State Estimation)의 신뢰성을 저하시킬 수 있다.

인식 이상(Perception Anomalies)은 예상하지 못한 객체 구성(Object Configurations), 불안정한 탐지, 일관되지 않은 분할(Segmentation), 비정상적인 깊이 추정(Depth Estimates), 급격한 의미론적 변화(Semantic Changes)의 형태로 나타날 수 있다. 새로운 객체와 익숙하지 않은 장면은 기존 사례와 크게 떨어진 잠재 표현(Latent Representations)을 생성할 수도 있다. 출력 행동과 내부 특징 표현(Internal Feature Representations)을 함께 모니터링하면 인식 시스템이 검증된 경험과 상당히 다른 조건을 처리하고 있는 시점을 탐지할 수 있다.

월드 모델(World Models)은 상태가 어떻게 변화해야 하는지에 대한 기대를 표현하기 때문에 이상 탐지를 위한 강력한 기반을 제공한다. 이후의 실제 관측이 예측된 점유 상태(Occupancy), 객체 움직임(Object Motion), 로봇 상태(Robot State), 상호작용 결과(Interaction Outcomes), 환경 동역학(Environmental Dynamics)과 크게 다를 경우 예측 잔차(Prediction Residuals)가 이상 신호(Anomaly Signals)가 된다. 지속적이거나 구조적인 잔차는 내부 모델이 현재 조건을 충분히 설명하지 못하고 있음을 나타낼 수 있다.

행동 이상 탐지(Behavioral Anomaly Detection)는 행동과 궤적이 정상적인 운영 패턴과 일관성을 유지하는지를 평가한다. 예상하지 못한 조향 진동(Steering Oscillation), 반복적인 재계획(Replanning), 비정상적인 가속, 과도한 보정 움직임(Corrective Motion), 불안정한 조작(Manipulation), 빈번한 정책 전환(Policy Switching)은 개별 명령이 허용된 제한 범위 안에 있더라도 문제를 나타낼 수 있다. 따라서 행동 모니터링은 명시적인 제약 위반이 발생하기 전에 비정상 패턴을 탐지함으로써 결정론적 안전 제약조건(Deterministic Safety Constraints)을 보완한다.

신규성 탐지(Novelty Detection)는 익숙한 운용 조건을 학습한 표현(Learned Representations)을 사용하는 경우가 많다. 임베딩 거리(Embedding Distance), 밀도 추정(Density Estimation), 재구성 오류(Reconstruction Error), 에너지 점수(Energy Scores), 클러스터링(Clustering), 최근접 이웃 관계(Nearest-Neighbor Relationships), 전용 신규성 모델(Dedicated Novelty Models)을 이용하여 새로운 관측이 기존에 알려진 데이터와 얼마나 다른지를 추정할 수 있다. 이러한 방법은 배포 이전에 모든 비정상 조건을 열거하는 것이 불가능한 경우 특히 유용하다.

많은 이상은 하나의 관측만으로 식별할 수 없기 때문에 시간적 상황(Temporal Context)이 필수적이다. 하나의 센서 값 자체는 타당할 수 있지만 연속적인 시퀀스의 일부로 고려하면 비정상적일 수 있다. 런타임 모니터링(Runtime Monitoring)은 지속성(Persistence), 변화율(Rate of Change), 주기성(Periodicity), 전이 패턴(Transition Patterns), 시간적 일관성(Temporal Consistency)을 검사하여 일시적인 노이즈와 시스템 또는 환경 행동의 의미 있는 변화를 구분할 수 있다.

상황(Context)은 이상이 운영 측면에서 중요한지를 결정한다. 로봇으로부터 멀리 떨어진 비정상 객체는 관찰만 필요할 수 있지만 동일한 신규성이 계획된 경로 바로 내부에 존재한다면 즉각적인 개입이 필요할 수 있다. 따라서 이상 심각도(Anomaly Severity)는 근접도(Proximity), 속도(Velocity), 정지 거리(Stopping Distance), 불확실성(Uncertainty), 임무 중요도(Mission Criticality), 인간 노출(Human Exposure), 사용 가능한 복구 옵션(Recovery Options)을 이용하여 해석해야 한다.

이상 탐지(Anomaly Detection)는 모든 비정상적인 사건을 자동으로 고장(Fault)으로 분류해서는 안 된다. 새롭게 배치된 객체, 변경된 시설 배치, 예상하지 못한 인간 행동, 일시적인 기상 조건 또는 정상적인 임무 변화는 시스템 고장을 의미하지 않으면서도 비정상적일 수 있다. 런타임 보증(Runtime Assurance)은 대응을 결정하기 전에 환경 증거(Environmental Evidence), 모델 신뢰도(Model Confidence), 센서 건전성(Sensor Health), 시간적 지속성, 운영 상황을 결합해야 한다.

교차 모달 일관성(Cross-Modal Consistency)은 실제 환경의 신규성과 센서 또는 모델 고장을 구분하는 데 유용한 증거를 제공한다. 카메라, 라이다, 레이더(Radar) 및 기타 센서가 동일한 비정상 객체를 독립적으로 관측한다면 해당 사건은 실제 환경의 신규성일 가능성이 높다. 반대로 하나의 센싱 채널에서만 이상이 보고되고 다른 센서들이 일관된 상태를 유지한다면 센서 성능 저하(Sensor Degradation) 또는 처리 실패(Processing Failure)의 가능성이 더 높아진다.

이상 점수(Anomaly Scores)는 대표적인 정상 변동성(Normal Variability)을 기준으로 캘리브레이션되어야 한다. 탐지기의 민감도가 지나치게 높으면 과도한 오경보(False Alarms)가 발생하여 불필요하게 자율성을 제한할 수 있으며, 반대로 민감도가 부족하면 새롭게 발생하는 위험을 놓칠 수 있다. 임계값(Thresholds)은 운영 상황에 따라 달라질 수 있으며, 모든 비정상 사건을 정상 또는 고장이라는 이진 분류(Binary Classification)로 처리하는 대신 여러 단계의 심각도 수준을 사용할 수 있다.

런타임 대응(Runtime Responses)은 이상의 심각도와 신뢰 수준에 따라 조정되어야 한다. 낮은 수준의 이상은 모니터링 강화 또는 추가 센서 검사를 유발할 수 있다. 중간 수준의 이상에서는 속도를 낮추고, 안전 여유(Safety Margins)를 확대하고, 계획 범위(Planning Horizons)를 단축하거나 재계획을 요청할 수 있다. 중요한 안전 경계 근처에서 발생한 심각하거나 설명할 수 없는 이상은 성능 저하 자율 운용(Degraded Autonomy), 독립 검증(Independent Verification), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop)를 요구할 수 있다.

충분한 안전 여유가 존재한다면 새로운 조건(Novel Conditions)을 정보 수집(Information Gathering)의 기회로 활용할 수 있다. 로봇은 속도를 줄이고, 관측 시점(Viewpoint)을 변경하고, 추가적인 센서 관측을 수집하거나, 위험 노출을 증가시키지 않으면서 환경 이해를 개선할 수 있는 보수적인 궤적(Conservative Trajectory)을 선택할 수 있다. 이러한 능동 관측 전략(Active Observation Strategy)은 불확실한 해석에 크게 의존하는 행동을 실행하기 전에 시스템이 모호성을 해소하도록 한다.

복구(Recovery)를 위해서는 이상이 사라졌거나 충분히 이해되었다는 증거가 필요하다. 일시적인 비정상 측정값은 빠르게 정상화될 수 있지만 지속적인 새로운 환경에서는 제한된 운용(Restricted Operation)을 계속해야 할 수 있다. 히스테리시스(Hysteresis)와 지속성 기준(Persistence Criteria)을 사용하면 정상 모드와 제한 모드 사이의 빠른 전환을 방지할 수 있으며, 완전 자율 운용(Full Autonomy)으로의 복귀는 관련 신뢰도와 일관성 지표가 회복된 이후에만 이루어져야 한다.

이상 이벤트(Anomaly Events)는 이후 분석에 필요한 상황 정보와 함께 기록되어야 한다. 센서 데이터, 잠재 특징(Latent Features), 이상 점수, 월드 모델 예측(World-Model Predictions), 행동, 궤적, 환경 조건, 시스템 자원(System Resources), 개입(Interventions), 모델 버전(Model Versions)을 각 이벤트를 중심으로 시간적으로 동기화하여 기록할 수 있다. 이러한 기록은 근본 원인 분석(Root-Cause Analysis), 탐지기 조정(Detector Tuning), 시나리오 재구성(Scenario Reconstruction), 데이터셋 확장(Dataset Expansion), 재학습(Retraining), 안전 검증(Safety Validation)을 지원한다.

플릿 규모(Fleet Scale)에서는 여러 로봇의 관측을 비교할 수 있기 때문에 이상 탐지(Anomaly Detection)가 더욱 강력해진다. 하나의 로봇에는 새로운 사건이 다른 로봇에서는 이미 경험된 상황일 수 있으며, 여러 로봇에서 동시에 발생하는 이상은 사이트 수준의 환경 또는 인프라 변화(Site-Level Environmental or Infrastructure Change)를 나타낼 수 있다. 공유된 증거(Shared Evidence)는 개별적인 신규성을 집단 운영 지식(Collective Operational Knowledge)으로 전환할 수 있다.

플릿 수준 신규성 관리(Fleet-Level Novelty Management)는 여전히 로컬 안전 권한(Local Safety Authority)을 유지해야 한다. 통신 지연(Communication Delay), 중앙 처리 실패(Centralized Processing Failure), 불완전한 공유 지식 때문에 개별 로봇이 즉각적인 이상에 대응하지 못해서는 안 된다. 따라서 로컬 탐지기(Local Detectors)는 신속한 보호 결정을 지원해야 하며, 플릿 또는 온프레미스 지능(On-Premise Intelligence)은 이벤트를 집계하고, 패턴을 식별하며, 지식을 배포하고, 향후 인식 성능을 향상시킬 수 있다.

탐지된 이상과 신규성(Anomalies and Novelties)은 시스템 수명주기(System Lifecycle)에 다시 반영되어야 한다. 반복적으로 나타나는 비정상 장면, 이전에 경험하지 못한 객체, 비정상적인 상호작용, 새로운 운영 조건은 데이터셋, 시뮬레이션 시나리오(Simulation Scenarios), 검증 범위(Validation Coverage), 안전 가정(Safety Assumptions)의 공백을 드러낼 수 있다. 엔지니어링 팀은 이러한 이벤트를 활용하여 학습 데이터를 확장하고, 월드 모델을 개선하고, 탐지기를 업데이트하며, 검증된 운영 지식(Validated Operating Knowledge)을 확대할 수 있다.

궁극적으로 이상 및 신규성 탐지(Anomaly and Novelty Detection)는 물리 인공지능(Physical AI)이 현실이 예상과 다르게 변화하고 있음을 인식할 수 있는 메커니즘을 제공한다. 센서 증거(Sensor Evidence), 학습 표현(Learned Representations), 예측 잔차(Prediction Residuals), 행동 패턴(Behavioral Patterns), 시간적 일관성, 상황(Context), 플릿 지식(Fleet Knowledge)을 결합함으로써 런타임 보증(Runtime Assurance)은 예상하지 못한 상황을 조기에 탐지할 수 있다. 이를 통해 익숙하지 않거나 비정상적인 조건이 위험한 물리적 행동으로 발전하기 전에 자율 권한(Autonomous Authority)을 적절하게 조정할 수 있다.

##  

## 07.13. Runtime Shielding and Safety Filters

![](images/image14.png){width="7.268055555555556in" height="7.268055555555556in"}

Runtime shielding and safety filters provide a protective control layer between autonomous intelligence and physical actuation. Their purpose is not to replace perception, planning, world models, or learned policies, but to ensure that proposed actions remain inside verified safety constraints. Even when an AI component produces an unsafe command, the shield can block, modify, or replace it before physical execution occurs.

A runtime shield acts as an independent decision boundary around the primary autonomy system. The primary controller may optimize task performance, efficiency, or learned objectives, while the shield evaluates whether its proposed action is admissible. This separation allows advanced AI to operate with flexibility while preserving a simpler and more interpretable mechanism responsible for enforcing critical safety properties.

Safety filters can be positioned at several points in the autonomy pipeline. They may validate high-level task commands, planned trajectories, velocity requests, actuator commands, or learned policy outputs. Filtering closer to physical actuation provides strong final protection, while earlier filtering can prevent unsafe plans from propagating through the system. Layered filtering can therefore provide defense across multiple abstraction levels.

The fundamental input to a safety filter is the current estimated state together with a proposed action. The filter evaluates whether executing that action could violate constraints involving collision avoidance, speed, acceleration, stability, workspace limits, human separation, actuator capability, or operational permissions. State uncertainty should also be considered so that uncertain conditions produce more conservative admissibility decisions.

A simple shield may reject any action that directly violates a predefined constraint. More advanced shields evaluate future consequences before allowing execution. Robot dynamics, reachable sets, short-horizon simulation, control barrier functions, predictive models, or verified transition rules can determine whether an apparently safe immediate action could lead the system toward an unsafe state from which recovery becomes impossible.

The concept of a safe action set is central to runtime shielding. For each relevant system state, the assurance mechanism can determine which actions preserve required safety properties. The primary controller retains freedom to choose among these admissible actions. When uncertainty or hazard increases, the safe action set contracts, progressively reducing autonomous authority without necessarily stopping the entire mission.

Action projection provides an alternative to simple rejection. If a proposed command lies outside the safe set, the filter can project it onto the nearest acceptable action according to defined criteria. Excessive velocity may be reduced, steering may be limited, or manipulator motion may be constrained. This preserves as much of the original intent as possible while preventing execution of the unsafe component.

Trajectory safety filters evaluate sequences of future states rather than isolated commands. A planned path may currently be collision-free while entering a region with insufficient stopping distance or limited recovery options. The filter can inspect predicted trajectories against obstacles, humans, restricted areas, stability boundaries, dynamic constraints, and uncertainty margins before granting authority for execution.

Control barrier functions provide one mathematical approach for maintaining safety constraints during continuous control. A barrier function represents the boundary between safe and unsafe states, and the controller modifies commands when necessary to prevent crossing that boundary. Such methods can preserve relatively smooth behavior while formally constraining the system to remain within a defined safe region under specified assumptions.

Runtime shielding can also use reachability analysis to reason about future safety. Instead of predicting only one nominal trajectory, reachable-state methods estimate sets of states the robot could enter under uncertainty, disturbances, or control variation. If any sufficiently plausible evolution intersects an unsafe region, the shield can restrict actions earlier, creating protection against uncertainty that a single deterministic trajectory may overlook.

Learned policies and VLA systems particularly benefit from independent safety filtering because their outputs may be difficult to verify internally. A language-conditioned or learned action can be semantically reasonable yet physically inappropriate. Before execution, the safety layer can check kinematic feasibility, collision risk, force limits, workspace permissions, task authorization, human proximity, and other deterministic constraints.

Safety filters should incorporate operational context because allowable actions depend on the environment and mission. A velocity permitted in an empty warehouse may be inappropriate near people, fragile equipment, or narrow passages. Context-aware filtering can adapt speed limits, separation margins, force limits, permitted zones, and maneuver constraints while maintaining explicit rules governing how these limits may change.

Uncertainty should make shielding more conservative rather than less effective. Poor localization, uncertain obstacle position, degraded perception, unknown surface conditions, or unreliable human-motion predictions should reduce the set of actions considered safe. Safety margins can expand dynamically, and the system can restrict velocity or maneuver complexity until sufficient confidence in the current state and environment is restored.

Shielding must operate within strict timing requirements. A safety decision that arrives after an unsafe command has already reached the actuator provides little protection. Filters therefore need bounded execution time, predictable scheduling, protected computational resources, and direct access to required state information. Critical filters may use simplified models specifically because deterministic and timely evaluation is more valuable than sophisticated but delayed reasoning.

Independence is another important architectural property. The shield should avoid sharing every assumption, model, sensor dependency, and failure mode with the controller it supervises. Deterministic geometry, safety-rated sensors, simplified dynamics, independent state checks, or separate computing resources can provide diversity. This reduces the possibility that one common error simultaneously corrupts both autonomous decision making and its protective filter.

When a proposed action cannot be safely modified, the shield should invoke a defined fallback response. Depending on the remaining safety margin, this may involve rejecting the command, holding the previous safe state, controlled deceleration, replanning, minimum-risk maneuver, or protective stopping. The response should prioritize maintaining a recoverable condition rather than preserving task completion at the expense of safety.

Repeated shield intervention is itself an important health signal. Occasional filtering may be expected during difficult situations, but frequent command rejection or modification can indicate model degradation, planner instability, environmental novelty, poor calibration, or inappropriate mission assumptions. Runtime assurance should therefore monitor intervention frequency, severity, causes, and patterns rather than treating each correction as an isolated event.

Recovery from shielding should be controlled. Once the triggering hazard disappears, the system should verify that state estimates, perception confidence, environmental conditions, and safety margins have stabilized before restoring unrestricted autonomy. Hysteresis and persistence requirements prevent rapid switching between filtered and unrestricted modes when the system operates near a safety boundary.

Shield events should be logged with enough information to reconstruct why intervention occurred. Relevant records include the estimated state, uncertainty, original action, modified or rejected action, active constraints, predicted violation, safety margins, model version, environmental context, and resulting physical behavior. These traces support debugging, safety validation, policy improvement, and refinement of operational limits.

At fleet scale, shield interventions can reveal shared weaknesses across robots. Repeated filtering at the same location may indicate environmental complexity, map problems, or inappropriate site-level policies. Similar interventions across multiple robots can reveal common model or planner limitations. Aggregating these events supports collective learning while each robot retains independent local shielding for immediate protection.

Runtime shielding and safety filters ultimately establish a controlled interface between intelligent intent and physical authority. The autonomy system may propose sophisticated actions, but only actions that satisfy the active safety conditions are permitted to reach the physical system. By combining constraint enforcement, prediction, uncertainty margins, intervention, fallback, and independent supervision, shielding ensures that intelligence remains subordinate to verified safety boundaries.

런타임 차폐 및 안전 필터(Runtime Shielding and Safety Filters)는 자율 지능(Autonomous Intelligence)과 물리적 구동(Physical Actuation) 사이에 보호 제어 계층(Protective Control Layer)을 제공한다. 그 목적은 인식(Perception), 계획(Planning), 월드 모델(World Models), 학습 정책(Learned Policies)을 대체하는 것이 아니라 제안된 행동이 검증된 안전 제약조건(Verified Safety Constraints) 내부에 유지되도록 보장하는 것이다. 인공지능 구성요소가 안전하지 않은 명령을 생성하더라도 차폐 시스템(Shield)은 물리적으로 실행되기 전에 해당 명령을 차단하거나 수정하거나 다른 안전한 명령으로 대체할 수 있다.

런타임 차폐(Runtime Shield)는 주 자율 시스템(Primary Autonomy System)을 둘러싸는 독립적인 의사결정 경계(Independent Decision Boundary)로 동작한다. 주 제어기(Primary Controller)는 작업 성능, 효율성 또는 학습된 목적함수(Learned Objectives)를 최적화할 수 있으며, 차폐 시스템은 제안된 행동이 허용 가능한지 평가한다. 이러한 분리는 고급 인공지능이 유연하게 동작할 수 있도록 하면서도 중요한 안전 속성(Critical Safety Properties)을 강제하는 더 단순하고 해석 가능한 메커니즘을 유지할 수 있게 한다.

안전 필터(Safety Filters)는 자율 시스템 파이프라인(Autonomy Pipeline)의 여러 지점에 배치될 수 있다. 높은 수준의 작업 명령(High-Level Task Commands), 계획된 궤적(Planned Trajectories), 속도 요청(Velocity Requests), 액추에이터 명령(Actuator Commands), 학습 정책 출력(Learned Policy Outputs)을 검증할 수 있다. 물리적 구동에 가까운 위치에서 필터링하면 강력한 최종 보호 기능을 제공하며, 더 앞단에서 필터링하면 안전하지 않은 계획이 시스템 내부로 전파되는 것을 방지할 수 있다. 따라서 계층화된 필터링(Layered Filtering)은 여러 추상화 수준에 걸쳐 방어 기능을 제공할 수 있다.

안전 필터(Safety Filter)의 기본 입력은 현재 추정 상태(Current Estimated State)와 제안된 행동(Proposed Action)이다. 필터는 해당 행동을 실행할 경우 충돌 회피(Collision Avoidance), 속도, 가속도, 안정성(Stability), 작업공간 제한(Workspace Limits), 인간 이격 거리(Human Separation), 액추에이터 능력(Actuator Capability), 운영 권한(Operational Permissions)과 관련된 제약조건을 위반할 가능성이 있는지를 평가한다. 상태 불확실성(State Uncertainty)도 함께 고려하여 불확실성이 높은 조건에서는 더욱 보수적인 허용성 판단(Admissibility Decision)을 수행해야 한다.

단순한 차폐 시스템(Simple Shield)은 사전에 정의된 제약조건을 직접 위반하는 모든 행동을 거부할 수 있다. 더욱 발전된 차폐 시스템은 실행을 허용하기 전에 미래 결과(Future Consequences)를 평가한다. 로봇 동역학(Robot Dynamics), 도달 가능 집합(Reachable Sets), 단기 시뮬레이션(Short-Horizon Simulation), 제어 장벽 함수(Control Barrier Functions), 예측 모델(Predictive Models), 검증된 전이 규칙(Verified Transition Rules)을 이용하여 현재는 안전해 보이는 행동이 시스템을 복구가 불가능한 위험 상태로 이동시킬 가능성이 있는지를 판단할 수 있다.

안전 행동 집합(Safe Action Set)의 개념은 런타임 차폐(Runtime Shielding)의 핵심이다. 각각의 관련 시스템 상태에 대해 보증 메커니즘(Assurance Mechanism)은 요구되는 안전 속성을 유지할 수 있는 행동을 결정할 수 있다. 주 제어기는 이러한 허용 가능한 행동(Admissible Actions) 가운데 자유롭게 선택할 수 있다. 불확실성이나 위험이 증가하면 안전 행동 집합이 축소되어 전체 임무를 반드시 중지시키지 않으면서 자율 권한(Autonomous Authority)을 점진적으로 제한할 수 있다.

행동 투영(Action Projection)은 단순한 행동 거부(Action Rejection)를 대신할 수 있는 방법이다. 제안된 명령이 안전 집합(Safe Set)을 벗어나는 경우 필터는 정의된 기준에 따라 가장 가까운 허용 가능한 행동으로 해당 명령을 투영할 수 있다. 과도한 속도를 낮추거나, 조향을 제한하거나, 매니퓰레이터 움직임(Manipulator Motion)을 제약할 수 있다. 이를 통해 안전하지 않은 요소의 실행을 방지하면서 원래 행동 의도(Action Intent)를 가능한 한 많이 유지할 수 있다.

궤적 안전 필터(Trajectory Safety Filters)는 개별 명령이 아니라 미래 상태의 연속적인 시퀀스를 평가한다. 계획된 경로가 현재 충돌이 없는 상태이더라도 충분한 정지 거리(Stopping Distance)나 복구 옵션(Recovery Options)을 확보할 수 없는 영역으로 진입할 수 있다. 필터는 실행 권한을 부여하기 전에 예측된 궤적(Predicted Trajectories)을 장애물, 인간, 제한 구역(Restricted Areas), 안정성 경계(Stability Boundaries), 동적 제약조건(Dynamic Constraints), 불확실성 여유(Uncertainty Margins)와 비교하여 검사할 수 있다.

제어 장벽 함수(Control Barrier Functions)는 연속 제어(Continuous Control) 과정에서 안전 제약조건을 유지하기 위한 하나의 수학적 접근법을 제공한다. 장벽 함수(Barrier Function)는 안전 상태와 위험 상태 사이의 경계를 표현하며, 제어기는 해당 경계를 넘지 않도록 필요한 경우 명령을 수정한다. 이러한 방법은 특정 가정 아래에서 시스템을 정의된 안전 영역(Safe Region) 내부에 제한하면서 비교적 부드러운 행동을 유지할 수 있다.

런타임 차폐(Runtime Shielding)는 도달 가능성 분석(Reachability Analysis)을 이용하여 미래의 안전성을 판단할 수도 있다. 하나의 명목 궤적(Nominal Trajectory)만 예측하는 대신 도달 가능 상태 방법(Reachable-State Methods)은 불확실성, 외부 교란(Disturbances), 제어 변화에 따라 로봇이 진입할 수 있는 상태 집합을 추정한다. 충분히 발생 가능한 시스템 변화 중 하나라도 위험 영역과 교차한다면 차폐 시스템은 더 일찍 행동을 제한하여 단일 결정론적 궤적(Deterministic Trajectory)만으로는 놓칠 수 있는 불확실성에 대한 보호 기능을 제공할 수 있다.

학습 정책(Learned Policies)과 시각-언어-행동 시스템(VLA Systems)은 내부적으로 출력을 검증하기 어려울 수 있기 때문에 독립적인 안전 필터링(Independent Safety Filtering)의 이점을 특히 크게 얻을 수 있다. 언어 조건 기반(Language-Conditioned) 또는 학습 기반 행동은 의미론적으로 합리적이더라도 물리적으로 부적절할 수 있다. 실행 이전에 안전 계층은 운동학적 실행 가능성(Kinematic Feasibility), 충돌 위험, 힘 제한(Force Limits), 작업공간 권한, 작업 승인(Task Authorization), 인간 근접도 등의 결정론적 제약조건(Deterministic Constraints)을 검사할 수 있다.

허용 가능한 행동은 환경과 임무에 따라 달라지므로 안전 필터(Safety Filters)는 운영 상황(Operational Context)을 반영해야 한다. 사람이 없는 창고에서 허용되는 속도도 사람, 취약한 장비 또는 좁은 통로 주변에서는 부적절할 수 있다. 상황 인식 필터링(Context-Aware Filtering)은 속도 제한, 이격 여유(Separation Margins), 힘 제한, 허용 구역(Permitted Zones), 기동 제약조건(Maneuver Constraints)을 조정하면서 이러한 제한이 어떻게 변경될 수 있는지를 규정하는 명시적인 규칙을 유지할 수 있다.

불확실성(Uncertainty)은 차폐 기능을 약화시키는 것이 아니라 더욱 보수적으로 동작하도록 해야 한다. 낮은 위치추정 신뢰도(Poor Localization), 불확실한 장애물 위치, 성능이 저하된 인식, 알려지지 않은 노면 상태 또는 신뢰할 수 없는 인간 움직임 예측은 안전하다고 판단되는 행동의 범위를 축소해야 한다. 안전 여유(Safety Margins)를 동적으로 확대하고 현재 상태와 환경에 대한 충분한 신뢰도가 회복될 때까지 속도 또는 기동 복잡성(Maneuver Complexity)을 제한할 수 있다.

차폐 시스템(Shielding)은 엄격한 타이밍 요구조건(Timing Requirements) 내에서 동작해야 한다. 안전하지 않은 명령이 이미 액추에이터에 전달된 이후 도착하는 안전 판단은 충분한 보호 기능을 제공하지 못한다. 따라서 필터는 제한된 실행 시간(Bounded Execution Time), 예측 가능한 스케줄링(Predictable Scheduling), 보호된 연산 자원(Protected Computational Resources), 필요한 상태 정보에 대한 직접적인 접근을 확보해야 한다. 중요한 필터에서는 정교하지만 지연되는 추론보다 결정론적이고 적시에 수행되는 평가가 더 중요하기 때문에 의도적으로 단순화된 모델(Simplified Models)을 사용할 수 있다.

독립성(Independence) 역시 중요한 아키텍처 속성이다. 차폐 시스템은 감독하는 제어기와 모든 가정, 모델, 센서 의존성(Sensor Dependency), 고장 형태(Failure Mode)를 공유하지 않는 것이 바람직하다. 결정론적 기하학(Deterministic Geometry), 안전 등급 센서(Safety-Rated Sensors), 단순화된 동역학(Simplified Dynamics), 독립 상태 검사(Independent State Checks), 별도의 연산 자원(Separate Computing Resources)을 통해 다양성(Diversity)을 확보할 수 있다. 이를 통해 하나의 공통 오류가 자율 의사결정과 보호 필터를 동시에 손상시킬 가능성을 줄일 수 있다.

제안된 행동을 안전하게 수정할 수 없는 경우 차폐 시스템은 정의된 폴백 대응(Fallback Response)을 실행해야 한다. 남아 있는 안전 여유에 따라 명령 거부, 이전의 안전 상태 유지, 제어된 감속(Controlled Deceleration), 재계획(Replanning), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stop) 등을 수행할 수 있다. 이러한 대응은 임무 완료를 위해 안전을 희생하기보다 시스템을 복구 가능한 상태(Recoverable Condition)로 유지하는 것을 우선해야 한다.

반복적인 차폐 개입(Shield Intervention)은 그 자체로 중요한 건전성 신호(Health Signal)가 된다. 어려운 상황에서는 간헐적인 필터링이 정상적일 수 있지만 명령의 거부나 수정이 빈번하게 발생한다면 모델 성능 저하(Model Degradation), 계획기 불안정성(Planner Instability), 환경 신규성(Environmental Novelty), 부정확한 캘리브레이션 또는 부적절한 임무 가정(Mission Assumptions)을 의미할 수 있다. 따라서 런타임 보증은 각각의 수정 동작을 독립적인 사건으로만 처리하지 않고 개입 빈도, 심각도, 원인, 패턴을 함께 모니터링해야 한다.

차폐 상태로부터의 복구(Recovery)는 통제된 방식으로 이루어져야 한다. 개입을 유발했던 위험이 사라진 이후에도 시스템은 제한 없는 자율성(Unrestricted Autonomy)을 복원하기 전에 상태 추정, 인식 신뢰도(Perception Confidence), 환경 조건, 안전 여유가 안정화되었는지를 확인해야 한다. 히스테리시스(Hysteresis)와 지속성 요구조건(Persistence Requirements)은 시스템이 안전 경계 근처에서 동작할 때 필터링 모드와 비제한 모드 사이를 빠르게 반복 전환하는 현상을 방지한다.

차폐 이벤트(Shield Events)는 개입이 발생한 이유를 재구성할 수 있을 만큼 충분한 정보와 함께 기록되어야 한다. 관련 기록에는 추정 상태, 불확실성, 원래 행동(Original Action), 수정되거나 거부된 행동, 활성 제약조건(Active Constraints), 예측된 위반(Predicted Violation), 안전 여유, 모델 버전(Model Version), 환경 상황, 결과적인 물리적 행동이 포함된다. 이러한 추적 기록(Traces)은 디버깅(Debugging), 안전 검증(Safety Validation), 정책 개선(Policy Improvement), 운영 제한(Operational Limits)의 개선을 지원한다.

플릿 규모(Fleet Scale)에서는 차폐 개입을 통해 여러 로봇이 공유하는 취약점을 발견할 수 있다. 동일한 위치에서 반복적인 필터링이 발생하면 환경 복잡성(Environmental Complexity), 지도 문제(Map Problems), 부적절한 사이트 수준 정책(Site-Level Policies)을 의미할 수 있다. 여러 로봇에서 유사한 개입이 발생하면 공통된 모델 또는 계획기 한계를 발견할 수 있다. 이러한 이벤트를 통합하면 집단 학습(Collective Learning)을 지원할 수 있으며, 동시에 각 로봇은 즉각적인 보호를 위해 독립적인 로컬 차폐(Local Shielding)를 유지해야 한다.

궁극적으로 런타임 차폐 및 안전 필터(Runtime Shielding and Safety Filters)는 지능적 의도(Intelligent Intent)와 물리적 권한(Physical Authority) 사이에 통제된 인터페이스(Controlled Interface)를 구축한다. 자율 시스템은 정교한 행동을 제안할 수 있지만 활성화된 안전 조건(Active Safety Conditions)을 만족하는 행동만 실제 물리 시스템에 전달될 수 있다. 제약조건 강제(Constraint Enforcement), 예측(Prediction), 불확실성 여유(Uncertainty Margins), 개입(Intervention), 폴백(Fallback), 독립적 감독(Independent Supervision)을 결합함으로써 차폐 시스템은 지능(Intelligence)이 검증된 안전 경계(Verified Safety Boundaries)에 종속된 상태로 유지되도록 보장한다.

##  

## 07.14. Simplex and Safety Controller Architectures

![](images/image15.png){width="7.268055555555556in" height="7.268055555555556in"}

Simplex and safety controller architectures provide runtime assurance by separating high-performance autonomous control from a simpler, highly trusted safety controller. The advanced controller may use learned policies, world models, optimization, or complex planning to achieve mission objectives, while the safety controller preserves essential safety properties when the advanced controller can no longer be trusted to maintain them.

The classical Simplex architecture contains an advanced controller, a safety controller, and a decision module that supervises which controller has physical authority. Under normal conditions, the advanced controller operates the system because it can provide greater capability and performance. When monitored conditions indicate unacceptable future risk, the decision module transfers control to the safety controller before safety constraints are violated.

The advanced controller is allowed to be complex because system safety does not depend exclusively on proving every aspect of its internal behavior. It may include neural networks, reinforcement learning, VLA models, nonlinear optimization, or adaptive planning mechanisms that are difficult to verify completely. The architecture instead limits their authority through independent monitoring and a trusted recovery mechanism.

The safety controller is intentionally simpler and more conservative than the advanced controller. Its objective is not maximum mission performance but preservation of a verified safe state or transition toward a minimum-risk condition. It may enforce reduced velocity, restricted maneuvering, collision avoidance, controlled deceleration, stable posture, safe separation, return-to-safe-region behavior, or protective stopping.

A decision module acts as the supervisory mechanism between the two controllers. It continuously evaluates system state, environmental conditions, uncertainty, predicted trajectories, controller behavior, and available recovery margin. Its critical responsibility is to determine when the advanced controller must lose authority, ensuring that switching occurs early enough for the safety controller to prevent entry into an unrecoverable state.

Recoverability is therefore central to Simplex design. The system should not wait until a safety constraint has already been violated before switching controllers. Instead, the monitor determines whether the current state remains inside a recoverable region from which the safety controller can still maintain or restore safety. Approaching the boundary of this region becomes a trigger for preventive intervention.

Reachability analysis can provide a formal basis for defining recoverable regions. Given robot dynamics, actuator limits, disturbances, and environmental constraints, the system estimates states that can evolve toward hazards and states from which the safety controller can guarantee an acceptable response. These reachable sets help the decision module determine whether continued advanced control remains sufficiently safe.

Prediction-based switching offers another implementation strategy. The runtime monitor can simulate or estimate the future trajectory produced by the advanced controller and compare it with safety boundaries. If predicted motion approaches obstacles, stability limits, restricted regions, or insufficient stopping margins, control can be transferred before the dangerous state occurs. Prediction horizon must be long enough to preserve intervention time.

Uncertainty must be incorporated into switching decisions because state estimation and environmental predictions are never exact. Localization uncertainty, perception ambiguity, uncertain human motion, actuator variation, and model mismatch should reduce the region in which advanced control is permitted. Conservative margins allow the safety controller to receive authority earlier when the system has less reliable knowledge about its physical situation.

Controller switching must itself be safe. Abruptly replacing one controller with another can introduce discontinuities in steering, velocity, acceleration, force, or actuator commands. Transition logic may therefore require command blending, bounded rate changes, state synchronization, or predefined handover conditions. The transfer mechanism should prevent the assurance architecture from creating the instability it is intended to avoid.

Once the safety controller assumes authority, the system may enter a degraded operational mode rather than immediately stopping. If sufficient safety margin remains, the robot can reduce speed, follow a conservative route, maintain separation, complete a controlled retreat, or move toward a designated safe location. This preserves useful operation while ensuring that safety takes precedence over performance or mission completion.

Protective stopping becomes necessary when continued motion cannot be justified safely. The safety controller should then drive the system toward a defined minimum-risk condition using controlled braking, stable actuator states, safe manipulator posture, or other platform-specific responses. The appropriate safe state depends on robot dynamics, environment, payload, human proximity, and hazards associated with stopping in place.

Returning authority to the advanced controller requires stronger evidence than the disappearance of a single warning signal. The system should confirm that state estimation, perception confidence, computational health, environmental conditions, and recovery margins have stabilized. Hysteresis and persistence criteria prevent repeated switching between controllers when operating near the decision boundary and improve overall behavioral stability.

A Simplex architecture depends strongly on independence and diversity. The safety controller and decision module should avoid sharing all models, assumptions, software components, sensors, and computing resources with the advanced controller. Simplified dynamics, deterministic algorithms, independent sensors, separate processors, or protected execution partitions reduce common-cause failures that could otherwise disable both autonomy and safety simultaneously.

Timing guarantees are equally important because controller switching must occur before recovery becomes impossible. The monitor, decision logic, communication path, and safety controller require bounded execution latency and protected computational resources. A theoretically correct safety controller provides little protection if overloaded processors, delayed messages, or scheduling failures prevent it from receiving physical authority at the required moment.

Runtime shielding and Simplex control can complement each other. A safety filter may continuously modify small unsafe deviations while the advanced controller remains active, whereas the Simplex decision module handles larger failures by transferring authority entirely to the safety controller. This layered approach allows minor violations to be corrected locally while preserving a stronger fallback mechanism for severe or persistent degradation.

Multiple fallback controllers can extend the classical two-controller Simplex architecture. Different controllers may support reduced-speed autonomy, deterministic navigation, emergency retreat, controlled stopping, or hardware-level protection. The supervisory logic can select the least restrictive controller capable of maintaining safety, creating a graded architecture rather than a single transition directly from full autonomy to complete shutdown.

Controller authority should be explicit and unambiguous at every moment. The architecture must define which controller owns each actuator command, how stale commands are discarded, how command arbitration occurs, and how communication failure is handled. Conflicting simultaneous commands from advanced and safety controllers can undermine assurance, making deterministic authority management an essential part of the design.

Simplex events should be recorded for verification and lifecycle improvement. Relevant information includes system state, uncertainty, advanced-controller commands, predicted violations, switching criteria, controller selected, transition timing, safety margins, resulting trajectory, and recovery conditions. These traces allow engineers to determine whether intervention occurred early enough and whether the safety controller behaved as validated.

Repeated transfers to the safety controller are themselves evidence of degraded autonomous performance. Frequent switching may reveal planner instability, model drift, perception problems, environmental novelty, insufficient operational margins, or inappropriate mission assumptions. Monitoring intervention frequency and causes transforms the Simplex architecture from a passive emergency mechanism into an important source of system-health information.

At fleet scale, switching events can be aggregated to identify shared hazards and systematic weaknesses. Multiple robots entering safety control at the same location may indicate environmental complexity or map errors, while similar transitions across platforms may reveal common software limitations. Fleet intelligence can distribute these findings, but every robot should retain local authority to execute safety transitions independently.

Simplex and safety controller architectures ultimately establish a hierarchy of trust between capability and safety. Advanced intelligence is permitted to control the physical system only while runtime evidence indicates that sufficient recovery margin remains. When that confidence is lost, authority transfers to a simpler trusted controller whose primary purpose is preserving safety, ensuring that mission performance remains subordinate to recoverable physical operation.

심플렉스 및 안전 제어기 아키텍처(Simplex and Safety Controller Architectures)는 고성능 자율 제어(High-Performance Autonomous Control)를 보다 단순하고 높은 신뢰성을 가진 안전 제어기(Safety Controller)와 분리함으로써 런타임 보증(Runtime Assurance)을 제공한다. 고급 제어기(Advanced Controller)는 학습 정책(Learned Policies), 월드 모델(World Models), 최적화(Optimization), 복잡한 계획(Complex Planning)을 활용하여 임무 목표를 달성할 수 있으며, 안전 제어기는 고급 제어기가 더 이상 안전을 유지할 수 있다고 신뢰하기 어려운 상황에서 핵심적인 안전 속성(Safety Properties)을 보존한다.

전통적인 심플렉스 아키텍처(Simplex Architecture)는 고급 제어기(Advanced Controller), 안전 제어기(Safety Controller), 그리고 어느 제어기가 물리적 제어 권한(Physical Authority)을 가질지를 감독하는 결정 모듈(Decision Module)로 구성된다. 정상 조건에서는 더 높은 기능과 성능을 제공할 수 있는 고급 제어기가 시스템을 운용한다. 모니터링된 조건이 허용할 수 없는 미래 위험을 나타내면 결정 모듈은 안전 제약조건(Safety Constraints)이 위반되기 전에 제어 권한을 안전 제어기로 이전한다.

고급 제어기(Advanced Controller)는 시스템 안전이 내부 동작의 모든 측면을 완전히 증명하는 것에만 의존하지 않기 때문에 복잡한 구조를 사용할 수 있다. 신경망(Neural Networks), 강화학습(Reinforcement Learning), 시각-언어-행동 모델(VLA Models), 비선형 최적화(Nonlinear Optimization), 적응형 계획 메커니즘(Adaptive Planning Mechanisms)과 같이 완전한 검증이 어려운 기술이 포함될 수 있다. 대신 아키텍처는 독립적인 모니터링(Independent Monitoring)과 신뢰할 수 있는 복구 메커니즘(Trusted Recovery Mechanism)을 통해 이들의 제어 권한을 제한한다.

안전 제어기(Safety Controller)는 의도적으로 고급 제어기보다 단순하고 보수적으로 설계된다. 그 목적은 최대의 임무 성능을 달성하는 것이 아니라 검증된 안전 상태(Verified Safe State)를 유지하거나 최소 위험 상태(Minimum-Risk Condition)로 전환하는 것이다. 이를 위해 속도 감소, 제한된 기동(Restricted Maneuvering), 충돌 회피(Collision Avoidance), 제어된 감속(Controlled Deceleration), 안정적인 자세(Stable Posture), 안전 이격(Safe Separation), 안전 영역 복귀(Return-to-Safe-Region), 보호 정지(Protective Stopping) 등을 강제할 수 있다.

결정 모듈(Decision Module)은 두 제어기 사이의 감독 메커니즘(Supervisory Mechanism)으로 동작한다. 시스템 상태(System State), 환경 조건(Environmental Conditions), 불확실성(Uncertainty), 예측 궤적(Predicted Trajectories), 제어기 동작, 사용 가능한 복구 여유(Recovery Margin)를 지속적으로 평가한다. 결정 모듈의 핵심 책임은 고급 제어기가 언제 제어 권한을 상실해야 하는지를 판단하고, 시스템이 복구 불가능 상태(Unrecoverable State)에 진입하기 전에 안전 제어기로 전환되도록 하는 것이다.

따라서 복구 가능성(Recoverability)은 심플렉스 설계(Simplex Design)의 핵심 개념이다. 시스템은 안전 제약조건이 이미 위반된 이후에 제어기를 전환해서는 안 된다. 대신 모니터는 현재 상태가 안전 제어기를 통해 안전성을 유지하거나 복원할 수 있는 복구 가능 영역(Recoverable Region) 내부에 있는지를 판단한다. 시스템이 이 영역의 경계에 접근하는 것이 예방적 개입(Preventive Intervention)을 시작하는 조건이 된다.

도달 가능성 분석(Reachability Analysis)은 복구 가능 영역(Recoverable Regions)을 정의하기 위한 형식적인 기반을 제공할 수 있다. 로봇 동역학(Robot Dynamics), 액추에이터 한계(Actuator Limits), 외부 교란(Disturbances), 환경 제약조건(Environmental Constraints)을 기반으로 시스템이 위험으로 발전할 수 있는 상태와 안전 제어기가 허용 가능한 대응을 보장할 수 있는 상태를 추정한다. 이러한 도달 가능 집합(Reachable Sets)은 결정 모듈이 고급 제어를 계속 사용하는 것이 충분히 안전한지를 판단하는 데 도움을 준다.

예측 기반 전환(Prediction-Based Switching)은 또 다른 구현 전략을 제공한다. 런타임 모니터(Runtime Monitor)는 고급 제어기가 생성한 미래 궤적을 시뮬레이션하거나 추정하고 이를 안전 경계(Safety Boundaries)와 비교할 수 있다. 예측된 움직임이 장애물, 안정성 한계(Stability Limits), 제한 구역(Restricted Regions) 또는 불충분한 정지 여유(Stopping Margins)에 접근하면 위험 상태가 발생하기 전에 제어 권한을 이전할 수 있다. 예측 범위(Prediction Horizon)는 개입에 필요한 시간을 확보할 수 있을 만큼 충분히 길어야 한다.

상태 추정(State Estimation)과 환경 예측은 완벽하게 정확할 수 없으므로 불확실성(Uncertainty)을 제어기 전환 결정에 포함해야 한다. 위치추정 불확실성(Localization Uncertainty), 인식 모호성(Perception Ambiguity), 불확실한 인간 움직임, 액추에이터 변동(Actuator Variation), 모델 불일치(Model Mismatch)는 고급 제어가 허용되는 영역을 축소해야 한다. 보수적인 안전 여유(Conservative Margins)를 적용하면 시스템이 자신의 물리적 상황을 신뢰성 있게 파악하기 어려워질수록 안전 제어기가 더 일찍 권한을 인계받을 수 있다.

제어기 전환(Controller Switching) 자체도 안전해야 한다. 하나의 제어기를 다른 제어기로 갑자기 교체하면 조향, 속도, 가속도, 힘 또는 액추에이터 명령에서 불연속성(Discontinuities)이 발생할 수 있다. 따라서 전환 로직(Transition Logic)은 명령 혼합(Command Blending), 제한된 변화율(Bounded Rate Changes), 상태 동기화(State Synchronization), 사전에 정의된 인계 조건(Handover Conditions)을 필요로 할 수 있다. 제어 권한 이전 메커니즘 자체가 방지하려던 불안정성을 발생시켜서는 안 된다.

안전 제어기(Safety Controller)가 제어 권한을 인계받은 이후에도 시스템이 즉시 정지하는 대신 성능 저하 운용 모드(Degraded Operational Mode)로 진입할 수 있다. 충분한 안전 여유가 남아 있다면 로봇은 속도를 낮추고, 보수적인 경로(Conservative Route)를 따르며, 안전 이격을 유지하고, 통제된 후퇴(Controlled Retreat)를 수행하거나 지정된 안전 위치로 이동할 수 있다. 이를 통해 안전을 성능이나 임무 완료보다 우선하면서도 유용한 운용 능력을 유지할 수 있다.

계속 움직이는 것을 안전하게 정당화할 수 없는 경우에는 보호 정지(Protective Stopping)가 필요하다. 안전 제어기는 제어된 제동(Controlled Braking), 안정적인 액추에이터 상태, 안전한 매니퓰레이터 자세(Safe Manipulator Posture) 또는 기타 플랫폼별 대응을 사용하여 시스템을 정의된 최소 위험 상태(Minimum-Risk Condition)로 이동시켜야 한다. 적절한 안전 상태는 로봇 동역학, 환경, 페이로드(Payload), 인간 근접도(Human Proximity), 제자리 정지와 관련된 위험에 따라 달라진다.

고급 제어기(Advanced Controller)로 제어 권한을 다시 반환하려면 하나의 경고 신호가 사라진 것보다 더 강력한 증거가 필요하다. 시스템은 상태 추정, 인식 신뢰도(Perception Confidence), 연산 건전성(Computational Health), 환경 조건, 복구 여유가 안정화되었는지를 확인해야 한다. 히스테리시스(Hysteresis)와 지속성 기준(Persistence Criteria)은 결정 경계 근처에서 두 제어기 사이의 반복적인 전환을 방지하고 전체 시스템 행동의 안정성을 향상시킨다.

심플렉스 아키텍처(Simplex Architecture)는 독립성(Independence)과 다양성(Diversity)에 크게 의존한다. 안전 제어기와 결정 모듈은 고급 제어기와 모든 모델, 가정, 소프트웨어 구성요소, 센서 및 연산 자원을 공유하지 않는 것이 바람직하다. 단순화된 동역학(Simplified Dynamics), 결정론적 알고리즘(Deterministic Algorithms), 독립 센서(Independent Sensors), 별도의 프로세서(Separate Processors), 보호된 실행 파티션(Protected Execution Partitions)은 자율 제어와 안전 기능을 동시에 무력화할 수 있는 공통 원인 고장(Common-Cause Failures)을 줄인다.

제어기 전환은 복구가 불가능해지기 전에 수행되어야 하므로 타이밍 보장(Timing Guarantees) 역시 중요하다. 모니터, 결정 로직(Decision Logic), 통신 경로(Communication Path), 안전 제어기는 제한된 실행 지연시간(Bounded Execution Latency)과 보호된 연산 자원(Protected Computational Resources)을 필요로 한다. 이론적으로 정확한 안전 제어기라도 프로세서 과부하, 메시지 지연 또는 스케줄링 실패로 필요한 시점에 물리적 제어 권한을 확보하지 못한다면 충분한 보호 기능을 제공할 수 없다.

런타임 차폐(Runtime Shielding)와 심플렉스 제어(Simplex Control)는 서로 보완적으로 사용할 수 있다. 안전 필터(Safety Filter)는 고급 제어기가 활성화된 상태에서 작은 안전 위반을 지속적으로 수정할 수 있으며, 심플렉스 결정 모듈은 더 큰 고장 상황에서 제어 권한 전체를 안전 제어기로 이전할 수 있다. 이러한 계층적 접근(Layered Approach)은 작은 위반을 로컬 수준에서 수정하면서 심각하거나 지속적인 성능 저하에 대응하기 위한 더욱 강력한 폴백 메커니즘(Fallback Mechanism)을 유지할 수 있도록 한다.

여러 폴백 제어기(Multiple Fallback Controllers)를 사용하면 전통적인 두 제어기 기반 심플렉스 아키텍처를 확장할 수 있다. 서로 다른 제어기가 저속 자율 운용(Reduced-Speed Autonomy), 결정론적 내비게이션(Deterministic Navigation), 비상 후퇴(Emergency Retreat), 제어된 정지(Controlled Stopping), 하드웨어 수준 보호(Hardware-Level Protection)를 담당할 수 있다. 감독 로직(Supervisory Logic)은 안전을 유지할 수 있는 가장 제한이 적은 제어기를 선택함으로써 완전 자율 운용에서 전체 정지로 즉시 전환하는 대신 단계적인 아키텍처(Graded Architecture)를 구성할 수 있다.

제어기 권한(Controller Authority)은 모든 순간에 명확하고 모호하지 않아야 한다. 아키텍처는 각 액추에이터 명령을 어느 제어기가 소유하는지, 오래된 명령(Stale Commands)을 어떻게 폐기하는지, 명령 중재(Command Arbitration)를 어떻게 수행하는지, 통신 고장에 어떻게 대응하는지를 정의해야 한다. 고급 제어기와 안전 제어기가 동시에 서로 충돌하는 명령을 전달하면 보증 체계를 훼손할 수 있으므로 결정론적 권한 관리(Deterministic Authority Management)는 설계의 필수 요소가 된다.

심플렉스 이벤트(Simplex Events)는 검증 및 수명주기 개선(Verification and Lifecycle Improvement)을 위해 기록되어야 한다. 관련 정보에는 시스템 상태, 불확실성, 고급 제어기 명령, 예측된 위반(Predicted Violations), 전환 기준(Switching Criteria), 선택된 제어기, 전환 타이밍(Transition Timing), 안전 여유(Safety Margins), 결과 궤적(Resulting Trajectory), 복구 조건(Recovery Conditions)이 포함된다. 이러한 기록을 통해 엔지니어는 개입이 충분히 일찍 이루어졌는지와 안전 제어기가 검증된 방식으로 동작했는지를 판단할 수 있다.

안전 제어기로의 반복적인 권한 이전은 그 자체로 자율 시스템 성능 저하(Degraded Autonomous Performance)의 증거가 된다. 빈번한 전환은 계획기 불안정성(Planner Instability), 모델 드리프트(Model Drift), 인식 문제(Perception Problems), 환경 신규성(Environmental Novelty), 불충분한 운영 여유(Operational Margins), 부적절한 임무 가정(Mission Assumptions)을 나타낼 수 있다. 개입 빈도와 원인을 모니터링하면 심플렉스 아키텍처를 수동적인 비상 메커니즘에서 중요한 시스템 건전성 정보(System-Health Information)의 공급원으로 확장할 수 있다.

플릿 규모(Fleet Scale)에서는 제어기 전환 이벤트를 통합하여 공유 위험(Shared Hazards)과 체계적인 취약점을 식별할 수 있다. 여러 로봇이 동일한 위치에서 안전 제어 모드(Safety Control)에 진입한다면 환경 복잡성 또는 지도 오류(Map Errors)를 의미할 수 있으며, 여러 플랫폼에서 유사한 전환이 발생하면 공통적인 소프트웨어 한계를 나타낼 수 있다. 플릿 지능(Fleet Intelligence)은 이러한 정보를 공유할 수 있지만 각 로봇은 안전 전환을 독립적으로 실행할 수 있는 로컬 권한(Local Authority)을 유지해야 한다.

궁극적으로 심플렉스 및 안전 제어기 아키텍처(Simplex and Safety Controller Architectures)는 기능적 역량(Capability)과 안전(Safety) 사이에 신뢰 계층(Hierarchy of Trust)을 구축한다. 런타임 증거(Runtime Evidence)가 충분한 복구 여유가 남아 있음을 나타내는 동안에만 고급 지능(Advanced Intelligence)이 물리 시스템을 제어하도록 허용된다. 이러한 신뢰가 상실되면 제어 권한은 안전 보존을 주요 목적으로 하는 보다 단순하고 신뢰할 수 있는 제어기로 이전되며, 이를 통해 임무 성능(Mission Performance)이 항상 복구 가능한 물리적 운용(Recoverable Physical Operation)과 안전보다 우선하지 않도록 보장한다.

##  

## 07.15. Logging Traceability and Post Event Analysis

![](images/image16.png){width="7.268055555555556in" height="7.268055555555556in"}

Logging, traceability, and post-event analysis provide the historical evidence required to understand how a Physical AI system behaved before, during, and after significant runtime events. Runtime assurance is incomplete if it can detect hazards but cannot reconstruct their causes. Structured records connect sensor observations, internal decisions, safety interventions, physical actions, and outcomes into an auditable operational history.

Logging should capture the information necessary to reconstruct the system state without attempting to record every signal at maximum resolution indefinitely. Physical AI platforms generate large volumes of camera, LiDAR, state, model, planning, control, and diagnostic data. A practical architecture therefore distinguishes continuous baseline logging from high-resolution event logging that is activated around safety-relevant conditions.

Traceability links each important decision to the information and software configuration that produced it. A trajectory or actuator command should be associated with relevant sensor observations, state estimates, world-model predictions, planner outputs, safety constraints, and controller authority. This relationship allows engineers to move backward from physical behavior to the chain of computational decisions responsible for that behavior.

Time synchronization is fundamental because evidence from different subsystems is useful only when events can be aligned accurately. Cameras, LiDAR, IMUs, controllers, GPUs, distributed computers, and fleet services may operate with different clocks and update rates. Consistent timestamps and monitored clock synchronization allow investigators to determine which observations were actually available when a particular decision was made.

Runtime logs should preserve the state of perception and localization that influenced autonomous decisions. Relevant records may include detected objects, confidence values, occupancy estimates, localization pose, uncertainty, map alignment, sensor-health indicators, and fusion outputs. Raw sensor data can be retained selectively when necessary to verify whether a later failure originated in sensing, interpretation, or downstream reasoning.

AI model traceability requires explicit identification of the models involved in each decision. Model name, version, weights or configuration identifier, calibration state, inference parameters, adaptation history, and deployment package can be recorded. Without this information, identical input data may be difficult to reproduce because later software or model updates can produce substantially different outputs.

World-model logging should capture predictions together with the observations that later confirm or contradict them. Predicted states, trajectories, occupancy, object motion, uncertainty ranges, prediction horizons, and subsequent residual errors provide evidence about whether the internal representation of the future was reliable. This history supports prediction-consistency analysis and identification of model drift or unfamiliar operating conditions.

Planning and control traces should preserve both intended and executed behavior. Candidate trajectories, selected plans, optimization costs, constraints, velocity commands, actuator requests, controller states, and measured responses can reveal where an unsafe sequence originated. Differences between planned commands and actual motion may distinguish planning errors from actuator faults, communication delays, or low-level control problems.

Safety interventions require particularly detailed logging because they represent moments when runtime assurance changed or restricted autonomous authority. Constraint violations, anomaly scores, OOD indicators, shield modifications, Simplex switching events, fallback activation, protective stops, and recovery decisions should be recorded together with the conditions and thresholds that triggered them.

Resource and timing evidence is also essential for reconstruction. CPU and GPU utilization, memory pressure, inference latency, queue depth, network delay, missed deadlines, thermal conditions, watchdog events, and process failures may explain behavior that appears algorithmically incorrect. A correct perception or planning result can still become unsafe when delivered after its useful temporal window has expired.

Event-triggered logging can preserve high-value evidence without requiring permanent storage of every high-bandwidth stream. A rolling buffer can continuously retain recent history and freeze selected intervals when a collision risk, emergency stop, anomaly, safety-controller transition, or major performance degradation occurs. Capturing time before and after the trigger provides context for both causal analysis and recovery assessment.

Event records should contain enough metadata to establish the operating context. Robot identity, hardware configuration, software build, model versions, mission identifier, autonomy mode, map version, environmental conditions, payload state, operator interventions, and maintenance status may all affect interpretation. Context prevents investigators from comparing events that appear similar but occurred under fundamentally different operating assumptions.

Integrity of logs is important because safety evidence must remain trustworthy after the event. Records should be protected against accidental modification, corruption, incomplete writes, timestamp ambiguity, and uncontrolled deletion. Checksums, append-oriented storage, access controls, redundant event summaries, or authenticated records can improve confidence that post-event analysis is based on the data actually generated during operation.

Logging must also remain resilient during failures. A system crash, power interruption, network disconnection, or storage fault should not automatically destroy the evidence needed to understand the incident. Critical event summaries can be written to protected local storage, while less critical high-volume data may be transferred later. Safety logging should therefore degrade gracefully when normal infrastructure becomes unavailable.

Post-event analysis begins by reconstructing a synchronized timeline. Investigators can align sensor observations, state estimates, AI outputs, plans, commands, safety-monitor decisions, controller transitions, and physical responses. This timeline establishes what the system knew, what it predicted, what it decided, what was actually executed, and how the environment responded at each significant moment.

Causal analysis should distinguish the initiating condition from downstream consequences. A localization error may create an incorrect world-model state, which then produces a poor trajectory and eventually triggers a safety shield. Treating the shield intervention as the root cause would miss the actual failure chain. Traceability allows analysts to follow dependencies backward until the earliest credible initiating factor is identified.

Counterfactual replay can strengthen post-event understanding. Recorded inputs may be replayed through alternative model versions, planners, thresholds, or safety policies to examine whether different configurations would have changed the outcome. Such replay does not prove what would have happened physically, but it can identify sensitive decision points and support controlled regression testing of proposed corrections.

Near misses should be analyzed alongside actual failures because they contain valuable safety information without requiring harmful outcomes. Small stopping margins, repeated shield interventions, unstable replanning, temporary loss of localization, or safety-controller activation may reveal weaknesses that have not yet produced an incident. Systematic near-miss analysis supports proactive improvement rather than waiting for confirmed accidents.

Fleet-scale traceability allows patterns to be identified across robots, sites, missions, and software versions. Similar anomalies occurring on multiple platforms may reveal common model weaknesses, while events isolated to one robot may indicate local hardware or calibration problems. Aggregated evidence can distinguish individual faults from systematic issues and prioritize engineering actions according to recurrence and severity.

Post-event findings should feed directly into the Physical AI lifecycle. Confirmed failure patterns can generate new simulation scenarios, regression tests, dataset examples, safety constraints, maintenance rules, model updates, or operational restrictions. Each corrective action should remain linked to the evidence that motivated it, creating traceability from runtime event through engineering change and subsequent validation.

Logging policies must balance diagnostic value with storage, bandwidth, privacy, security, and operational constraints. High-bandwidth raw data may require selective retention, compression, event prioritization, or controlled access. The objective is not maximum data accumulation but preservation of sufficient, reliable evidence to explain safety-relevant decisions while respecting deployment constraints and data-governance requirements.

Logging, traceability, and post-event analysis ultimately create the memory of runtime assurance. They transform transient sensor observations, AI decisions, interventions, and physical outcomes into evidence that can be inspected, reproduced, compared, and improved. By connecting runtime behavior with its causes and subsequent corrective actions, Physical AI systems can learn systematically from anomalies, near misses, degradations, and failures throughout their operational lifecycle.

로깅, 추적성 및 사후 이벤트 분석(Logging, Traceability, and Post-Event Analysis)은 물리 인공지능(Physical AI) 시스템이 중요한 런타임 이벤트(Runtime Event)의 발생 전, 발생 중, 발생 후에 어떻게 동작했는지를 이해하는 데 필요한 역사적 증거(Historical Evidence)를 제공한다. 런타임 보증(Runtime Assurance)이 위험을 탐지할 수 있더라도 그 원인을 재구성할 수 없다면 충분하지 않다. 구조화된 기록(Structured Records)은 센서 관측, 내부 의사결정, 안전 개입(Safety Interventions), 물리적 행동, 결과를 감사 가능한 운영 이력(Auditable Operational History)으로 연결한다.

로깅(Logging)은 모든 신호를 최대 해상도로 무기한 기록하려는 것이 아니라 시스템 상태를 재구성하는 데 필요한 정보를 포착해야 한다. 물리 인공지능 플랫폼은 카메라, 라이다(LiDAR), 상태, 모델, 계획, 제어, 진단 데이터에서 막대한 양의 정보를 생성한다. 따라서 실용적인 아키텍처는 지속적인 기본 로깅(Continuous Baseline Logging)과 안전 관련 조건이 발생했을 때 활성화되는 고해상도 이벤트 로깅(High-Resolution Event Logging)을 구분한다.

추적성(Traceability)은 각각의 중요한 의사결정을 해당 결정을 생성한 정보 및 소프트웨어 구성(Software Configuration)과 연결한다. 궤적(Trajectory)이나 액추에이터 명령(Actuator Command)은 관련 센서 관측, 상태 추정(State Estimates), 월드 모델 예측(World-Model Predictions), 계획기 출력(Planner Outputs), 안전 제약조건(Safety Constraints), 제어기 권한(Controller Authority)과 연결되어야 한다. 이러한 관계를 통해 엔지니어는 물리적 행동으로부터 역방향으로 추적하여 해당 행동을 발생시킨 연산 의사결정의 연쇄(Chain of Computational Decisions)를 확인할 수 있다.

서로 다른 서브시스템의 증거는 이벤트를 정확하게 정렬할 수 있을 때에만 유용하므로 시간 동기화(Time Synchronization)는 기본적인 요소이다. 카메라, 라이다, 관성 측정 장치(IMU), 제어기, GPU, 분산 컴퓨터(Distributed Computers), 플릿 서비스(Fleet Services)는 서로 다른 클록(Clock)과 업데이트 주기로 동작할 수 있다. 일관된 타임스탬프(Consistent Timestamps)와 모니터링되는 클록 동기화를 통해 조사자는 특정 의사결정이 내려진 시점에 실제로 어떤 관측 정보가 사용 가능했는지를 판단할 수 있다.

런타임 로그(Runtime Logs)는 자율 의사결정에 영향을 준 인식(Perception)과 위치추정(Localization)의 상태를 보존해야 한다. 관련 기록에는 탐지된 객체, 신뢰도 값(Confidence Values), 점유 추정(Occupancy Estimates), 위치추정 자세(Localization Pose), 불확실성(Uncertainty), 지도 정렬(Map Alignment), 센서 건전성 지표(Sensor-Health Indicators), 센서 융합 출력(Fusion Outputs)이 포함될 수 있다. 이후의 고장이 센싱(Sensing), 해석(Interpretation), 또는 후속 추론(Downstream Reasoning) 중 어디에서 발생했는지를 검증할 필요가 있을 때 원시 센서 데이터(Raw Sensor Data)를 선택적으로 보존할 수 있다.

인공지능 모델 추적성(AI Model Traceability)을 위해서는 각 의사결정에 관여한 모델을 명시적으로 식별해야 한다. 모델 이름, 버전, 가중치 또는 구성 식별자(Configuration Identifier), 캘리브레이션 상태(Calibration State), 추론 파라미터(Inference Parameters), 적응 이력(Adaptation History), 배포 패키지(Deployment Package)를 기록할 수 있다. 이러한 정보가 없으면 이후의 소프트웨어 또는 모델 업데이트가 상당히 다른 출력을 생성할 수 있기 때문에 동일한 입력 데이터를 사용하더라도 결과를 재현하기 어려울 수 있다.

월드 모델 로깅(World-Model Logging)은 예측과 함께 이후에 그 예측을 확인하거나 반박하는 실제 관측을 기록해야 한다. 예측 상태(Predicted States), 궤적, 점유 상태(Occupancy), 객체 움직임(Object Motion), 불확실성 범위(Uncertainty Ranges), 예측 범위(Prediction Horizons), 이후의 잔차 오류(Residual Errors)는 미래에 대한 내부 표현이 신뢰할 수 있었는지를 판단할 수 있는 증거를 제공한다. 이러한 이력은 예측 일관성 분석(Prediction-Consistency Analysis)과 모델 드리프트(Model Drift) 또는 익숙하지 않은 운용 조건의 식별을 지원한다.

계획 및 제어 추적(Planning and Control Traces)은 의도된 행동과 실제로 실행된 행동을 모두 보존해야 한다. 후보 궤적(Candidate Trajectories), 선택된 계획(Selected Plans), 최적화 비용(Optimization Costs), 제약조건, 속도 명령, 액추에이터 요청(Actuator Requests), 제어기 상태(Controller States), 측정된 응답(Measured Responses)을 통해 안전하지 않은 동작 시퀀스가 어디에서 시작되었는지를 확인할 수 있다. 계획된 명령과 실제 움직임의 차이를 분석하면 계획 오류를 액추에이터 고장, 통신 지연 또는 저수준 제어 문제(Low-Level Control Problems)와 구분할 수 있다.

안전 개입(Safety Interventions)은 런타임 보증이 자율 권한(Autonomous Authority)을 변경하거나 제한한 순간을 나타내므로 특히 상세한 로깅이 필요하다. 제약조건 위반(Constraint Violations), 이상 점수(Anomaly Scores), 분포 외 지표(OOD Indicators), 차폐 수정(Shield Modifications), 심플렉스 전환 이벤트(Simplex Switching Events), 폴백 활성화(Fallback Activation), 보호 정지(Protective Stops), 복구 결정(Recovery Decisions)을 이를 발생시킨 조건 및 임계값(Thresholds)과 함께 기록해야 한다.

자원 및 타이밍 증거(Resource and Timing Evidence) 역시 이벤트 재구성에 필수적이다. CPU와 GPU 사용률, 메모리 압박(Memory Pressure), 추론 지연시간(Inference Latency), 큐 깊이(Queue Depth), 네트워크 지연(Network Delay), 마감시간 초과(Missed Deadlines), 열 상태(Thermal Conditions), 워치독 이벤트(Watchdog Events), 프로세스 고장(Process Failures)은 알고리즘 오류처럼 보이는 행동의 실제 원인을 설명할 수 있다. 정확한 인식 또는 계획 결과라도 유효한 시간 범위(Useful Temporal Window)가 지난 이후 전달되면 위험해질 수 있다.

이벤트 트리거 로깅(Event-Triggered Logging)은 모든 고대역폭 데이터 스트림을 영구적으로 저장하지 않고도 가치가 높은 증거를 보존할 수 있다. 순환 버퍼(Rolling Buffer)는 최근 이력을 지속적으로 유지하다가 충돌 위험, 비상 정지, 이상(Anomaly), 안전 제어기 전환, 심각한 성능 저하가 발생하면 선택된 시간 구간을 고정하여 보존할 수 있다. 트리거 발생 전후의 시간을 함께 기록하면 인과관계 분석(Causal Analysis)과 복구 평가(Recovery Assessment)에 필요한 상황 정보를 확보할 수 있다.

이벤트 기록(Event Records)은 운영 상황(Operating Context)을 확인할 수 있을 만큼 충분한 메타데이터(Metadata)를 포함해야 한다. 로봇 식별 정보(Robot Identity), 하드웨어 구성, 소프트웨어 빌드(Software Build), 모델 버전, 임무 식별자(Mission Identifier), 자율 운용 모드(Autonomy Mode), 지도 버전(Map Version), 환경 조건, 페이로드 상태(Payload State), 운영자 개입(Operator Interventions), 유지보수 상태(Maintenance Status) 등이 해석에 영향을 줄 수 있다. 이러한 상황 정보는 겉보기에는 유사하지만 근본적으로 다른 운영 가정 아래에서 발생한 이벤트를 잘못 비교하는 것을 방지한다.

안전 증거(Safety Evidence)는 이벤트 이후에도 신뢰할 수 있어야 하므로 로그 무결성(Log Integrity)이 중요하다. 기록은 우발적인 변경, 손상(Corruption), 불완전한 쓰기(Incomplete Writes), 타임스탬프 모호성, 통제되지 않은 삭제로부터 보호되어야 한다. 체크섬(Checksums), 추가 기록 중심 저장 방식(Append-Oriented Storage), 접근 제어(Access Controls), 중복 이벤트 요약(Redundant Event Summaries), 인증된 기록(Authenticated Records)을 사용하면 사후 이벤트 분석이 실제 운용 중 생성된 데이터에 기반한다는 신뢰도를 높일 수 있다.

로깅은 고장 상황에서도 회복탄력성(Resilience)을 유지해야 한다. 시스템 충돌(System Crash), 전원 중단(Power Interruption), 네트워크 연결 해제, 저장장치 고장이 사고를 이해하는 데 필요한 증거를 자동으로 파괴해서는 안 된다. 중요한 이벤트 요약(Critical Event Summaries)은 보호된 로컬 저장장치(Protected Local Storage)에 기록하고, 중요도가 낮은 대용량 데이터는 이후에 전송할 수 있다. 따라서 안전 로깅(Safety Logging)은 정상적인 인프라를 사용할 수 없게 되더라도 점진적으로 기능을 축소하면서 핵심 증거를 보존해야 한다.

사후 이벤트 분석(Post-Event Analysis)은 동기화된 타임라인(Synchronized Timeline)을 재구성하는 것에서 시작한다. 조사자는 센서 관측, 상태 추정, 인공지능 출력(AI Outputs), 계획, 명령, 안전 모니터 결정(Safety-Monitor Decisions), 제어기 전환, 물리적 응답을 시간적으로 정렬할 수 있다. 이 타임라인은 각각의 중요한 순간에 시스템이 무엇을 알고 있었는지, 무엇을 예측했는지, 무엇을 결정했는지, 실제로 무엇이 실행되었는지, 그리고 환경이 어떻게 반응했는지를 보여준다.

인과 분석(Causal Analysis)은 최초 발생 조건(Initiating Condition)과 이후에 발생한 결과(Downstream Consequences)를 구분해야 한다. 예를 들어 위치추정 오류(Localization Error)가 잘못된 월드 모델 상태를 생성하고, 이것이 부적절한 궤적을 만들며, 결국 안전 차폐(Safety Shield)를 작동시킬 수 있다. 이 경우 차폐 개입을 근본 원인(Root Cause)으로 판단하면 실제 고장 연쇄(Failure Chain)를 놓치게 된다. 추적성을 활용하면 분석가는 가장 초기의 신뢰할 수 있는 발생 요인까지 의존관계를 역방향으로 추적할 수 있다.

반사실적 재생(Counterfactual Replay)은 사후 이벤트에 대한 이해를 강화할 수 있다. 기록된 입력을 다른 모델 버전, 계획기(Planner), 임계값 또는 안전 정책(Safety Policies)을 통해 다시 실행하여 다른 구성이 결과를 변화시켰을 가능성을 조사할 수 있다. 이러한 재생은 실제 물리적 세계에서 무엇이 발생했을지를 증명하지는 않지만 민감한 의사결정 지점(Sensitive Decision Points)을 식별하고 제안된 수정 사항에 대한 통제된 회귀 시험(Regression Testing)을 지원할 수 있다.

근접 사고(Near Misses)는 실제 고장과 함께 분석해야 한다. 유해한 결과가 발생하지 않더라도 중요한 안전 정보를 포함하기 때문이다. 작은 정지 여유(Stopping Margins), 반복적인 차폐 개입, 불안정한 재계획(Replanning), 일시적인 위치추정 손실, 안전 제어기 활성화는 아직 사고로 이어지지 않은 시스템 취약점을 보여줄 수 있다. 체계적인 근접 사고 분석(Near-Miss Analysis)은 실제 사고가 발생할 때까지 기다리는 대신 선제적인 시스템 개선(Proactive Improvement)을 지원한다.

플릿 규모 추적성(Fleet-Scale Traceability)을 사용하면 여러 로봇, 사이트, 임무, 소프트웨어 버전에 걸쳐 패턴을 식별할 수 있다. 여러 플랫폼에서 유사한 이상이 발생하면 공통적인 모델 취약점(Common Model Weaknesses)을 나타낼 수 있으며, 특정 로봇에서만 발생하는 이벤트는 로컬 하드웨어 또는 캘리브레이션 문제를 의미할 수 있다. 통합된 증거(Aggregated Evidence)는 개별적인 고장과 체계적인 문제(Systematic Issues)를 구분하고 발생 빈도와 심각도에 따라 엔지니어링 조치의 우선순위를 결정할 수 있도록 한다.

사후 이벤트 분석 결과(Post-Event Findings)는 물리 인공지능 수명주기(Physical AI Lifecycle)에 직접 피드백되어야 한다. 확인된 고장 패턴은 새로운 시뮬레이션 시나리오(Simulation Scenarios), 회귀 시험(Regression Tests), 데이터셋 사례(Dataset Examples), 안전 제약조건, 유지보수 규칙(Maintenance Rules), 모델 업데이트(Model Updates), 운영 제한(Operational Restrictions)을 생성할 수 있다. 각각의 수정 조치는 이를 유발한 증거와 연결되어야 하며, 이를 통해 런타임 이벤트에서 엔지니어링 변경(Engineering Change), 이후의 검증까지 이어지는 추적성을 형성할 수 있다.

로깅 정책(Logging Policies)은 진단 가치(Diagnostic Value)와 저장 공간, 대역폭, 개인정보 보호(Privacy), 보안(Security), 운영 제약조건 사이에서 균형을 유지해야 한다. 고대역폭 원시 데이터는 선택적 보존(Selective Retention), 압축(Compression), 이벤트 우선순위화(Event Prioritization), 통제된 접근(Controlled Access)이 필요할 수 있다. 목적은 최대한 많은 데이터를 축적하는 것이 아니라 배포 환경의 제약과 데이터 거버넌스(Data Governance) 요구사항을 준수하면서 안전 관련 의사결정을 설명할 수 있는 충분하고 신뢰할 수 있는 증거를 보존하는 것이다.

궁극적으로 로깅, 추적성 및 사후 이벤트 분석(Logging, Traceability, and Post-Event Analysis)은 런타임 보증(Runtime Assurance)의 기억(Memory)을 구축한다. 일시적으로 발생하는 센서 관측, 인공지능 의사결정, 안전 개입, 물리적 결과를 검사하고 재현하며 비교하고 개선할 수 있는 증거로 변환한다. 런타임 행동을 그 원인 및 이후의 수정 조치(Corrective Actions)와 연결함으로써 물리 인공지능 시스템은 전체 운영 수명주기(Operational Lifecycle)에 걸쳐 이상, 근접 사고, 성능 저하, 고장으로부터 체계적으로 학습하고 지속적으로 개선될 수 있다.

##  

## 07.16. Fleet Level Runtime Assurance

![](images/image17.png){width="7.268055555555556in" height="7.268055555555556in"}

Fleet-level runtime assurance extends safety monitoring from an individual Physical AI robot to a coordinated population of robots operating across shared environments, missions, infrastructure, and computational services. Each robot retains responsibility for immediate local safety, while fleet-level assurance aggregates operational evidence to identify hazards, degradation, anomalies, and systemic risks that may remain invisible from the perspective of a single platform.

The fundamental architecture separates local assurance from fleet assurance. Local runtime monitors supervise perception, localization, world-model predictions, trajectories, control, resources, and safety constraints with sufficiently low latency for immediate intervention. Fleet-level mechanisms operate above this layer, combining information from multiple robots without making local protective actions dependent on continuous communication with a centralized system.

Local safety authority must remain available when network connectivity is degraded or completely lost. Collision avoidance, safety-envelope enforcement, runtime shielding, emergency control, and protective stopping should therefore execute on the robot whenever possible. Fleet services may improve awareness and coordination, but communication delay, server failure, congestion, or infrastructure outages must not eliminate the robot\'s ability to enter a safe state independently.

Fleet assurance begins by collecting standardized health and safety indicators from participating robots. These can include perception confidence, localization residuals, world-model prediction errors, OOD scores, anomaly events, planning failures, shield interventions, controller switches, timing violations, resource pressure, communication quality, mission status, and maintenance indicators. Common semantics allow meaningful comparison across platforms and deployments.

Aggregation transforms isolated events into fleet-level patterns. A single localization anomaly may indicate a robot-specific issue, while similar anomalies reported by several robots in the same region may indicate a map error, environmental change, GNSS disturbance, or infrastructure problem. Fleet runtime assurance therefore evaluates both individual deviations and correlated behavior across robots, locations, missions, and time.

Spatial correlation is particularly valuable in shared operating environments. Repeated emergency braking, perception uncertainty, localization degradation, or trajectory replanning at the same location can identify hazardous zones that were not represented in the original map or safety analysis. Fleet intelligence can mark these regions, increase local caution, or distribute temporary operational restrictions to robots approaching the affected area.

Temporal correlation can reveal emerging conditions that develop across the fleet. Increasing inference latency after a software update, growing prediction errors during particular environmental conditions, or simultaneous communication instability may indicate a systematic issue. Comparing event timing with software deployments, configuration changes, weather, site operations, and infrastructure events helps distinguish coincidental failures from common-cause degradation.

Fleet-level anomaly detection can use peer behavior as a dynamic reference. Robots with comparable hardware, software, payload, tasks, and environments provide baselines for localization quality, energy consumption, tracking error, intervention frequency, and computational performance. A robot that deviates significantly from its peers may require inspection even when its measurements have not crossed absolute safety thresholds.

Shared world information can improve runtime assurance when handled conservatively. Robots may report temporary obstacles, blocked routes, slippery surfaces, construction areas, abnormal human activity, communication dead zones, or other operational hazards. Other robots can use this collective evidence to adjust planning and safety margins, but locally observed information should retain priority when shared information is stale, uncertain, or contradictory.

Fleet-level world-model consistency can reveal whether predictive failures are local or systematic. If one robot repeatedly mispredicts object motion while peers remain accurate, the problem may involve its sensors or model state. If many robots produce similar residual errors under the same conditions, the evidence may indicate a broader model-domain mismatch requiring fleet-wide mitigation, validation, or model improvement.

Runtime interventions themselves provide valuable collective evidence. Safety-filter corrections, Simplex controller transitions, fallback activations, minimum-risk maneuvers, and protective stops can be aggregated across the fleet. High intervention frequency associated with a particular location, task, model version, or operational condition can reveal hidden weaknesses even when no collision or explicit safety violation has occurred.

Fleet assurance must manage software and model versions explicitly. Different robots may operate with different perception models, world models, policies, calibration files, maps, or safety configurations during staged deployment. Runtime events should therefore remain linked to exact versions so that degradation can be associated with a specific update rather than incorrectly attributed to the entire fleet or environment.

Canary deployment provides an important mechanism for controlling fleet-wide risk. New models or software can first be deployed to a limited subset of robots operating under controlled conditions. Runtime assurance compares their performance, intervention frequency, anomalies, timing behavior, and safety margins against established fleet baselines. Wider deployment can proceed only when evidence supports acceptable behavior.

Fleet-level assurance should support rollback when a deployed update produces unacceptable behavior. If anomaly rates, prediction residuals, resource consumption, safety interventions, or mission failures increase significantly after deployment, the system can suspend further rollout and return affected robots to a previously validated configuration. Versioned software and reproducible configurations make such recovery practical.

Communication health becomes part of the assurance problem because collective intelligence depends on information exchange. The system should monitor latency, packet loss, bandwidth, synchronization, message freshness, connectivity, and server availability. Fleet-level decisions should account for communication uncertainty and avoid treating delayed or missing information as equivalent to confirmed knowledge about another robot or the environment.

Centralized fleet services can themselves become common points of failure. Runtime assurance should therefore monitor fleet servers, shared maps, databases, orchestration services, message brokers, and on-premise computational resources. Redundancy, health checks, failover mechanisms, protected resources, and graceful degradation can prevent a single infrastructure failure from simultaneously compromising many robots.

Safety-related fleet commands require clear authority and validation. A central system may distribute speed restrictions, exclusion zones, mission suspensions, model rollbacks, or hazard alerts, but robots should verify message authenticity, freshness, applicability, and consistency with local safety rules. Fleet coordination must not create a path through which erroneous centralized information directly overrides essential local protection.

Conflict resolution becomes important when local and fleet-level information disagree. A shared map may classify a corridor as clear while local perception detects an obstacle, or fleet services may recommend a route that local assurance considers unsafe. Safety architecture should generally favor the more conservative credible interpretation, ensuring that centralized optimization does not override immediate physical evidence available to the robot.

Fleet-level degradation management can coordinate responses according to the scope of the problem. A robot-specific fault may isolate one platform, while a site-level localization problem may restrict operations within a geographic region. A defective software release may require fleet-wide rollback. Determining whether degradation is local, regional, configuration-specific, or systemic allows mitigation to remain proportionate to the evidence.

Logging and traceability provide the historical foundation for fleet assurance. Events should retain robot identity, timestamps, location context, mission state, hardware configuration, model versions, safety interventions, environmental conditions, and relevant health indicators. Cross-fleet timelines allow investigators to reconstruct how an issue propagated and whether multiple events originated from a common condition or independent failures.

Fleet-level post-event analysis converts distributed runtime evidence into engineering knowledge. Correlated anomalies, near misses, controller transitions, communication failures, and performance degradation can generate new test scenarios, dataset examples, map corrections, maintenance actions, operational restrictions, and safety requirements. Lessons learned from one robot can therefore improve protection for many other robots before they encounter the same condition.

Fleet-level runtime assurance ultimately creates a distributed safety intelligence in which local autonomy and collective knowledge reinforce each other. Individual robots retain immediate authority to protect themselves and nearby people, while fleet mechanisms identify patterns that no single robot can observe. By combining local independence, shared evidence, correlation, version control, coordinated mitigation, and lifecycle feedback, the fleet becomes progressively safer through accumulated operational experience.

플릿 수준 런타임 보증(Fleet-Level Runtime Assurance)은 개별 물리 인공지능(Physical AI) 로봇의 안전 모니터링을 공유 환경, 임무, 인프라 및 연산 서비스에서 협력하여 운용되는 로봇 집단 전체로 확장한다. 각 로봇은 즉각적인 로컬 안전(Local Safety)에 대한 책임을 유지하는 동시에, 플릿 수준 보증(Fleet-Level Assurance)은 운영 증거를 통합하여 단일 플랫폼의 관점에서는 발견하기 어려운 위험, 성능 저하, 이상 및 시스템적 위험(Systemic Risks)을 식별한다.

기본 아키텍처는 로컬 보증(Local Assurance)과 플릿 보증(Fleet Assurance)을 분리한다. 로컬 런타임 모니터(Local Runtime Monitors)는 즉각적인 개입에 충분히 낮은 지연시간으로 인식(Perception), 위치추정(Localization), 월드 모델 예측(World-Model Predictions), 궤적(Trajectories), 제어(Control), 자원(Resources), 안전 제약조건(Safety Constraints)을 감독한다. 플릿 수준 메커니즘은 이 계층의 상위에서 동작하며, 로컬 보호 행동이 중앙 시스템과의 지속적인 통신에 의존하지 않도록 하면서 여러 로봇의 정보를 통합한다.

네트워크 연결이 저하되거나 완전히 끊어진 경우에도 로컬 안전 권한(Local Safety Authority)은 유지되어야 한다. 따라서 충돌 회피(Collision Avoidance), 안전 영역 강제(Safety-Envelope Enforcement), 런타임 차폐(Runtime Shielding), 비상 제어(Emergency Control), 보호 정지(Protective Stopping)는 가능한 한 로봇 자체에서 실행되어야 한다. 플릿 서비스(Fleet Services)는 상황 인식과 협업을 향상시킬 수 있지만 통신 지연, 서버 고장, 네트워크 혼잡 또는 인프라 장애가 로봇의 독립적인 안전 상태 진입 능력을 제거해서는 안 된다.

플릿 보증(Fleet Assurance)은 참여 로봇들로부터 표준화된 건전성 및 안전 지표(Standardized Health and Safety Indicators)를 수집하는 것에서 시작한다. 여기에는 인식 신뢰도(Perception Confidence), 위치추정 잔차(Localization Residuals), 월드 모델 예측 오류(World-Model Prediction Errors), 분포 외 점수(OOD Scores), 이상 이벤트(Anomaly Events), 계획 실패(Planning Failures), 차폐 개입(Shield Interventions), 제어기 전환(Controller Switches), 타이밍 위반(Timing Violations), 자원 압박(Resource Pressure), 통신 품질, 임무 상태, 유지보수 지표 등이 포함될 수 있다. 공통 의미 체계(Common Semantics)는 서로 다른 플랫폼과 배포 환경 간의 의미 있는 비교를 가능하게 한다.

집계(Aggregation)는 개별적인 이벤트를 플릿 수준 패턴(Fleet-Level Patterns)으로 변환한다. 하나의 위치추정 이상(Localization Anomaly)은 특정 로봇의 문제를 의미할 수 있지만 동일한 지역에서 여러 로봇이 유사한 이상을 보고한다면 지도 오류(Map Error), 환경 변화, 위성항법시스템 교란(GNSS Disturbance) 또는 인프라 문제를 의미할 수 있다. 따라서 플릿 런타임 보증은 개별 편차와 함께 로봇, 위치, 임무 및 시간에 걸쳐 나타나는 상관된 행동(Correlated Behavior)을 평가한다.

공유 운영 환경에서는 공간적 상관관계(Spatial Correlation)가 특히 중요하다. 동일한 위치에서 반복적인 비상 제동(Emergency Braking), 인식 불확실성(Perception Uncertainty), 위치추정 성능 저하, 궤적 재계획(Trajectory Replanning)이 발생하면 기존 지도나 안전 분석에 반영되지 않았던 위험 구역(Hazardous Zones)을 식별할 수 있다. 플릿 지능(Fleet Intelligence)은 이러한 영역을 표시하고 로컬 주의 수준을 높이거나 해당 지역에 접근하는 로봇들에게 임시 운영 제한(Temporary Operational Restrictions)을 배포할 수 있다.

시간적 상관관계(Temporal Correlation)는 플릿 전체에서 점진적으로 발생하는 새로운 조건을 발견할 수 있다. 소프트웨어 업데이트 이후 증가하는 추론 지연시간(Inference Latency), 특정 환경 조건에서 증가하는 예측 오류 또는 동시에 발생하는 통신 불안정은 시스템적 문제(Systematic Issue)를 나타낼 수 있다. 이벤트 발생 시점을 소프트웨어 배포, 구성 변경(Configuration Changes), 날씨, 사이트 운영, 인프라 이벤트와 비교하면 우연히 동시에 발생한 고장과 공통 원인 성능 저하(Common-Cause Degradation)를 구분할 수 있다.

플릿 수준 이상 탐지(Fleet-Level Anomaly Detection)는 다른 로봇의 행동을 동적 기준(Dynamic Reference)으로 사용할 수 있다. 유사한 하드웨어, 소프트웨어, 페이로드(Payload), 작업 및 환경을 가진 로봇들은 위치추정 품질, 에너지 소비, 추종 오차(Tracking Error), 개입 빈도, 연산 성능에 대한 기준선(Baselines)을 제공한다. 특정 로봇이 절대적인 안전 임계값을 넘지 않았더라도 동료 로봇(Peers)과 상당한 차이를 보인다면 점검이 필요할 수 있다.

공유 월드 정보(Shared World Information)는 보수적으로 처리할 경우 런타임 보증을 향상시킬 수 있다. 로봇은 임시 장애물, 차단된 경로, 미끄러운 노면, 공사 구역, 비정상적인 인간 활동, 통신 음영 지역(Communication Dead Zones) 또는 기타 운영 위험을 보고할 수 있다. 다른 로봇은 이러한 집단적 증거(Collective Evidence)를 활용하여 계획과 안전 여유(Safety Margins)를 조정할 수 있지만 공유 정보가 오래되었거나 불확실하거나 상충할 경우 로컬에서 직접 관측한 정보가 우선되어야 한다.

플릿 수준 월드 모델 일관성(Fleet-Level World-Model Consistency)을 분석하면 예측 실패가 로컬 문제인지 시스템적 문제인지를 파악할 수 있다. 하나의 로봇에서 객체 움직임 예측 오류가 반복되지만 다른 로봇들은 정확하다면 해당 로봇의 센서 또는 모델 상태가 원인일 수 있다. 반대로 여러 로봇이 동일한 조건에서 유사한 잔차 오류(Residual Errors)를 생성한다면 플릿 전체의 완화, 검증 또는 모델 개선이 필요한 광범위한 모델-도메인 불일치(Model-Domain Mismatch)를 의미할 수 있다.

런타임 개입(Runtime Interventions) 자체도 중요한 집단적 증거가 된다. 안전 필터 수정(Safety-Filter Corrections), 심플렉스 제어기 전환(Simplex Controller Transitions), 폴백 활성화(Fallback Activations), 최소 위험 기동(Minimum-Risk Maneuvers), 보호 정지 등을 플릿 전체에서 통합할 수 있다. 특정 위치, 작업, 모델 버전 또는 운영 조건에서 높은 개입 빈도가 발생한다면 충돌이나 명시적인 안전 위반이 발생하지 않았더라도 숨겨진 취약점을 발견할 수 있다.

플릿 보증은 소프트웨어 및 모델 버전(Software and Model Versions)을 명시적으로 관리해야 한다. 단계적 배포(Staged Deployment) 과정에서는 서로 다른 로봇이 서로 다른 인식 모델, 월드 모델, 정책(Policies), 캘리브레이션 파일, 지도 또는 안전 구성을 사용할 수 있다. 따라서 런타임 이벤트는 정확한 버전 정보와 연결되어야 하며, 이를 통해 성능 저하가 전체 플릿이나 환경의 문제로 잘못 판단되지 않고 특정 업데이트와 연관되어 있는지를 확인할 수 있다.

카나리 배포(Canary Deployment)는 플릿 전체의 위험을 통제하기 위한 중요한 메커니즘을 제공한다. 새로운 모델이나 소프트웨어를 먼저 통제된 조건에서 운용되는 제한된 수의 로봇에 배포할 수 있다. 런타임 보증은 이들의 성능, 개입 빈도, 이상, 타이밍 동작(Timing Behavior), 안전 여유를 기존 플릿 기준선과 비교한다. 충분한 증거가 허용 가능한 동작을 뒷받침하는 경우에만 더 넓은 범위로 배포를 확대할 수 있다.

배포된 업데이트가 허용할 수 없는 동작을 발생시키는 경우 플릿 수준 보증은 롤백(Rollback)을 지원해야 한다. 배포 이후 이상 발생률, 예측 잔차, 자원 소비(Resource Consumption), 안전 개입 또는 임무 실패가 크게 증가한다면 추가 배포를 중단하고 영향을 받은 로봇을 이전에 검증된 구성(Previously Validated Configuration)으로 복귀시킬 수 있다. 버전 관리된 소프트웨어와 재현 가능한 구성(Reproducible Configurations)은 이러한 복구를 실용적으로 만든다.

집단 지능(Collective Intelligence)은 정보 교환에 의존하기 때문에 통신 건전성(Communication Health) 자체가 보증 문제의 일부가 된다. 시스템은 지연시간, 패킷 손실(Packet Loss), 대역폭, 동기화(Synchronization), 메시지 최신성(Message Freshness), 연결 상태, 서버 가용성(Server Availability)을 모니터링해야 한다. 플릿 수준 의사결정은 통신 불확실성을 고려해야 하며, 지연되거나 누락된 정보를 다른 로봇 또는 환경에 대한 확인된 지식과 동일하게 취급해서는 안 된다.

중앙 집중형 플릿 서비스(Centralized Fleet Services)는 그 자체로 공통 고장 지점(Common Points of Failure)이 될 수 있다. 따라서 런타임 보증은 플릿 서버(Fleet Servers), 공유 지도(Shared Maps), 데이터베이스, 오케스트레이션 서비스(Orchestration Services), 메시지 브로커(Message Brokers), 온프레미스 연산 자원(On-Premise Computational Resources)을 모니터링해야 한다. 이중화(Redundancy), 건전성 검사(Health Checks), 장애 조치 메커니즘(Failover Mechanisms), 보호된 자원, 점진적 성능 저하(Graceful Degradation)를 통해 하나의 인프라 고장이 여러 로봇의 안전을 동시에 손상시키는 것을 방지할 수 있다.

안전 관련 플릿 명령(Safety-Related Fleet Commands)은 명확한 권한과 검증을 필요로 한다. 중앙 시스템은 속도 제한, 제외 구역(Exclusion Zones), 임무 중단(Mission Suspensions), 모델 롤백, 위험 경고(Hazard Alerts)를 배포할 수 있지만 로봇은 메시지의 인증성(Authenticity), 최신성(Freshness), 적용 가능성(Applicability), 로컬 안전 규칙과의 일관성을 검증해야 한다. 플릿 협업(Fleet Coordination)이 잘못된 중앙 정보가 필수적인 로컬 보호 기능을 직접 무시할 수 있는 경로를 만들어서는 안 된다.

로컬 정보와 플릿 수준 정보가 서로 일치하지 않을 경우 충돌 해결(Conflict Resolution)이 중요해진다. 공유 지도는 통로가 비어 있다고 판단하지만 로컬 인식이 장애물을 탐지할 수 있으며, 플릿 서비스가 추천한 경로를 로컬 보증이 위험하다고 판단할 수도 있다. 안전 아키텍처는 일반적으로 신뢰할 수 있는 정보 중 더 보수적인 해석(Conservative Interpretation)을 우선하여 중앙 집중형 최적화(Centralized Optimization)가 로봇이 직접 확보한 즉각적인 물리적 증거를 무시하지 못하도록 해야 한다.

플릿 수준 성능 저하 관리(Fleet-Level Degradation Management)는 문제의 범위에 따라 대응을 조정할 수 있다. 특정 로봇의 고장은 하나의 플랫폼만 격리(Isolation)하면 될 수 있지만 사이트 수준의 위치추정 문제는 특정 지리적 영역의 운용을 제한해야 할 수 있다. 결함이 있는 소프트웨어 릴리스는 플릿 전체 롤백을 요구할 수 있다. 성능 저하가 로컬(Local), 지역적(Regional), 구성 특화(Configuration-Specific), 시스템적(Systemic) 문제인지를 판단하면 증거에 비례하는 완화 조치(Mitigation)를 수행할 수 있다.

로깅 및 추적성(Logging and Traceability)은 플릿 보증의 역사적 기반을 제공한다. 이벤트에는 로봇 식별 정보(Robot Identity), 타임스탬프(Timestamps), 위치 상황(Location Context), 임무 상태, 하드웨어 구성, 모델 버전, 안전 개입, 환경 조건, 관련 건전성 지표가 유지되어야 한다. 플릿 전체의 타임라인(Cross-Fleet Timelines)을 통해 조사자는 문제가 어떻게 전파되었는지와 여러 이벤트가 하나의 공통 조건에서 발생했는지 또는 서로 독립적인 고장에서 발생했는지를 재구성할 수 있다.

플릿 수준 사후 이벤트 분석(Fleet-Level Post-Event Analysis)은 분산된 런타임 증거(Distributed Runtime Evidence)를 엔지니어링 지식(Engineering Knowledge)으로 변환한다. 상관된 이상, 근접 사고(Near Misses), 제어기 전환, 통신 고장, 성능 저하는 새로운 시험 시나리오(Test Scenarios), 데이터셋 사례(Dataset Examples), 지도 수정(Map Corrections), 유지보수 조치(Maintenance Actions), 운영 제한, 안전 요구사항(Safety Requirements)을 생성할 수 있다. 따라서 하나의 로봇에서 얻은 교훈을 다른 로봇들이 동일한 상황을 경험하기 전에 플릿 전체의 보호 수준 향상에 활용할 수 있다.

궁극적으로 플릿 수준 런타임 보증(Fleet-Level Runtime Assurance)은 로컬 자율성(Local Autonomy)과 집단적 지식(Collective Knowledge)이 서로를 강화하는 분산 안전 지능(Distributed Safety Intelligence)을 구축한다. 개별 로봇은 자신과 주변 사람들을 보호하기 위한 즉각적인 권한을 유지하며, 플릿 수준 메커니즘은 하나의 로봇만으로는 관찰할 수 없는 패턴을 식별한다. 로컬 독립성(Local Independence), 공유 증거(Shared Evidence), 상관관계 분석(Correlation), 버전 관리(Version Control), 협력적 완화(Coordinated Mitigation), 수명주기 피드백(Lifecycle Feedback)을 결합함으로써 플릿은 축적된 운영 경험(Accumulated Operational Experience)을 통해 지속적으로 더 안전한 시스템으로 발전할 수 있다.

##  

## 07.17. Runtime Safety Monitor [w/Code]

![](images/image18.png){width="7.268055555555556in" height="7.268055555555556in"}

A runtime safety monitor continuously evaluates whether a Physical AI system remains within conditions that permit safe autonomous operation. It observes the robot, environment, autonomy stack, and computational platform while decisions are being executed. Rather than controlling the mission directly, the monitor provides independent evidence about whether current and predicted behavior remains compatible with defined safety requirements.

The monitor operates as a supervisory layer surrounding the primary autonomy functions. Perception, localization, world modeling, planning, learned policies, and control may pursue mission performance, while the safety monitor evaluates their outputs against explicit operational constraints. This architectural separation prevents safety from depending entirely on the same algorithms that generate autonomous behavior.

Runtime monitoring begins with the estimated physical state of the robot. Position, orientation, velocity, acceleration, actuator state, payload condition, energy level, and stability indicators provide evidence about whether the platform remains dynamically controllable. State uncertainty must accompany these estimates because apparently safe values may become unacceptable when their confidence intervals approach critical boundaries.

Environmental monitoring determines whether surrounding conditions remain compatible with safe operation. Obstacles, people, vehicles, terrain, restricted zones, visibility, surface conditions, weather, infrastructure, and dynamic objects may alter the available safety margin. The monitor should evaluate not only detected hazards but also whether perception quality is sufficient to justify continued autonomous movement.

Perception health is therefore a major input to runtime safety monitoring. Sensor availability, data freshness, confidence, cross-sensor consistency, calibration status, detection stability, and OOD indicators can reveal when environmental understanding is becoming unreliable. A robot should not interpret the absence of detected hazards as evidence of safety when the sensing system itself is degraded or uncertain.

Localization health determines whether the robot knows its own state accurately enough to execute planned actions. Pose uncertainty, map alignment, odometry consistency, GNSS quality, loop-closure behavior, and disagreement among localization sources can be monitored continuously. When localization confidence deteriorates, safety margins may need to expand even if the planned trajectory itself has not changed.

World-model predictions provide another monitoring channel by estimating how the environment and robot state are expected to evolve. The safety monitor can compare predicted occupancy, object motion, interaction outcomes, and future robot states with subsequent observations. Increasing prediction residuals or inconsistent futures can indicate model mismatch and reduce confidence in planning based on those predictions.

Planning supervision evaluates whether proposed trajectories remain inside the operational safety envelope. Collision risk, stopping distance, dynamic feasibility, stability, restricted areas, human separation, uncertainty margins, and recovery options can be checked before execution. A trajectory may satisfy immediate geometric constraints while still leading toward a state from which safe recovery would become difficult or impossible.

Action and control monitoring extends supervision to commands approaching physical execution. Velocity, steering, force, torque, acceleration, manipulator motion, and actuator requests can be checked against platform limits and contextual safety constraints. Runtime filters may reject or modify commands that violate these conditions, preventing unsafe outputs from reaching the physical system even when upstream planning fails.

The safety monitor should reason about trajectories rather than isolated states whenever possible. A robot may currently occupy a safe state while moving toward a hazard with insufficient braking distance. Short-horizon prediction, reachable sets, control barrier functions, or verified transition rules can estimate whether continued execution preserves recoverability and whether intervention must begin before an explicit boundary is crossed.

Recoverability provides an important criterion for determining when autonomous authority should be reduced. The monitor evaluates whether a trusted safety controller can still return the system to a safe condition from the current state. If the remaining recovery margin becomes too small, intervention should occur before the system reaches a state in which braking, avoidance, stabilization, or retreat can no longer guarantee acceptable safety.

Uncertainty should directly influence the monitor\'s decisions. High confidence can permit operation closer to validated limits, while uncertain perception, localization, prediction, or environmental state should produce more conservative behavior. Safety envelopes can expand, allowable speed can decrease, and permitted maneuver complexity can be reduced as uncertainty grows, preserving margin against errors that cannot be resolved immediately.

System resources and timing must also be monitored because autonomous safety depends on computations arriving when they are needed. CPU and GPU load, memory pressure, inference latency, scheduling deadlines, queue depth, communication delay, thermal throttling, watchdog status, and process health can reveal whether critical autonomy functions are becoming temporally unreliable even when their algorithms remain logically correct.

The runtime safety monitor should integrate evidence rather than treating every signal independently. Moderate localization uncertainty, increased perception latency, and rising prediction error may together represent a serious condition even when none individually exceeds its threshold. Cross-layer reasoning allows combinations of weak indicators to reveal degradation that isolated threshold checks could miss.

Monitoring logic can use multiple severity levels rather than a single binary safe-or-unsafe decision. Normal operation may transition to increased observation, cautious operation, degraded autonomy, safety-controller authority, minimum-risk maneuver, and protective stopping as evidence becomes more severe. Graded responses preserve useful functionality while ensuring that autonomous authority decreases as confidence in safe operation declines.

Runtime shielding provides an immediate enforcement mechanism for conditions identified by the safety monitor. When a proposed action lies outside the safe action set, a shield may modify velocity, steering, force, trajectory, or other commands before execution. Small deviations can therefore be corrected without transferring complete control away from the advanced autonomy system.

More severe conditions may require a Simplex-style controller transition. The safety monitor can serve as an input to the decision module that determines when the advanced controller must relinquish authority to a trusted safety controller. Such switching should occur while sufficient recovery margin remains, rather than waiting until the primary controller has already violated a critical safety constraint.

Fallback behavior should correspond to the nature and severity of the detected condition. The system may reduce speed, increase separation, replan, disable uncertain capabilities, retreat, request human assistance, hold position, or execute a protective stop. The selected response should prioritize maintaining a stable and recoverable physical condition rather than maximizing mission completion.

Recovery to normal autonomy requires evidence that the triggering condition has genuinely cleared. Sensor health, localization confidence, prediction consistency, resource availability, environmental conditions, and safety margins should remain stable for an appropriate period before authority is restored. Hysteresis and persistence rules prevent rapid oscillation between normal and degraded operating states.

Independence is essential for a safety monitor intended to supervise complex AI. It should avoid relying exclusively on the same models, software paths, assumptions, and computational resources used by the functions it monitors. Deterministic checks, simplified models, independent sensors, protected execution partitions, or separate processors can reduce common-cause failures and strengthen assurance.

The monitor itself must satisfy timing and reliability requirements. Safety evaluation must complete before the physical system passes the point at which intervention remains effective. Bounded execution latency, prioritized scheduling, watchdog supervision, protected memory, and fail-safe behavior are therefore part of the monitor architecture, not merely implementation details.

Every significant monitoring event should be logged with sufficient context for later reconstruction. State estimates, uncertainty, sensor health, model versions, predictions, proposed actions, active constraints, monitor decisions, interventions, controller authority, and physical outcomes provide a traceable record. These records support root-cause analysis, validation, threshold refinement, and lifecycle improvement.

At fleet scale, runtime safety monitors remain locally authoritative while sharing selected health and safety evidence with fleet or on-premise systems. Correlated anomalies, repeated interventions, common prediction errors, and location-specific hazards can reveal patterns invisible to one robot. Collective analysis can improve future operation without making immediate local safety dependent on centralized connectivity.

The runtime safety monitor ultimately functions as the continuously active guardian of autonomous physical behavior. It connects sensing, state estimation, prediction, planning, control, computational health, uncertainty, and recovery into one supervisory safety process. By detecting shrinking safety margins early and progressively restricting authority, it helps ensure that Physical AI remains controllable, recoverable, and bounded by verified safety conditions throughout operation.

런타임 안전 모니터(Runtime Safety Monitor)는 물리 인공지능(Physical AI) 시스템이 안전한 자율 운용을 허용하는 조건 내에 계속 머물러 있는지를 지속적으로 평가한다. 로봇, 환경, 자율 시스템 스택(Autonomy Stack), 연산 플랫폼(Computational Platform)을 의사결정이 실행되는 동안 관찰한다. 임무를 직접 제어하기보다는 현재 및 예측된 행동이 정의된 안전 요구사항(Safety Requirements)에 부합하는지에 대한 독립적인 증거를 제공한다.

모니터는 주요 자율 기능(Primary Autonomy Functions)을 둘러싸는 감독 계층(Supervisory Layer)으로 동작한다. 인식(Perception), 위치추정(Localization), 월드 모델링(World Modeling), 계획(Planning), 학습 정책(Learned Policies), 제어(Control)는 임무 성능을 추구할 수 있으며, 안전 모니터는 이들의 출력을 명시적인 운영 제약조건(Operational Constraints)에 따라 평가한다. 이러한 아키텍처적 분리는 안전성이 자율 행동을 생성하는 동일한 알고리즘에 전적으로 의존하는 것을 방지한다.

런타임 모니터링(Runtime Monitoring)은 로봇의 추정된 물리 상태(Estimated Physical State)에서 시작한다. 위치, 자세(Orientation), 속도, 가속도, 액추에이터 상태(Actuator State), 페이로드 상태(Payload Condition), 에너지 수준, 안정성 지표(Stability Indicators)는 플랫폼이 동적으로 제어 가능한 상태를 유지하는지에 대한 증거를 제공한다. 겉보기에는 안전한 값이라도 신뢰 구간(Confidence Intervals)이 중요한 경계에 접근하면 허용할 수 없게 될 수 있으므로 상태 불확실성(State Uncertainty)을 이러한 추정값과 함께 고려해야 한다.

환경 모니터링(Environmental Monitoring)은 주변 조건이 안전한 운용과 계속 양립할 수 있는지를 판단한다. 장애물, 사람, 차량, 지형, 제한 구역(Restricted Zones), 가시성(Visibility), 노면 상태(Surface Conditions), 날씨, 인프라, 동적 객체(Dynamic Objects)는 사용 가능한 안전 여유(Safety Margin)를 변화시킬 수 있다. 모니터는 탐지된 위험뿐만 아니라 지속적인 자율 이동을 정당화할 만큼 인식 품질(Perception Quality)이 충분한지도 평가해야 한다.

따라서 인식 건전성(Perception Health)은 런타임 안전 모니터링의 주요 입력이다. 센서 가용성(Sensor Availability), 데이터 최신성(Data Freshness), 신뢰도(Confidence), 센서 간 일관성(Cross-Sensor Consistency), 캘리브레이션 상태(Calibration Status), 탐지 안정성(Detection Stability), 분포 외 지표(OOD Indicators)를 통해 환경에 대한 이해가 신뢰성을 잃고 있는지를 파악할 수 있다. 센싱 시스템 자체가 성능 저하 또는 불확실한 상태라면 로봇은 위험이 탐지되지 않았다는 사실을 안전하다는 증거로 해석해서는 안 된다.

위치추정 건전성(Localization Health)은 로봇이 계획된 행동을 실행할 만큼 자신의 상태를 정확하게 알고 있는지를 결정한다. 자세 불확실성(Pose Uncertainty), 지도 정렬(Map Alignment), 오도메트리 일관성(Odometry Consistency), 위성항법시스템 품질(GNSS Quality), 루프 폐쇄 동작(Loop-Closure Behavior), 위치추정 정보원 간 불일치 등을 지속적으로 모니터링할 수 있다. 위치추정 신뢰도가 저하되면 계획된 궤적 자체가 변경되지 않았더라도 안전 여유를 확대해야 할 수 있다.

월드 모델 예측(World-Model Predictions)은 환경과 로봇 상태가 어떻게 변화할 것으로 예상되는지를 추정함으로써 또 다른 모니터링 채널을 제공한다. 안전 모니터는 예측된 점유 상태(Occupancy), 객체 움직임(Object Motion), 상호작용 결과(Interaction Outcomes), 미래 로봇 상태를 이후의 실제 관측과 비교할 수 있다. 예측 잔차(Prediction Residuals)가 증가하거나 미래 예측의 일관성이 떨어지면 모델 불일치(Model Mismatch)를 나타낼 수 있으며, 이러한 예측을 기반으로 수행되는 계획에 대한 신뢰도를 낮춰야 한다.

계획 감독(Planning Supervision)은 제안된 궤적이 운영 안전 영역(Operational Safety Envelope) 내부에 유지되는지를 평가한다. 충돌 위험(Collision Risk), 정지 거리(Stopping Distance), 동적 실행 가능성(Dynamic Feasibility), 안정성(Stability), 제한 구역, 인간 이격 거리(Human Separation), 불확실성 여유(Uncertainty Margins), 복구 옵션(Recovery Options)을 실행 전에 확인할 수 있다. 하나의 궤적이 즉각적인 기하학적 제약조건을 만족하더라도 안전한 복구가 어렵거나 불가능해지는 상태로 시스템을 유도할 수 있다.

행동 및 제어 모니터링(Action and Control Monitoring)은 물리적 실행에 가까운 명령까지 감독 범위를 확장한다. 속도, 조향(Steering), 힘, 토크(Torque), 가속도, 매니퓰레이터 움직임(Manipulator Motion), 액추에이터 요청을 플랫폼 한계와 상황별 안전 제약조건(Contextual Safety Constraints)에 따라 검사할 수 있다. 런타임 필터(Runtime Filters)는 이러한 조건을 위반하는 명령을 거부하거나 수정하여 상위 계획 계층에서 문제가 발생하더라도 안전하지 않은 출력이 실제 물리 시스템에 전달되는 것을 방지할 수 있다.

가능하다면 안전 모니터는 고립된 상태(Isolated States)가 아니라 궤적(Trajectories)을 기반으로 판단해야 한다. 로봇이 현재 안전한 상태에 있더라도 충분한 제동 거리를 확보하지 못한 채 위험 요소를 향해 이동하고 있을 수 있다. 단기 예측(Short-Horizon Prediction), 도달 가능 집합(Reachable Sets), 제어 장벽 함수(Control Barrier Functions), 검증된 전이 규칙(Verified Transition Rules)을 이용하여 지속적인 실행이 복구 가능성(Recoverability)을 유지하는지와 명시적인 경계를 넘기 전에 개입을 시작해야 하는지를 판단할 수 있다.

복구 가능성(Recoverability)은 자율 권한(Autonomous Authority)을 언제 축소해야 하는지를 결정하는 중요한 기준을 제공한다. 모니터는 신뢰할 수 있는 안전 제어기(Trusted Safety Controller)가 현재 상태에서 시스템을 다시 안전한 상태로 복귀시킬 수 있는지를 평가한다. 남아 있는 복구 여유(Recovery Margin)가 지나치게 작아지면 시스템이 제동, 회피, 안정화 또는 후퇴를 통해 허용 가능한 안전성을 더 이상 보장할 수 없는 상태에 도달하기 전에 개입해야 한다.

불확실성(Uncertainty)은 모니터의 의사결정에 직접적인 영향을 주어야 한다. 높은 신뢰도는 검증된 한계에 보다 가까운 운용을 허용할 수 있지만, 인식, 위치추정, 예측 또는 환경 상태가 불확실할수록 더욱 보수적인 행동이 필요하다. 불확실성이 증가하면 안전 영역(Safety Envelopes)을 확대하고, 허용 속도를 낮추며, 허용되는 기동 복잡성(Maneuver Complexity)을 제한함으로써 즉시 해결할 수 없는 오류에 대한 안전 여유를 유지할 수 있다.

자율 시스템의 안전은 필요한 시점에 연산 결과가 제공되는 것에 의존하므로 시스템 자원 및 타이밍(System Resources and Timing)도 모니터링해야 한다. CPU 및 GPU 부하, 메모리 압박(Memory Pressure), 추론 지연시간(Inference Latency), 스케줄링 마감시간(Scheduling Deadlines), 큐 깊이(Queue Depth), 통신 지연, 열 스로틀링(Thermal Throttling), 워치독 상태(Watchdog Status), 프로세스 건전성(Process Health)을 통해 알고리즘 자체가 논리적으로 정확하더라도 중요한 자율 기능이 시간적으로 신뢰할 수 없는 상태가 되고 있는지를 파악할 수 있다.

런타임 안전 모니터는 각각의 신호를 독립적으로 처리하는 대신 여러 증거를 통합하여 판단해야 한다. 중간 수준의 위치추정 불확실성, 증가한 인식 지연시간, 상승하는 예측 오류가 함께 나타난다면 각각이 개별 임계값을 초과하지 않더라도 심각한 상태를 의미할 수 있다. 계층 간 추론(Cross-Layer Reasoning)은 개별 임계값 검사만으로는 놓칠 수 있는 성능 저하를 여러 약한 지표의 조합을 통해 탐지할 수 있도록 한다.

모니터링 로직(Monitoring Logic)은 하나의 이진적인 안전 또는 위험 판단(Binary Safe-or-Unsafe Decision) 대신 여러 단계의 심각도 수준(Severity Levels)을 사용할 수 있다. 증거가 심각해짐에 따라 정상 운용(Normal Operation)에서 강화된 관찰(Increased Observation), 주의 운용(Cautious Operation), 성능 저하 자율 운용(Degraded Autonomy), 안전 제어기 권한(Safety-Controller Authority), 최소 위험 기동(Minimum-Risk Maneuver), 보호 정지(Protective Stopping)로 전환할 수 있다. 이러한 단계적 대응은 안전 운용에 대한 신뢰도가 낮아질수록 자율 권한을 축소하면서 유용한 기능을 최대한 유지한다.

런타임 차폐(Runtime Shielding)는 안전 모니터가 식별한 조건을 즉시 강제할 수 있는 메커니즘을 제공한다. 제안된 행동이 안전 행동 집합(Safe Action Set)을 벗어나면 차폐 시스템(Shield)은 실행 전에 속도, 조향, 힘, 궤적 또는 기타 명령을 수정할 수 있다. 따라서 작은 편차는 고급 자율 시스템(Advanced Autonomy System)으로부터 전체 제어 권한을 이전하지 않고도 수정할 수 있다.

더 심각한 조건에서는 심플렉스 방식의 제어기 전환(Simplex-Style Controller Transition)이 필요할 수 있다. 안전 모니터는 고급 제어기(Advanced Controller)가 신뢰할 수 있는 안전 제어기에게 언제 권한을 넘겨야 하는지를 판단하는 결정 모듈(Decision Module)의 입력으로 사용될 수 있다. 이러한 전환은 주 제어기가 이미 중요한 안전 제약조건을 위반할 때까지 기다리는 것이 아니라 충분한 복구 여유가 남아 있는 동안 이루어져야 한다.

폴백 동작(Fallback Behavior)은 탐지된 조건의 특성과 심각도에 대응해야 한다. 시스템은 속도를 낮추고, 이격 거리를 확대하고, 재계획(Replanning)을 수행하고, 불확실한 기능을 비활성화하거나, 후퇴하거나, 인간의 지원(Human Assistance)을 요청하거나, 위치를 유지하거나, 보호 정지를 실행할 수 있다. 선택된 대응은 임무 완료를 극대화하기보다 안정적이고 복구 가능한 물리적 상태(Recoverable Physical Condition)를 유지하는 것을 우선해야 한다.

정상 자율 운용(Normal Autonomy)으로 복귀하려면 개입을 유발했던 조건이 실제로 해소되었다는 증거가 필요하다. 센서 건전성, 위치추정 신뢰도, 예측 일관성(Prediction Consistency), 자원 가용성(Resource Availability), 환경 조건, 안전 여유가 적절한 시간 동안 안정적으로 유지된 이후에 권한을 복원해야 한다. 히스테리시스(Hysteresis)와 지속성 규칙(Persistence Rules)은 정상 상태와 성능 저하 운용 상태 사이의 빠른 반복 전환을 방지한다.

복잡한 인공지능을 감독하도록 설계된 안전 모니터에서는 독립성(Independence)이 필수적이다. 모니터가 감독 대상 기능과 동일한 모델, 소프트웨어 경로(Software Paths), 가정, 연산 자원에만 의존해서는 안 된다. 결정론적 검사(Deterministic Checks), 단순화된 모델(Simplified Models), 독립 센서(Independent Sensors), 보호된 실행 파티션(Protected Execution Partitions), 별도의 프로세서(Separate Processors)를 활용하면 공통 원인 고장(Common-Cause Failures)을 줄이고 보증 수준을 강화할 수 있다.

모니터 자체도 타이밍 및 신뢰성 요구사항(Timing and Reliability Requirements)을 충족해야 한다. 안전 평가는 물리 시스템이 효과적인 개입이 가능한 지점을 지나기 전에 완료되어야 한다. 따라서 제한된 실행 지연시간(Bounded Execution Latency), 우선순위 스케줄링(Prioritized Scheduling), 워치독 감독(Watchdog Supervision), 보호된 메모리(Protected Memory), 고장 안전 동작(Fail-Safe Behavior)은 단순한 구현 세부사항이 아니라 모니터 아키텍처 자체의 구성요소이다.

모든 중요한 모니터링 이벤트(Monitoring Events)는 이후에 상황을 재구성할 수 있도록 충분한 맥락 정보와 함께 기록되어야 한다. 상태 추정, 불확실성, 센서 건전성, 모델 버전(Model Versions), 예측, 제안된 행동(Proposed Actions), 활성 제약조건(Active Constraints), 모니터의 판단, 개입, 제어기 권한, 물리적 결과를 기록하면 추적 가능한 이력(Traceable Record)을 구축할 수 있다. 이러한 기록은 근본 원인 분석(Root-Cause Analysis), 검증(Validation), 임계값 개선(Threshold Refinement), 수명주기 개선(Lifecycle Improvement)을 지원한다.

플릿 규모(Fleet Scale)에서 런타임 안전 모니터는 로컬 제어 권한(Local Authority)을 유지하면서 선택된 건전성 및 안전 증거를 플릿 또는 온프레미스 시스템(On-Premise Systems)과 공유한다. 상관된 이상(Correlated Anomalies), 반복적인 개입, 공통적인 예측 오류, 특정 위치의 위험(Location-Specific Hazards)을 분석하면 하나의 로봇만으로는 발견할 수 없는 패턴을 식별할 수 있다. 집단 분석(Collective Analysis)은 즉각적인 로컬 안전을 중앙 연결에 의존시키지 않으면서 향후 운용을 개선할 수 있다.

궁극적으로 런타임 안전 모니터(Runtime Safety Monitor)는 자율적인 물리적 행동을 지속적으로 보호하는 감시자(Guardian)의 역할을 수행한다. 센싱(Sensing), 상태 추정(State Estimation), 예측(Prediction), 계획, 제어, 연산 건전성(Computational Health), 불확실성, 복구(Recovery)를 하나의 감독 안전 프로세스(Supervisory Safety Process)로 연결한다. 감소하는 안전 여유를 조기에 탐지하고 자율 권한을 단계적으로 제한함으로써 물리 인공지능이 전체 운용 과정에서 제어 가능(Controllable)하고, 복구 가능(Recoverable)하며, 검증된 안전 조건(Verified Safety Conditions)의 경계 내에 유지되도록 지원한다.
