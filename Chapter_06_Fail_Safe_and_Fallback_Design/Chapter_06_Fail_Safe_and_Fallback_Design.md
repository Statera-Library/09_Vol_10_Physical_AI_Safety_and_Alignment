**Volume 10. Physical AI Safety and Alignment**


# Chapter 06. Fail Safe and Fallback Design

##  

## 06.01. Fail Safe Fail Operational and Fault Tolerant Design

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Physical AI systems operate in environments where computational failures can immediately become physical hazards. A perception error, processor fault, communication loss, actuator malfunction, or corrupted AI inference may affect motion before a human can intervene. Fail-safe, fail-operational, and fault-tolerant design therefore provide complementary strategies for controlling how a robot behaves when parts of the system no longer operate as intended.

Fail-safe design assumes that certain failures should cause the system to transition toward a predefined condition in which unacceptable risk is minimized. For a mobile robot, this may involve controlled deceleration and stopping, while a manipulator may halt motion, maintain a safe pose, release energy where appropriate, or prevent further actuator commands. The objective is not continued productivity but predictable containment of hazardous behavior.

A fail-safe response must consider that stopping is not universally safe. An autonomous vehicle stopping in an active traffic lane, a mobile manipulator freezing while carrying an unstable load, or an aerial robot immediately disabling propulsion may create greater hazards than temporary continued operation. Physical AI therefore requires context-dependent safe states that account for motion, stored energy, payload, surrounding humans, terrain, traffic, and environmental conditions.

Fail-operational design addresses situations in which some functionality must remain available after a failure. Instead of immediately terminating operation, the system preserves enough sensing, computation, communication, or control capability to complete a safety-critical maneuver. An autonomous robot may lose its primary localization method yet continue using an independent source long enough to reduce speed, leave a hazardous area, reach a designated location, or achieve a minimum risk condition.

The amount of fail-operational capability required depends on the consequences of losing functionality and the time needed to reach safety. A warehouse AMR may often stop safely within a short distance, whereas a road vehicle, aerial robot, heavy mobile platform, or robot interacting closely with people may require continued steering, braking, stabilization, perception, or state estimation. Safety analysis must therefore identify which functions must survive particular faults and for how long.

Fault tolerance is the broader ability of a system to continue providing an acceptable service despite faults. It combines mechanisms such as redundancy, fault detection, isolation, reconfiguration, graceful degradation, and recovery. Rather than treating every component failure as a complete system failure, fault-tolerant architecture determines which capabilities remain trustworthy and restructures operation around the surviving resources while preserving defined safety constraints.

Redundancy is an important mechanism, but simply duplicating components does not guarantee fault tolerance. Two identical sensors, processors, or AI models may fail simultaneously because they share power, software defects, environmental exposure, training data, or assumptions. Effective designs examine common-cause and correlated failures and may introduce diversity through different sensing modalities, algorithms, compute channels, power paths, communication links, or independently developed safety mechanisms.

Physical AI introduces additional challenges because learned components do not fail only through conventional hardware or software faults. An AI model may remain computationally healthy while producing unsafe predictions because of distribution shift, unfamiliar objects, ambiguous scenes, sensor degradation, or excessive confidence. Fault-tolerant design must therefore monitor both component health and behavioral validity, including uncertainty, consistency, operational boundaries, and violations of physical safety constraints.

A useful architecture separates high-performance autonomy from independently enforceable safety functions. The primary AI system may perform perception, prediction, reasoning, planning, and adaptive control, while a simpler safety layer observes critical states and constrains dangerous actions. If the AI becomes unavailable or untrustworthy, authority can migrate toward deterministic fallback control, restricted motion, reduced speed, emergency stabilization, or another independently validated control path.

The transition between normal and fallback operation is itself safety-critical. Abruptly switching controllers can introduce discontinuities in velocity, steering, torque, trajectory, or actuator commands. A robust design defines explicit transition conditions, synchronization rules, state transfer, command arbitration, and hysteresis so that temporary anomalies do not cause unstable switching. The fallback controller must also receive enough reliable state information to assume control safely.

Graceful degradation provides an intermediate strategy between unrestricted operation and complete shutdown. When sensing quality, computational capacity, localization accuracy, communication reliability, or actuator capability deteriorates, the robot progressively restricts its operating envelope. It may reduce velocity, increase obstacle clearance, prohibit complex manipulation, shorten planning horizons, avoid uncertain regions, disable autonomous functions, or request human assistance while retaining essential safety functions.

Fault containment prevents a local problem from propagating across the architecture. Compute partitions, communication boundaries, independent watchdogs, protected power domains, command validation, and safety-rated control paths can isolate failures before they corrupt unrelated functions. This principle is especially important when foundation models, VLA policies, world models, fleet services, and conventional robot controllers coexist within the same Physical AI system.

Temporal behavior must also be included in the fault model. A function can produce logically correct results but still become unsafe when computation exceeds its deadline, sensor information becomes stale, communication latency grows, or synchronization is lost. Watchdogs and freshness checks therefore monitor not only whether information exists but whether it remains valid for the current physical state and whether the system still has sufficient time to react safely.

Recovery should be distinguished from immediate fault containment. After entering a safe or degraded condition, the system may diagnose the fault, restart components, switch resources, recalibrate sensors, rebuild localization, or replan its mission. Automatic recovery should occur only when the system can establish that required safety assumptions have been restored. Otherwise, the robot should remain restricted, request supervision, or terminate the mission rather than repeatedly re-entering unsafe operation.

Fail-safe, fail-operational, and fault-tolerant strategies ultimately form a coordinated hierarchy rather than competing design choices. Fail-safe behavior defines how risk is contained when continued operation cannot be justified, fail-operational behavior preserves essential functions long enough to reach safety, and fault tolerance enables acceptable service despite selected failures. Their combination creates a structured path from normal autonomy through degradation, fallback, minimum-risk behavior, and controlled recovery.

For Physical AI, the central design question is therefore not simply whether the robot can survive a component failure, but whether it can preserve control over physical risk while its internal assumptions are being invalidated. A robust system detects loss of trust, limits authority, maintains essential capabilities, and moves toward increasingly conservative behavior. This layered philosophy provides the foundation for the fault detection, safe-state, degraded-mode, fallback, and recovery mechanisms developed throughout the remainder of the chapter.

물리 인공지능(Physical AI) 시스템은 계산상의 고장(computational failure)이 즉각적인 물리적 위험(physical hazard)으로 이어질 수 있는 환경에서 작동한다. 인지 오류(perception error), 프로세서 고장(processor fault), 통신 손실(communication loss), 액추에이터 오작동(actuator malfunction), 손상된 AI 추론(corrupted AI inference)은 사람이 개입하기 전에 로봇의 움직임에 영향을 줄 수 있다. 따라서 고장 안전(fail-safe), 고장 시 운용 지속(fail-operational), 결함 허용 설계(fault-tolerant design)는 시스템 일부가 의도대로 작동하지 않을 때 로봇의 행동을 제어하기 위한 상호 보완적인 전략을 제공한다.

고장 안전 설계(fail-safe design)는 특정 고장이 발생하면 시스템이 허용할 수 없는 위험(unacceptable risk)을 최소화할 수 있는 사전에 정의된 상태(predefined condition)로 전환되어야 한다고 가정한다. 이동 로봇(mobile robot)의 경우 제어된 감속과 정지가 포함될 수 있으며, 매니퓰레이터(manipulator)는 움직임을 중단하거나 안전한 자세를 유지하고, 필요한 경우 에너지를 해제하거나 추가적인 액추에이터 명령을 차단할 수 있다. 목적은 생산성을 계속 유지하는 것이 아니라 위험한 행동을 예측 가능한 방식으로 억제하는 것이다.

고장 안전 대응(fail-safe response)을 설계할 때는 정지가 항상 안전한 것은 아니라는 점을 고려해야 한다. 자율주행차(autonomous vehicle)가 운행 중인 차선에서 정지하거나, 이동형 매니퓰레이터(mobile manipulator)가 불안정한 화물을 운반하는 도중 멈추거나, 비행 로봇(aerial robot)이 즉시 추진력을 차단한다면 오히려 더 큰 위험이 발생할 수 있다. 따라서 물리 인공지능(Physical AI)에는 움직임, 저장 에너지(stored energy), 적재물(payload), 주변 사람, 지형, 교통 및 환경 조건을 고려하는 상황 의존적 안전 상태(context-dependent safe state)가 필요하다.

고장 시 운용 지속 설계(fail-operational design)는 고장이 발생한 이후에도 일부 기능을 유지해야 하는 상황을 다룬다. 시스템은 즉시 작동을 종료하는 대신 안전에 중요한 기동(safety-critical maneuver)을 완료할 수 있을 정도의 센싱(sensing), 계산(computation), 통신(communication), 제어(control) 능력을 유지한다. 자율 로봇은 주 위치추정(primary localization) 방법을 상실하더라도 독립적인 위치 정보원을 이용하여 속도를 줄이고 위험 지역에서 벗어나거나 지정된 위치에 도달하고 최소 위험 상태(minimum risk condition)를 달성할 때까지 운용을 계속할 수 있다.

필요한 고장 시 운용 지속 능력(fail-operational capability)의 수준은 기능 상실에 따른 결과와 안전 상태에 도달하는 데 필요한 시간에 따라 달라진다. 창고 자율이동로봇(AMR)은 비교적 짧은 거리에서 안전하게 정지할 수 있지만, 도로 차량, 비행 로봇, 중량 이동 플랫폼(heavy mobile platform), 사람과 밀접하게 상호작용하는 로봇은 조향, 제동, 안정화, 인지 또는 상태 추정(state estimation)을 계속 유지해야 할 수 있다. 따라서 안전 분석(safety analysis)은 특정 고장 이후 어떤 기능이 얼마 동안 유지되어야 하는지를 식별해야 한다.

결함 허용(fault tolerance)은 고장이 존재하더라도 시스템이 허용 가능한 서비스를 계속 제공할 수 있는 보다 포괄적인 능력이다. 여기에는 중복성(redundancy), 결함 탐지(fault detection), 격리(isolation), 재구성(reconfiguration), 점진적 성능 저하(graceful degradation), 복구(recovery) 등의 메커니즘이 결합된다. 모든 구성요소의 고장을 전체 시스템의 고장으로 간주하는 대신, 결함 허용 아키텍처(fault-tolerant architecture)는 어떤 기능이 여전히 신뢰 가능한지를 판단하고 정의된 안전 제약조건(safety constraints)을 유지하면서 생존한 자원을 중심으로 운용을 재구성한다.

중복성(redundancy)은 중요한 메커니즘이지만 구성요소를 단순히 복제하는 것만으로 결함 허용성을 보장할 수는 없다. 동일한 두 개의 센서, 프로세서 또는 AI 모델은 전원, 소프트웨어 결함, 환경적 노출, 학습 데이터 또는 기본 가정을 공유하기 때문에 동시에 실패할 수 있다. 효과적인 설계에서는 공통 원인 고장(common-cause failure)과 상관 고장(correlated failure)을 분석하고 서로 다른 센싱 방식, 알고리즘, 계산 채널, 전원 경로, 통신 링크 또는 독립적으로 개발된 안전 메커니즘을 이용하여 다양성(diversity)을 확보할 수 있다.

물리 인공지능(Physical AI)은 학습 기반 구성요소(learned component)가 기존의 하드웨어나 소프트웨어 고장만으로 실패하는 것이 아니기 때문에 추가적인 문제를 발생시킨다. AI 모델은 계산상 정상적으로 작동하면서도 분포 변화(distribution shift), 익숙하지 않은 객체, 모호한 장면, 센서 성능 저하 또는 과도한 확신 때문에 위험한 예측을 생성할 수 있다. 따라서 결함 허용 설계는 구성요소 상태(component health)뿐만 아니라 불확실성(uncertainty), 일관성(consistency), 운용 경계(operational boundary), 물리적 안전 제약 위반 등을 포함한 행동의 유효성(behavioral validity)까지 감시해야 한다.

유용한 아키텍처는 고성능 자율성(high-performance autonomy)과 독립적으로 강제할 수 있는 안전 기능(safety function)을 분리한다. 주 AI 시스템(primary AI system)은 인지, 예측, 추론, 계획 및 적응형 제어(adaptive control)를 수행하고, 보다 단순한 안전 계층(safety layer)은 핵심 상태를 감시하면서 위험한 행동을 제한한다. AI가 사용 불가능하거나 신뢰할 수 없는 상태가 되면 제어 권한은 결정론적 폴백 제어(deterministic fallback control), 제한된 움직임, 감속 운행, 비상 안정화(emergency stabilization) 또는 독립적으로 검증된 다른 제어 경로로 이전될 수 있다.

정상 운용(normal operation)과 폴백 운용(fallback operation) 사이의 전환 자체도 안전에 매우 중요하다. 제어기를 갑작스럽게 전환하면 속도, 조향, 토크, 궤적 또는 액추에이터 명령에 불연속성(discontinuity)이 발생할 수 있다. 견고한 설계는 명시적인 전환 조건(transition condition), 동기화 규칙(synchronization rule), 상태 전달(state transfer), 명령 중재(command arbitration), 히스테리시스(hysteresis)를 정의하여 일시적인 이상 현상이 불안정한 전환을 유발하지 않도록 한다. 또한 폴백 제어기(fallback controller)는 안전하게 제어를 인수할 수 있도록 충분히 신뢰할 수 있는 상태 정보를 제공받아야 한다.

점진적 성능 저하(graceful degradation)는 제한 없는 정상 운용과 완전한 시스템 종료 사이의 중간 전략을 제공한다. 센싱 품질, 계산 능력, 위치추정 정확도, 통신 신뢰성 또는 액추에이터 성능이 저하되면 로봇은 운용 범위(operating envelope)를 점진적으로 제한한다. 속도를 낮추고, 장애물과의 안전거리를 확대하며, 복잡한 조작을 금지하고, 계획 범위(planning horizon)를 단축하거나 불확실한 영역을 회피하고, 자율 기능을 비활성화하거나 필수적인 안전 기능을 유지하면서 사람의 지원을 요청할 수 있다.

결함 격리(fault containment)는 국부적인 문제가 전체 아키텍처로 확산되는 것을 방지한다. 계산 파티션(compute partition), 통신 경계(communication boundary), 독립적인 감시 장치(watchdog), 보호된 전원 영역(protected power domain), 명령 검증(command validation), 안전 등급 제어 경로(safety-rated control path)는 고장이 관련되지 않은 다른 기능을 손상시키기 전에 이를 격리할 수 있다. 이러한 원칙은 파운데이션 모델(foundation model), 비전-언어-행동 정책(VLA policy), 월드 모델(world model), 플릿 서비스(fleet service), 기존 로봇 제어기(conventional robot controller)가 동일한 물리 인공지능 시스템에서 공존할 때 특히 중요하다.

시간적 동작(temporal behavior) 역시 결함 모델(fault model)에 포함되어야 한다. 어떤 기능이 논리적으로 올바른 결과를 생성하더라도 계산 시간이 마감시간(deadline)을 초과하거나 센서 정보가 오래되어 유효성을 잃고, 통신 지연이 증가하거나 동기화가 손실되면 안전하지 않을 수 있다. 따라서 감시 장치(watchdog)와 정보 최신성 검사(freshness check)는 정보의 존재 여부뿐만 아니라 현재의 물리적 상태에서 해당 정보가 여전히 유효한지, 그리고 시스템이 안전하게 반응할 충분한 시간을 확보하고 있는지를 감시한다.

복구(recovery)는 즉각적인 결함 억제(fault containment)와 구분되어야 한다. 안전 상태 또는 성능 저하 상태(degraded condition)에 진입한 이후 시스템은 결함을 진단하고, 구성요소를 재시작하며, 자원을 전환하고, 센서를 재보정하거나 위치추정을 재구축하고 임무를 다시 계획할 수 있다. 자동 복구(automatic recovery)는 필요한 안전 가정(safety assumption)이 복원되었다는 사실을 시스템이 확인할 수 있을 때만 수행되어야 한다. 그렇지 않다면 위험한 운용으로 반복적으로 복귀하기보다 제한된 상태를 유지하거나 감독을 요청하고 임무를 종료해야 한다.

고장 안전(fail-safe), 고장 시 운용 지속(fail-operational), 결함 허용(fault-tolerant) 전략은 서로 경쟁하는 설계 방식이 아니라 궁극적으로 하나의 조정된 계층 구조(coordinated hierarchy)를 형성한다. 고장 안전은 지속적인 운용을 정당화할 수 없을 때 위험을 억제하는 방법을 정의하고, 고장 시 운용 지속은 안전에 도달할 때까지 필수 기능을 유지하며, 결함 허용은 선택된 고장에도 불구하고 허용 가능한 서비스를 제공한다. 이들의 결합은 정상 자율 운용에서 성능 저하, 폴백, 최소 위험 행동(minimum-risk behavior), 제어된 복구(controlled recovery)로 이어지는 체계적인 경로를 형성한다.

따라서 물리 인공지능(Physical AI)에서 핵심적인 설계 질문은 단순히 로봇이 구성요소 고장을 견딜 수 있는가가 아니라, 내부 가정이 더 이상 유효하지 않게 되는 과정에서도 물리적 위험에 대한 통제력을 유지할 수 있는가이다. 견고한 시스템은 신뢰 상실(loss of trust)을 탐지하고, 제어 권한을 제한하며, 필수 기능을 유지하면서 점차 보수적인 행동(conservative behavior)으로 전환한다. 이러한 계층적 철학(layered philosophy)은 이후 장에서 다루는 결함 탐지, 안전 상태, 성능 저하 모드, 폴백 및 복구 메커니즘의 기반을 제공한다.

##  

## 06.02. Fault Detection Isolation and Recovery

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Fault Detection, Isolation, and Recovery (FDIR) provides the mechanisms that allow a Physical AI system to recognize abnormal conditions, determine where they originate, and respond before they develop into hazardous physical behavior. Unlike conventional monitoring that mainly reports component status, FDIR connects diagnosis directly to safety decisions, degraded operation, fallback control, and restoration of trustworthy autonomy.

Fault detection determines whether observed system behavior remains consistent with expected operating conditions. Detection mechanisms may examine sensor signals, actuator responses, localization estimates, communication status, computational timing, power conditions, and AI outputs. The objective is to identify meaningful deviations early enough that the robot still has sufficient control authority and physical margin to execute a safe response.

Detection can rely on explicit thresholds, consistency rules, watchdogs, analytical models, redundant measurements, or learned anomaly detectors. Simple limits remain valuable because they are predictable and independently verifiable, while model-based approaches can recognize complex relationships among system variables. Physical AI architectures often combine several methods so that no single diagnostic assumption becomes the only defense against unsafe behavior.

Temporal information is particularly important because many faults emerge gradually rather than appearing as immediate failures. Sensor drift, increasing inference latency, battery degradation, thermal throttling, localization divergence, or deteriorating communication quality may initially remain within nominal limits. Trend monitoring and persistence checks help distinguish developing faults from harmless transient disturbances and provide additional time for controlled degradation.

Fault isolation follows detection by identifying the component, subsystem, interface, or functional chain most likely responsible for the abnormal behavior. Isolation prevents the system from unnecessarily disabling healthy capabilities and supports selection of an appropriate fallback strategy. For example, determining whether navigation inconsistency originates from a camera, LiDAR, localization algorithm, map mismatch, or timing problem can lead to very different recovery actions.

Isolation frequently depends on relationships between multiple observations. If wheel odometry, inertial sensing, and visual localization disagree, cross-checking their residuals may indicate which estimate has become unreliable. Similarly, commanded actuator motion can be compared with measured motion, power consumption, and encoder feedback. Diagnostic reasoning therefore converts distributed evidence into hypotheses about the location and nature of a fault.

Physical AI requires fault isolation beyond conventional hardware diagnosis because failures can occur at semantic and behavioral levels. A perception network may continue producing outputs while systematically missing an unfamiliar obstacle class, or a world model may generate physically inconsistent predictions despite normal computation. Isolation must therefore distinguish hardware faults, data corruption, model uncertainty, distribution shift, planning errors, and violations of operational assumptions.

Confidence alone is insufficient for detecting or isolating AI failures because learned models can be confidently wrong. More robust diagnosis combines uncertainty estimates with sensor agreement, temporal consistency, physical constraints, trajectory feasibility, operational design boundaries, and independent safety observations. When evidence conflicts, the system should reduce trust in the affected function rather than assuming that a numerically confident AI output is correct.

Fault identification may additionally characterize severity, persistence, and recoverability. A brief packet loss may require no more than temporary buffering, whereas persistent communication loss may trigger autonomous fallback. A slightly degraded sensor may permit reduced-speed operation, while complete loss of safety-critical perception may require stopping. Diagnostic results therefore need to represent operational consequences rather than merely assigning binary healthy or failed labels.

Recovery begins once the fault has been sufficiently characterized and the system has entered an acceptable operating condition. Recovery actions may include resetting software, restarting an AI inference process, switching sensors, selecting a redundant compute channel, recalibrating state estimation, rebuilding localization, rerouting communication, reducing workload, or reconfiguring control. The selected action must preserve safety throughout the transition rather than focusing only on restoring functionality.

Not every detected fault should trigger immediate automatic recovery. Repeated restart cycles, unstable controller switching, or rapid transitions between primary and backup components can create new hazards. Recovery logic therefore benefits from persistence criteria, retry limits, hysteresis, cooldown intervals, and explicit escalation policies. If recovery repeatedly fails, the system should progressively move toward a more conservative degraded mode or mission termination.

Recovery must also distinguish between restoring a component and restoring confidence in the system. A restarted perception process may execute normally but still receive corrupted sensor data, while recovered localization may remain inconsistent with the physical environment. Before returning authority to a recovered function, the system should verify output plausibility, timing, cross-sensor consistency, safety constraints, and other assumptions required for trustworthy operation.

Reconfiguration provides continuity when direct repair is impossible. A failed camera may be excluded while remaining sensors support restricted perception, a lost localization source may be replaced by another estimator, or a failed AI planner may transfer authority to a simpler classical controller. Such reconfiguration enables graceful degradation by matching the robot\'s permitted behavior to the capabilities that remain demonstrably available.

FDIR architecture should preserve independence between the function being diagnosed and the mechanisms responsible for critical safety decisions. If the same AI model both generates behavior and determines whether that behavior is safe, a common failure may compromise both roles. Independent watchdogs, safety processors, redundant sensing paths, protected communication channels, and deterministic constraint checks can provide stronger diagnostic and containment boundaries.

The effectiveness of FDIR depends heavily on observability and diagnostic coverage designed into the system from the beginning. Components should expose meaningful health information, timestamps, confidence indicators, error states, resource utilization, and relevant internal measurements. Logging should preserve the sequence from fault onset through detection, isolation, fallback, and recovery so that field incidents can be reconstructed and diagnostic mechanisms can be improved.

In a complete Physical AI safety architecture, FDIR forms the decision bridge between runtime monitoring and fallback behavior. Detection establishes that trust has been reduced, isolation determines which capability should no longer be relied upon, and recovery attempts to restore or reconfigure that capability under controlled conditions. When recovery cannot be justified, the same diagnostic information guides degraded operation, minimum-risk behavior, human intervention, or mission abort.

결함 탐지, 격리 및 복구(Fault Detection, Isolation, and Recovery, FDIR)는 물리 인공지능(Physical AI) 시스템이 비정상 상태(abnormal condition)를 인식하고, 그 발생 위치와 원인을 판단하며, 위험한 물리적 행동으로 발전하기 전에 대응할 수 있도록 하는 메커니즘을 제공한다. 단순히 구성요소 상태를 보고하는 기존 모니터링과 달리, FDIR은 진단(diagnosis)을 안전 의사결정, 성능 저하 운용(degraded operation), 폴백 제어(fallback control), 신뢰 가능한 자율성(trustworthy autonomy)의 복원과 직접 연결한다.

결함 탐지(fault detection)는 관측된 시스템 행동이 예상된 운용 조건(expected operating condition)과 일치하는지를 판단한다. 탐지 메커니즘은 센서 신호, 액추에이터 응답, 위치추정 결과, 통신 상태, 계산 타이밍, 전력 상태 및 AI 출력을 검사할 수 있다. 목적은 로봇이 안전한 대응을 실행할 수 있는 충분한 제어 권한(control authority)과 물리적 여유(physical margin)를 보유하고 있을 때 의미 있는 이상을 조기에 식별하는 것이다.

탐지는 명시적 임계값(explicit threshold), 일관성 규칙(consistency rule), 감시 장치(watchdog), 분석 모델(analytical model), 중복 측정(redundant measurement), 학습 기반 이상 탐지기(learned anomaly detector)를 활용할 수 있다. 단순한 한계값은 예측 가능하고 독립적으로 검증할 수 있기 때문에 여전히 중요하며, 모델 기반 접근법은 시스템 변수 사이의 복잡한 관계를 인식할 수 있다. 물리 인공지능 아키텍처는 일반적으로 여러 방법을 결합하여 하나의 진단 가정이 위험 행동을 방지하는 유일한 방어 수단이 되지 않도록 한다.

많은 결함은 즉각적인 고장으로 나타나기보다 점진적으로 발생하기 때문에 시간적 정보(temporal information)가 특히 중요하다. 센서 드리프트(sensor drift), 증가하는 추론 지연(inference latency), 배터리 성능 저하, 열 스로틀링(thermal throttling), 위치추정 발산(localization divergence), 통신 품질 저하는 초기에는 정상 범위 안에 머무를 수 있다. 추세 모니터링(trend monitoring)과 지속성 검사(persistence check)는 진행 중인 결함과 일시적인 무해한 교란을 구분하고 제어된 성능 저하를 수행할 추가 시간을 제공한다.

결함 격리(fault isolation)는 탐지 이후 비정상 행동의 원인일 가능성이 가장 높은 구성요소, 서브시스템, 인터페이스 또는 기능 체인(functional chain)을 식별하는 과정이다. 격리는 시스템이 정상적인 기능까지 불필요하게 비활성화하는 것을 방지하고 적절한 폴백 전략(fallback strategy)을 선택하도록 지원한다. 예를 들어 내비게이션 불일치가 카메라, 라이다(LiDAR), 위치추정 알고리즘, 지도 불일치 또는 타이밍 문제 중 어디에서 발생했는지를 판단하면 서로 다른 복구 조치를 선택할 수 있다.

결함 격리는 여러 관측값 사이의 관계를 활용하는 경우가 많다. 휠 오도메트리(wheel odometry), 관성 센싱(inertial sensing), 시각 위치추정(visual localization)이 서로 일치하지 않는다면 잔차(residual)를 교차 검증하여 어떤 추정값의 신뢰성이 저하되었는지 판단할 수 있다. 마찬가지로 명령된 액추에이터 움직임을 실제 측정 움직임, 전력 소비 및 엔코더 피드백(encoder feedback)과 비교할 수 있다. 따라서 진단 추론(diagnostic reasoning)은 분산된 증거를 결함의 위치와 특성에 대한 가설로 변환한다.

물리 인공지능은 의미론적 수준(semantic level)과 행동 수준(behavioral level)에서도 고장이 발생할 수 있기 때문에 기존 하드웨어 진단을 넘어서는 결함 격리가 필요하다. 인지 네트워크(perception network)는 계속 출력을 생성하면서도 익숙하지 않은 장애물 종류를 지속적으로 놓칠 수 있으며, 월드 모델(world model)은 계산 자체가 정상임에도 물리적으로 일관되지 않은 예측을 생성할 수 있다. 따라서 격리는 하드웨어 결함, 데이터 손상, 모델 불확실성(model uncertainty), 분포 변화(distribution shift), 계획 오류 및 운용 가정 위반을 구분해야 한다.

학습된 모델은 높은 확신을 가지면서도 잘못된 결과를 생성할 수 있기 때문에 신뢰도(confidence)만으로 AI 결함을 탐지하거나 격리하기에는 충분하지 않다. 보다 견고한 진단은 불확실성 추정(uncertainty estimation)을 센서 간 일치성, 시간적 일관성, 물리적 제약조건, 궤적 실행 가능성(trajectory feasibility), 운용 설계 경계(operational design boundary), 독립적인 안전 관측과 결합한다. 증거가 서로 충돌하면 수치적으로 높은 확신을 가진 AI 출력을 정확하다고 가정하기보다 해당 기능에 대한 신뢰도를 낮춰야 한다.

결함 식별(fault identification)은 추가적으로 심각도(severity), 지속성(persistence), 복구 가능성(recoverability)을 특성화할 수 있다. 짧은 패킷 손실(packet loss)은 일시적인 버퍼링만 필요할 수 있지만 지속적인 통신 손실은 자율 폴백(autonomous fallback)을 유발할 수 있다. 약간 성능이 저하된 센서는 감속 운용을 허용할 수 있지만 안전 필수 인지(safety-critical perception)가 완전히 상실되면 정지가 필요할 수 있다. 따라서 진단 결과는 단순한 정상 또는 고장이라는 이진 상태가 아니라 운용상의 결과를 표현해야 한다.

복구(recovery)는 결함이 충분히 특성화되고 시스템이 허용 가능한 운용 상태에 진입한 이후 시작된다. 복구 조치에는 소프트웨어 초기화, AI 추론 프로세스 재시작, 센서 전환, 중복 계산 채널(redundant compute channel) 선택, 상태 추정 재보정, 위치추정 재구축, 통신 경로 변경, 작업 부하 감소 또는 제어 재구성(control reconfiguration)이 포함될 수 있다. 선택된 조치는 단순히 기능을 복원하는 데 집중하는 것이 아니라 전환 과정 전체에서 안전을 유지해야 한다.

탐지된 모든 결함이 즉각적인 자동 복구(automatic recovery)를 유발해서는 안 된다. 반복적인 재시작 주기, 불안정한 제어기 전환 또는 주 구성요소와 백업 구성요소 사이의 빠른 전환은 새로운 위험을 만들 수 있다. 따라서 복구 로직(recovery logic)에는 지속성 기준, 재시도 제한, 히스테리시스(hysteresis), 대기 간격(cooldown interval), 명시적 단계 상승 정책(escalation policy)을 적용하는 것이 효과적이다. 복구가 반복적으로 실패하면 시스템은 점진적으로 더욱 보수적인 성능 저하 모드 또는 임무 종료 상태로 전환해야 한다.

복구는 구성요소를 다시 작동시키는 것과 시스템에 대한 신뢰를 복원하는 것을 구분해야 한다. 재시작된 인지 프로세스가 정상적으로 실행되더라도 손상된 센서 데이터를 계속 입력받을 수 있으며, 복구된 위치추정 역시 실제 물리적 환경과 불일치할 수 있다. 복구된 기능에 다시 제어 권한을 부여하기 전에 시스템은 출력 타당성(output plausibility), 타이밍, 센서 간 일관성, 안전 제약조건 및 신뢰 가능한 운용에 필요한 기타 가정이 충족되는지를 검증해야 한다.

직접적인 수리가 불가능한 경우 재구성(reconfiguration)은 운용의 연속성을 제공한다. 고장 난 카메라를 제외하고 남아 있는 센서를 이용하여 제한된 인지를 수행하거나, 손실된 위치추정 정보원을 다른 추정기(estimator)로 대체하거나, 고장 난 AI 플래너(AI planner)의 제어 권한을 보다 단순한 고전적 제어기(classical controller)로 이전할 수 있다. 이러한 재구성은 검증된 상태로 남아 있는 기능에 로봇의 허용 행동을 맞춤으로써 점진적 성능 저하(graceful degradation)를 가능하게 한다.

FDIR 아키텍처는 진단 대상 기능과 핵심적인 안전 의사결정을 담당하는 메커니즘 사이의 독립성(independence)을 유지해야 한다. 동일한 AI 모델이 행동을 생성하면서 동시에 그 행동의 안전 여부까지 판단한다면 공통 고장(common failure)이 두 역할을 모두 손상시킬 수 있다. 독립적인 감시 장치, 안전 프로세서(safety processor), 중복 센싱 경로, 보호된 통신 채널 및 결정론적 제약조건 검사(deterministic constraint check)는 더욱 강력한 진단 및 결함 억제 경계(diagnostic and containment boundary)를 제공할 수 있다.

FDIR의 효과는 시스템 설계 초기부터 확보된 관측 가능성(observability)과 진단 커버리지(diagnostic coverage)에 크게 좌우된다. 구성요소는 의미 있는 상태 정보, 타임스탬프(timestamp), 신뢰도 지표, 오류 상태, 자원 사용량 및 관련 내부 측정값을 제공해야 한다. 로깅(logging)은 결함 발생에서 탐지, 격리, 폴백 및 복구에 이르는 전체 순서를 보존하여 현장 사고를 재구성하고 진단 메커니즘을 지속적으로 개선할 수 있도록 해야 한다.

완전한 물리 인공지능 안전 아키텍처(Physical AI safety architecture)에서 FDIR은 런타임 모니터링(runtime monitoring)과 폴백 행동(fallback behavior)을 연결하는 의사결정 가교 역할을 한다. 탐지(detection)는 신뢰가 저하되었음을 확인하고, 격리(isolation)는 더 이상 의존해서는 안 되는 기능을 결정하며, 복구(recovery)는 통제된 조건에서 해당 기능을 복원하거나 재구성한다. 복구의 안전성을 정당화할 수 없는 경우 동일한 진단 정보는 성능 저하 운용, 최소 위험 행동(minimum-risk behavior), 사람의 개입(human intervention) 또는 임무 중단(mission abort)을 결정하는 근거가 된다.

##  

## 06.03. Safe State Definition

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

A safe state is a system condition in which the risk of unacceptable physical harm has been reduced to an acceptable level after a fault, uncertainty, loss of capability, or violation of operational assumptions. For Physical AI, a safe state cannot be defined merely as "powered off" or "stopped." It must describe a physically stable and controllable condition appropriate to the robot, environment, mission, payload, and surrounding people.

The concept originates from the need to ensure that failures lead toward bounded and predictable behavior rather than uncontrolled continuation. When perception, localization, planning, AI inference, communication, compute, power, or actuation becomes unreliable, the system needs a defined destination for its safety response. The safe state therefore provides the target condition toward which fail-safe mechanisms and fallback strategies attempt to move the system.

A complete safe-state definition specifies more than robot velocity. It may include position, pose, actuator torque, stored mechanical energy, brake condition, payload stability, power state, communication status, control authority, and distance from people or hazards. These variables collectively determine whether the physical system can remain in its current condition without creating an unacceptable risk while awaiting recovery or intervention.

Stopping is a common safe-state strategy for indoor mobile robots because removing motion can eliminate a major source of kinetic risk. However, even a stopped robot must remain stable, prevent unintended restart, maintain braking where required, and preserve essential safety sensing. A stationary condition that permits uncontrolled rolling, payload movement, actuator collapse, or unexpected reactivation cannot be considered a properly established safe state.

For manipulators, safe-state definition requires consideration of configuration and stored energy. Immediately removing actuator power may allow a heavy arm or suspended object to fall, while rigidly maintaining position may generate excessive force or thermal stress. Depending on the system, a safer response may involve controlled deceleration, maintaining a stable pose, lowering a payload, engaging brakes, limiting torque, or moving away from a human interaction zone.

Mobile platforms operating outdoors may require a different safe state because stopping at the current location can expose the robot or other traffic to additional hazards. A robot may need to leave an intersection, avoid a slope, move away from machinery, or reach a designated stopping area before terminating autonomous motion. Safe-state selection must therefore consider not only the robot\'s internal condition but also the safety characteristics of its surrounding environment.

Aerial robots illustrate why zero motion cannot universally represent safety. Immediate propulsion shutdown can cause an uncontrolled descent, making continued stabilization temporarily safer than termination. The safe-state objective may instead be controlled hovering, emergency landing, reduced-flight operation, or navigation toward an acceptable landing location. The required behavior depends on altitude, remaining energy, vehicle health, terrain, and nearby people.

Safe states should be defined for identifiable fault classes rather than relying on a single universal response. Loss of cloud connectivity may allow continued local operation, whereas loss of primary localization may require reduced speed or stopping. A degraded sensor may permit restricted autonomy, while failure of a safety-critical actuator may require immediate containment. Mapping faults to appropriate states enables proportional responses instead of unnecessary emergency shutdowns.

The definition must also distinguish a safe state from a minimum risk condition. A safe state describes a condition that satisfies specified safety requirements, while a minimum risk condition may represent the safest achievable condition when normal safety objectives cannot be completely satisfied. In complex environments, the system may first enter degraded operation and then execute a controlled maneuver toward the best achievable minimum-risk condition.

Transitioning into a safe state is as important as the state itself. A theoretically safe destination provides little protection if the robot must perform an unstable or hazardous maneuver to reach it. Safe-state design therefore includes transition trajectories, allowable acceleration and deceleration, braking profiles, actuator sequencing, collision constraints, energy management, and command arbitration. The entire transition must remain inside an acceptable safety envelope.

The system must also determine when a safe state has actually been achieved. Confirmation may require measured zero or limited velocity, verified brake engagement, stable actuator position, acceptable payload condition, valid safety sensing, sufficient separation from humans, or confirmation that hazardous energy has been controlled. Safety should depend on observed physical conditions rather than simply assuming that issuing a stop or shutdown command produced the intended result.

Safe-state logic should remain available even when high-level AI functions are unavailable. An independent safety controller, deterministic state machine, protected compute channel, or dedicated safety hardware can maintain essential transition and holding functions. This separation prevents failure of a foundation model, VLA policy, world model, planner, or primary compute platform from simultaneously eliminating the mechanism responsible for establishing physical safety.

Maintaining the safe state may require continued resources. Brakes can require power, stabilization may require active control, safety sensors may need to remain operational, and communication may be necessary for human intervention. Power architecture and resource allocation should therefore reserve sufficient capacity for safety functions. A system that can enter a safe state but cannot sustain it for the required duration has an incomplete safety strategy.

Exit conditions must be defined as carefully as entry conditions. Recovery should not occur merely because a fault indicator disappears or a component restarts. The system should verify that required sensors, localization, computation, communication, control, and safety assumptions have returned to acceptable conditions. Where uncertainty remains, human authorization, additional diagnostics, or a restricted restart may be required before full autonomous operation resumes.

Safe-state definitions should ultimately be traceable to hazard analysis, operational scenarios, and system safety requirements. Different robot classes and environments may require several context-dependent safe states connected through explicit transition rules. By defining what physical safety actually means before failures occur, Physical AI systems can convert uncertain or degraded situations into predictable behavior and provide a reliable foundation for minimum-risk conditions, degraded modes, fallback control, and recovery.

안전 상태(safe state)는 결함(fault), 불확실성(uncertainty), 기능 상실(loss of capability) 또는 운용 가정(operational assumption)의 위반이 발생한 이후 허용할 수 없는 물리적 피해(unacceptable physical harm)의 위험이 허용 가능한 수준으로 감소된 시스템 상태를 의미한다. 물리 인공지능(Physical AI)에서 안전 상태는 단순히 "전원 차단(powered off)"이나 "정지(stopped)"로 정의할 수 없다. 로봇, 환경, 임무, 적재물(payload), 주변 사람의 상황에 적합한 물리적으로 안정되고 제어 가능한 상태를 의미해야 한다.

안전 상태의 개념은 고장이 발생했을 때 시스템이 통제되지 않은 운용을 계속하는 것이 아니라 제한되고 예측 가능한 행동(bounded and predictable behavior)으로 전환되도록 해야 한다는 필요성에서 출발한다. 인지(perception), 위치추정(localization), 계획(planning), AI 추론(AI inference), 통신, 계산, 전력 또는 구동 기능이 신뢰할 수 없게 되면 시스템에는 안전 대응이 도달해야 할 명확한 목표 상태가 필요하다. 따라서 안전 상태는 고장 안전 메커니즘(fail-safe mechanism)과 폴백 전략(fallback strategy)이 시스템을 이동시키려는 목표 조건을 제공한다.

완전한 안전 상태 정의(safe-state definition)는 로봇의 속도만을 규정하지 않는다. 위치(position), 자세(pose), 액추에이터 토크(actuator torque), 저장된 기계적 에너지(stored mechanical energy), 브레이크 상태, 적재물 안정성(payload stability), 전력 상태, 통신 상태, 제어 권한(control authority), 사람이나 위험 요소와의 거리 등이 포함될 수 있다. 이러한 변수들은 복구 또는 개입을 기다리는 동안 물리 시스템이 허용할 수 없는 위험을 발생시키지 않고 현재 상태를 유지할 수 있는지를 종합적으로 결정한다.

정지(stopping)는 움직임을 제거함으로써 주요 운동 위험(kinetic risk)을 줄일 수 있기 때문에 실내 이동 로봇(indoor mobile robot)에서 일반적으로 사용되는 안전 상태 전략이다. 그러나 정지된 로봇도 안정적인 상태를 유지하고 의도하지 않은 재시작을 방지하며, 필요한 경우 제동 상태를 유지하고 필수 안전 센싱(safety sensing)을 보존해야 한다. 제어되지 않은 굴러감, 적재물 이동, 액추에이터 붕괴 또는 예상하지 못한 재작동이 가능한 정지 상태는 적절하게 확립된 안전 상태라고 할 수 없다.

매니퓰레이터(manipulator)의 안전 상태를 정의할 때는 로봇의 구성(configuration)과 저장 에너지(stored energy)를 고려해야 한다. 액추에이터 전원을 즉시 제거하면 무거운 로봇 팔이나 매달린 물체가 떨어질 수 있으며, 반대로 위치를 강제로 유지하면 과도한 힘이나 열적 스트레스(thermal stress)가 발생할 수 있다. 시스템에 따라 제어된 감속, 안정된 자세 유지, 적재물 내려놓기, 브레이크 체결, 토크 제한 또는 사람과의 상호작용 영역에서 벗어나는 행동이 더욱 안전한 대응이 될 수 있다.

실외에서 운용되는 이동 플랫폼(mobile platform)은 현재 위치에서 정지하는 것이 로봇이나 주변 교통에 추가적인 위험을 발생시킬 수 있기 때문에 다른 형태의 안전 상태가 필요할 수 있다. 로봇은 자율 이동을 종료하기 전에 교차로를 벗어나거나, 경사면을 피하거나, 기계 장비로부터 멀어지거나, 지정된 정지 구역에 도달해야 할 수 있다. 따라서 안전 상태의 선택은 로봇 내부 상태뿐만 아니라 주변 환경이 가지는 안전 특성(safety characteristics)도 함께 고려해야 한다.

비행 로봇(aerial robot)은 움직임이 없는 상태가 항상 안전을 의미하지 않는 이유를 잘 보여준다. 추진력을 즉시 차단하면 통제되지 않은 하강(uncontrolled descent)이 발생할 수 있으므로 일시적으로 안정화 제어를 계속하는 것이 운용 종료보다 안전할 수 있다. 안전 상태의 목표는 제어된 호버링(controlled hovering), 비상 착륙(emergency landing), 제한된 비행 운용 또는 적절한 착륙 지점으로 이동하는 것이 될 수 있다. 필요한 행동은 고도, 잔여 에너지, 기체 상태, 지형 및 주변 사람의 존재에 따라 달라진다.

안전 상태는 하나의 보편적인 대응에 의존하기보다 식별 가능한 결함 유형(fault class)에 따라 정의되어야 한다. 클라우드 연결 손실(loss of cloud connectivity)은 로컬 운용의 지속을 허용할 수 있지만, 주 위치추정(primary localization)의 상실은 감속이나 정지를 요구할 수 있다. 성능이 저하된 센서는 제한적인 자율 운용을 허용할 수 있는 반면, 안전 필수 액추에이터(safety-critical actuator)의 고장은 즉각적인 위험 억제를 요구할 수 있다. 결함을 적절한 상태와 연결하면 불필요한 비상 정지 대신 위험 수준에 비례하는 대응이 가능하다.

또한 안전 상태(safe state)와 최소 위험 상태(minimum risk condition)를 구분해야 한다. 안전 상태는 명시된 안전 요구사항(safety requirement)을 충족하는 상태를 의미하는 반면, 최소 위험 상태는 정상적인 안전 목표를 완전히 충족할 수 없을 때 현실적으로 달성할 수 있는 가장 안전한 상태를 의미할 수 있다. 복잡한 환경에서는 시스템이 먼저 성능 저하 운용(degraded operation)에 진입한 다음 제어된 기동을 수행하여 달성 가능한 최선의 최소 위험 상태로 이동할 수 있다.

안전 상태로 전환하는 과정은 안전 상태 자체만큼 중요하다. 이론적으로 안전한 목표 상태라 하더라도 로봇이 그 상태에 도달하기 위해 불안정하거나 위험한 기동을 수행해야 한다면 충분한 보호를 제공하지 못한다. 따라서 안전 상태 설계에는 전환 궤적(transition trajectory), 허용 가능한 가속 및 감속, 제동 프로파일(braking profile), 액추에이터 작동 순서, 충돌 제약조건, 에너지 관리 및 명령 중재(command arbitration)가 포함된다. 전체 전환 과정은 허용 가능한 안전 영역(safety envelope) 내부에서 이루어져야 한다.

시스템은 안전 상태가 실제로 달성되었는지도 판단해야 한다. 이를 확인하려면 측정된 영속도 또는 제한 속도, 브레이크 체결 확인, 안정적인 액추에이터 위치, 허용 가능한 적재물 상태, 유효한 안전 센싱, 사람과의 충분한 이격거리 또는 위험 에너지가 통제되었다는 확인이 필요할 수 있다. 안전은 단순히 정지 또는 종료 명령을 내렸다는 사실을 근거로 판단하는 것이 아니라 실제로 관측된 물리적 조건(observed physical condition)에 기반해야 한다.

안전 상태 로직(safe-state logic)은 상위 수준 AI 기능이 사용 불가능한 상황에서도 유지되어야 한다. 독립 안전 제어기(independent safety controller), 결정론적 상태 머신(deterministic state machine), 보호된 계산 채널(protected compute channel) 또는 전용 안전 하드웨어(dedicated safety hardware)가 필수적인 전환 및 상태 유지 기능을 담당할 수 있다. 이러한 분리는 파운데이션 모델(foundation model), 비전-언어-행동 정책(VLA policy), 월드 모델(world model), 플래너(planner) 또는 주 계산 플랫폼(primary compute platform)의 고장이 물리적 안전을 확립하는 메커니즘까지 동시에 상실시키는 것을 방지한다.

안전 상태를 유지하기 위해서도 지속적인 자원이 필요할 수 있다. 브레이크는 전력을 필요로 할 수 있고, 안정화를 위해 능동 제어(active control)가 필요할 수 있으며, 안전 센서는 계속 작동해야 하고, 사람의 개입을 위해 통신이 필요할 수도 있다. 따라서 전력 아키텍처(power architecture)와 자원 할당(resource allocation)은 안전 기능을 위한 충분한 용량을 확보해야 한다. 안전 상태에 진입할 수는 있지만 필요한 시간 동안 그 상태를 유지할 수 없는 시스템은 불완전한 안전 전략을 가진 것이다.

안전 상태의 진입 조건(entry condition)만큼 이탈 조건(exit condition)도 신중하게 정의해야 한다. 결함 표시가 사라지거나 구성요소가 재시작되었다는 이유만으로 복구가 이루어져서는 안 된다. 시스템은 필요한 센서, 위치추정, 계산, 통신, 제어 및 안전 가정이 허용 가능한 조건으로 복원되었는지를 검증해야 한다. 불확실성이 남아 있는 경우 완전한 자율 운용을 재개하기 전에 사람의 승인(human authorization), 추가적인 진단 또는 제한된 재시작(restricted restart)이 필요할 수 있다.

궁극적으로 안전 상태 정의(safe-state definition)는 위험 분석(hazard analysis), 운용 시나리오(operational scenario), 시스템 안전 요구사항(system safety requirement)과 추적 가능하게 연결되어야 한다. 서로 다른 로봇 유형과 환경에는 명시적인 전환 규칙으로 연결된 여러 상황 의존적 안전 상태(context-dependent safe state)가 필요할 수 있다. 고장이 발생하기 전에 물리적 안전이 실제로 무엇을 의미하는지 정의함으로써 물리 인공지능 시스템은 불확실하거나 성능이 저하된 상황을 예측 가능한 행동으로 전환하고, 최소 위험 상태, 성능 저하 모드, 폴백 제어 및 복구를 위한 신뢰성 있는 기반을 제공할 수 있다.

##  

## 06.04. Minimum Risk Condition

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

A Minimum Risk Condition (MRC) is the condition a Physical AI system seeks when normal operation can no longer be safely maintained and the preferred safe state cannot be reached immediately or completely. Rather than assuming that every failure can be resolved by stopping, the MRC represents the lowest reasonably achievable level of physical risk under the actual circumstances, available capabilities, and environmental constraints.

The concept is particularly important for autonomous physical systems because the safest achievable outcome may depend on where and how a failure occurs. A mobile robot inside an open warehouse aisle may safely stop in place, while the same robot crossing a vehicle route may need to continue moving temporarily. The MRC therefore connects fault response with situational reasoning about hazards, exposure, controllability, and remaining system capability.

An MRC should be distinguished from a predefined safe state. A safe state normally describes a condition known to satisfy specified safety requirements, whereas an MRC addresses situations where such a condition may not be directly reachable. The system may have to choose among imperfect alternatives and execute the action expected to minimize overall risk rather than simply applying a fixed shutdown response regardless of context.

Determining the MRC requires understanding both current hazards and the consequences of alternative actions. Relevant factors can include robot velocity, stopping distance, terrain, traffic, nearby people, payload stability, remaining battery energy, actuator condition, localization confidence, sensor coverage, communication availability, and environmental obstacles. These variables define which actions remain physically feasible and how much residual risk each option creates.

The MRC is therefore inherently context-dependent. For an indoor AMR, it may involve controlled deceleration followed by brake engagement and motion inhibition. For an outdoor autonomous platform, it may require leaving an intersection or moving to the side of a route. For a manipulator, the appropriate condition may involve stabilizing or lowering a payload before disabling motion rather than immediately removing actuator power.

For an aerial robot, minimum-risk behavior may require continued flight even after a significant fault. Immediate propulsion shutdown could create uncontrolled descent, while maintaining stabilization and navigating toward an emergency landing location may reduce risk. Remaining energy, propulsion capability, altitude, terrain, weather, and human presence influence whether hovering, controlled descent, diversion, or immediate landing provides the lowest achievable risk.

Reaching an MRC usually involves a Minimum Risk Maneuver (MRM), which is the controlled sequence of actions used to move the system toward the selected condition. The distinction is important: the MRC describes the desired final condition, while the MRM describes how the robot gets there. A safe architecture must reason about both because an inappropriate transition maneuver can introduce hazards even when the intended final state is comparatively safe.

Minimum-risk maneuvers should remain within verified physical and operational constraints. Speed, acceleration, steering, braking, actuator force, separation distance, collision margins, and energy consumption may need tighter limits than during normal autonomy. Complex objectives can be abandoned so that computation and control authority focus on essential stabilization, obstacle avoidance, controlled motion, and establishment of the minimum-risk condition.

The selection process should consider the capabilities that remain trustworthy after a fault. If primary perception is degraded but independent safety sensing remains available, restricted movement may still be justified. If localization confidence is lost, movement through a complex environment may become unacceptable. If communication disappears but local control remains healthy, the robot may autonomously complete an MRM without depending on cloud or fleet infrastructure.

Uncertainty should push MRC selection toward conservative behavior. Physical AI may not know precisely whether a sensor has failed, whether an obstacle prediction is correct, or whether localization error is increasing. Rather than requiring perfect diagnosis before acting, the system can reduce speed, enlarge safety margins, restrict maneuver choices, and favor conditions whose safety depends on fewer uncertain assumptions.

MRC execution should not depend entirely on the high-level AI function whose reliability may already be compromised. Independent monitoring, deterministic safety logic, fallback controllers, protected compute resources, and redundant sensing can provide the essential capabilities needed to execute a minimum-risk maneuver. High-level AI may assist with context interpretation, but safety-critical constraints should remain enforceable independently whenever practical.

The system must verify that the MRC has actually been achieved. Issuing a braking, landing, parking, or stabilization command does not prove that physical risk has been controlled. Confirmation may require measured motion limits, verified brake status, stable pose, acceptable payload condition, safe separation, successful landing detection, controlled energy state, or evidence that the robot is no longer exposed to the hazard that triggered the maneuver.

Once established, the MRC may need to be maintained for an extended period. Safety sensing, braking, stabilization, communication, logging, warning interfaces, and supervisory functions may remain active while the system waits for recovery or human assistance. Resource management must therefore reserve sufficient power and computational capability to sustain the condition instead of consuming all remaining resources during the transition.

An MRC does not automatically imply mission termination. After the triggering fault has been isolated and required capabilities have been restored, the system may evaluate whether controlled recovery is justified. Restart should require verification of sensor health, localization, computation, communication, control authority, environmental conditions, and relevant safety assumptions. Otherwise, the system should remain in the MRC or escalate to human intervention.

Minimum Risk Condition design should be derived from hazard analysis and operational scenarios rather than added as a generic emergency function after system development. Designers should identify credible failure situations, determine achievable risk-reduction options, define corresponding minimum-risk maneuvers, establish verification criteria, and ensure that the necessary safety functions remain available under the faults that make those maneuvers necessary.

Within the broader Physical AI fallback architecture, the MRC provides a practical bridge between safe-state definitions and real-world uncertainty. It recognizes that perfect safety may not always be immediately achievable, yet uncontrolled behavior is unacceptable. By selecting and executing the safest feasible response with the trustworthy capabilities that remain, the system can minimize residual physical risk until recovery, human assistance, or controlled mission termination becomes possible.

최소 위험 상태(Minimum Risk Condition, MRC)는 정상 운용(normal operation)을 더 이상 안전하게 유지할 수 없고 선호되는 안전 상태(safe state)에 즉시 또는 완전하게 도달할 수 없을 때 물리 인공지능(Physical AI) 시스템이 도달하고자 하는 상태이다. 모든 고장을 단순한 정지로 해결할 수 있다고 가정하는 대신, MRC는 실제 상황, 사용 가능한 기능 및 환경적 제약조건에서 합리적으로 달성할 수 있는 가장 낮은 수준의 물리적 위험(physical risk)을 나타낸다.

이 개념은 고장이 발생한 위치와 상황에 따라 달성 가능한 가장 안전한 결과가 달라질 수 있기 때문에 자율 물리 시스템(autonomous physical system)에서 특히 중요하다. 개방된 창고 통로에 있는 이동 로봇은 현재 위치에서 안전하게 정지할 수 있지만, 동일한 로봇이 차량 이동 경로를 횡단하는 중이라면 일시적으로 계속 움직여야 할 수 있다. 따라서 MRC는 결함 대응(fault response)을 위험요소, 노출(exposure), 제어 가능성(controllability), 잔존 시스템 기능에 대한 상황적 추론(situational reasoning)과 연결한다.

MRC는 사전에 정의된 안전 상태(predefined safe state)와 구분되어야 한다. 안전 상태는 일반적으로 명시된 안전 요구사항(safety requirement)을 충족한다고 알려진 상태를 의미하지만, MRC는 그러한 상태에 직접 도달할 수 없는 상황을 다룬다. 시스템은 불완전한 여러 대안 중 하나를 선택해야 할 수 있으며, 상황에 관계없이 고정된 종료 대응을 적용하는 대신 전체적인 위험을 최소화할 것으로 예상되는 행동을 수행해야 한다.

MRC를 결정하려면 현재의 위험요소뿐만 아니라 가능한 대체 행동의 결과도 이해해야 한다. 관련 요소에는 로봇 속도, 정지 거리, 지형, 교통, 주변 사람, 적재물 안정성(payload stability), 잔여 배터리 에너지, 액추에이터 상태, 위치추정 신뢰도(localization confidence), 센서 커버리지(sensor coverage), 통신 가용성 및 환경 장애물이 포함될 수 있다. 이러한 변수들은 어떤 행동이 물리적으로 실행 가능한지와 각 선택지가 어느 정도의 잔여 위험(residual risk)을 발생시키는지를 결정한다.

따라서 MRC는 본질적으로 상황 의존적(context-dependent)이다. 실내 자율이동로봇(AMR)의 경우 제어된 감속 후 브레이크를 체결하고 움직임을 차단하는 것이 될 수 있다. 실외 자율 플랫폼에서는 교차로를 벗어나거나 이동 경로의 측면으로 이동해야 할 수 있다. 매니퓰레이터(manipulator)의 경우 액추에이터 전원을 즉시 차단하기보다 적재물을 안정화하거나 내려놓은 후 움직임을 비활성화하는 것이 적절한 상태일 수 있다.

비행 로봇(aerial robot)의 경우 최소 위험 행동(minimum-risk behavior)은 심각한 결함이 발생한 이후에도 비행을 계속해야 할 수 있다. 추진력을 즉시 차단하면 통제되지 않은 하강(uncontrolled descent)이 발생할 수 있는 반면, 안정화를 유지하면서 비상 착륙 위치로 이동하면 위험을 줄일 수 있다. 잔여 에너지, 추진 능력, 고도, 지형, 기상 조건 및 주변 사람의 존재는 호버링(hovering), 제어된 하강, 우회 또는 즉각적인 착륙 중 어느 방법이 달성 가능한 가장 낮은 위험을 제공하는지에 영향을 미친다.

MRC에 도달하려면 일반적으로 최소 위험 기동(Minimum Risk Maneuver, MRM)이 필요하며, 이는 시스템을 선택된 상태로 이동시키기 위해 수행하는 제어된 일련의 행동을 의미한다. 이러한 구분은 중요하다. MRC는 원하는 최종 상태를 설명하는 반면, MRM은 로봇이 그 상태에 어떻게 도달하는지를 설명한다. 의도된 최종 상태가 비교적 안전하더라도 부적절한 전환 기동이 새로운 위험을 발생시킬 수 있으므로 안전 아키텍처는 두 가지 모두를 고려해야 한다.

최소 위험 기동(minimum-risk maneuver)은 검증된 물리적 및 운용 제약조건(physical and operational constraints) 내에서 수행되어야 한다. 속도, 가속도, 조향, 제동, 액추에이터 힘, 이격거리, 충돌 여유(collision margin), 에너지 소비는 정상 자율 운용보다 더욱 엄격하게 제한될 수 있다. 복잡한 임무 목표는 포기하고 계산 자원과 제어 권한을 필수적인 안정화, 장애물 회피, 제어된 움직임 및 최소 위험 상태 확립에 집중할 수 있다.

MRC 선택 과정에서는 결함 이후에도 신뢰할 수 있는 기능이 무엇인지 고려해야 한다. 주 인지(primary perception) 기능이 저하되었지만 독립적인 안전 센싱(independent safety sensing)이 유지된다면 제한된 이동이 여전히 허용될 수 있다. 위치추정 신뢰도를 상실했다면 복잡한 환경에서 이동하는 것이 허용되지 않을 수 있다. 통신이 단절되더라도 로컬 제어(local control)가 정상이라면 로봇은 클라우드 또는 플릿 인프라(fleet infrastructure)에 의존하지 않고 자율적으로 MRM을 완료할 수 있다.

불확실성(uncertainty)이 증가할수록 MRC 선택은 더욱 보수적인 행동(conservative behavior)을 지향해야 한다. 물리 인공지능은 센서가 실제로 고장 났는지, 장애물 예측이 정확한지 또는 위치추정 오류가 증가하고 있는지를 정확하게 판단하지 못할 수 있다. 완벽한 진단이 이루어질 때까지 기다리는 대신 시스템은 속도를 줄이고, 안전 여유(safety margin)를 확대하며, 선택 가능한 기동을 제한하고, 더 적은 불확실한 가정에 의존하는 상태를 우선적으로 선택할 수 있다.

MRC 실행은 신뢰성이 이미 손상되었을 가능성이 있는 상위 수준 AI 기능(high-level AI function)에 전적으로 의존해서는 안 된다. 독립적인 모니터링(independent monitoring), 결정론적 안전 로직(deterministic safety logic), 폴백 제어기(fallback controller), 보호된 계산 자원(protected compute resource), 중복 센싱(redundant sensing)은 최소 위험 기동을 수행하는 데 필요한 핵심 기능을 제공할 수 있다. 상위 수준 AI가 상황 해석을 지원할 수 있지만, 안전 필수 제약조건(safety-critical constraint)은 가능한 경우 독립적으로 강제할 수 있어야 한다.

시스템은 MRC가 실제로 달성되었는지를 검증해야 한다. 제동, 착륙, 주차 또는 안정화 명령을 내렸다는 사실만으로 물리적 위험이 통제되었다고 판단할 수 없다. 확인 과정에는 측정된 움직임 제한, 검증된 브레이크 상태, 안정된 자세, 허용 가능한 적재물 상태, 안전한 이격거리, 성공적인 착륙 감지, 통제된 에너지 상태 또는 로봇이 해당 기동을 유발한 위험에 더 이상 노출되지 않는다는 증거가 필요할 수 있다.

MRC가 확립된 이후에도 해당 상태를 장시간 유지해야 할 수 있다. 시스템이 복구 또는 사람의 지원(human assistance)을 기다리는 동안 안전 센싱, 제동, 안정화, 통신, 로깅(logging), 경고 인터페이스(warning interface), 감독 기능(supervisory function)이 계속 활성화되어야 할 수 있다. 따라서 자원 관리(resource management)는 전환 과정에서 남아 있는 자원을 모두 소모하는 대신 해당 상태를 유지할 수 있도록 충분한 전력과 계산 능력을 확보해야 한다.

MRC가 반드시 임무 종료(mission termination)를 의미하는 것은 아니다. MRC를 유발한 결함이 격리되고 필요한 기능이 복원된 이후 시스템은 제어된 복구(controlled recovery)가 정당한지를 평가할 수 있다. 재시작을 위해서는 센서 상태, 위치추정, 계산, 통신, 제어 권한, 환경 조건 및 관련 안전 가정(safety assumption)이 검증되어야 한다. 그렇지 않다면 시스템은 MRC를 유지하거나 사람의 개입(human intervention) 단계로 전환해야 한다.

최소 위험 상태 설계(Minimum Risk Condition design)는 시스템 개발 이후 일반적인 비상 기능으로 추가되는 것이 아니라 위험 분석(hazard analysis)과 운용 시나리오(operational scenario)에서 도출되어야 한다. 설계자는 발생 가능한 고장 상황을 식별하고, 달성 가능한 위험 감소 방안을 결정하며, 이에 대응하는 최소 위험 기동을 정의하고, 검증 기준(verification criteria)을 확립하며, 해당 기동을 필요하게 만드는 고장 상황에서도 필요한 안전 기능이 계속 사용 가능한지를 보장해야 한다.

보다 광범위한 물리 인공지능 폴백 아키텍처(Physical AI fallback architecture)에서 MRC는 안전 상태 정의(safe-state definition)와 현실 세계의 불확실성을 연결하는 실질적인 가교를 제공한다. 완벽한 안전을 항상 즉시 달성할 수 있는 것은 아니지만 통제되지 않은 행동은 허용될 수 없다는 점을 전제로 한다. 시스템은 남아 있는 신뢰 가능한 기능을 이용하여 실행 가능한 가장 안전한 대응을 선택하고 수행함으로써 복구, 사람의 지원 또는 통제된 임무 종료가 가능해질 때까지 잔여 물리적 위험을 최소화할 수 있다.

##  

## 06.05. Degraded Mode Operation

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Degraded mode operation allows a Physical AI system to continue functioning with deliberately reduced capability when one or more components, resources, or assumptions can no longer support normal autonomous operation. Instead of treating every fault as a reason for immediate shutdown, the system restricts its behavior to a smaller operational envelope whose safety can still be justified using the capabilities that remain trustworthy.

The central principle of degraded operation is graceful degradation rather than abrupt loss of functionality. A robot may lose performance, autonomy, speed, sensing coverage, planning sophistication, or mission capability while preserving essential safety functions. This creates an intermediate operating region between full autonomous operation and a safe state or Minimum Risk Condition, allowing risk to be managed proportionally to the severity of degradation.

Entering degraded mode requires an assessment of what has failed and what remains reliable. Fault Detection, Isolation, and Recovery mechanisms can identify affected sensors, compute resources, communication channels, actuators, localization functions, or AI models. The system then determines whether the remaining capabilities provide sufficient observability, controllability, and safety assurance to support continued operation under explicitly restricted conditions.

Restrictions should directly compensate for the lost capability. Reduced perception range may require lower speed and greater obstacle clearance, while degraded localization may require operation only within well-observed areas. Limited compute capacity may force simpler planning, shorter prediction horizons, or lower model update rates. The objective is to reduce operational demands until they become compatible with the system\'s remaining trustworthy capability.

Degraded operation is especially useful for sensor and perception faults. If one camera fails in a multi-camera system, complete autonomy may not need to terminate if LiDAR, radar, or other cameras still provide sufficient coverage. However, blind regions and reduced detection performance must be reflected in behavior. The robot may restrict direction changes, increase separation distances, avoid complex environments, or operate at a lower maximum velocity.

Localization degradation requires similar adaptation. A robot that loses high-accuracy localization may continue using wheel odometry, inertial sensing, visual localization, map constraints, or another independent estimator, but accumulated uncertainty limits how long and where this remains acceptable. The operating envelope can progressively shrink as uncertainty increases, eventually triggering stopping or transition toward a Minimum Risk Condition if localization becomes insufficient.

Compute degradation can arise from processor faults, overload, memory pressure, thermal throttling, or excessive AI inference latency. Instead of allowing missed deadlines to propagate unpredictably into control, the system may reduce computational demand. Optional models can be disabled, perception resolution lowered, planning frequency reduced, or a simpler fallback algorithm activated while safety-critical monitoring and control retain prioritized computational resources.

Communication loss also illustrates the importance of capability-aware degradation. A robot designed with sufficient local autonomy may continue operating when cloud or fleet communication disappears, but functions requiring remote coordination should be suspended. Mission scope may be reduced, shared-map updates frozen, cooperative maneuvers prohibited, and remote-dependent decisions deferred until communication returns or the robot reaches an appropriate fallback condition.

Actuator degradation requires careful consideration because remaining control authority directly determines physical maneuverability. Loss of an actuator may permit restricted motion in some robot architectures but make continued operation unacceptable in others. The system must evaluate braking, steering, stabilization, payload support, force limits, and achievable trajectories before authorizing degraded movement, rather than assuming that partial actuation automatically provides sufficient control.

Power degradation can similarly produce staged responses. As available energy decreases or battery abnormalities emerge, nonessential computation, sensing, payload functions, or mission activities may be disabled to preserve resources for locomotion, braking, communication, safety monitoring, and recovery. The robot may shorten its mission, reduce speed, return to a charging location, or transition toward a safe state before energy falls below the level required for controlled operation.

AI degradation introduces challenges that may not correspond to explicit component failures. Increasing uncertainty, out-of-distribution observations, inconsistent world-model predictions, or unreliable VLA outputs can indicate that learned autonomy is operating beyond its trustworthy domain. The system can respond by limiting AI authority, enforcing stronger deterministic constraints, simplifying tasks, requesting confirmation, or transferring control to classical or independently validated fallback functions.

Degraded mode should therefore be represented as an explicit operating state rather than an informal collection of emergency behaviors. Entry conditions, permitted capabilities, prohibited actions, speed and force limits, environmental restrictions, monitoring requirements, and exit criteria should be defined for each relevant mode. Multiple degradation levels may be appropriate so that restrictions increase progressively as capability or confidence declines.

Runtime monitoring remains essential throughout degraded operation because the condition may improve or deteriorate. The system must continuously evaluate sensor health, localization confidence, compute timing, communication, power, actuator capability, environmental complexity, and AI behavior. If the remaining safety margin decreases below an acceptable threshold, the robot should transition to a more restrictive mode, execute a Minimum Risk Maneuver, or establish a safe state.

Recovery from degraded operation should occur only after the capability that caused the restriction has been restored and verified. A restarted sensor, recovered network connection, cooled processor, or recalibrated localization system should demonstrate stable and consistent behavior before restrictions are removed. Progressive restoration can be safer than immediately returning from a severely degraded condition to unrestricted autonomous operation.

Human supervision can become increasingly important as autonomy degrades. The robot may notify an operator, explain which capability has been lost, report current restrictions, request remote assistance, or require authorization for particular actions. Human intervention should complement rather than replace fundamental safety mechanisms, because communication latency, operator availability, or incomplete situational awareness may prevent immediate assistance.

Degraded mode operation ultimately provides the controlled middle ground of a Physical AI fallback architecture. Normal autonomy can progressively surrender performance and mission objectives while preserving safety, controllability, and essential functions. When continued restricted operation remains justified, the robot can complete limited tasks or move toward recovery; when it does not, the same architecture guides transition toward a safe state, Minimum Risk Condition, human intervention, or controlled mission termination.

성능 저하 모드 운용(degraded mode operation)은 하나 이상의 구성요소, 자원 또는 운용 가정(operational assumption)이 더 이상 정상적인 자율 운용(normal autonomous operation)을 지원할 수 없을 때 물리 인공지능(Physical AI) 시스템이 의도적으로 기능을 제한하면서 계속 작동할 수 있도록 한다. 모든 결함을 즉각적인 시스템 종료의 원인으로 처리하는 대신, 시스템은 신뢰할 수 있는 상태로 남아 있는 기능을 이용하여 안전성을 정당화할 수 있는 보다 제한된 운용 영역(operational envelope)으로 행동 범위를 축소한다.

성능 저하 운용의 핵심 원칙은 갑작스러운 기능 상실이 아니라 점진적 성능 저하(graceful degradation)이다. 로봇은 필수 안전 기능(essential safety function)을 유지하면서 성능, 자율성, 속도, 센싱 범위, 계획의 복잡성 또는 임무 수행 능력을 낮출 수 있다. 이를 통해 완전한 자율 운용과 안전 상태(safe state) 또는 최소 위험 상태(Minimum Risk Condition) 사이에 중간 운용 영역이 형성되며, 성능 저하의 심각도에 비례하여 위험을 관리할 수 있다.

성능 저하 모드에 진입하려면 어떤 기능이 고장 났으며 어떤 기능이 여전히 신뢰할 수 있는지를 평가해야 한다. 결함 탐지, 격리 및 복구(Fault Detection, Isolation, and Recovery, FDIR) 메커니즘은 영향을 받은 센서, 계산 자원, 통신 채널, 액추에이터, 위치추정 기능 또는 AI 모델을 식별할 수 있다. 이후 시스템은 남아 있는 기능이 명시적으로 제한된 조건에서 지속적인 운용을 지원하기에 충분한 관측 가능성(observability), 제어 가능성(controllability), 안전 보증(safety assurance)을 제공하는지를 판단한다.

운용 제한은 상실된 기능을 직접적으로 보완하도록 설정되어야 한다. 인지 범위(perception range)가 감소하면 속도를 낮추고 장애물과의 이격거리를 확대해야 하며, 위치추정 성능이 저하되면 충분히 관측 가능한 영역에서만 운용해야 할 수 있다. 계산 능력이 제한되면 보다 단순한 계획, 짧은 예측 범위(prediction horizon), 낮은 모델 갱신 주기를 적용할 수 있다. 목적은 운용 요구 수준을 낮추어 시스템에 남아 있는 신뢰 가능한 기능과 일치시키는 것이다.

성능 저하 운용은 센서 및 인지 결함(sensor and perception fault)에 특히 유용하다. 다중 카메라 시스템에서 하나의 카메라가 고장 나더라도 라이다(LiDAR), 레이더(radar) 또는 다른 카메라가 충분한 범위를 제공한다면 완전한 자율 운용을 반드시 종료할 필요는 없다. 그러나 사각 영역(blind region)과 감소된 탐지 성능은 로봇의 행동에 반영되어야 한다. 로봇은 방향 전환을 제한하고, 이격거리를 확대하며, 복잡한 환경을 회피하거나 최대 운행 속도를 낮출 수 있다.

위치추정 성능 저하(localization degradation)에도 유사한 적응이 필요하다. 고정밀 위치추정 기능을 상실한 로봇은 휠 오도메트리(wheel odometry), 관성 센싱(inertial sensing), 시각 위치추정(visual localization), 지도 제약조건(map constraint) 또는 다른 독립 추정기(independent estimator)를 이용하여 계속 운용할 수 있지만, 누적되는 불확실성은 이러한 운용이 허용되는 시간과 영역을 제한한다. 불확실성이 증가하면 운용 영역을 점진적으로 축소하고, 위치추정이 불충분해지면 최종적으로 정지하거나 최소 위험 상태로 전환해야 한다.

계산 성능 저하(compute degradation)는 프로세서 고장, 과부하, 메모리 부족, 열 스로틀링(thermal throttling) 또는 과도한 AI 추론 지연(AI inference latency)으로 인해 발생할 수 있다. 마감시간 누락(missed deadline)이 예측할 수 없는 방식으로 제어 시스템에 전파되도록 두는 대신 시스템은 계산 요구량을 줄일 수 있다. 선택적 모델을 비활성화하고, 인지 해상도를 낮추며, 계획 주기를 감소시키거나 보다 단순한 폴백 알고리즘(fallback algorithm)을 활성화하면서 안전 필수 모니터링과 제어에는 우선적으로 계산 자원을 할당할 수 있다.

통신 손실(communication loss) 역시 기능 인식형 성능 저하(capability-aware degradation)의 중요성을 보여준다. 충분한 로컬 자율성(local autonomy)을 갖도록 설계된 로봇은 클라우드 또는 플릿 통신(fleet communication)이 단절되더라도 계속 운용할 수 있지만, 원격 협조가 필요한 기능은 중단해야 한다. 임무 범위를 축소하고, 공유 지도 갱신을 중지하며, 협력 기동(cooperative maneuver)을 금지하고, 원격 시스템에 의존하는 의사결정을 통신이 복구되거나 로봇이 적절한 폴백 상태에 도달할 때까지 연기할 수 있다.

액추에이터 성능 저하(actuator degradation)는 남아 있는 제어 권한(control authority)이 물리적인 기동 능력을 직접 결정하기 때문에 신중하게 고려해야 한다. 일부 로봇 아키텍처에서는 하나의 액추에이터를 상실하더라도 제한된 움직임이 가능하지만, 다른 시스템에서는 지속적인 운용 자체가 허용되지 않을 수 있다. 시스템은 부분적인 구동 기능이 자동적으로 충분한 제어 능력을 제공한다고 가정하지 않고, 성능 저하 상태의 이동을 허용하기 전에 제동, 조향, 안정화, 적재물 지지, 힘 제한 및 실행 가능한 궤적을 평가해야 한다.

전력 성능 저하(power degradation) 역시 단계적인 대응을 유발할 수 있다. 가용 에너지가 감소하거나 배터리 이상이 발생하면 이동, 제동, 통신, 안전 모니터링 및 복구를 위한 자원을 보존하기 위해 필수적이지 않은 계산, 센싱, 적재물 기능 또는 임무 활동을 비활성화할 수 있다. 로봇은 임무를 단축하거나 속도를 낮추고, 충전 위치로 복귀하거나, 제어된 운용에 필요한 수준 이하로 에너지가 감소하기 전에 안전 상태로 전환할 수 있다.

AI 성능 저하(AI degradation)는 명시적인 구성요소 고장과 일치하지 않는 문제를 발생시킬 수 있다. 증가하는 불확실성, 분포 외 관측(out-of-distribution observation), 일관되지 않은 월드 모델 예측(world-model prediction) 또는 신뢰할 수 없는 비전-언어-행동(VLA) 출력은 학습 기반 자율 시스템이 신뢰 가능한 영역을 벗어나 작동하고 있음을 나타낼 수 있다. 시스템은 AI의 제어 권한을 제한하고, 보다 강력한 결정론적 제약조건(deterministic constraint)을 적용하며, 작업을 단순화하고, 확인을 요청하거나 고전적 또는 독립적으로 검증된 폴백 기능으로 제어를 이전할 수 있다.

따라서 성능 저하 모드(degraded mode)는 비공식적인 비상 행동의 집합이 아니라 명시적인 운용 상태(explicit operating state)로 표현되어야 한다. 각각의 관련 모드에 대해 진입 조건(entry condition), 허용되는 기능, 금지되는 행동, 속도 및 힘 제한, 환경적 제한, 모니터링 요구사항, 이탈 조건(exit criteria)을 정의해야 한다. 기능이나 신뢰도가 감소함에 따라 제한 수준을 점진적으로 높일 수 있도록 여러 단계의 성능 저하 수준(degradation level)을 정의하는 것도 적절할 수 있다.

성능 저하 운용 중에도 상태가 개선되거나 더욱 악화될 수 있으므로 런타임 모니터링(runtime monitoring)은 계속해서 필수적이다. 시스템은 센서 상태, 위치추정 신뢰도, 계산 타이밍, 통신, 전력, 액추에이터 기능, 환경 복잡도 및 AI 행동을 지속적으로 평가해야 한다. 남아 있는 안전 여유(safety margin)가 허용 가능한 임계값 이하로 감소하면 로봇은 더욱 제한적인 모드로 전환하거나 최소 위험 기동(Minimum Risk Maneuver)을 수행하고, 또는 안전 상태를 확립해야 한다.

성능 저하 운용에서의 복구(recovery)는 제한의 원인이 된 기능이 복원되고 검증된 이후에만 수행되어야 한다. 재시작된 센서, 복구된 네트워크 연결, 냉각된 프로세서 또는 재보정된 위치추정 시스템은 제한을 해제하기 전에 안정적이고 일관된 동작을 입증해야 한다. 심각하게 성능이 저하된 상태에서 제한 없는 자율 운용으로 즉시 복귀하는 것보다 기능을 단계적으로 복원하는 점진적 복구(progressive restoration)가 더 안전할 수 있다.

자율 기능이 저하될수록 사람의 감독(human supervision)이 더욱 중요해질 수 있다. 로봇은 운영자에게 상태를 알리고, 어떤 기능이 상실되었는지를 설명하며, 현재 적용된 제한을 보고하고, 원격 지원(remote assistance)을 요청하거나 특정 행동에 대한 승인을 요구할 수 있다. 그러나 통신 지연, 운영자 부재 또는 불완전한 상황 인식으로 즉각적인 지원이 불가능할 수 있으므로 사람의 개입은 기본적인 안전 메커니즘을 대체하는 것이 아니라 이를 보완해야 한다.

궁극적으로 성능 저하 모드 운용(degraded mode operation)은 물리 인공지능 폴백 아키텍처(Physical AI fallback architecture)에서 통제된 중간 영역을 제공한다. 정상 자율 시스템은 안전, 제어 가능성 및 필수 기능을 유지하면서 성능과 임무 목표를 단계적으로 포기할 수 있다. 제한된 운용을 계속하는 것이 정당화되면 로봇은 제한된 작업을 완료하거나 복구를 향해 이동할 수 있으며, 그렇지 않다면 동일한 아키텍처를 통해 안전 상태, 최소 위험 상태, 사람의 개입 또는 통제된 임무 종료(controlled mission termination)로 전환할 수 있다.

##  

## 06.06. AI to Classical Control Fallback

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

AI-to-classical control fallback provides a structured mechanism for transferring control from a learned or high-level autonomous system to a simpler, more predictable control architecture when AI behavior can no longer be trusted. In Physical AI, the objective is not to eliminate AI when uncertainty appears, but to preserve safe physical control by reducing dependence on functions whose behavior cannot be sufficiently verified at runtime.

Modern autonomous robots may use foundation models, Vision-Language-Action models, learned planners, neural perception, or world models to interpret complex environments and generate flexible behavior. These capabilities provide adaptability beyond traditional control systems, but their outputs may become unreliable under distribution shift, ambiguous observations, corrupted inputs, excessive inference latency, or situations outside the conditions represented during development and validation.

Classical control provides a complementary safety property because many of its behaviors can be expressed through explicit models, constraints, state machines, feedback laws, and deterministic algorithms. PID control, model-based control, trajectory tracking, geometric planning, velocity limiting, emergency braking, and predefined motion primitives can often be analyzed more directly than learned policies. They therefore provide useful fallback functions when advanced autonomy loses trustworthiness.

The fallback architecture should separate high-level intelligence from safety-critical motion authority. AI may propose goals, trajectories, actions, or task sequences, while a lower-level control layer verifies whether those commands remain within physical and operational constraints. If AI outputs violate limits, become inconsistent, arrive too late, or lose sufficient confidence, the supervisory architecture can reject them and transfer authority to an independently executable classical control path.

Fallback does not necessarily mean replacing every AI function simultaneously. A system may retain reliable perception while replacing learned planning, or preserve AI-based object recognition while switching motion generation to deterministic navigation. Conversely, classical localization and control may remain active while an unreliable semantic reasoning model is removed from the decision loop. Functional decomposition enables the system to isolate only the capability whose trust has been lost.

Trigger conditions must be defined explicitly because unnecessary switching can reduce availability while delayed switching can create hazards. Relevant indicators include excessive model uncertainty, out-of-distribution detection, disagreement between sensors and AI predictions, infeasible trajectories, repeated safety-constraint violations, missed inference deadlines, compute faults, corrupted model outputs, or failures detected by independent runtime monitors. Multiple indicators may be combined before control authority is changed.

The classical fallback controller must be capable of operating with information that remains trustworthy after the triggering failure. If the fallback depends on the same failed perception pipeline, corrupted state estimate, compute resource, or communication channel as the AI controller, nominal architectural redundancy may provide little actual protection. Independence in sensing, state estimation, computation, power, and safety monitoring should therefore be considered according to the hazards being controlled.

Control transfer itself must be treated as a safety-critical maneuver. AI and classical controllers may represent trajectories, velocities, actuator commands, or internal states differently, and abrupt switching can generate discontinuities in steering, torque, acceleration, or braking. State synchronization, command arbitration, bounded transitions, bumpless transfer, and actuator-rate limits help ensure that fallback activation does not introduce a new physical instability.

Once classical fallback assumes authority, the robot normally operates with a reduced objective set. Instead of maximizing mission performance, it may prioritize stabilization, collision avoidance, controlled deceleration, lane or path keeping, payload protection, or movement toward a designated safe location. Complex task reasoning can be suspended so that available computation and sensing focus on maintaining controllability and reducing physical risk.

Classical fallback should operate inside a deliberately restricted operational envelope. Speed, acceleration, steering angle, actuator force, workspace, route complexity, obstacle clearance, and allowable environmental conditions may be tightened because the fallback controller generally has less semantic and adaptive capability than the primary AI system. These restrictions transform reduced intelligence into predictable behavior rather than attempting to reproduce full AI performance.

For a mobile robot, fallback may switch from an AI planner to a deterministic local planner and trajectory tracker that follows a known route, reduces speed, and stops when obstacles violate conservative clearance limits. A manipulator may abandon AI-generated manipulation and execute predefined retreat, hold, or payload-lowering motions. An autonomous vehicle or outdoor platform may maintain basic steering and braking while moving toward a minimum-risk location.

AI-to-classical fallback can also be hierarchical. The first response may preserve limited AI capability under stronger deterministic constraints, followed by classical degraded operation if confidence continues to fall. Further deterioration can activate a Minimum Risk Maneuver, and inability to maintain the required control authority can lead to a safe state. This creates progressive reduction of autonomy rather than a single binary transition between intelligent operation and shutdown.

Runtime monitoring must continue after the transfer because classical control is not inherently immune to failure. Sensors can degrade, state estimates can diverge, actuators can lose authority, and deterministic software can still contain faults. The system must verify that the fallback controller is achieving expected physical responses and retain the ability to escalate toward a more restrictive degraded mode, Minimum Risk Condition, emergency stop, or other safe response.

Returning authority to AI requires more than detecting that the original fault indicator has disappeared. The affected AI function should demonstrate stable outputs, acceptable timing, consistency with independent observations, compliance with safety constraints, and operation within its validated domain. A staged recovery may initially allow AI recommendations without control authority before progressively restoring its ability to influence planning and physical action.

Logging and traceability are important because every fallback event provides evidence about the boundary between trusted and untrusted autonomy. The system should record triggering conditions, AI outputs, monitor decisions, control-transfer timing, fallback commands, physical responses, recovery attempts, and final outcomes. These records support safety validation, failure analysis, model improvement, and refinement of the operational conditions under which AI control is permitted.

AI-to-classical control fallback ultimately establishes a layered relationship between adaptive intelligence and deterministic safety. AI provides semantic understanding, prediction, reasoning, and flexible behavior when its operating assumptions remain valid, while classical control preserves essential physical controllability when those assumptions fail. By designing the transition, restrictions, independence, monitoring, and recovery together, Physical AI can fail toward simpler and more predictable behavior instead of losing control when advanced intelligence becomes unreliable.

AI에서 고전 제어로의 폴백(AI-to-classical control fallback)은 AI의 행동을 더 이상 신뢰할 수 없을 때 학습 기반 또는 상위 수준 자율 시스템(learned or high-level autonomous system)에서 보다 단순하고 예측 가능한 제어 아키텍처로 제어 권한을 이전하는 구조화된 메커니즘이다. 물리 인공지능(Physical AI)에서 목적은 불확실성이 나타날 때 AI를 무조건 제거하는 것이 아니라, 런타임(runtime)에서 충분히 검증할 수 없는 기능에 대한 의존도를 낮춤으로써 안전한 물리적 제어를 유지하는 것이다.

현대의 자율 로봇은 복잡한 환경을 해석하고 유연한 행동을 생성하기 위해 파운데이션 모델(foundation model), 비전-언어-행동 모델(Vision-Language-Action model), 학습 기반 플래너(learned planner), 신경망 기반 인지(neural perception), 월드 모델(world model)을 사용할 수 있다. 이러한 기능은 기존 제어 시스템을 넘어서는 적응성을 제공하지만, 분포 변화(distribution shift), 모호한 관측, 손상된 입력, 과도한 추론 지연(inference latency), 개발 및 검증 과정에서 다루지 않은 상황에서는 출력의 신뢰성이 저하될 수 있다.

고전 제어(classical control)는 많은 행동을 명시적인 모델, 제약조건, 상태 머신(state machine), 피드백 법칙(feedback law), 결정론적 알고리즘(deterministic algorithm)을 통해 표현할 수 있기 때문에 상호 보완적인 안전 특성을 제공한다. PID 제어, 모델 기반 제어(model-based control), 궤적 추종(trajectory tracking), 기하학적 계획(geometric planning), 속도 제한, 비상 제동 및 사전 정의된 모션 프리미티브(motion primitive)는 일반적으로 학습 정책보다 직접적으로 분석할 수 있다. 따라서 고급 자율 기능의 신뢰성이 상실될 때 유용한 폴백 기능을 제공한다.

폴백 아키텍처(fallback architecture)는 상위 수준 지능(high-level intelligence)과 안전 필수 물리적 제어 권한(safety-critical motion authority)을 분리해야 한다. AI는 목표, 궤적, 행동 또는 작업 순서를 제안하고, 하위 수준 제어 계층은 이러한 명령이 물리적 및 운용 제약조건 내에 있는지를 검증할 수 있다. AI 출력이 제한을 위반하거나 일관성을 잃고, 지나치게 늦게 도착하거나 충분한 신뢰도를 상실하면 감독 아키텍처(supervisory architecture)는 해당 출력을 거부하고 독립적으로 실행 가능한 고전 제어 경로로 권한을 이전할 수 있다.

폴백이 모든 AI 기능을 동시에 교체해야 한다는 의미는 아니다. 시스템은 신뢰 가능한 인지(perception)를 유지하면서 학습 기반 계획 기능만 교체하거나, AI 기반 객체 인식(object recognition)을 유지하면서 움직임 생성(motion generation)을 결정론적 내비게이션으로 전환할 수 있다. 반대로 신뢰할 수 없는 의미론적 추론 모델(semantic reasoning model)을 의사결정 루프에서 제거하면서 고전적 위치추정과 제어를 계속 사용할 수도 있다. 기능적 분해(functional decomposition)를 통해 신뢰가 상실된 기능만 선택적으로 격리할 수 있다.

불필요한 전환은 시스템 가용성(availability)을 감소시키는 반면, 지나치게 늦은 전환은 위험을 발생시킬 수 있으므로 폴백의 트리거 조건(trigger condition)을 명확하게 정의해야 한다. 관련 지표에는 과도한 모델 불확실성(model uncertainty), 분포 외 탐지(out-of-distribution detection), 센서와 AI 예측 간의 불일치, 실행 불가능한 궤적, 반복적인 안전 제약조건 위반, 추론 마감시간 누락, 계산 결함, 손상된 모델 출력 또는 독립적인 런타임 모니터(runtime monitor)가 탐지한 고장이 포함될 수 있다. 제어 권한을 변경하기 전에 여러 지표를 결합하여 판단할 수도 있다.

고전적 폴백 제어기(classical fallback controller)는 폴백을 유발한 고장 이후에도 신뢰할 수 있는 정보만을 이용하여 작동할 수 있어야 한다. 폴백 시스템이 AI 제어기와 동일한 고장 난 인지 파이프라인, 손상된 상태 추정값, 계산 자원 또는 통신 채널에 의존한다면 명목상의 아키텍처 중복성(architectural redundancy)은 실질적인 보호를 거의 제공하지 못할 수 있다. 따라서 제어해야 하는 위험에 따라 센싱, 상태 추정(state estimation), 계산, 전력 및 안전 모니터링의 독립성을 고려해야 한다.

제어 전환(control transfer) 자체도 안전 필수 기동(safety-critical maneuver)으로 취급해야 한다. AI 제어기와 고전 제어기는 궤적, 속도, 액추에이터 명령 또는 내부 상태를 서로 다른 방식으로 표현할 수 있으며, 갑작스러운 전환은 조향, 토크, 가속 또는 제동에 불연속성(discontinuity)을 발생시킬 수 있다. 상태 동기화(state synchronization), 명령 중재(command arbitration), 제한된 전환(bounded transition), 무충격 전환(bumpless transfer), 액추에이터 변화율 제한(actuator-rate limit)을 적용하면 폴백 활성화가 새로운 물리적 불안정성을 발생시키는 것을 방지할 수 있다.

고전적 폴백이 제어 권한을 인수하면 로봇은 일반적으로 축소된 목표 집합(reduced objective set)을 기반으로 운용된다. 임무 성능을 최대화하는 대신 안정화, 충돌 회피, 제어된 감속, 차선 또는 경로 유지, 적재물 보호 또는 지정된 안전 위치로의 이동을 우선할 수 있다. 복잡한 작업 추론(task reasoning)을 중단하고 사용 가능한 계산 및 센싱 자원을 제어 가능성 유지와 물리적 위험 감소에 집중할 수 있다.

고전적 폴백은 의도적으로 제한된 운용 영역(restricted operational envelope) 내에서 작동해야 한다. 폴백 제어기는 일반적으로 주 AI 시스템보다 의미론적 및 적응적 능력이 낮기 때문에 속도, 가속도, 조향각, 액추에이터 힘, 작업 공간, 경로 복잡도, 장애물 이격거리 및 허용 가능한 환경 조건을 더욱 엄격하게 제한할 수 있다. 이러한 제한은 완전한 AI 성능을 재현하려 하기보다 감소된 지능을 예측 가능한 행동으로 전환한다.

이동 로봇(mobile robot)의 경우 폴백은 AI 플래너에서 결정론적 로컬 플래너(deterministic local planner)와 궤적 추종기(trajectory tracker)로 전환하여 알려진 경로를 따라 이동하고 속도를 낮추며, 장애물이 보수적인 이격거리 기준을 위반하면 정지하도록 구성할 수 있다. 매니퓰레이터(manipulator)는 AI가 생성한 조작을 포기하고 사전 정의된 후퇴, 자세 유지 또는 적재물 하강 동작을 수행할 수 있다. 자율주행차나 실외 플랫폼은 최소 위험 위치로 이동하면서 기본적인 조향과 제동 기능을 유지할 수 있다.

AI에서 고전 제어로의 폴백은 계층적(hierarchical)으로 구성될 수도 있다. 첫 번째 대응 단계에서는 보다 강력한 결정론적 제약조건 아래에서 제한적인 AI 기능을 유지하고, 신뢰도가 계속 감소하면 고전 제어 기반의 성능 저하 운용(classical degraded operation)으로 전환할 수 있다. 상태가 더욱 악화되면 최소 위험 기동(Minimum Risk Maneuver)을 활성화하고, 필요한 제어 권한을 유지할 수 없게 되면 안전 상태(safe state)로 전환할 수 있다. 이를 통해 지능적 운용과 시스템 종료 사이의 단일 이진 전환이 아니라 자율성을 단계적으로 축소할 수 있다.

고전 제어 자체도 본질적으로 고장에 면역되어 있는 것은 아니므로 제어 권한을 이전한 이후에도 런타임 모니터링(runtime monitoring)을 계속해야 한다. 센서의 성능이 저하되고, 상태 추정값이 발산하며, 액추에이터가 제어 권한을 상실하거나 결정론적 소프트웨어에도 결함이 존재할 수 있다. 시스템은 폴백 제어기가 예상된 물리적 응답을 실제로 달성하고 있는지 검증하고, 필요한 경우 더욱 제한적인 성능 저하 모드, 최소 위험 상태(Minimum Risk Condition), 비상 정지 또는 다른 안전 대응으로 전환할 수 있어야 한다.

AI에 제어 권한을 다시 부여하려면 기존의 결함 표시가 사라졌다는 사실만으로는 충분하지 않다. 영향을 받았던 AI 기능은 안정적인 출력, 허용 가능한 타이밍, 독립적인 관측과의 일관성, 안전 제약조건 준수 및 검증된 운용 영역(validated domain) 내에서의 작동을 입증해야 한다. 단계적 복구(staged recovery)를 적용하면 처음에는 AI가 제어 권한 없이 권고만 제공하도록 하고, 이후 계획 및 물리적 행동에 영향을 미치는 권한을 점진적으로 복원할 수 있다.

모든 폴백 이벤트(fallback event)는 신뢰 가능한 자율성과 신뢰할 수 없는 자율성 사이의 경계에 대한 중요한 증거를 제공하기 때문에 로깅(logging)과 추적성(traceability)이 중요하다. 시스템은 폴백 트리거 조건, AI 출력, 모니터의 판단, 제어 전환 시점, 폴백 명령, 물리적 응답, 복구 시도 및 최종 결과를 기록해야 한다. 이러한 기록은 안전 검증(safety validation), 고장 분석, 모델 개선 및 AI 제어가 허용되는 운용 조건을 정교화하는 데 활용될 수 있다.

궁극적으로 AI에서 고전 제어로의 폴백(AI-to-classical control fallback)은 적응형 지능(adaptive intelligence)과 결정론적 안전(deterministic safety) 사이에 계층적 관계를 확립한다. AI는 운용 가정이 유효하게 유지되는 동안 의미론적 이해, 예측, 추론 및 유연한 행동을 제공하고, 고전 제어는 이러한 가정이 무너졌을 때 필수적인 물리적 제어 가능성을 보존한다. 전환, 제한, 독립성, 모니터링 및 복구를 통합적으로 설계함으로써 물리 인공지능은 고급 지능이 신뢰할 수 없게 되었을 때 제어력을 상실하는 대신 보다 단순하고 예측 가능한 행동으로 안전하게 전환할 수 있다.

##  

## 06.07. Primary and Backup AI Models

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Primary and backup AI models provide redundancy at the intelligence layer of a Physical AI system, allowing selected autonomous capabilities to continue when the preferred model becomes unavailable, unreliable, or unsuitable for the current operating condition. The primary model normally delivers the highest performance, while the backup model provides a deliberately constrained alternative designed to preserve essential perception, prediction, reasoning, or action capabilities.

This architecture recognizes that AI failure is not limited to complete model shutdown. A primary model may continue executing while producing unreliable outputs because of distribution shift, unfamiliar environments, corrupted observations, excessive inference latency, memory pressure, numerical instability, or uncertainty beyond validated limits. Backup AI therefore addresses both explicit computational failure and loss of confidence in the behavioral validity of the primary model.

The primary AI model is generally optimized for normal operation and broad capability. It may use a large foundation model, Vision-Language-Action model, high-capacity perception network, learned planner, or sophisticated world model capable of handling diverse tasks and environments. Its computational cost and complexity are justified by improved understanding and adaptability, provided that runtime evidence indicates operation remains within acceptable assumptions and constraints.

A backup AI model should not simply be an identical copy of the primary model. Identical models can share the same architecture, training data, optimization artifacts, software defects, and failure modes, creating common-cause or correlated failures. Greater resilience can be achieved through diversity in model architecture, training methodology, input modalities, model size, inference framework, data sources, or the assumptions under which the backup function operates.

The backup model is often smaller and intentionally less capable than the primary model. Reduced complexity can provide lower inference latency, smaller memory requirements, improved computational predictability, and operation on independent or resource-constrained hardware. Rather than reproducing every function of the primary model, the backup should preserve the subset of intelligence required for degraded operation, controlled fallback, or transition toward a Minimum Risk Condition.

Model diversity must be designed according to the failure being mitigated. If both primary and backup perception models depend entirely on the same camera stream, sensor corruption may defeat both regardless of architectural differences. A more resilient arrangement may combine camera-based primary perception with LiDAR, radar, geometric processing, or another independent sensing path for backup. Independence should therefore extend beyond neural network architecture to the complete information chain.

Runtime monitoring determines when authority should move between models. Relevant indicators may include uncertainty, confidence calibration, disagreement with independent sensors, temporal inconsistency, physically implausible predictions, out-of-distribution observations, missed inference deadlines, resource exhaustion, repeated constraint violations, or internal model errors. A supervisory mechanism evaluates these signals rather than allowing either model to determine its own trustworthiness without independent checks.

Primary and backup models can also operate simultaneously to provide cross-validation. Their outputs may be compared for object detection, state estimation, trajectory prediction, semantic interpretation, or action selection. Persistent disagreement can indicate that at least one model is operating outside its reliable region. However, agreement alone does not prove correctness because models trained on similar data or assumptions may produce the same incorrect conclusion.

Switching to the backup model must preserve state continuity. Stateful AI components may maintain temporal context, latent memory, tracked objects, maps, task history, or internal world representations that cannot be transferred trivially. The architecture should define which state is shared, reconstructed, independently maintained, or discarded during transition. Poor state synchronization can cause the backup model to begin operation with incomplete or inconsistent situational understanding.

Control authority should normally pass through a supervisory safety layer rather than directly from one model to another. The supervisor can validate model outputs against deterministic safety constraints, robot dynamics, workspace limits, collision margins, and operational rules. Even when the backup model is active, its commands should remain subject to independent enforcement because backup status does not automatically imply that its outputs are safe.

Backup AI can support several levels of degradation. A smaller perception model may maintain basic obstacle detection while advanced semantic understanding is disabled, or a simplified world model may predict only short-horizon motion. A lightweight planner may support known routes but reject complex exploration. This capability-based approach allows the system to preserve useful autonomy without requiring the backup model to reproduce the complete intelligence of normal operation.

Resource isolation is important because a primary model failure caused by compute overload, memory exhaustion, thermal limits, or accelerator faults may also prevent the backup from running on the same hardware. Critical backup functions may therefore require reserved CPU or accelerator capacity, separate memory allocation, protected execution environments, or independent compute hardware. The required degree of separation should be determined by hazard and availability analysis.

The architecture may contain more than one fallback layer. Normal operation can begin with the primary AI model, transition to a backup AI model when confidence or availability decreases, then move to deterministic classical control if AI trust continues to deteriorate. Further loss of capability may trigger a Minimum Risk Maneuver and ultimately a safe state. Such a hierarchy provides progressive reduction of intelligence while preserving physical controllability.

Recovery to the primary model should require explicit revalidation rather than automatic restoration after a restart. The primary model should demonstrate stable inference timing, plausible outputs, agreement with independent observations, acceptable uncertainty, and operation within its validated domain. A staged transition can initially run the recovered model in shadow mode, compare its outputs with the active backup, and restore authority only after sufficient evidence of trustworthy behavior.

Testing primary and backup AI requires failure scenarios that examine both independent and correlated faults. Validation should include sensor degradation, unusual environments, model corruption, compute overload, latency spikes, distribution shift, communication loss, inconsistent predictions, and transition failures. The objective is not merely to prove that the backup model executes, but to demonstrate that the complete architecture detects loss of trust and transfers capability safely.

Primary and backup AI models ultimately create an intermediate resilience layer between full AI autonomy and deterministic fallback control. The primary model provides maximum intelligence when conditions support trustworthy operation, while the backup preserves a smaller verified capability when that trust declines. Combined with independent monitoring, diverse sensing, protected resources, classical fallback, and safe-state mechanisms, this architecture allows Physical AI to reduce intelligence progressively without immediately losing safe physical control.

주 AI 모델(primary AI model)과 백업 AI 모델(backup AI model)은 물리 인공지능(Physical AI) 시스템의 지능 계층(intelligence layer)에 중복성(redundancy)을 제공하여, 우선적으로 사용되는 모델이 이용 불가능하거나 신뢰할 수 없거나 현재 운용 조건에 적합하지 않을 때 선택된 자율 기능을 계속 유지할 수 있도록 한다. 주 모델은 일반적으로 가장 높은 성능을 제공하며, 백업 모델은 필수적인 인지, 예측, 추론 또는 행동 능력을 유지하도록 의도적으로 제한된 대안으로 설계된다.

이러한 아키텍처는 AI 고장이 단순히 모델이 완전히 작동을 멈추는 경우에만 한정되지 않는다는 점을 전제로 한다. 주 모델은 계속 실행되면서도 분포 변화(distribution shift), 익숙하지 않은 환경, 손상된 관측 데이터, 과도한 추론 지연(inference latency), 메모리 부족, 수치적 불안정성(numerical instability) 또는 검증된 한계를 초과하는 불확실성 때문에 신뢰할 수 없는 출력을 생성할 수 있다. 따라서 백업 AI는 명시적인 계산 고장뿐만 아니라 주 모델의 행동 유효성(behavioral validity)에 대한 신뢰 상실에도 대응한다.

주 AI 모델은 일반적으로 정상 운용(normal operation)과 광범위한 기능을 위해 최적화된다. 대규모 파운데이션 모델(foundation model), 비전-언어-행동 모델(Vision-Language-Action model), 고용량 인지 네트워크(high-capacity perception network), 학습 기반 플래너(learned planner) 또는 다양한 작업과 환경을 처리할 수 있는 정교한 월드 모델(world model)을 사용할 수 있다. 런타임 증거가 시스템이 허용 가능한 가정과 제약조건 내에서 작동하고 있음을 나타내는 경우, 향상된 이해 능력과 적응성을 위해 높은 계산 비용과 복잡성을 사용할 수 있다.

백업 AI 모델은 단순히 주 모델과 동일한 복제본이어서는 안 된다. 동일한 모델은 같은 아키텍처, 학습 데이터, 최적화 과정의 특성, 소프트웨어 결함 및 고장 모드(failure mode)를 공유할 수 있기 때문에 공통 원인 고장(common-cause failure)이나 상관 고장(correlated failure)이 발생할 수 있다. 모델 아키텍처, 학습 방법, 입력 모달리티(input modality), 모델 크기, 추론 프레임워크(inference framework), 데이터 출처 또는 백업 기능이 작동하는 기본 가정에 다양성(diversity)을 적용하면 보다 높은 회복탄력성(resilience)을 확보할 수 있다.

백업 모델은 주 모델보다 크기가 작고 의도적으로 기능이 제한되는 경우가 많다. 복잡도를 낮추면 추론 지연 감소, 메모리 요구량 축소, 계산 예측 가능성(computational predictability) 향상 및 독립적이거나 자원이 제한된 하드웨어에서의 실행이 가능해질 수 있다. 백업 모델은 주 모델의 모든 기능을 재현하는 대신 성능 저하 운용(degraded operation), 제어된 폴백(controlled fallback) 또는 최소 위험 상태(Minimum Risk Condition)로의 전환에 필요한 지능 기능의 일부를 유지해야 한다.

모델 다양성(model diversity)은 완화하려는 고장 유형에 따라 설계되어야 한다. 주 인지 모델과 백업 인지 모델이 모두 동일한 카메라 스트림에 완전히 의존한다면 아키텍처가 서로 다르더라도 센서 데이터 손상이 두 모델을 동시에 무력화할 수 있다. 보다 회복탄력적인 구성에서는 카메라 기반 주 인지와 라이다(LiDAR), 레이더(radar), 기하학적 처리(geometric processing) 또는 다른 독립적인 센싱 경로를 사용하는 백업 기능을 결합할 수 있다. 따라서 독립성(independence)은 신경망 아키텍처뿐만 아니라 전체 정보 체인(information chain)에 적용되어야 한다.

런타임 모니터링(runtime monitoring)은 모델 사이에서 제어 권한을 언제 이전해야 하는지를 결정한다. 관련 지표에는 불확실성, 신뢰도 보정(confidence calibration), 독립 센서와의 불일치, 시간적 비일관성(temporal inconsistency), 물리적으로 타당하지 않은 예측, 분포 외 관측(out-of-distribution observation), 추론 마감시간 누락, 자원 고갈(resource exhaustion), 반복적인 제약조건 위반 또는 모델 내부 오류가 포함될 수 있다. 감독 메커니즘(supervisory mechanism)은 어느 한 모델이 독립적인 검사 없이 자신의 신뢰성을 스스로 판단하도록 하지 않고 이러한 신호를 종합적으로 평가한다.

주 모델과 백업 모델을 동시에 운용하여 교차 검증(cross-validation)을 수행할 수도 있다. 객체 탐지, 상태 추정(state estimation), 궤적 예측, 의미론적 해석 또는 행동 선택에 대해 두 모델의 출력을 비교할 수 있다. 지속적인 불일치는 적어도 하나의 모델이 신뢰 가능한 영역을 벗어나 작동하고 있음을 나타낼 수 있다. 그러나 유사한 데이터나 가정을 기반으로 학습된 모델들은 동일하게 잘못된 결론을 생성할 수 있으므로 두 모델의 일치만으로 정확성을 보장할 수는 없다.

백업 모델로 전환할 때는 상태 연속성(state continuity)을 유지해야 한다. 상태를 유지하는 AI 구성요소는 시간적 문맥(temporal context), 잠재 메모리(latent memory), 추적 객체, 지도, 작업 이력 또는 내부 월드 표현(world representation)을 유지할 수 있으며, 이러한 정보는 단순하게 전달되지 않을 수 있다. 따라서 아키텍처는 전환 과정에서 어떤 상태를 공유하고, 재구성하고, 독립적으로 유지하거나 폐기할 것인지를 정의해야 한다. 상태 동기화(state synchronization)가 적절하지 않으면 백업 모델이 불완전하거나 일관되지 않은 상황 이해를 기반으로 운용을 시작할 수 있다.

제어 권한(control authority)은 일반적으로 한 모델에서 다른 모델로 직접 전달되기보다 감독 안전 계층(supervisory safety layer)을 통과해야 한다. 감독 계층은 모델 출력을 결정론적 안전 제약조건(deterministic safety constraint), 로봇 동역학(robot dynamics), 작업 공간 제한(workspace limit), 충돌 여유(collision margin), 운용 규칙과 비교하여 검증할 수 있다. 백업 모델이 활성화된 상태에서도 백업이라는 사실 자체가 출력의 안전성을 보장하는 것은 아니므로 해당 명령은 독립적인 안전 제약의 적용을 계속 받아야 한다.

백업 AI는 여러 수준의 성능 저하(degradation)를 지원할 수 있다. 소형 인지 모델이 기본적인 장애물 탐지 기능을 유지하는 동안 고급 의미론적 이해 기능은 비활성화될 수 있으며, 단순화된 월드 모델은 단기 예측(short-horizon prediction)만 수행할 수 있다. 경량 플래너(lightweight planner)는 알려진 경로의 운용을 지원하면서 복잡한 탐색은 거부할 수 있다. 이러한 기능 기반 접근법(capability-based approach)을 통해 백업 모델이 정상 운용의 전체 지능을 재현하지 않더라도 유용한 자율 기능을 유지할 수 있다.

주 모델의 고장이 계산 과부하, 메모리 고갈, 열적 한계(thermal limit) 또는 가속기 고장(accelerator fault)으로 발생한 경우 동일한 하드웨어에서 백업 모델도 실행할 수 없게 될 수 있으므로 자원 격리(resource isolation)가 중요하다. 따라서 핵심 백업 기능에는 예약된 CPU 또는 가속기 용량, 독립적인 메모리 할당, 보호된 실행 환경(protected execution environment) 또는 독립적인 계산 하드웨어가 필요할 수 있다. 필요한 분리 수준은 위험 분석(hazard analysis)과 가용성 분석(availability analysis)에 따라 결정되어야 한다.

아키텍처는 하나 이상의 폴백 계층(fallback layer)을 포함할 수 있다. 정상 운용은 주 AI 모델에서 시작하고 신뢰도나 가용성이 감소하면 백업 AI 모델로 전환한 다음, AI에 대한 신뢰가 계속 악화되면 결정론적 고전 제어(deterministic classical control)로 이동할 수 있다. 기능이 추가로 상실되면 최소 위험 기동(Minimum Risk Maneuver)이 실행되고 궁극적으로 안전 상태(safe state)로 전환될 수 있다. 이러한 계층 구조는 물리적 제어 가능성(physical controllability)을 유지하면서 지능 수준을 점진적으로 낮출 수 있도록 한다.

주 모델로의 복구(recovery)는 재시작 이후 자동적으로 복원하는 방식이 아니라 명시적인 재검증(revalidation)을 요구해야 한다. 주 모델은 안정적인 추론 타이밍, 타당한 출력, 독립적인 관측과의 일치, 허용 가능한 불확실성 및 검증된 운용 영역(validated domain) 내에서의 작동을 입증해야 한다. 단계적 전환(staged transition)을 적용하면 복구된 모델을 먼저 섀도 모드(shadow mode)로 실행하여 활성화된 백업 모델과 출력을 비교한 후 신뢰 가능한 행동에 대한 충분한 증거가 확보되었을 때만 제어 권한을 복원할 수 있다.

주 AI와 백업 AI를 시험할 때는 독립적인 고장뿐만 아니라 상관된 고장(correlated fault)을 포함하는 고장 시나리오가 필요하다. 검증(validation)에는 센서 성능 저하, 비정상적인 환경, 모델 손상, 계산 과부하, 지연 급증(latency spike), 분포 변화, 통신 손실, 일관되지 않은 예측 및 전환 실패가 포함되어야 한다. 목적은 단순히 백업 모델이 실행되는지를 입증하는 것이 아니라 전체 아키텍처가 신뢰 상실을 탐지하고 기능을 안전하게 이전할 수 있음을 입증하는 것이다.

궁극적으로 주 AI 모델과 백업 AI 모델(primary and backup AI models)은 완전한 AI 자율성(full AI autonomy)과 결정론적 폴백 제어(deterministic fallback control) 사이에 중간 회복탄력성 계층(intermediate resilience layer)을 형성한다. 주 모델은 조건이 신뢰 가능한 운용을 지원할 때 최대 수준의 지능을 제공하고, 백업 모델은 그 신뢰가 감소할 때 보다 작고 검증된 기능을 유지한다. 독립적인 모니터링, 다양한 센싱, 보호된 자원, 고전 제어 폴백 및 안전 상태 메커니즘과 결합함으로써 물리 인공지능은 안전한 물리적 제어를 즉시 상실하지 않으면서 지능 수준을 단계적으로 낮출 수 있다.

##  

## 06.08. Sensor Failure and Perception Fallback

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Sensor failure is a critical concern in Physical AI because autonomous behavior depends on continuous and trustworthy observation of the physical environment. Cameras, LiDAR, radar, ultrasonic sensors, GNSS, IMUs, encoders, force sensors, and tactile devices can fail completely or degrade gradually. Perception fallback ensures that loss of one sensing capability does not immediately produce uncontrolled or unjustified autonomous behavior.

Sensor faults include more than complete signal loss. A device may continue transmitting data while suffering from drift, calibration errors, contamination, saturation, occlusion, synchronization problems, packet corruption, reduced field of view, or environmental interference. Such failures are especially dangerous because downstream AI models may process apparently valid measurements without recognizing that the physical information represented by those measurements has become unreliable.

Runtime sensor-health monitoring should therefore evaluate both device availability and measurement quality. Diagnostics may examine timestamps, update rates, signal statistics, calibration consistency, temperature, internal error codes, communication integrity, and agreement with other sensors. Temporal monitoring is also important because gradual deterioration can be detected through trends before the sensor crosses a hard failure threshold or begins significantly affecting autonomous behavior.

Cross-modal consistency provides another important mechanism for detecting perception degradation. Camera detections can be compared with LiDAR geometry, radar motion estimates, map constraints, inertial measurements, or expected object dynamics. Persistent disagreement does not automatically identify which sensor is faulty, but it provides evidence that the perception system should reduce confidence, isolate suspicious information sources, and restrict autonomy until reliability is restored.

Perception fallback begins by determining which sensing capabilities remain trustworthy after a fault. If one camera fails in a multi-camera configuration, neighboring cameras may preserve partial visual coverage. If visual perception becomes unreliable because of darkness or glare, LiDAR or radar may continue supporting obstacle detection. If GNSS becomes unavailable, inertial sensing, wheel odometry, visual odometry, or map-based localization may temporarily preserve state estimation.

Effective fallback requires sensor diversity rather than simple duplication. Two identical cameras mounted together may experience the same glare, contamination, vibration, or environmental obstruction. Similarly, redundant GNSS receivers may share the same satellite visibility problem. Combining sensing principles with different physical failure characteristics can reduce common-cause failures and provide more meaningful redundancy for safety-critical perception.

The fallback perception function does not necessarily need to reproduce the full capability of the primary perception system. A backup path may detect only obstacles, free space, lane boundaries, ground geometry, or basic motion while advanced semantic recognition is disabled. This reduced perception can still support controlled deceleration, restricted navigation, collision avoidance, or movement toward a Minimum Risk Condition when complex autonomous behavior can no longer be justified.

Behavior must be adapted to the reduced sensing envelope. If long-range perception is lost, maximum speed should decrease so that stopping distance remains within reliable observation range. If side or rear coverage becomes unavailable, turning and reversing may be prohibited. Reduced depth accuracy may require larger obstacle margins, while uncertain object classification may cause the system to treat ambiguous objects conservatively rather than relying on semantic interpretation.

Sensor failure can also affect localization and world-model consistency even when obstacle perception remains available. Loss of GNSS, visual landmarks, LiDAR features, or inertial accuracy may increase uncertainty in robot pose and predicted environmental state. The system should track this uncertainty explicitly and limit travel distance, route complexity, planning horizon, or allowable speed as state-estimation confidence deteriorates.

AI perception models introduce another layer of failure because the sensors themselves may remain healthy while learned interpretation becomes unreliable. Distribution shift, unusual weather, unfamiliar objects, image artifacts, adversarial environmental patterns, or conditions outside the validated domain can degrade perception without producing hardware alarms. Monitoring should therefore distinguish sensor health from perception-model validity and provide fallback paths for both categories of failure.

Independent safety perception can provide a protective layer beneath high-performance AI perception. A sophisticated neural perception stack may perform semantic scene understanding, while a simpler geometric or deterministic function monitors minimum obstacle distance, free space, collision boundaries, or emergency stopping zones. If AI perception becomes uncertain or inconsistent, the independent safety path can constrain motion even when it cannot provide complete environmental understanding.

Sensor isolation should prevent corrupted measurements from contaminating fused estimates. Once a sensor is identified as unreliable, its contribution to localization, tracking, mapping, world modeling, or planning may need to be reduced or removed. Fusion algorithms should support dynamic weighting and exclusion so that a faulty measurement source does not continue influencing the system merely because it remains electrically connected and produces syntactically valid data.

Transitioning to fallback perception requires careful management of internal state. Object tracks, occupancy maps, localization estimates, temporal histories, and world-model representations may have been constructed using the failed sensor. The system must determine which state remains valid, which uncertainty should be increased, and which information must be reconstructed. Continuing to trust stale derived information can defeat the purpose of isolating the original sensor fault.

If remaining sensors cannot support sufficient perception, the system should progressively restrict physical behavior rather than attempting to maintain normal autonomy. The sequence may move from reduced-speed operation to route restrictions, limited maneuvering, deterministic collision avoidance, controlled stopping, or a Minimum Risk Maneuver. The appropriate escalation depends on the environment, robot dynamics, remaining sensing coverage, and consequences of continued movement.

Recovery requires more than detecting that a failed sensor has started producing data again. Calibration, timing, signal quality, cross-sensor consistency, environmental visibility, and downstream perception outputs should be verified before the sensor regains full authority. A recovered sensor may initially operate in observation or shadow mode while its measurements are compared with trusted sources before being reintegrated into fused perception and autonomous decision making.

Sensor failure and perception fallback ultimately transform sensing redundancy into behavioral resilience. The objective is not simply to keep perception software running, but to maintain a justified relationship between what the robot can reliably observe and what it is permitted to do. By combining health monitoring, sensor diversity, fault isolation, independent safety perception, restricted operation, and verified recovery, Physical AI can degrade safely as environmental awareness is progressively reduced.

센서 고장(sensor failure)은 자율 행동(autonomous behavior)이 물리적 환경에 대한 지속적이고 신뢰할 수 있는 관측에 의존하기 때문에 물리 인공지능(Physical AI)에서 매우 중요한 문제이다. 카메라, 라이다(LiDAR), 레이더(radar), 초음파 센서(ultrasonic sensor), 위성항법시스템(GNSS), 관성측정장치(IMU), 엔코더(encoder), 힘 센서(force sensor), 촉각 장치(tactile device)는 완전히 고장 나거나 점진적으로 성능이 저하될 수 있다. 인지 폴백(perception fallback)은 하나의 센싱 기능이 상실되더라도 즉시 통제되지 않거나 정당화할 수 없는 자율 행동으로 이어지지 않도록 한다.

센서 결함(sensor fault)은 단순한 신호의 완전한 손실보다 훨씬 다양한 형태를 포함한다. 장치는 계속 데이터를 전송하면서도 드리프트(drift), 보정 오류(calibration error), 오염(contamination), 포화(saturation), 가림(occlusion), 동기화 문제, 패킷 손상(packet corruption), 시야각 감소 또는 환경적 간섭(environmental interference)을 겪을 수 있다. 이러한 고장은 하위 AI 모델이 물리적 정보를 나타내는 측정값의 신뢰성이 이미 저하되었다는 사실을 인식하지 못한 채 겉보기에는 정상적인 데이터를 처리할 수 있기 때문에 특히 위험하다.

따라서 런타임 센서 상태 모니터링(runtime sensor-health monitoring)은 장치의 가용성뿐만 아니라 측정 품질(measurement quality)까지 평가해야 한다. 진단 과정에서는 타임스탬프(timestamp), 갱신 주기, 신호 통계, 보정 일관성(calibration consistency), 온도, 내부 오류 코드, 통신 무결성(communication integrity), 다른 센서와의 일치성을 검사할 수 있다. 또한 점진적인 성능 저하는 센서가 명확한 고장 임계값을 넘거나 자율 행동에 심각한 영향을 미치기 전에 추세를 통해 탐지할 수 있으므로 시간적 모니터링(temporal monitoring)도 중요하다.

교차 모달 일관성(cross-modal consistency)은 인지 성능 저하를 탐지하는 또 다른 중요한 메커니즘을 제공한다. 카메라 탐지 결과를 라이다 기하 정보(LiDAR geometry), 레이더 움직임 추정, 지도 제약조건(map constraint), 관성 측정값 또는 예상되는 객체 동역학(object dynamics)과 비교할 수 있다. 지속적인 불일치가 어느 센서에 결함이 있는지를 자동으로 결정하는 것은 아니지만, 인지 시스템이 신뢰도를 낮추고 의심스러운 정보원을 격리하며 신뢰성이 복원될 때까지 자율성을 제한해야 한다는 근거를 제공한다.

인지 폴백은 결함 발생 이후 어떤 센싱 기능이 여전히 신뢰할 수 있는지를 판단하는 것에서 시작한다. 다중 카메라 구성에서 하나의 카메라가 고장 나면 인접한 카메라가 부분적인 시각 범위를 유지할 수 있다. 어둠이나 눈부심으로 시각 인지(visual perception)의 신뢰성이 저하되더라도 라이다나 레이더는 장애물 탐지를 계속 지원할 수 있다. GNSS를 사용할 수 없게 되면 관성 센싱, 휠 오도메트리(wheel odometry), 비주얼 오도메트리(visual odometry) 또는 지도 기반 위치추정(map-based localization)이 일시적으로 상태 추정(state estimation)을 유지할 수 있다.

효과적인 폴백에는 단순한 센서 복제가 아니라 센서 다양성(sensor diversity)이 필요하다. 동일한 위치에 장착된 두 개의 동일한 카메라는 같은 눈부심, 오염, 진동 또는 환경적 가림의 영향을 동시에 받을 수 있다. 마찬가지로 중복된 GNSS 수신기도 동일한 위성 가시성 문제를 공유할 수 있다. 서로 다른 물리적 고장 특성을 가진 센싱 원리(sensing principle)를 결합하면 공통 원인 고장(common-cause failure)을 줄이고 안전 필수 인지(safety-critical perception)에 보다 의미 있는 중복성을 제공할 수 있다.

폴백 인지 기능(fallback perception function)이 반드시 주 인지 시스템의 전체 기능을 재현해야 하는 것은 아니다. 백업 경로는 고급 의미론적 인식(semantic recognition)을 비활성화하면서 장애물, 자유 공간(free space), 차선 경계, 지면 형상 또는 기본적인 움직임만 탐지할 수 있다. 이러한 축소된 인지 기능도 복잡한 자율 행동을 더 이상 정당화할 수 없는 상황에서 제어된 감속, 제한된 내비게이션, 충돌 회피 또는 최소 위험 상태(Minimum Risk Condition)로의 이동을 지원할 수 있다.

로봇의 행동은 감소된 센싱 영역(reduced sensing envelope)에 맞추어 조정되어야 한다. 장거리 인지 기능을 상실하면 정지 거리가 신뢰 가능한 관측 범위 안에 유지되도록 최대 속도를 낮춰야 한다. 측면이나 후방의 센싱 범위를 상실하면 방향 전환이나 후진을 금지할 수 있다. 깊이 정확도가 저하되면 장애물 안전 여유(obstacle margin)를 확대해야 하며, 객체 분류가 불확실하면 의미론적 해석에 의존하기보다 모호한 객체를 보수적으로 처리해야 한다.

센서 고장은 장애물 인지가 유지되는 상황에서도 위치추정(localization)과 월드 모델 일관성(world-model consistency)에 영향을 줄 수 있다. GNSS, 시각 랜드마크(visual landmark), 라이다 특징(LiDAR feature) 또는 관성 정확도를 상실하면 로봇 자세와 예측된 환경 상태에 대한 불확실성이 증가할 수 있다. 시스템은 이러한 불확실성을 명시적으로 추적하고 상태 추정의 신뢰도가 저하됨에 따라 이동 거리, 경로 복잡도, 계획 범위(planning horizon) 또는 허용 속도를 제한해야 한다.

AI 인지 모델(AI perception model)은 센서 자체가 정상인 상태에서도 학습 기반 해석이 신뢰할 수 없게 될 수 있기 때문에 또 다른 고장 계층을 발생시킨다. 분포 변화(distribution shift), 비정상적인 기상 조건, 익숙하지 않은 객체, 이미지 아티팩트(image artifact), 적대적 환경 패턴(adversarial environmental pattern) 또는 검증된 영역 밖의 조건은 하드웨어 경보를 발생시키지 않으면서 인지 성능을 저하시킬 수 있다. 따라서 모니터링은 센서 상태(sensor health)와 인지 모델 유효성(perception-model validity)을 구분하고 두 종류의 고장 모두에 대해 폴백 경로를 제공해야 한다.

독립 안전 인지(independent safety perception)는 고성능 AI 인지 아래에서 보호 계층(protective layer)을 제공할 수 있다. 정교한 신경망 기반 인지 스택(neural perception stack)이 의미론적 장면 이해를 수행하는 동안 보다 단순한 기하학적 또는 결정론적 기능이 최소 장애물 거리, 자유 공간, 충돌 경계 또는 비상 정지 영역(emergency stopping zone)을 감시할 수 있다. AI 인지가 불확실하거나 일관성을 상실하면 독립 안전 경로는 완전한 환경 이해를 제공하지 못하더라도 로봇의 움직임을 제한할 수 있다.

센서 격리(sensor isolation)는 손상된 측정값이 융합된 추정 결과(fused estimate)를 오염시키는 것을 방지해야 한다. 센서가 신뢰할 수 없는 것으로 판단되면 위치추정, 추적, 매핑(mapping), 월드 모델링(world modeling) 또는 계획에 대한 해당 센서의 기여도를 줄이거나 완전히 제거해야 할 수 있다. 센서가 전기적으로 연결되어 있고 형식적으로 유효한 데이터를 생성한다는 이유만으로 결함 측정값이 계속 시스템에 영향을 미치지 않도록 센서 융합 알고리즘(sensor fusion algorithm)은 동적 가중치 조정(dynamic weighting)과 제외 기능을 지원해야 한다.

폴백 인지로 전환할 때는 내부 상태(internal state)를 신중하게 관리해야 한다. 객체 추적 정보(object track), 점유 지도(occupancy map), 위치추정 결과, 시간적 이력(temporal history), 월드 모델 표현은 고장 난 센서를 이용하여 생성되었을 수 있다. 시스템은 어떤 상태가 여전히 유효한지, 어떤 정보의 불확실성을 증가시켜야 하는지, 어떤 정보를 다시 구축해야 하는지를 판단해야 한다. 오래되어 유효하지 않은 파생 정보(stale derived information)를 계속 신뢰한다면 원래의 센서 결함을 격리하는 목적 자체가 무효화될 수 있다.

남아 있는 센서만으로 충분한 인지를 지원할 수 없다면 시스템은 정상적인 자율성을 유지하려 하기보다 물리적 행동을 점진적으로 제한해야 한다. 이러한 과정은 감속 운용에서 시작하여 경로 제한, 제한된 기동, 결정론적 충돌 회피(deterministic collision avoidance), 제어된 정지 또는 최소 위험 기동(Minimum Risk Maneuver)으로 단계적으로 전환될 수 있다. 적절한 단계 상승(escalation)은 환경, 로봇 동역학, 남아 있는 센싱 범위 및 지속적인 움직임으로 인해 발생할 수 있는 결과에 따라 결정된다.

복구(recovery)는 고장 난 센서가 다시 데이터를 생성하기 시작했다는 사실을 탐지하는 것만으로 완료되지 않는다. 센서에 완전한 권한을 다시 부여하기 전에 보정 상태, 타이밍, 신호 품질, 센서 간 일관성, 환경 가시성(environmental visibility), 하위 인지 출력이 검증되어야 한다. 복구된 센서는 신뢰 가능한 정보원과 측정값을 비교하는 관측 모드(observation mode) 또는 섀도 모드(shadow mode)로 먼저 작동한 후 융합 인지와 자율 의사결정 과정에 다시 통합될 수 있다.

궁극적으로 센서 고장 및 인지 폴백(sensor failure and perception fallback)은 센싱 중복성(sensing redundancy)을 행동 회복탄력성(behavioral resilience)으로 전환한다. 목적은 단순히 인지 소프트웨어를 계속 실행하는 것이 아니라 로봇이 신뢰성 있게 관측할 수 있는 범위와 실제로 허용되는 행동 사이에 정당화 가능한 관계를 유지하는 것이다. 상태 모니터링, 센서 다양성, 결함 격리, 독립 안전 인지, 제한 운용 및 검증된 복구를 결합함으로써 물리 인공지능은 환경 인식 능력이 점진적으로 감소하는 상황에서도 안전하게 성능을 저하시킬 수 있다.

##  

## 06.09. Localization and Navigation Fallback

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Localization and navigation fallback defines how a Physical AI system preserves safe mobility when its primary ability to estimate position, orientation, motion, or navigable space becomes unreliable. Because autonomous movement depends on knowing both where the robot is and how it can move through the environment, localization degradation can rapidly invalidate planning assumptions. Fallback therefore links state-estimation confidence directly to permitted navigation behavior.

Localization failure is not limited to complete loss of position. A system may continue producing poses while accumulating drift, jumping between hypotheses, using stale map information, or becoming inconsistent with physical observations. GNSS multipath, visual feature loss, LiDAR degradation, wheel slip, IMU bias, map changes, synchronization errors, and calibration faults can all reduce localization integrity without immediately causing an explicit failure signal.

Runtime monitoring should evaluate localization quality as well as availability. Relevant evidence includes covariance, innovation residuals, map-matching quality, sensor agreement, pose continuity, update rate, timestamp freshness, trajectory consistency, and physically plausible motion. Sudden jumps or gradually increasing uncertainty should trigger investigation before the navigation system continues to build plans around a state estimate that no longer represents the robot reliably.

Localization fallback begins by identifying which independent sources remain trustworthy. Loss of GNSS may permit continued operation using visual-inertial odometry, LiDAR localization, wheel odometry, IMU integration, or map constraints. Failure of visual localization may be compensated by LiDAR or radar-based methods. The objective is not necessarily to preserve the original accuracy, but to maintain enough state knowledge for a reduced and explicitly bounded form of mobility.

Fallback localization should account for uncertainty accumulation. Dead reckoning can maintain short-term motion estimates after an absolute reference disappears, but error normally grows with distance and time. Rather than treating the fallback estimate as indefinitely valid, the system should track uncertainty and progressively restrict speed, travel distance, route complexity, turning behavior, and planning horizon as confidence decreases.

Navigation behavior must be adapted to the quality of localization that remains. High-precision autonomous navigation may require centimeter-level positioning, while degraded operation may only support corridor following, lane keeping, landmark-to-landmark movement, or travel along a previously verified route. When precise global position is unavailable, the robot may temporarily rely on local obstacle avoidance and relative motion instead of attempting complex global replanning.

Map reliability is another important part of navigation fallback. A robot may be accurately localized against a map that no longer represents the physical environment because objects, walls, traffic patterns, construction zones, or traversable areas have changed. Runtime systems should therefore distinguish localization confidence from map confidence. Strong pose estimates do not justify navigation when the underlying environmental representation has become invalid.

A robust architecture can maintain multiple navigation representations at different levels of dependency. Global route planning may rely on maps and absolute localization, while local navigation can use nearby geometry, free-space estimates, obstacle detection, and short-horizon trajectories. If global localization fails but local perception remains trustworthy, the robot may suspend mission-level navigation while preserving enough local control to stop safely or move toward a nearby low-risk location.

Navigation fallback should also separate AI-dependent planning from deterministic mobility functions. A learned planner or world model may normally select sophisticated routes and predict interactions, while a classical local planner, trajectory tracker, or reactive obstacle-avoidance layer preserves basic controllability. When AI planning becomes unreliable, the system can reduce semantic reasoning and continue only with movements that satisfy explicit geometric, dynamic, and safety constraints.

Route restrictions provide a practical mechanism for degraded navigation. The robot may prohibit exploration, narrow passages, intersections, reversing, high-speed segments, unstructured terrain, or areas requiring precise localization. Instead, it can remain on known corridors, follow predefined waypoints, return along a recently verified path, move toward a localization recovery zone, or approach a designated stopping area where uncertainty creates less physical risk.

Relocalization can be attempted while the robot remains in a restricted operating mode. The system may search for known visual landmarks, LiDAR features, fiducial markers, GNSS visibility, map correspondences, or other absolute references. Motion used for relocalization must itself remain safe; aggressive exploratory movement should not be justified merely to improve localization when the robot already has insufficient confidence about its physical state.

Navigation fallback must consider dynamic obstacles and changing environments independently of localization. Even if approximate position remains available, reduced perception or prediction capability may make continued movement unsafe around people, vehicles, or machinery. Localization confidence, perception coverage, obstacle dynamics, stopping capability, and route geometry should therefore be evaluated together when deciding whether restricted navigation remains acceptable.

If uncertainty exceeds the limits required for controlled mobility, the system should transition toward a Minimum Risk Maneuver rather than continuing navigation indefinitely. Depending on context, this may involve controlled deceleration, moving out of an intersection, reaching the side of a route, stopping in a clear area, or maintaining a stable pose. The selected maneuver should require only capabilities that remain demonstrably trustworthy after the localization failure.

Recovery requires more than obtaining a new position estimate. The recovered localization system should demonstrate temporal stability, consistency across sensors, acceptable uncertainty, agreement with map features, and plausible continuity with the robot\'s physical motion. Navigation plans created using uncertain or stale state information may also need to be discarded and regenerated before normal autonomous movement is restored.

A staged recovery can reduce the risk of immediately returning to unrestricted navigation. The recovered estimator may first operate in parallel with the active fallback source, allowing the system to compare trajectories and confidence over time. Once localization has remained stable and environmental assumptions have been revalidated, route restrictions can be progressively removed and planning authority can return to the primary navigation architecture.

Localization and navigation fallback ultimately preserve the relationship between positional knowledge and authorized motion. As confidence in the robot\'s state decreases, the complexity and freedom of movement should decrease with it. By combining diverse localization sources, explicit uncertainty tracking, local navigation, deterministic fallback, route restrictions, relocalization, Minimum Risk Maneuvers, and verified recovery, Physical AI can lose navigational precision without immediately losing safe physical controllability.

위치추정 및 내비게이션 폴백(localization and navigation fallback)은 위치, 방향, 움직임 또는 주행 가능 공간을 추정하는 주 기능의 신뢰성이 저하되었을 때 물리 인공지능(Physical AI) 시스템이 안전한 이동성을 유지하는 방법을 정의한다. 자율 이동은 로봇이 현재 어디에 있는지와 환경을 통해 어떻게 이동할 수 있는지를 모두 알아야 하므로 위치추정 성능 저하는 계획 가정(planning assumption)을 빠르게 무효화할 수 있다. 따라서 폴백은 상태 추정 신뢰도(state-estimation confidence)를 허용되는 내비게이션 행동과 직접 연결한다.

위치추정 고장(localization failure)은 위치 정보를 완전히 상실하는 경우에만 한정되지 않는다. 시스템은 위치와 자세(pose)를 계속 출력하면서도 드리프트(drift)가 누적되거나, 여러 가설 사이에서 위치가 급격하게 변경되거나, 오래된 지도 정보를 사용하거나, 실제 물리적 관측과 불일치할 수 있다. GNSS 다중경로(GNSS multipath), 시각 특징 손실, 라이다 성능 저하, 휠 슬립(wheel slip), IMU 바이어스(IMU bias), 지도 변화, 동기화 오류 및 보정 결함은 명확한 고장 신호를 즉시 발생시키지 않으면서 위치추정 무결성(localization integrity)을 저하시킬 수 있다.

런타임 모니터링(runtime monitoring)은 위치추정의 가용성뿐만 아니라 품질도 평가해야 한다. 관련 증거에는 공분산(covariance), 혁신 잔차(innovation residual), 지도 정합 품질(map-matching quality), 센서 간 일치성, 자세 연속성(pose continuity), 갱신 주기, 타임스탬프 최신성(timestamp freshness), 궤적 일관성 및 물리적으로 타당한 움직임이 포함된다. 갑작스러운 위치 변화나 점진적으로 증가하는 불확실성은 내비게이션 시스템이 더 이상 로봇의 실제 상태를 신뢰성 있게 나타내지 못하는 상태 추정값을 기반으로 계획을 계속 생성하기 전에 조사되어야 한다.

위치추정 폴백(localization fallback)은 어떤 독립적인 정보원이 여전히 신뢰 가능한지를 식별하는 것에서 시작한다. GNSS를 상실하더라도 시각-관성 오도메트리(visual-inertial odometry), 라이다 위치추정(LiDAR localization), 휠 오도메트리(wheel odometry), IMU 적분(IMU integration) 또는 지도 제약조건을 사용하여 운용을 계속할 수 있다. 시각 위치추정이 실패하면 라이다 또는 레이더 기반 방법으로 보완할 수 있다. 목적은 반드시 기존 정확도를 유지하는 것이 아니라 제한되고 명확하게 경계가 설정된 이동성을 지원하기에 충분한 상태 정보를 유지하는 것이다.

폴백 위치추정은 불확실성 누적(uncertainty accumulation)을 고려해야 한다. 추측 항법(dead reckoning)은 절대 위치 기준을 상실한 이후 단기간 동안 움직임 추정을 유지할 수 있지만, 일반적으로 이동 거리와 시간이 증가함에 따라 오차도 증가한다. 시스템은 폴백 추정값을 무기한 유효한 것으로 간주하지 않고 불확실성을 지속적으로 추적하며, 신뢰도가 감소함에 따라 속도, 이동 거리, 경로 복잡도, 회전 행동 및 계획 범위(planning horizon)를 점진적으로 제한해야 한다.

내비게이션 행동은 남아 있는 위치추정 품질에 맞추어 조정되어야 한다. 고정밀 자율 내비게이션에는 센티미터 수준의 위치 정확도가 필요할 수 있지만, 성능 저하 운용(degraded operation)에서는 복도 추종(corridor following), 차선 유지(lane keeping), 랜드마크 간 이동 또는 이전에 검증된 경로를 따라가는 정도만 지원할 수 있다. 정밀한 전역 위치(global position)를 사용할 수 없다면 복잡한 전역 재계획(global replanning)을 시도하는 대신 일시적으로 로컬 장애물 회피와 상대적 움직임(relative motion)에 의존할 수 있다.

지도 신뢰성(map reliability) 역시 내비게이션 폴백의 중요한 부분이다. 로봇이 정확하게 위치추정되어 있더라도 객체, 벽, 교통 패턴, 공사 구역 또는 주행 가능 영역이 변경되어 지도가 실제 물리적 환경을 더 이상 나타내지 못할 수 있다. 따라서 런타임 시스템은 위치추정 신뢰도(localization confidence)와 지도 신뢰도(map confidence)를 구분해야 한다. 정확한 자세 추정값을 확보하고 있더라도 기반 환경 표현(environmental representation)이 유효하지 않다면 안전한 내비게이션을 정당화할 수 없다.

견고한 아키텍처(robust architecture)는 의존 수준이 서로 다른 여러 내비게이션 표현(navigation representation)을 유지할 수 있다. 전역 경로 계획(global route planning)은 지도와 절대 위치추정에 의존하는 반면, 로컬 내비게이션(local navigation)은 주변 기하 정보, 자유 공간 추정(free-space estimation), 장애물 탐지 및 단기 궤적(short-horizon trajectory)을 사용할 수 있다. 전역 위치추정이 실패하더라도 로컬 인지가 신뢰 가능하다면 임무 수준 내비게이션을 중단하면서 안전하게 정지하거나 가까운 저위험 위치로 이동할 수 있는 충분한 로컬 제어를 유지할 수 있다.

내비게이션 폴백은 AI 의존형 계획(AI-dependent planning)과 결정론적 이동 기능(deterministic mobility function)도 분리해야 한다. 학습 기반 플래너(learned planner)나 월드 모델(world model)이 정상적으로 정교한 경로를 선택하고 상호작용을 예측할 수 있는 반면, 고전적 로컬 플래너(classical local planner), 궤적 추종기(trajectory tracker) 또는 반응형 장애물 회피 계층(reactive obstacle-avoidance layer)은 기본적인 제어 가능성을 유지한다. AI 계획의 신뢰성이 저하되면 의미론적 추론을 축소하고 명시적인 기하학적, 동역학적 및 안전 제약조건을 만족하는 움직임만 계속 수행할 수 있다.

경로 제한(route restriction)은 성능 저하 내비게이션을 구현하는 실질적인 메커니즘을 제공한다. 로봇은 탐색(exploration), 좁은 통로, 교차로, 후진, 고속 구간, 비정형 지형(unstructured terrain) 또는 정밀한 위치추정이 필요한 영역의 진입을 금지할 수 있다. 대신 알려진 통로에 머물거나 사전 정의된 웨이포인트(waypoint)를 따라가고, 최근 검증된 경로를 통해 복귀하거나, 위치추정 복구 구역(localization recovery zone) 또는 불확실성으로 인한 물리적 위험이 상대적으로 낮은 지정 정지 구역으로 이동할 수 있다.

로봇이 제한된 운용 모드(restricted operating mode)에 있는 동안 재위치추정(relocalization)을 시도할 수 있다. 시스템은 알려진 시각 랜드마크, 라이다 특징, 기준 마커(fiducial marker), GNSS 가시성, 지도 대응 관계(map correspondence) 또는 다른 절대 위치 기준을 탐색할 수 있다. 그러나 재위치추정을 위해 수행되는 움직임 자체도 안전해야 한다. 로봇이 이미 자신의 물리적 상태에 대해 충분한 신뢰도를 확보하지 못한 상황에서 위치추정을 개선하기 위한 목적으로 공격적인 탐색 움직임을 정당화해서는 안 된다.

내비게이션 폴백은 위치추정과 별개로 동적 장애물(dynamic obstacle)과 변화하는 환경도 고려해야 한다. 대략적인 위치를 계속 파악할 수 있더라도 인지 또는 예측 능력이 저하되면 사람, 차량 또는 기계 장비 주변에서 이동을 계속하는 것이 안전하지 않을 수 있다. 따라서 제한된 내비게이션의 지속 가능 여부를 결정할 때 위치추정 신뢰도, 인지 범위(perception coverage), 장애물 동역학, 정지 능력 및 경로 기하(route geometry)를 함께 평가해야 한다.

불확실성이 제어된 이동에 필요한 한계를 초과하면 시스템은 내비게이션을 무기한 지속하는 대신 최소 위험 기동(Minimum Risk Maneuver)으로 전환해야 한다. 상황에 따라 제어된 감속, 교차로에서 벗어나기, 이동 경로의 측면으로 이동하기, 장애물이 없는 구역에서 정지하기 또는 안정적인 자세 유지가 포함될 수 있다. 선택된 기동은 위치추정 고장 이후에도 신뢰할 수 있음이 입증된 기능만을 이용하여 수행할 수 있어야 한다.

복구(recovery)는 단순히 새로운 위치 추정값을 획득하는 것만으로 완료되지 않는다. 복구된 위치추정 시스템은 시간적 안정성(temporal stability), 센서 간 일관성, 허용 가능한 불확실성, 지도 특징과의 일치 및 로봇의 실제 물리적 움직임과 타당한 연속성을 입증해야 한다. 불확실하거나 오래된 상태 정보를 기반으로 생성된 내비게이션 계획 역시 정상적인 자율 이동을 복원하기 전에 폐기하고 새롭게 생성해야 할 수 있다.

단계적 복구(staged recovery)는 제한 없는 내비게이션으로 즉시 복귀할 때 발생할 수 있는 위험을 줄일 수 있다. 복구된 추정기(estimator)를 현재 활성화된 폴백 정보원과 병렬로 먼저 운용하여 일정 시간 동안 궤적과 신뢰도를 비교할 수 있다. 위치추정이 안정적으로 유지되고 환경에 대한 가정이 다시 검증된 이후 경로 제한을 단계적으로 제거하고 계획 권한(planning authority)을 주 내비게이션 아키텍처(primary navigation architecture)로 복원할 수 있다.

궁극적으로 위치추정 및 내비게이션 폴백(localization and navigation fallback)은 로봇이 자신의 위치를 얼마나 정확하게 알고 있는지와 어느 정도의 움직임이 허용되는지 사이의 관계를 유지한다. 로봇 상태에 대한 신뢰도가 감소할수록 움직임의 복잡성과 자유도 역시 함께 감소해야 한다. 다양한 위치추정 정보원, 명시적 불확실성 추적, 로컬 내비게이션, 결정론적 폴백, 경로 제한, 재위치추정, 최소 위험 기동 및 검증된 복구를 결합함으로써 물리 인공지능은 내비게이션 정밀도를 상실하더라도 안전한 물리적 제어 가능성을 즉시 상실하지 않도록 설계할 수 있다.

##  

## 06.10. Communication and Cloud Loss Fallback

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Communication and cloud loss fallback defines how a Physical AI system maintains safe and predictable operation when connectivity to remote services, fleet infrastructure, edge servers, on-premise computing, or cloud intelligence becomes unavailable or unreliable. Because physical safety cannot depend on continuous network availability, essential sensing, stabilization, collision avoidance, control, and fallback functions should remain executable locally whenever their loss could create unacceptable physical risk.

Communication failure is broader than complete disconnection. Networks may experience increased latency, jitter, packet loss, reduced bandwidth, intermittent connectivity, duplicated messages, out-of-order delivery, or stale information while technically remaining connected. These degraded conditions can be more difficult to manage than an obvious outage because remote commands, shared maps, predictions, or coordination data may arrive late enough to become inconsistent with the current physical environment.

Runtime monitoring should therefore evaluate communication quality rather than relying only on a connected or disconnected state. Relevant indicators include round-trip latency, packet-loss rate, message age, heartbeat status, bandwidth, synchronization quality, retransmission frequency, sequence continuity, and command acknowledgment. The system should detect trends toward degradation early enough to reduce dependence on remote functions before communication becomes unusable.

A distributed Physical AI architecture should explicitly classify functions according to their dependence on communication. Safety-critical control loops generally require local execution, while remote systems may provide mission planning, fleet optimization, shared world models, semantic reasoning, large-model inference, long-term memory, software services, or global coordination. This separation establishes which capabilities must survive locally and which capabilities may be temporarily suspended during connectivity loss.

Local autonomy forms the primary defense against communication failure. The robot should preserve enough onboard perception, localization, state estimation, planning, and control to remain physically safe without immediate remote assistance. The required level of local autonomy depends on the platform and environment, but communication loss should never leave actuators uncontrolled or force the robot to wait indefinitely for a remote decision while continuing hazardous motion.

Cloud-dependent AI functions require particularly careful fallback design. A robot may normally use remote foundation models, large Vision-Language-Action models, computationally intensive world models, or cloud-based reasoning services that cannot be replicated fully onboard. When connectivity is lost, the architecture can switch to smaller local models, cached policies, deterministic planners, predefined behaviors, or classical control while reducing the complexity of tasks that the robot is permitted to perform.

Loss of communication should therefore trigger capability degradation rather than automatically reproducing normal operation with incomplete information. Cooperative planning, remote supervision, shared-map updates, fleet-wide optimization, cloud reasoning, and tasks requiring current external knowledge may be suspended. The robot can continue only those activities whose required information and control authority remain locally available and sufficiently trustworthy.

Fleet and multi-robot systems introduce additional challenges because communication supports coordination among physically independent agents. When connectivity deteriorates, robots may lose shared intentions, reservations, trajectories, task assignments, or information about other agents. Fallback behavior should reduce interdependence by avoiding tightly coupled maneuvers, increasing separation, preserving local right-of-way rules, and preventing conflicting actions based on stale coordination data.

Information freshness is critical during partial network failure. A message can be syntactically valid and authenticated yet no longer describe the current world. Remote trajectories, obstacle states, map updates, task commands, or shared predictions should therefore include timestamps, sequence information, validity intervals, or expiration conditions. Once information becomes stale, the system should reject or downgrade it instead of continuing to act on outdated assumptions.

Command authority must also be protected during disconnection and reconnection. If a remote command is interrupted halfway through execution, the robot needs explicit rules defining whether to complete, cancel, hold, or replace the action. After connectivity returns, delayed commands should not suddenly regain authority without validation. Local and remote control states must be synchronized before higher-level command authority is restored.

Communication fallback can be hierarchical. The system may first switch from a primary network to a redundant communication channel, then continue with reduced bandwidth and lower update rates, followed by local autonomous operation if remote services remain unavailable. If local capability is insufficient for the environment or mission, the robot can progressively restrict motion and transition toward a Minimum Risk Maneuver or safe state.

Network redundancy is useful only when redundant channels do not share the same dominant failure mechanism. Multiple wireless links connected through the same access point, power source, gateway, or network provider may fail together. More resilient designs consider diversity across communication technologies, routing paths, infrastructure, power domains, and local processing so that loss of one dependency does not simultaneously remove every fallback path.

Local caching can preserve selected capabilities during temporary outages. Maps, mission constraints, safety zones, robot configuration, authorized task rules, compact models, and recently validated environmental information may be retained onboard. Cached information should have explicit validity conditions because old data can become hazardous when environments change. The system must know not only what information is available locally, but also how long it remains trustworthy.

Recovery from communication loss should be treated as a synchronization process rather than an immediate return to normal operation. The system may need to reconcile local state changes, completed actions, map modifications, task progress, robot positions, shared reservations, and remote commands generated during the outage. Conflicting information should be resolved before cloud or fleet systems resume authoritative control over physical behavior.

Reconnection should also include verification of communication quality. A briefly restored link may remain unstable, and rapid switching between connected and disconnected modes can produce oscillating control decisions. Persistence thresholds, hysteresis, minimum stability intervals, and staged restoration can ensure that remote functions regain authority only after the network has demonstrated sufficiently reliable performance.

Communication and cloud loss fallback ultimately establishes local safety sovereignty for Physical AI. Remote infrastructure can significantly enhance intelligence, coordination, memory, and computational capability, but it should not become a single point of failure for physical control. By combining local autonomy, communication monitoring, network diversity, cached information, degraded operation, explicit authority management, and controlled resynchronization, the system can safely reduce distributed intelligence while preserving essential physical controllability.

통신 및 클라우드 손실 폴백(communication and cloud loss fallback)은 원격 서비스, 플릿 인프라(fleet infrastructure), 엣지 서버(edge server), 온프레미스 컴퓨팅(on-premise computing) 또는 클라우드 지능(cloud intelligence)과의 연결을 사용할 수 없거나 신뢰할 수 없게 되었을 때 물리 인공지능(Physical AI) 시스템이 안전하고 예측 가능한 운용을 유지하는 방법을 정의한다. 물리적 안전은 지속적인 네트워크 가용성(network availability)에 의존해서는 안 되므로, 필수 센싱, 안정화, 충돌 회피, 제어 및 폴백 기능은 그 기능의 상실이 허용할 수 없는 물리적 위험을 발생시킬 수 있는 경우 가능한 한 로컬에서 실행될 수 있어야 한다.

통신 고장(communication failure)은 완전한 연결 단절보다 광범위한 개념이다. 네트워크는 기술적으로 연결된 상태를 유지하면서도 지연 증가, 지터(jitter), 패킷 손실(packet loss), 대역폭 감소, 간헐적인 연결, 메시지 중복, 순서가 뒤바뀐 전달 또는 오래된 정보(stale information)를 경험할 수 있다. 이러한 성능 저하 상태는 원격 명령, 공유 지도, 예측 또는 협조 데이터가 현재의 물리적 환경과 일치하지 않을 정도로 늦게 도착할 수 있기 때문에 명확한 통신 단절보다 관리하기 어려울 수 있다.

따라서 런타임 모니터링(runtime monitoring)은 단순히 연결 또는 연결 해제 상태에 의존하지 않고 통신 품질(communication quality)을 평가해야 한다. 관련 지표에는 왕복 지연시간(round-trip latency), 패킷 손실률, 메시지 경과 시간(message age), 하트비트 상태(heartbeat status), 대역폭, 동기화 품질, 재전송 빈도, 시퀀스 연속성(sequence continuity), 명령 승인(command acknowledgment)이 포함된다. 시스템은 통신이 완전히 사용할 수 없게 되기 전에 원격 기능에 대한 의존도를 줄일 수 있도록 성능 저하 추세를 조기에 탐지해야 한다.

분산 물리 인공지능 아키텍처(distributed Physical AI architecture)는 각 기능을 통신 의존성(communication dependency)에 따라 명확하게 분류해야 한다. 안전 필수 제어 루프(safety-critical control loop)는 일반적으로 로컬 실행이 필요하지만, 원격 시스템은 임무 계획, 플릿 최적화, 공유 월드 모델(shared world model), 의미론적 추론, 대규모 모델 추론, 장기 메모리(long-term memory), 소프트웨어 서비스 또는 전역 협조(global coordination)를 제공할 수 있다. 이러한 분리는 연결이 상실되었을 때 로컬에서 반드시 유지되어야 하는 기능과 일시적으로 중단할 수 있는 기능을 구분한다.

로컬 자율성(local autonomy)은 통신 고장에 대한 주요 방어 수단을 형성한다. 로봇은 즉각적인 원격 지원 없이도 물리적 안전을 유지할 수 있도록 충분한 온보드 인지(onboard perception), 위치추정(localization), 상태 추정(state estimation), 계획 및 제어 기능을 유지해야 한다. 필요한 로컬 자율성 수준은 플랫폼과 환경에 따라 달라지지만, 통신 손실로 인해 액추에이터가 제어되지 않거나 로봇이 위험한 움직임을 계속하면서 원격 결정을 무기한 기다리는 상황이 발생해서는 안 된다.

클라우드 의존형 AI 기능(cloud-dependent AI function)은 특히 신중한 폴백 설계가 필요하다. 로봇은 일반적으로 원격 파운데이션 모델(foundation model), 대규모 비전-언어-행동 모델(Vision-Language-Action model), 계산 집약적인 월드 모델(world model) 또는 온보드에서 완전히 복제할 수 없는 클라우드 기반 추론 서비스(cloud-based reasoning service)를 사용할 수 있다. 연결이 상실되면 아키텍처는 소형 로컬 모델, 캐시된 정책(cached policy), 결정론적 플래너(deterministic planner), 사전 정의된 행동 또는 고전 제어(classical control)로 전환하면서 로봇이 수행할 수 있는 작업의 복잡도를 낮출 수 있다.

따라서 통신 손실은 불완전한 정보를 이용하여 정상 운용을 그대로 재현하려 하기보다 기능 성능 저하(capability degradation)를 유발해야 한다. 협력 계획(cooperative planning), 원격 감독, 공유 지도 갱신, 플릿 전체 최적화, 클라우드 추론 및 최신 외부 정보가 필요한 작업은 중단될 수 있다. 로봇은 필요한 정보와 제어 권한(control authority)이 로컬에서 계속 이용 가능하고 충분히 신뢰할 수 있는 활동만 수행할 수 있다.

플릿 및 다중 로봇 시스템(fleet and multi-robot system)은 통신이 물리적으로 독립된 에이전트 사이의 협조를 지원하기 때문에 추가적인 문제를 발생시킨다. 연결 성능이 저하되면 로봇은 공유 의도(shared intention), 예약 정보(reservation), 궤적, 작업 할당 또는 다른 에이전트에 대한 정보를 상실할 수 있다. 폴백 행동은 긴밀하게 결합된 기동을 피하고, 로봇 간 이격거리를 확대하며, 로컬 우선 통행 규칙(local right-of-way rule)을 유지하고, 오래된 협조 데이터를 기반으로 상충하는 행동이 발생하지 않도록 하여 상호 의존성을 줄여야 한다.

부분적인 네트워크 고장 상황에서는 정보 최신성(information freshness)이 매우 중요하다. 메시지는 형식적으로 유효하고 인증되어 있더라도 현재의 세계 상태를 더 이상 나타내지 못할 수 있다. 따라서 원격 궤적, 장애물 상태, 지도 갱신, 작업 명령 또는 공유 예측에는 타임스탬프(timestamp), 시퀀스 정보, 유효 기간(validity interval) 또는 만료 조건(expiration condition)이 포함되어야 한다. 정보가 오래되면 시스템은 오래된 가정을 기반으로 계속 행동하는 대신 해당 정보를 거부하거나 신뢰 수준을 낮춰야 한다.

연결 단절과 재연결 과정에서도 명령 권한(command authority)을 보호해야 한다. 원격 명령의 실행 도중 통신이 중단되면 로봇은 해당 행동을 완료할 것인지, 취소할 것인지, 현재 상태를 유지할 것인지 또는 다른 행동으로 대체할 것인지를 결정하는 명확한 규칙을 가져야 한다. 연결이 복구된 이후에도 지연된 명령이 검증 없이 갑자기 제어 권한을 다시 획득해서는 안 된다. 상위 수준의 명령 권한을 복원하기 전에 로컬과 원격의 제어 상태를 동기화해야 한다.

통신 폴백(communication fallback)은 계층적으로 구성할 수 있다. 시스템은 먼저 주 네트워크에서 중복 통신 채널(redundant communication channel)로 전환하고, 이후 대역폭과 갱신 주기를 낮춘 상태로 운용을 계속할 수 있으며, 원격 서비스를 계속 사용할 수 없다면 로컬 자율 운용으로 전환할 수 있다. 로컬 기능이 환경이나 임무를 수행하기에 충분하지 않다면 로봇은 움직임을 단계적으로 제한하고 최소 위험 기동(Minimum Risk Maneuver) 또는 안전 상태(safe state)로 전환할 수 있다.

중복 네트워크 채널이 동일한 주요 고장 메커니즘을 공유하지 않을 때에만 네트워크 중복성(network redundancy)이 실질적인 의미를 갖는다. 동일한 액세스 포인트(access point), 전원, 게이트웨이 또는 네트워크 사업자를 사용하는 여러 무선 링크는 동시에 고장 날 수 있다. 보다 회복탄력적인 설계는 하나의 의존성 상실로 모든 폴백 경로가 동시에 제거되지 않도록 통신 기술, 라우팅 경로, 인프라, 전력 도메인(power domain), 로컬 처리 기능의 다양성을 고려한다.

로컬 캐싱(local caching)은 일시적인 통신 단절 동안 일부 기능을 유지할 수 있도록 한다. 지도, 임무 제약조건, 안전 구역, 로봇 구성 정보, 허가된 작업 규칙, 소형 모델 및 최근 검증된 환경 정보를 온보드에 보관할 수 있다. 그러나 환경이 변화하면 오래된 데이터가 위험해질 수 있으므로 캐시된 정보에는 명시적인 유효 조건(validity condition)이 필요하다. 시스템은 어떤 정보가 로컬에 존재하는지뿐만 아니라 해당 정보를 얼마 동안 신뢰할 수 있는지도 알고 있어야 한다.

통신 손실로부터의 복구(recovery)는 정상 운용으로 즉시 복귀하는 과정이 아니라 동기화 과정(synchronization process)으로 취급해야 한다. 시스템은 연결 단절 중 발생한 로컬 상태 변화, 완료된 행동, 지도 수정, 작업 진행 상태, 로봇 위치, 공유 예약 및 원격 명령을 조정해야 할 수 있다. 클라우드 또는 플릿 시스템이 물리적 행동에 대한 권한 있는 제어(authoritative control)를 다시 시작하기 전에 서로 충돌하는 정보를 해결해야 한다.

재연결(reconnection) 과정에는 통신 품질 검증도 포함되어야 한다. 잠시 복구된 연결이 계속 불안정할 수 있으며, 연결과 단절 상태 사이의 빠른 전환은 제어 의사결정의 진동(oscillation)을 발생시킬 수 있다. 지속성 임계값(persistence threshold), 히스테리시스(hysteresis), 최소 안정 시간(minimum stability interval), 단계적 복원(staged restoration)을 적용하면 네트워크가 충분히 신뢰할 수 있는 성능을 입증한 이후에만 원격 기능이 다시 제어 권한을 획득하도록 할 수 있다.

궁극적으로 통신 및 클라우드 손실 폴백(communication and cloud loss fallback)은 물리 인공지능을 위한 로컬 안전 주권(local safety sovereignty)을 확립한다. 원격 인프라는 지능, 협조, 메모리 및 계산 능력을 크게 향상시킬 수 있지만 물리적 제어의 단일 장애점(single point of failure)이 되어서는 안 된다. 로컬 자율성, 통신 모니터링, 네트워크 다양성, 캐시된 정보, 성능 저하 운용, 명시적인 권한 관리 및 제어된 재동기화를 결합함으로써 시스템은 필수적인 물리적 제어 가능성을 유지하면서 분산 지능(distributed intelligence)을 안전하게 축소할 수 있다.

##  

## 06.11. Compute Overload and Thermal Fallback

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

Compute overload occurs when a Physical AI system demands more processing capacity than its CPU, GPU, accelerator, memory, or communication architecture can reliably provide within required timing constraints. Thermal overload occurs when sustained computation or environmental heat pushes hardware beyond acceptable operating limits. Both conditions can degrade autonomy gradually before producing an obvious hardware failure, making controlled fallback essential.

In Physical AI, computational correctness includes timing as well as numerical accuracy. A perception model that produces an accurate result after its deadline may already be unsafe because the physical environment has changed. Delayed localization, world-model updates, trajectory prediction, planning, or control commands can create stale decisions. Runtime supervision must therefore treat excessive latency and missed deadlines as functional degradation rather than only performance problems.

Compute-health monitoring should observe processor utilization, accelerator load, memory consumption, queue depth, inference latency, scheduling delay, frame-processing rate, deadline misses, and resource contention. Thermal monitoring should additionally track device temperature, cooling performance, fan status, power consumption, clock frequency, and throttling events. Trends are important because gradual saturation can provide enough warning to activate fallback before critical services become unstable.

Resource saturation can propagate through the autonomy stack. A delayed perception pipeline can produce stale environmental observations, which then affect localization, world modeling, prediction, planning, and finally control. Memory pressure may cause unpredictable allocation delays or model eviction, while excessive accelerator contention can prevent safety-related inference from executing on time. Fallback design should therefore consider end-to-end computational dependency rather than monitoring individual processors in isolation.

Thermal degradation introduces a similar cascading effect. As temperature rises, hardware may reduce clock frequency or power limits to protect itself, decreasing available compute precisely when complex environmental conditions may require greater processing. If the autonomy architecture assumes fixed inference rates, thermal throttling can silently invalidate timing assumptions. Temperature should therefore be treated as an operational state variable that directly influences permitted AI workload and robot behavior.

A robust system should classify computational functions by criticality. Stabilization, emergency braking, safety monitoring, actuator control, essential state estimation, and minimum obstacle detection generally require stronger resource guarantees than semantic reasoning, large-model inference, detailed world modeling, logging, visualization, or mission optimization. Explicit prioritization allows nonessential workloads to be sacrificed before computational pressure affects functions required for physical safety.

Graceful compute degradation can begin by reducing workload rather than immediately terminating autonomy. The system may lower camera resolution, reduce perception frame rate, shorten prediction horizons, decrease world-model update frequency, simplify planning, disable optional neural networks, reduce logging, or suspend background optimization. These measures release resources while retaining a smaller set of functions necessary for controlled operation.

Model-level fallback provides another response to computational overload. A large foundation model, VLA model, perception network, or learned planner may be replaced by a smaller backup model with lower memory and inference requirements. The backup does not need to reproduce full intelligence. It may support only essential object detection, local navigation, short-horizon prediction, or restricted task execution while the robot operates inside a reduced operational envelope.

Compute isolation is particularly important for safety-critical functions. If mission AI, perception, planning, and safety supervision compete for the same accelerator without guaranteed scheduling, overload in one component can starve another. Reserved CPU cores, protected memory, independent safety processors, dedicated execution queues, priority scheduling, or separate compute domains can preserve essential control even when the primary AI compute environment becomes saturated.

Thermal fallback should combine computational and physical responses. Software can reduce model complexity, inference frequency, accelerator utilization, and nonessential workloads, while the robot may also lower speed, reduce actuator demand, avoid thermally stressful tasks, move toward a cooler environment, or pause operation. Cooling fans, pumps, airflow paths, heat sinks, and thermal interfaces become part of the safety-relevant architecture when continued computation depends on effective heat removal.

Power and thermal management are closely coupled. High accelerator utilization increases electrical consumption and heat generation, while reduced cooling efficiency can force additional throttling. The fallback controller should therefore consider available electrical power, battery condition, processor temperature, cooling capability, and required mission duration together. Preserving maximum AI performance until thermal shutdown is generally less desirable than reducing workload early and maintaining predictable control.

The system should define multiple degradation thresholds instead of relying on a single critical-temperature or utilization limit. An early warning level can remove optional workloads, a higher level can activate lightweight models and reduce robot performance, and a severe level can transfer control to deterministic fallback functions. If sufficient computational or thermal margin cannot be maintained, the system should execute a Minimum Risk Maneuver or transition to a safe state.

Deterministic classical control can provide the final computational fallback when high-capacity AI processing is no longer sustainable. Basic trajectory tracking, speed limiting, braking, predefined retreat behavior, or controlled stopping can often execute with significantly lower computational demand than complex learned autonomy. This enables the system to surrender semantic capability and mission performance while preserving the minimum computation necessary for physical controllability.

Fallback decisions should account for environmental complexity because identical compute degradation can create different risks in different situations. Reduced perception frequency may remain acceptable in a static, low-speed area but become unacceptable near people, vehicles, intersections, or rapidly changing obstacles. The permissible operational envelope should therefore shrink as both computational margin decreases and environmental demand increases.

Recovery from overload or thermal degradation should be gradual. A processor returning below a temperature threshold does not guarantee that full workloads can immediately resume without causing another overload cycle. Hysteresis, stabilization intervals, workload ramping, resource verification, and staged model reactivation can prevent oscillation between normal and degraded modes. Restored functions should demonstrate acceptable latency before receiving full operational authority.

Compute overload and thermal fallback ultimately protect the timing foundation on which Physical AI depends. Intelligence is useful only when perception, prediction, planning, and control execute within the time available for safe physical action. By combining health monitoring, workload prioritization, lightweight models, resource isolation, thermal management, deterministic fallback, progressive degradation, and verified recovery, the system can reduce computational intelligence before resource exhaustion becomes loss of physical control.

연산 과부하(compute overload)는 물리 인공지능(Physical AI) 시스템이 CPU, GPU, 가속기(accelerator), 메모리 또는 통신 아키텍처가 요구되는 시간 제약 내에서 안정적으로 제공할 수 있는 것보다 더 많은 처리 능력을 요구할 때 발생한다. 열 과부하(thermal overload)는 지속적인 연산 또는 환경의 열로 인해 하드웨어가 허용 가능한 운용 한계를 초과할 때 발생한다. 두 조건 모두 명확한 하드웨어 고장이 발생하기 전에 자율 기능을 점진적으로 저하시킬 수 있으므로 제어된 폴백(controlled fallback)이 필수적이다.

물리 인공지능에서 연산 정확성(computational correctness)은 수치적 정확성뿐만 아니라 타이밍(timing)도 포함한다. 인지 모델(perception model)이 정확한 결과를 생성하더라도 마감시간 이후에 결과가 나온다면 물리적 환경이 이미 변화했기 때문에 안전하지 않을 수 있다. 지연된 위치추정(localization), 월드 모델 갱신(world-model update), 궤적 예측, 계획 또는 제어 명령은 오래된 의사결정(stale decision)을 발생시킬 수 있다. 따라서 런타임 감독(runtime supervision)은 과도한 지연과 마감시간 누락을 단순한 성능 문제가 아니라 기능 성능 저하(functional degradation)로 처리해야 한다.

연산 상태 모니터링(compute-health monitoring)은 프로세서 사용률, 가속기 부하, 메모리 사용량, 큐 깊이(queue depth), 추론 지연(inference latency), 스케줄링 지연, 프레임 처리율, 마감시간 누락 및 자원 경합(resource contention)을 관찰해야 한다. 열 모니터링(thermal monitoring)은 추가적으로 장치 온도, 냉각 성능, 팬 상태, 전력 소비, 클록 주파수 및 스로틀링 이벤트(throttling event)를 추적해야 한다. 점진적인 포화 상태는 핵심 서비스가 불안정해지기 전에 폴백을 활성화할 수 있는 충분한 경고를 제공할 수 있으므로 변화 추세도 중요하다.

자원 포화(resource saturation)는 전체 자율 시스템 스택(autonomy stack)을 통해 연쇄적으로 전파될 수 있다. 지연된 인지 파이프라인은 오래된 환경 관측을 생성하고, 이는 위치추정, 월드 모델링, 예측, 계획, 그리고 최종적으로 제어에 영향을 줄 수 있다. 메모리 압박(memory pressure)은 예측하기 어려운 할당 지연이나 모델 퇴출(model eviction)을 발생시킬 수 있으며, 과도한 가속기 경합은 안전 관련 추론이 제시간에 실행되지 못하게 할 수 있다. 따라서 폴백 설계는 개별 프로세서를 독립적으로 감시하는 데 그치지 않고 종단 간 연산 의존성(end-to-end computational dependency)을 고려해야 한다.

열적 성능 저하(thermal degradation)도 이와 유사한 연쇄 효과를 발생시킨다. 온도가 상승하면 하드웨어는 자체 보호를 위해 클록 주파수나 전력 제한을 낮출 수 있으며, 이는 복잡한 환경 조건으로 인해 더 많은 처리가 필요한 바로 그 시점에 가용 연산 능력을 감소시킬 수 있다. 자율 아키텍처가 고정된 추론 주기를 가정한다면 열 스로틀링(thermal throttling)은 타이밍 가정을 인지하지 못한 상태에서 무효화할 수 있다. 따라서 온도는 허용 가능한 AI 작업 부하와 로봇 행동에 직접적인 영향을 주는 운용 상태 변수(operational state variable)로 취급해야 한다.

견고한 시스템은 연산 기능을 중요도(criticality)에 따라 분류해야 한다. 안정화(stabilization), 비상 제동, 안전 모니터링, 액추에이터 제어, 필수 상태 추정 및 최소 장애물 탐지는 일반적으로 의미론적 추론, 대규모 모델 추론, 상세 월드 모델링, 로깅(logging), 시각화 또는 임무 최적화보다 강력한 자원 보장(resource guarantee)이 필요하다. 명시적인 우선순위 설정을 통해 연산 압박이 물리적 안전에 필요한 기능에 영향을 미치기 전에 비필수 작업 부하를 먼저 제거할 수 있다.

점진적 연산 성능 저하(graceful compute degradation)는 자율 기능을 즉시 종료하는 대신 작업 부하를 줄이는 것에서 시작할 수 있다. 시스템은 카메라 해상도를 낮추고, 인지 프레임 속도를 감소시키며, 예측 범위(prediction horizon)를 단축하고, 월드 모델 갱신 빈도를 낮추며, 계획을 단순화하거나 선택적인 신경망을 비활성화할 수 있다. 또한 로깅을 줄이거나 백그라운드 최적화를 중단함으로써 제어된 운용에 필요한 핵심 기능을 유지하면서 연산 자원을 확보할 수 있다.

모델 수준 폴백(model-level fallback)은 연산 과부하에 대응하는 또 다른 방법을 제공한다. 대규모 파운데이션 모델(foundation model), 비전-언어-행동 모델(VLA model), 인지 네트워크 또는 학습 기반 플래너(learned planner)를 메모리 및 추론 요구량이 더 낮은 소형 백업 모델로 교체할 수 있다. 백업 모델은 전체 지능을 재현할 필요가 없으며, 로봇이 축소된 운용 영역(reduced operational envelope)에서 작동하는 동안 필수 객체 탐지, 로컬 내비게이션, 단기 예측 또는 제한된 작업 수행만 지원할 수 있다.

연산 격리(compute isolation)는 안전 필수 기능(safety-critical function)에 특히 중요하다. 임무 AI, 인지, 계획 및 안전 감독이 보장된 스케줄링 없이 동일한 가속기를 놓고 경쟁한다면 하나의 구성요소에서 발생한 과부하가 다른 구성요소의 실행 자원을 빼앗을 수 있다. 예약된 CPU 코어, 보호된 메모리, 독립적인 안전 프로세서, 전용 실행 큐, 우선순위 스케줄링(priority scheduling) 또는 분리된 연산 도메인(compute domain)을 통해 주 AI 연산 환경이 포화된 경우에도 필수 제어 기능을 유지할 수 있다.

열 폴백(thermal fallback)은 연산적 대응과 물리적 대응을 결합해야 한다. 소프트웨어는 모델 복잡도, 추론 빈도, 가속기 사용률 및 비필수 작업 부하를 낮출 수 있으며, 동시에 로봇은 속도를 낮추고, 액추에이터 부하를 줄이며, 열적으로 부담이 큰 작업을 피하거나 더 낮은 온도의 환경으로 이동하거나 운용을 일시 중지할 수 있다. 지속적인 연산이 효과적인 열 제거에 의존한다면 냉각 팬, 펌프, 공기 흐름 경로, 방열판(heat sink), 열 인터페이스(thermal interface) 역시 안전 관련 아키텍처의 일부가 된다.

전력 관리(power management)와 열 관리(thermal management)는 밀접하게 연결되어 있다. 높은 가속기 사용률은 전력 소비와 발열을 증가시키며, 냉각 효율이 감소하면 추가적인 스로틀링이 필요할 수 있다. 따라서 폴백 제어기는 가용 전력, 배터리 상태, 프로세서 온도, 냉각 능력 및 필요한 임무 지속시간을 함께 고려해야 한다. 열적 셧다운(thermal shutdown)이 발생할 때까지 최대 AI 성능을 유지하는 것보다 조기에 작업 부하를 줄여 예측 가능한 제어를 유지하는 것이 일반적으로 더 바람직하다.

시스템은 하나의 임계 온도나 사용률 한계에만 의존하지 않고 여러 단계의 성능 저하 임계값(degradation threshold)을 정의해야 한다. 초기 경고 단계에서는 선택적인 작업 부하를 제거하고, 더 높은 단계에서는 경량 모델(lightweight model)을 활성화하면서 로봇 성능을 낮출 수 있으며, 심각한 단계에서는 제어 권한을 결정론적 폴백 기능(deterministic fallback function)으로 이전할 수 있다. 충분한 연산 또는 열적 여유(thermal margin)를 유지할 수 없다면 시스템은 최소 위험 기동(Minimum Risk Maneuver)을 수행하거나 안전 상태(safe state)로 전환해야 한다.

고용량 AI 처리를 더 이상 지속할 수 없는 경우 결정론적 고전 제어(deterministic classical control)가 최종적인 연산 폴백을 제공할 수 있다. 기본적인 궤적 추종, 속도 제한, 제동, 사전 정의된 후퇴 행동 또는 제어된 정지는 복잡한 학습 기반 자율 기능보다 훨씬 적은 연산량으로 실행할 수 있는 경우가 많다. 이를 통해 시스템은 의미론적 기능과 임무 성능을 포기하면서도 물리적 제어 가능성(physical controllability)을 유지하는 데 필요한 최소 연산 능력을 보존할 수 있다.

동일한 연산 성능 저하라도 상황에 따라 서로 다른 위험을 발생시킬 수 있으므로 폴백 결정은 환경 복잡도(environmental complexity)를 고려해야 한다. 인지 주기의 감소는 정적이고 저속인 환경에서는 허용될 수 있지만 사람, 차량, 교차로 또는 빠르게 변화하는 장애물 주변에서는 허용되지 않을 수 있다. 따라서 연산 여유(computational margin)가 감소하고 환경적 요구가 증가할수록 허용 가능한 운용 영역(permissible operational envelope)도 함께 축소되어야 한다.

과부하 또는 열적 성능 저하로부터의 복구(recovery)는 점진적으로 이루어져야 한다. 프로세서 온도가 임계값 아래로 내려갔다고 해서 모든 작업 부하를 즉시 복원해도 또 다른 과부하 사이클이 발생하지 않는다는 의미는 아니다. 히스테리시스(hysteresis), 안정화 시간(stabilization interval), 작업 부하 램핑(workload ramping), 자원 검증 및 단계적 모델 재활성화(staged model reactivation)를 적용하면 정상 모드와 성능 저하 모드 사이의 반복적인 진동을 방지할 수 있다. 복원된 기능은 완전한 운용 권한을 다시 부여받기 전에 허용 가능한 지연시간을 입증해야 한다.

궁극적으로 연산 과부하 및 열 폴백(compute overload and thermal fallback)은 물리 인공지능이 의존하는 타이밍 기반(timing foundation)을 보호한다. 인지, 예측, 계획 및 제어가 안전한 물리적 행동에 허용된 시간 내에서 실행될 때에만 지능은 실질적인 가치를 갖는다. 상태 모니터링, 작업 부하 우선순위화, 경량 모델, 자원 격리, 열 관리, 결정론적 폴백, 점진적 성능 저하 및 검증된 복구를 결합함으로써 시스템은 자원 고갈(resource exhaustion)이 물리적 제어 상실로 이어지기 전에 연산 지능(computational intelligence)을 안전하게 축소할 수 있다.

##  

## 06.12. Power and Battery Emergency Strategies

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

Power and battery emergency strategies define how a Physical AI system preserves controllability and reduces physical risk when electrical energy becomes insufficient, unstable, or unsafe. Power faults may affect sensing, computation, communication, actuation, braking, or payload systems simultaneously, so energy management must be treated as part of the safety architecture rather than only as a mission-duration or efficiency problem.

Battery emergencies include more than a low state of charge. Abnormal voltage, excessive current, cell imbalance, overheating, rapid capacity loss, internal resistance growth, communication failure with the Battery Management System, insulation faults, and unexpected discharge rates can indicate conditions requiring immediate response. The system must distinguish predictable energy depletion from faults that may rapidly threaten continued operation or battery integrity.

Runtime monitoring should continuously evaluate state of charge, state of health, pack and cell voltage, current, temperature, power demand, discharge rate, estimated remaining energy, and Battery Management System status. Trends are as important as absolute thresholds because an unexpectedly rapid voltage drop or temperature rise may indicate an emerging fault even when individual measurements remain inside nominal limits.

Energy prediction should consider the power required to reach a safe outcome rather than simply estimate remaining operating time. A robot may need sufficient reserve energy for braking, steering, stabilization, communication, sensing, computation, payload retention, or travel to a charging or minimum-risk location. The usable safety reserve must therefore reflect platform dynamics, environmental conditions, mission state, and the energy required for controlled fallback.

Power consumers should be classified according to safety criticality. Essential functions such as actuator control, braking, stabilization, safety sensing, state estimation, emergency communication, and fallback computation should receive priority over high-performance AI inference, nonessential sensors, payload services, visualization, detailed logging, or background optimization. Load shedding can then preserve the functions required to maintain physical controllability.

Graceful power degradation should begin before energy reaches a critical threshold. The system may reduce processor performance, disable optional AI models, lower sensor update rates, reduce communication bandwidth, limit payload operation, decrease speed, or simplify planning. By reducing consumption early, the robot preserves energy for essential control and avoids reaching a condition where power disappears before a safe transition can be completed.

Battery state should directly influence the permitted operational envelope. As available energy or battery confidence decreases, maximum speed, acceleration, payload activity, route length, terrain difficulty, and task complexity may need to decrease. New missions should be rejected when their estimated energy requirement would violate the safety reserve, even if the battery contains enough energy to begin the task under nominal assumptions.

Mobility platforms should maintain enough reserve to reach an appropriate fallback location when possible. An AMR may return to a charger, staging area, or safe parking zone, while an outdoor robot may move away from traffic or hazardous machinery before stopping. The selected destination should be based on achievable risk reduction and energy cost rather than automatically choosing the nearest charging station regardless of environmental conditions.

Manipulators require different power-loss strategies because electrical failure can release stored gravitational or mechanical energy. A robot arm holding a payload may need to place the object down, move to a mechanically stable configuration, engage brakes, reduce torque safely, or activate passive holding mechanisms before power becomes insufficient. Immediate power removal can be more hazardous than temporarily preserving controlled actuation.

Aerial robots make energy reserve management particularly critical because loss of propulsion directly affects the ability to remain airborne. Low-energy fallback may require terminating the mission early, selecting an emergency landing location, reducing maneuver demand, descending while sufficient control authority remains, or diverting to an alternative recovery point. Energy must be reserved not merely for flight time but for a controlled landing under credible adverse conditions.

Power architecture can provide additional resilience through separated power domains, protected safety supplies, backup batteries, capacitors, uninterruptible power modules, or mechanically fail-safe components. Critical monitoring and control should not necessarily lose power at the same instant as high-demand AI compute or payload systems. Limited independent energy can provide the seconds or minutes required to establish a controlled safe condition.

Electrical faults may require a response different from ordinary low-energy operation. Overtemperature, short-circuit indications, abnormal current, damaged cells, or isolation faults may make continued battery use unsafe even when substantial charge remains. In such cases, the objective changes from maximizing remaining operating time to reducing electrical and physical hazard, potentially requiring rapid load isolation, controlled shutdown, or movement to an appropriate safe location.

Power fallback should coordinate with compute and thermal fallback because these resources are strongly coupled. High GPU utilization increases electrical demand and heat generation, while cooling systems themselves consume power. Under an energy emergency, the system may replace large AI models with lightweight alternatives, reduce inference frequency, disable remote or background workloads, and reserve computation for essential perception, control, and safety supervision.

Multiple emergency thresholds provide more predictable behavior than a single low-battery alarm. An early stage can restrict mission acceptance and remove optional loads, a moderate stage can initiate return or reduced operation, and a severe stage can trigger a Minimum Risk Maneuver. A critical battery or electrical fault may require immediate transition toward a safe state while sufficient power remains to complete the necessary physical actions.

Recovery and restart should require verification that the energy system has returned to a trustworthy condition. Charging alone does not resolve overheating, cell imbalance, abnormal degradation, damaged wiring, or Battery Management System faults. Voltage stability, temperature, state estimates, fault records, charging behavior, and communication with power-management components should be validated before unrestricted autonomous operation resumes.

Power and battery emergency strategies ultimately ensure that energy depletion becomes a managed reduction of capability rather than an uncontrolled loss of control. By combining continuous monitoring, safety reserves, load prioritization, progressive degradation, platform-specific emergency actions, protected power domains, Minimum Risk Maneuvers, and verified recovery, Physical AI can use its remaining energy deliberately to preserve safety until a stable condition is reached.

전력 및 배터리 비상 전략(power and battery emergency strategies)은 전기 에너지가 부족하거나 불안정하거나 안전하지 않은 상태가 되었을 때 물리 인공지능(Physical AI) 시스템이 제어 가능성(controllability)을 유지하고 물리적 위험을 줄이는 방법을 정의한다. 전력 결함(power fault)은 센싱, 연산, 통신, 구동, 제동 또는 페이로드 시스템에 동시에 영향을 줄 수 있으므로 에너지 관리(energy management)는 단순한 임무 지속시간이나 효율성 문제가 아니라 안전 아키텍처(safety architecture)의 일부로 취급되어야 한다.

배터리 비상 상황(battery emergency)은 단순히 충전 상태(state of charge)가 낮은 경우만을 의미하지 않는다. 비정상 전압, 과도한 전류, 셀 불균형(cell imbalance), 과열, 급격한 용량 감소, 내부 저항 증가, 배터리 관리 시스템(Battery Management System, BMS)과의 통신 장애, 절연 결함 및 예상하지 못한 방전 속도는 즉각적인 대응이 필요한 상태를 나타낼 수 있다. 시스템은 예측 가능한 에너지 고갈과 지속적인 운용 또는 배터리 무결성(battery integrity)을 빠르게 위협할 수 있는 결함을 구분해야 한다.

런타임 모니터링(runtime monitoring)은 충전 상태(state of charge), 건전성 상태(state of health), 팩 및 셀 전압, 전류, 온도, 전력 요구량, 방전 속도, 추정 잔여 에너지 및 배터리 관리 시스템 상태를 지속적으로 평가해야 한다. 개별 측정값이 정상 범위 안에 있더라도 예상보다 빠른 전압 강하 또는 온도 상승은 발생 중인 결함을 나타낼 수 있으므로 절대적인 임계값뿐만 아니라 변화 추세(trend)도 중요하다.

에너지 예측(energy prediction)은 단순히 남은 운용 시간을 추정하는 것이 아니라 안전한 결과에 도달하는 데 필요한 전력을 고려해야 한다. 로봇은 제동, 조향, 안정화, 통신, 센싱, 연산, 페이로드 유지 또는 충전 위치나 최소 위험 위치까지 이동하기 위한 충분한 예비 에너지(reserve energy)를 필요로 할 수 있다. 따라서 사용 가능한 안전 예비량(safety reserve)은 플랫폼 동역학, 환경 조건, 임무 상태 및 제어된 폴백에 필요한 에너지를 반영해야 한다.

전력 소비 장치(power consumer)는 안전 중요도(safety criticality)에 따라 분류되어야 한다. 액추에이터 제어, 제동, 안정화, 안전 센싱, 상태 추정, 비상 통신 및 폴백 연산과 같은 필수 기능은 고성능 AI 추론, 비필수 센서, 페이로드 서비스, 시각화, 상세 로깅 또는 백그라운드 최적화보다 우선순위를 가져야 한다. 이를 통해 부하 차단(load shedding)은 물리적 제어 가능성을 유지하는 데 필요한 기능을 보존할 수 있다.

점진적 전력 성능 저하(graceful power degradation)는 에너지가 임계 수준에 도달하기 전에 시작되어야 한다. 시스템은 프로세서 성능을 낮추고, 선택적 AI 모델을 비활성화하며, 센서 갱신 주기를 낮추고, 통신 대역폭을 줄이며, 페이로드 운용을 제한하고, 속도를 감소시키거나 계획을 단순화할 수 있다. 소비 전력을 조기에 줄임으로써 로봇은 필수 제어를 위한 에너지를 보존하고 안전한 전환이 완료되기 전에 전력이 소진되는 상황을 방지할 수 있다.

배터리 상태는 허용되는 운용 영역(operational envelope)에 직접적인 영향을 주어야 한다. 가용 에너지 또는 배터리에 대한 신뢰도가 감소함에 따라 최대 속도, 가속도, 페이로드 활동, 경로 길이, 지형 난이도 및 작업 복잡도를 낮춰야 할 수 있다. 정상적인 가정에서는 작업을 시작할 충분한 배터리가 남아 있더라도 예상 에너지 요구량이 안전 예비량을 침해한다면 새로운 임무를 거부해야 한다.

이동 플랫폼(mobility platform)은 가능한 경우 적절한 폴백 위치까지 도달하기 위한 충분한 예비 에너지를 유지해야 한다. 자율이동로봇(AMR)은 충전기, 대기 구역(staging area) 또는 안전 주차 구역으로 복귀할 수 있으며, 실외 로봇은 정지하기 전에 교통 흐름이나 위험한 기계 장비로부터 벗어날 수 있다. 선택되는 목적지는 환경 조건을 고려하지 않고 가장 가까운 충전소를 자동으로 선택하는 것이 아니라 달성 가능한 위험 감소와 에너지 비용을 기준으로 결정되어야 한다.

매니퓰레이터(manipulator)는 전력 손실로 인해 저장된 중력 또는 기계적 에너지(stored gravitational or mechanical energy)가 방출될 수 있으므로 다른 형태의 전력 손실 전략이 필요하다. 페이로드를 들고 있는 로봇 팔은 전력이 부족해지기 전에 물체를 내려놓고, 기계적으로 안정된 구성으로 이동하며, 브레이크를 체결하고, 토크를 안전하게 낮추거나 수동 유지 메커니즘(passive holding mechanism)을 활성화해야 할 수 있다. 즉각적인 전력 차단은 일시적으로 제어된 구동을 유지하는 것보다 더 위험할 수 있다.

비행 로봇(aerial robot)은 추진력의 상실이 공중에 머무를 수 있는 능력에 직접적인 영향을 주기 때문에 에너지 예비량 관리가 특히 중요하다. 저에너지 폴백(low-energy fallback)은 임무의 조기 종료, 비상 착륙 위치 선정, 기동 요구 감소, 충분한 제어 권한(control authority)이 남아 있을 때의 하강 또는 대체 회수 지점으로의 우회를 요구할 수 있다. 에너지는 단순한 비행시간이 아니라 현실적으로 발생 가능한 불리한 조건에서도 제어된 착륙을 수행할 수 있도록 확보되어야 한다.

전력 아키텍처(power architecture)는 분리된 전력 도메인(separated power domain), 보호된 안전 전원(protected safety supply), 백업 배터리, 커패시터(capacitor), 무정전 전원 모듈(uninterruptible power module) 또는 기계적 고장 안전 구성요소(mechanically fail-safe component)를 통해 추가적인 회복탄력성(resilience)을 제공할 수 있다. 핵심 모니터링과 제어 기능은 고전력 AI 연산 또는 페이로드 시스템과 반드시 동시에 전원을 상실하도록 설계될 필요가 없다. 제한된 독립 에너지는 제어된 안전 상태를 확립하는 데 필요한 수초 또는 수분의 시간을 제공할 수 있다.

전기적 결함(electrical fault)은 일반적인 저에너지 운용과는 다른 대응을 요구할 수 있다. 과열, 단락 징후(short-circuit indication), 비정상 전류, 손상된 셀 또는 절연 결함은 상당한 충전량이 남아 있더라도 배터리를 계속 사용하는 것을 위험하게 만들 수 있다. 이러한 경우 목표는 남은 운용 시간을 최대화하는 것에서 전기적 및 물리적 위험을 줄이는 것으로 전환되며, 신속한 부하 격리(load isolation), 제어된 종료 또는 적절한 안전 위치로의 이동이 필요할 수 있다.

전력 폴백(power fallback)은 이러한 자원들이 강하게 결합되어 있으므로 연산 및 열 폴백(compute and thermal fallback)과 조정되어야 한다. 높은 GPU 사용률은 전력 요구량과 발열을 증가시키며 냉각 시스템 자체도 전력을 소비한다. 에너지 비상 상황에서는 대규모 AI 모델을 경량 대안으로 교체하고, 추론 빈도를 낮추며, 원격 또는 백그라운드 작업을 비활성화하고, 필수 인지, 제어 및 안전 감독에 연산 자원을 우선적으로 할당할 수 있다.

하나의 저전력 배터리 경보에 의존하는 것보다 여러 단계의 비상 임계값(emergency threshold)을 사용하는 것이 더욱 예측 가능한 행동을 제공한다. 초기 단계에서는 새로운 임무 수락을 제한하고 선택적 부하를 제거할 수 있으며, 중간 단계에서는 복귀 또는 제한 운용을 시작할 수 있다. 심각한 단계에서는 최소 위험 기동(Minimum Risk Maneuver)을 실행할 수 있으며, 치명적인 배터리 또는 전기적 결함이 발생하면 필요한 물리적 행동을 완료할 충분한 전력이 남아 있는 동안 즉시 안전 상태(safe state)로 전환해야 할 수 있다.

복구 및 재시작(recovery and restart)을 위해서는 에너지 시스템이 다시 신뢰 가능한 상태로 복원되었는지를 검증해야 한다. 단순한 충전만으로 과열, 셀 불균형, 비정상적인 열화, 손상된 배선 또는 배터리 관리 시스템 결함이 해결되는 것은 아니다. 제한 없는 자율 운용을 재개하기 전에 전압 안정성, 온도, 상태 추정값, 결함 기록, 충전 동작 및 전력 관리 구성요소와의 통신을 검증해야 한다.

궁극적으로 전력 및 배터리 비상 전략(power and battery emergency strategies)은 에너지 고갈이 통제되지 않은 제어 상실로 이어지는 대신 관리 가능한 기능 축소(managed reduction of capability)로 전환되도록 한다. 지속적인 모니터링, 안전 예비 에너지, 부하 우선순위화, 점진적 성능 저하, 플랫폼별 비상 행동, 보호된 전력 도메인, 최소 위험 기동 및 검증된 복구를 결합함으로써 물리 인공지능은 안정적인 상태에 도달할 때까지 남아 있는 에너지를 의도적으로 활용하여 안전을 유지할 수 있다.

##  

## 06.13. Human Takeover and Remote Assistance

![](images/image13.png){width="7.268055555555556in" height="7.268055555555556in"}

Human takeover and remote assistance provide a controlled transition from autonomous operation to human-supported decision making when a Physical AI system encounters conditions it cannot safely resolve alone. The objective is not to treat the human as an unlimited fallback mechanism, but to define when human involvement is appropriate, what authority can be transferred, and how the robot remains safe while assistance is requested, established, and completed.

Human intervention can take several forms depending on the remaining autonomy and the severity of the situation. An operator may provide semantic guidance, approve a proposed action, select among alternatives, modify a mission, specify a waypoint, or directly control robot motion. Remote assistance and direct teleoperation should be distinguished because advisory interaction preserves substantial robot autonomy, whereas takeover transfers greater responsibility and physical control authority to the human.

A takeover request should be triggered by observable conditions rather than vague model uncertainty alone. Relevant situations include repeated planning failure, unresolved perception ambiguity, localization degradation, blocked routes, unusual objects, task exceptions, conflicting safety constraints, communication with external infrastructure, or conditions outside the validated operational domain. Runtime supervision should determine whether the robot can continue autonomously, operate in a degraded mode, or requires human assistance.

Before human control becomes available, the robot must remain capable of maintaining a safe interim condition. Network establishment, operator authentication, situation assessment, and human response all require time. The robot may therefore reduce speed, hold position, move to a low-risk area, maintain stabilization, or execute a Minimum Risk Maneuver while waiting. Human assistance should never be assumed to arrive quickly enough to replace immediate onboard safety functions.

The human operator requires sufficient situational awareness to make reliable decisions. Remote interfaces may provide camera views, maps, robot pose, detected obstacles, planned trajectories, system health, battery condition, active faults, uncertainty indicators, mission context, and recent autonomous actions. Information should be prioritized according to decision relevance because excessive telemetry can increase cognitive load without improving the operator\'s understanding of the physical situation.

Communication latency significantly affects the type of authority that can safely be transferred. High-level commands such as selecting a destination or approving a route can tolerate more delay than direct steering or manipulator control. When latency, jitter, packet loss, or bandwidth becomes unsuitable for continuous teleoperation, the architecture should restrict the operator to supervisory commands while local controllers preserve stabilization, obstacle avoidance, collision constraints, and actuator safety.

Shared control can provide an intermediate mode between full autonomy and direct teleoperation. The human may specify intent, direction, target, or task preference while the robot retains responsibility for low-level trajectory generation and safety constraints. This arrangement allows human reasoning to resolve semantic or contextual uncertainty without requiring the operator to reproduce every fast control decision that the onboard system can execute more reliably.

Direct takeover requires explicit control-authority arbitration. Autonomous and human-generated commands must not compete simultaneously for the same actuators. The system should define who currently holds authority, which functions remain automatically enforced, and what conditions permit or revoke takeover. Safety monitors, emergency stopping, actuator limits, collision constraints, and stability control may remain active even when a human operator has primary motion authority.

The transition itself should be designed as a safety-critical process. Before transferring authority, the system may verify operator identity, communication quality, robot state, control-interface readiness, and acknowledgement from both sides. Command discontinuities should be prevented through state synchronization, bounded control transitions, speed restrictions, and initialization of the remote control interface to the robot\'s current physical state rather than an assumed default condition.

Human takeover should be constrained by the same physical safety envelope that protects autonomous operation. Remote operators should not automatically gain unrestricted access to speed, force, workspace, payload, or prohibited areas merely because autonomous reasoning has failed. Depending on the application, some safety constraints may be non-overridable, while exceptional overrides may require explicit authorization, additional confirmation, logging, or higher-level supervisory approval.

Remote assistance also introduces cybersecurity and identity risks because control commands cross communication boundaries. Authentication, authorization, encrypted communication, session integrity, command freshness, replay protection, and operator accountability become safety-relevant properties. A system unable to verify the legitimacy or freshness of a remote command should reject it rather than allowing uncertain network authority to influence physical actuators.

Loss of communication during human control requires a predefined response. The robot should not continue indefinitely using the last steering, velocity, or manipulation command after the operator disappears. Command timeouts, heartbeat monitoring, local safety supervision, controlled deceleration, hold behavior, or Minimum Risk Maneuvers can return the platform to a bounded condition. The appropriate response depends on robot dynamics and the consequences of stopping in the current environment.

Operator workload must also be considered when remote assistance is deployed across fleets. A single human cannot reliably supervise an unlimited number of robots, particularly when several systems request intervention simultaneously. Requests should therefore be prioritized by risk, urgency, remaining autonomous capability, and available safe waiting time. Fleet systems may queue noncritical assistance while escalating situations that require immediate human judgment or control.

After the exceptional situation has been resolved, authority should return to autonomy through a deliberate handback process. The autonomous system must understand the robot\'s current pose, environment, task state, payload condition, and any changes introduced by the human. Plans or world-model states generated before takeover may no longer be valid. Replanning and state reconciliation should therefore occur before unrestricted autonomous operation resumes.

Every takeover and remote-assistance event should be recorded as evidence about the boundaries of autonomous capability. Logs can capture trigger conditions, model uncertainty, robot state, operator identity, assistance type, commands, safety interventions, communication quality, duration, and final outcome. Repeated intervention patterns can reveal weaknesses in perception, planning, interface design, operational procedures, or the validated domain and can guide future system improvement.

Human takeover and remote assistance ultimately create a structured bridge between machine autonomy and human judgment. The safest architecture does not depend on humans for millisecond-level protection and does not grant remote operators unconstrained physical authority. Instead, it combines onboard safety, explicit authority transfer, appropriate human situational awareness, shared control, communication-aware restrictions, secure access, safe disconnection behavior, and verified handback to preserve controllability when autonomous intelligence reaches its limits.

인간 인수 및 원격 지원(human takeover and remote assistance)은 물리 인공지능(Physical AI) 시스템이 스스로 안전하게 해결할 수 없는 상황에 직면했을 때 자율 운용(autonomous operation)에서 인간이 지원하는 의사결정(human-supported decision making)으로 제어된 전환을 제공한다. 목적은 인간을 무제한적인 폴백 메커니즘(fallback mechanism)으로 취급하는 것이 아니라, 언제 인간의 개입이 적절한지, 어떤 권한을 이전할 수 있는지, 그리고 지원이 요청되고 연결되며 완료되는 동안 로봇이 어떻게 안전을 유지할지를 정의하는 것이다.

인간 개입(human intervention)은 남아 있는 자율성 수준과 상황의 심각도에 따라 여러 형태로 이루어질 수 있다. 운영자는 의미론적 지침(semantic guidance)을 제공하거나, 제안된 행동을 승인하거나, 여러 대안 중 하나를 선택하거나, 임무를 수정하거나, 웨이포인트(waypoint)를 지정하거나, 로봇의 움직임을 직접 제어할 수 있다. 원격 지원(remote assistance)과 직접 원격조작(direct teleoperation)은 구분되어야 하는데, 자문형 상호작용(advisory interaction)은 상당한 수준의 로봇 자율성을 유지하는 반면 인수(takeover)는 인간에게 더 큰 책임과 물리적 제어 권한(physical control authority)을 이전하기 때문이다.

인수 요청(takeover request)은 단순히 모호한 모델 불확실성(model uncertainty)에 의존하는 것이 아니라 관찰 가능한 조건에 의해 발생해야 한다. 관련 상황에는 반복적인 계획 실패, 해결되지 않은 인지 모호성(perception ambiguity), 위치추정 성능 저하, 차단된 경로, 비정상적인 객체, 작업 예외(task exception), 상충하는 안전 제약조건, 외부 인프라와의 통신 문제 또는 검증된 운용 영역(validated operational domain) 밖의 조건이 포함된다. 런타임 감독(runtime supervision)은 로봇이 자율적으로 계속 운용할 수 있는지, 성능 저하 모드(degraded mode)로 운용해야 하는지 또는 인간의 지원이 필요한지를 판단해야 한다.

인간의 제어가 가능해지기 전까지 로봇은 안전한 중간 상태(safe interim condition)를 유지할 수 있어야 한다. 네트워크 연결 설정, 운영자 인증(operator authentication), 상황 평가 및 인간의 응답에는 모두 시간이 필요하다. 따라서 로봇은 지원을 기다리는 동안 속도를 줄이고, 현재 위치를 유지하며, 저위험 구역으로 이동하거나, 안정화 상태를 유지하거나, 최소 위험 기동(Minimum Risk Maneuver)을 수행할 수 있다. 인간의 지원이 온보드 안전 기능(onboard safety function)을 대체할 만큼 신속하게 도착할 것이라고 가정해서는 안 된다.

인간 운영자(human operator)가 신뢰할 수 있는 의사결정을 내리기 위해서는 충분한 상황 인식(situational awareness)이 필요하다. 원격 인터페이스(remote interface)는 카메라 영상, 지도, 로봇 자세(robot pose), 탐지된 장애물, 계획된 궤적, 시스템 상태, 배터리 상태, 활성 결함(active fault), 불확실성 지표, 임무 문맥 및 최근 자율 행동을 제공할 수 있다. 지나치게 많은 텔레메트리(telemetry)는 물리적 상황에 대한 운영자의 이해를 향상시키지 않으면서 인지 부하(cognitive load)를 증가시킬 수 있으므로 정보는 의사결정 관련성에 따라 우선순위가 지정되어야 한다.

통신 지연(communication latency)은 안전하게 이전할 수 있는 권한의 유형에 큰 영향을 준다. 목적지 선택이나 경로 승인과 같은 상위 수준 명령(high-level command)은 직접적인 조향이나 매니퓰레이터 제어보다 더 큰 지연을 허용할 수 있다. 지연, 지터(jitter), 패킷 손실(packet loss) 또는 대역폭이 연속적인 원격조작에 적합하지 않다면 아키텍처는 운영자를 감독 명령(supervisory command)으로 제한하고 로컬 제어기가 안정화, 장애물 회피, 충돌 제약조건 및 액추에이터 안전을 유지하도록 해야 한다.

공유 제어(shared control)는 완전 자율(full autonomy)과 직접 원격조작 사이의 중간 모드를 제공할 수 있다. 인간은 의도, 방향, 목표 또는 작업 선호도를 지정하고 로봇은 저수준 궤적 생성(low-level trajectory generation)과 안전 제약조건에 대한 책임을 유지할 수 있다. 이러한 구성은 운영자가 온보드 시스템이 더욱 안정적으로 수행할 수 있는 모든 빠른 제어 의사결정을 직접 재현하지 않더라도 인간의 추론을 통해 의미론적 또는 상황적 불확실성을 해결할 수 있도록 한다.

직접 인수(direct takeover)에는 명시적인 제어 권한 중재(control-authority arbitration)가 필요하다. 자율 시스템과 인간이 생성한 명령이 동일한 액추에이터를 대상으로 동시에 경쟁해서는 안 된다. 시스템은 현재 누가 제어 권한을 보유하고 있는지, 어떤 기능이 계속 자동으로 적용되는지, 어떤 조건에서 인수가 허용되거나 철회되는지를 정의해야 한다. 인간 운영자가 주 움직임 제어 권한을 가지고 있더라도 안전 모니터(safety monitor), 비상 정지, 액추에이터 제한, 충돌 제약조건 및 안정성 제어(stability control)는 계속 활성화될 수 있다.

제어 전환(transition) 자체도 안전 필수 프로세스(safety-critical process)로 설계되어야 한다. 권한을 이전하기 전에 시스템은 운영자 신원, 통신 품질, 로봇 상태, 제어 인터페이스 준비 상태 및 양측의 승인(acknowledgement)을 확인할 수 있다. 명령 불연속(command discontinuity)은 상태 동기화(state synchronization), 제한된 제어 전환(bounded control transition), 속도 제한 및 가정된 기본 상태가 아니라 로봇의 현재 물리적 상태에 맞춘 원격 제어 인터페이스 초기화를 통해 방지해야 한다.

인간 인수는 자율 운용을 보호하는 것과 동일한 물리적 안전 영역(physical safety envelope)에 의해 제한되어야 한다. 자율 추론이 실패했다는 이유만으로 원격 운영자가 속도, 힘, 작업 공간, 페이로드 또는 금지 구역에 대한 무제한적인 접근 권한을 자동으로 획득해서는 안 된다. 응용 분야에 따라 일부 안전 제약조건은 해제할 수 없도록(non-overridable) 설계할 수 있으며, 예외적인 오버라이드(override)는 명시적 승인, 추가 확인, 로깅(logging) 또는 상위 수준 감독 승인을 요구할 수 있다.

원격 지원은 제어 명령이 통신 경계를 통과하기 때문에 사이버보안(cybersecurity) 및 신원 확인 위험(identity risk)도 발생시킨다. 인증(authentication), 권한 부여(authorization), 암호화 통신(encrypted communication), 세션 무결성(session integrity), 명령 최신성(command freshness), 재전송 공격 방지(replay protection) 및 운영자 책임 추적(operator accountability)은 안전과 관련된 특성이 된다. 원격 명령의 적법성이나 최신성을 검증할 수 없는 시스템은 불확실한 네트워크 권한이 물리적 액추에이터에 영향을 주도록 허용하는 대신 해당 명령을 거부해야 한다.

인간 제어 중 통신이 상실되는 상황에 대해서도 사전 정의된 대응이 필요하다. 운영자와의 연결이 사라진 이후 로봇은 마지막 조향, 속도 또는 조작 명령을 무기한 계속 실행해서는 안 된다. 명령 타임아웃(command timeout), 하트비트 모니터링(heartbeat monitoring), 로컬 안전 감독(local safety supervision), 제어된 감속, 위치 유지 행동 또는 최소 위험 기동을 통해 플랫폼을 제한된 안전 조건으로 복귀시킬 수 있다. 적절한 대응은 로봇의 동역학과 현재 환경에서 정지할 경우 발생할 수 있는 결과에 따라 달라진다.

플릿(fleet) 전체에 원격 지원을 적용할 경우 운영자 작업 부하(operator workload)도 고려해야 한다. 특히 여러 시스템이 동시에 개입을 요청하는 경우 한 명의 인간이 무제한의 로봇을 신뢰성 있게 감독할 수는 없다. 따라서 지원 요청은 위험도, 긴급성, 남아 있는 자율 기능(remaining autonomous capability), 안전하게 대기할 수 있는 시간에 따라 우선순위를 지정해야 한다. 플릿 시스템은 중요도가 낮은 지원 요청을 대기열(queue)에 배치하면서 즉각적인 인간의 판단이나 제어가 필요한 상황을 우선적으로 에스컬레이션(escalation)할 수 있다.

예외 상황이 해결된 이후에는 의도적인 권한 반환 과정(handback process)을 통해 제어 권한을 다시 자율 시스템으로 이전해야 한다. 자율 시스템은 로봇의 현재 자세, 환경, 작업 상태, 페이로드 상태 및 인간이 개입하면서 발생시킨 모든 변화를 이해해야 한다. 인수 이전에 생성된 계획이나 월드 모델 상태(world-model state)는 더 이상 유효하지 않을 수 있다. 따라서 제한 없는 자율 운용을 재개하기 전에 재계획(replanning)과 상태 조정(state reconciliation)을 수행해야 한다.

모든 인수 및 원격 지원 이벤트(takeover and remote-assistance event)는 자율 기능의 한계(boundaries of autonomous capability)를 나타내는 증거로 기록되어야 한다. 로그에는 트리거 조건, 모델 불확실성, 로봇 상태, 운영자 신원, 지원 유형, 명령, 안전 개입, 통신 품질, 지속시간 및 최종 결과를 기록할 수 있다. 반복되는 개입 패턴은 인지, 계획, 인터페이스 설계, 운용 절차 또는 검증된 영역의 취약점을 발견하는 데 활용할 수 있으며 향후 시스템 개선을 위한 근거가 될 수 있다.

궁극적으로 인간 인수 및 원격 지원(human takeover and remote assistance)은 기계 자율성(machine autonomy)과 인간 판단(human judgment) 사이에 구조화된 연결을 형성한다. 가장 안전한 아키텍처는 밀리초 수준의 보호를 인간에게 의존하지 않으며 원격 운영자에게 제한 없는 물리적 권한을 제공하지도 않는다. 대신 온보드 안전, 명시적 권한 이전, 적절한 인간 상황 인식, 공유 제어, 통신 상태를 고려한 제한, 안전한 접근, 통신 단절 시 안전 행동 및 검증된 권한 반환을 결합하여 자율 지능이 한계에 도달한 상황에서도 물리적 제어 가능성을 유지한다.

##  

## 06.14. Recovery Replanning and Mission Abort

![](images/image14.png){width="7.268055555555556in" height="7.268055555555556in"}

Recovery, replanning, and mission abort define how a Physical AI system responds after faults, uncertainty, environmental changes, or degraded capabilities disrupt normal autonomous operation. The objective is not simply to restart failed functions, but to determine whether safe operation can be restored, whether the mission must be reformulated, or whether continued execution creates unacceptable risk and should therefore be terminated.

Recovery begins with establishing a trustworthy understanding of the robot's current condition. A fault may have changed position, velocity, payload state, actuator availability, sensor coverage, battery reserve, communication status, or environmental assumptions. Before autonomous behavior resumes, the system should reconstruct its operational state and identify which capabilities remain available, degraded, isolated, or uncertain.

Fault clearance alone does not prove that recovery is complete. A sensor may begin transmitting again while remaining miscalibrated, a communication link may reconnect but remain unstable, or an AI model may restart while continuing to produce unreliable outputs. Recovery therefore requires validation of function, timing, consistency, uncertainty, and dependencies before affected components regain operational authority.

State reconciliation is particularly important because different subsystems may contain information generated before, during, and after the failure. Localization estimates, object tracks, occupancy maps, world-model states, task progress, shared fleet information, and cached commands may no longer agree. The system should identify stale or inconsistent information and rebuild the state required for safe decision making rather than blindly continuing from previous internal memory.

Once a trustworthy state has been established, the system determines whether the original mission remains feasible. The previous plan may depend on sensors, routes, compute resources, battery reserves, communication services, or environmental conditions that are no longer available. Mission feasibility should therefore be reassessed using current capability, remaining resources, operational constraints, safety margins, and the expected consequences of another failure.

Replanning provides a mechanism for adapting the mission to the changed situation. The robot may select a different route, reduce task scope, reorder objectives, avoid uncertain areas, lower speed, use alternative sensors, switch models, request remote assistance, or return to a known location. A valid recovery plan should rely only on capabilities that have been demonstrated to remain trustworthy after the disruptive event.

Replanning should also account for uncertainty introduced by the failure. Even when operation can continue, confidence in maps, localization, object states, predictions, or system health may be lower than before. Conservative margins, shorter planning horizons, reduced speed, restricted workspaces, simpler maneuvers, and additional monitoring can compensate for incomplete knowledge while allowing limited mission progress.

Not every mission objective should have equal priority during recovery. Safety-critical objectives, protection of people, stabilization of the platform, payload security, preservation of essential infrastructure, and maintaining controllability should take precedence over productivity or schedule completion. Mission management should be able to discard low-priority goals when continuing them would consume resources needed to maintain a safe fallback capability.

Repeated recovery attempts require explicit limits. A system that continuously retries a failed planner, localization process, network connection, manipulation action, or charging approach may remain in a hazardous environment while consuming battery and computational resources. Retry counts, time limits, resource budgets, spatial limits, and escalation criteria should prevent recovery logic from becoming an uncontrolled loop.

Mission abort becomes appropriate when the remaining capabilities cannot support the mission within acceptable risk. Abort conditions may include persistent safety-monitor violations, insufficient localization confidence, inadequate perception coverage, actuator degradation, critical battery reserve, unstable communication required for the task, repeated planning failure, environmental conditions outside validated limits, or inability to maintain required safety margins.

Mission abort should be distinguished from emergency stop. An emergency stop may immediately suppress motion because of an imminent hazard, while mission abort is a higher-level decision to discontinue the objective and transition toward a safer operational condition. After aborting, the robot may still need to navigate to a safe location, place down a payload, leave a traffic path, return to base, or execute another controlled termination sequence.

The abort destination or final condition should be selected according to risk rather than convenience alone. Returning to the original starting point may require more energy or traverse more hazardous terrain than reaching a nearby safe zone. The system should evaluate remaining battery, mobility, environmental hazards, human presence, payload condition, communication availability, and the reliability of navigation before choosing the termination strategy.

Recovery and abort logic should coordinate with Minimum Risk Maneuvers and safe-state definitions. If replanning remains possible, the robot may continue in a restricted degraded mode. If mission completion is no longer justified but controlled mobility remains available, it can execute an abort trajectory. If capability deteriorates further, a Minimum Risk Maneuver can reduce exposure before the system enters an appropriate safe state.

Human involvement may be useful when autonomous recovery cannot resolve semantic or operational ambiguity. A remote operator can confirm environmental conditions, modify mission priorities, approve an alternate route, release a blocked task, or authorize mission termination. However, human assistance should not be required for immediate physical safety, and the robot must remain in a bounded condition while waiting for intervention.

Fleet systems require additional recovery coordination because one robot's abort can affect shared tasks, traffic reservations, resource allocation, and other agents. When a robot withdraws from a mission, its tasks may need reassignment, reserved routes released, shared maps updated, and neighboring robots informed. Recovery therefore extends beyond the individual platform when mission state is distributed across a collective robotic system.

Every recovery, replanning, and abort event should be logged with the original fault, state changes, rejected plans, recovery attempts, safety constraints, human interventions, final decisions, and outcomes. These records reveal whether the system correctly recognized the limits of its remaining capability and provide evidence for improving fault handling, mission planning, validation scenarios, and future autonomy.

Recovery, replanning, and mission abort ultimately provide a disciplined decision hierarchy for Physical AI after normal operation has been disrupted. The system first seeks to establish trustworthy state, then evaluates whether capability can be restored, whether the mission can be safely reformulated, or whether the objective must be abandoned. By prioritizing safety over mission completion, Physical AI can recover when justified and terminate gracefully when continued autonomy is no longer defensible.

복구, 재계획 및 임무 중단(recovery, replanning, and mission abort)은 결함, 불확실성, 환경 변화 또는 기능 성능 저하로 인해 정상적인 자율 운용이 중단된 이후 물리 인공지능(Physical AI) 시스템이 어떻게 대응할지를 정의한다. 목적은 단순히 고장 난 기능을 재시작하는 것이 아니라 안전한 운용을 복원할 수 있는지, 임무를 재구성해야 하는지, 또는 계속 수행하는 것이 허용할 수 없는 위험을 발생시키므로 임무를 종료해야 하는지를 판단하는 것이다.

복구(recovery)는 로봇의 현재 상태를 신뢰할 수 있게 파악하는 것에서 시작한다. 결함으로 인해 위치, 속도, 페이로드 상태, 액추에이터 가용성, 센서 범위, 배터리 예비량, 통신 상태 또는 환경에 대한 가정이 변경되었을 수 있다. 자율 행동을 재개하기 전에 시스템은 운용 상태(operational state)를 재구성하고 어떤 기능이 여전히 사용 가능하고, 성능이 저하되었으며, 격리되었거나 불확실한지를 식별해야 한다.

결함이 해제되었다는 사실만으로 복구가 완료되었음을 입증할 수는 없다. 센서가 다시 데이터를 전송하기 시작했지만 여전히 보정 오류가 존재할 수 있고, 통신 링크가 재연결되었지만 불안정한 상태일 수 있으며, AI 모델이 재시작되었지만 계속해서 신뢰할 수 없는 출력을 생성할 수도 있다. 따라서 영향을 받은 구성요소에 운용 권한(operational authority)을 다시 부여하기 전에 기능, 타이밍, 일관성, 불확실성 및 의존 관계를 검증해야 한다.

상태 조정(state reconciliation)은 서로 다른 서브시스템에 고장 발생 전, 발생 중, 발생 후에 생성된 정보가 혼재할 수 있기 때문에 특히 중요하다. 위치추정 결과, 객체 추적 정보, 점유 지도(occupancy map), 월드 모델 상태(world-model state), 작업 진행 상태, 공유 플릿 정보 및 캐시된 명령(cached command)이 더 이상 서로 일치하지 않을 수 있다. 시스템은 이전의 내부 메모리에서 무조건 운용을 계속하기보다 오래되거나 일관되지 않은 정보를 식별하고 안전한 의사결정에 필요한 상태를 다시 구축해야 한다.

신뢰할 수 있는 상태가 확립되면 시스템은 기존 임무를 계속 수행할 수 있는지를 판단한다. 이전 계획은 더 이상 사용할 수 없는 센서, 경로, 연산 자원, 배터리 예비량, 통신 서비스 또는 환경 조건에 의존하고 있을 수 있다. 따라서 현재 기능, 남아 있는 자원, 운용 제약조건, 안전 여유(safety margin) 및 또 다른 고장이 발생했을 때 예상되는 결과를 바탕으로 임무 실행 가능성(mission feasibility)을 다시 평가해야 한다.

재계획(replanning)은 변화된 상황에 맞추어 임무를 조정하는 메커니즘을 제공한다. 로봇은 다른 경로를 선택하고, 작업 범위를 축소하며, 목표의 순서를 변경하고, 불확실한 영역을 회피하며, 속도를 낮추거나 대체 센서를 사용할 수 있다. 또한 모델을 전환하고, 원격 지원(remote assistance)을 요청하거나, 알려진 위치로 복귀할 수 있다. 유효한 복구 계획은 장애 사건 이후에도 신뢰할 수 있음이 입증된 기능만을 기반으로 해야 한다.

재계획은 고장으로 인해 발생한 불확실성도 고려해야 한다. 운용을 계속할 수 있더라도 지도, 위치추정, 객체 상태, 예측 또는 시스템 건전성(system health)에 대한 신뢰도는 이전보다 낮을 수 있다. 보수적인 안전 여유, 짧은 계획 범위(planning horizon), 낮은 속도, 제한된 작업 공간, 단순화된 기동 및 추가적인 모니터링을 적용하면 불완전한 정보를 보완하면서 제한적인 임무 진행을 허용할 수 있다.

복구 과정에서 모든 임무 목표가 동일한 우선순위를 가져서는 안 된다. 안전 필수 목표(safety-critical objective), 사람의 보호, 플랫폼 안정화, 페이로드 안전, 필수 인프라 보호 및 제어 가능성 유지가 생산성이나 일정 완료보다 우선해야 한다. 낮은 우선순위의 목표를 계속 수행함으로써 안전한 폴백 기능을 유지하는 데 필요한 자원이 소모된다면 임무 관리 시스템은 해당 목표를 폐기할 수 있어야 한다.

반복적인 복구 시도에는 명시적인 한계가 필요하다. 실패한 플래너, 위치추정 프로세스, 네트워크 연결, 조작 행동 또는 충전 접근을 시스템이 계속 반복해서 재시도하면 배터리와 연산 자원을 소비하면서 위험한 환경에 머무르게 될 수 있다. 복구 로직이 통제되지 않은 반복 루프가 되지 않도록 재시도 횟수, 시간 제한, 자원 예산(resource budget), 공간적 한계 및 에스컬레이션 기준(escalation criteria)을 정의해야 한다.

남아 있는 기능으로 허용 가능한 위험 수준에서 임무를 지원할 수 없을 때 임무 중단(mission abort)이 적절한 선택이 된다. 중단 조건에는 지속적인 안전 모니터 위반, 불충분한 위치추정 신뢰도, 부족한 인지 범위, 액추에이터 성능 저하, 임계 수준의 배터리 예비량, 작업 수행에 필요한 통신의 불안정, 반복적인 계획 실패, 검증된 한계를 벗어난 환경 조건 또는 필요한 안전 여유를 유지할 수 없는 상황이 포함될 수 있다.

임무 중단은 비상 정지(emergency stop)와 구분되어야 한다. 비상 정지는 임박한 위험으로 인해 움직임을 즉시 억제할 수 있지만, 임무 중단은 목표 수행을 중단하고 보다 안전한 운용 상태로 전환하기 위한 상위 수준의 의사결정이다. 임무를 중단한 이후에도 로봇은 안전한 위치로 이동하고, 페이로드를 내려놓으며, 교통 경로에서 벗어나거나, 기지로 복귀하거나, 다른 제어된 종료 절차(controlled termination sequence)를 수행해야 할 수 있다.

중단 목적지(abort destination) 또는 최종 상태는 단순한 편의성이 아니라 위험을 기준으로 선택되어야 한다. 원래 출발점으로 복귀하려면 가까운 안전 구역으로 이동하는 것보다 더 많은 에너지가 필요하거나 더 위험한 지형을 통과해야 할 수 있다. 시스템은 종료 전략을 선택하기 전에 남아 있는 배터리, 이동 능력, 환경 위험, 사람의 존재, 페이로드 상태, 통신 가용성 및 내비게이션 신뢰성을 평가해야 한다.

복구 및 중단 로직(recovery and abort logic)은 최소 위험 기동(Minimum Risk Maneuver) 및 안전 상태 정의(safe-state definition)와 연계되어야 한다. 재계획이 여전히 가능하다면 로봇은 제한된 성능 저하 모드(degraded mode)에서 계속 운용할 수 있다. 임무 완료는 더 이상 정당화할 수 없지만 제어된 이동성이 남아 있다면 중단 궤적(abort trajectory)을 실행할 수 있다. 기능이 더욱 악화되면 최소 위험 기동을 통해 위험 노출을 줄인 후 적절한 안전 상태(safe state)로 진입할 수 있다.

자율 복구가 의미론적 또는 운용상의 모호성을 해결할 수 없을 때 인간 개입(human involvement)이 유용할 수 있다. 원격 운영자는 환경 조건을 확인하고, 임무 우선순위를 변경하며, 대체 경로를 승인하고, 차단된 작업을 해제하거나, 임무 종료를 승인할 수 있다. 그러나 즉각적인 물리적 안전을 인간 지원에 의존해서는 안 되며, 로봇은 인간의 개입을 기다리는 동안 제한되고 안전한 상태(bounded condition)를 유지해야 한다.

플릿 시스템(fleet system)은 하나의 로봇이 임무를 중단하면 공유 작업, 교통 예약(traffic reservation), 자원 할당 및 다른 에이전트에도 영향을 미칠 수 있으므로 추가적인 복구 조정이 필요하다. 로봇이 임무에서 이탈하면 해당 작업을 다른 로봇에 재할당하고, 예약된 경로를 해제하며, 공유 지도를 갱신하고, 주변 로봇에 상황을 전달해야 할 수 있다. 따라서 임무 상태가 집단 로봇 시스템(collective robotic system)에 분산되어 있다면 복구는 개별 플랫폼을 넘어 전체 시스템 수준으로 확장된다.

모든 복구, 재계획 및 임무 중단 이벤트는 최초 결함, 상태 변화, 거부된 계획, 복구 시도, 안전 제약조건, 인간 개입, 최종 결정 및 결과와 함께 기록되어야 한다. 이러한 기록은 시스템이 남아 있는 기능의 한계를 올바르게 인식했는지를 보여주며, 결함 처리, 임무 계획, 검증 시나리오(validation scenario) 및 향후 자율 기능을 개선하기 위한 근거를 제공한다.

궁극적으로 복구, 재계획 및 임무 중단(recovery, replanning, and mission abort)은 정상 운용이 중단된 이후 물리 인공지능을 위한 체계적인 의사결정 계층(decision hierarchy)을 제공한다. 시스템은 먼저 신뢰 가능한 상태를 확립하고, 이후 기능을 복원할 수 있는지, 임무를 안전하게 재구성할 수 있는지, 또는 목표를 포기해야 하는지를 평가한다. 임무 완료보다 안전을 우선함으로써 물리 인공지능은 정당한 경우에는 운용을 복구하고, 지속적인 자율 운용을 더 이상 정당화할 수 없는 경우에는 안전하고 점진적으로 임무를 종료할 수 있다.

##  

## 06.15. Fallback State Machine [w/Code]

![](images/image15.png){width="7.268055555555556in" height="7.268055555555556in"}

A fallback state machine provides a formal control structure for managing transitions between normal autonomy, degraded operation, recovery, Minimum Risk Maneuvers, safe states, and mission termination. Instead of allowing individual subsystems to react independently to failures, the state machine coordinates system-wide behavior so that faults produce predictable changes in authority, capability, motion, and safety constraints.

Each state represents a defined operational condition rather than merely a diagnostic label. Normal operation assumes that required sensing, localization, computation, communication, power, planning, and control functions satisfy their acceptance criteria. Degraded states represent reduced but still usable capability, while recovery and safe states define increasingly restrictive behavior as uncertainty or fault severity increases.

Transitions between states should be triggered by explicit evidence. Sensor-health indicators, localization confidence, model uncertainty, communication quality, compute latency, temperature, battery reserve, actuator status, planning failures, safety-monitor violations, and human commands can contribute to transition decisions. Combining multiple indicators prevents a single noisy measurement from unnecessarily forcing the entire robot into a restrictive fallback mode.

Transition guards define the conditions that must be satisfied before a state change is permitted. A localization failure may trigger degraded navigation only if alternative localization remains trustworthy, while loss of both primary and backup localization may require a Minimum Risk Maneuver. Guards therefore connect diagnostic evidence with capability requirements, ensuring that the destination state can actually be supported by the functions that remain available.

The state machine should distinguish warning, degraded, critical, and terminal conditions. An early warning may activate additional monitoring or remove optional workloads without changing the mission. Continued degradation can restrict speed, routes, models, or task complexity. Critical conditions may initiate controlled termination, while unrecoverable faults can place the system in a stable safe state until maintenance or authorized intervention occurs.

Hierarchical state machines are useful because Physical AI contains multiple layers of autonomy. A high-level system state may indicate Normal, Degraded, Recovery, or Safe Operation, while nested states describe perception fallback, localization fallback, communication loss, compute reduction, battery emergency, or human takeover. This structure preserves subsystem detail without allowing local fallback logic to conflict with the global safety objective.

Fallback states should explicitly define control authority. In normal operation, an AI planner may command trajectories through validated control layers. During degradation, authority may shift toward lightweight models, deterministic planners, or restricted local autonomy. In critical states, classical controllers, emergency functions, or safety processors may dominate. Human takeover introduces another authority state that must be coordinated with onboard safety enforcement.

State entry actions define what happens immediately after a transition. Entering degraded operation may reduce speed, disable optional models, increase safety margins, restrict routes, or notify fleet infrastructure. Entering a Minimum Risk Maneuver state may cancel mission commands and initiate controlled deceleration or movement toward a safe area. Entry actions make the response deterministic instead of relying on loosely coordinated subsystem reactions.

State exit conditions are equally important. A fault disappearing momentarily should not automatically restore full autonomy. Recovery may require stable sensor outputs, acceptable localization confidence, sufficient battery reserve, normal compute latency, reliable communication, successful diagnostics, or agreement between primary and backup systems over a defined interval. These conditions prevent premature restoration of capabilities that have not yet demonstrated trustworthy operation.

Hysteresis and persistence mechanisms help prevent rapid oscillation between states. For example, a temperature crossing a threshold repeatedly or an intermittent network link could otherwise cause constant switching between normal and degraded operation. Separate entry and exit thresholds, minimum dwell times, confidence windows, and stability intervals allow the state machine to respond decisively while avoiding unstable mode transitions.

Timeouts provide protection when transitional states cannot complete their intended purpose. A robot attempting relocalization, network reconnection, model restart, charging, or remote assistance should not remain indefinitely in a temporary state. When a timeout expires, the state machine can escalate to a more restrictive state, initiate mission abort, or execute a Minimum Risk Maneuver according to the remaining capabilities and environmental risk.

Recovery should normally progress through controlled intermediate states rather than jumping directly from failure to full autonomy. A recovered sensor or AI model can first operate in observation or shadow mode, then participate with restricted authority, and finally return to normal operation after validation. This staged progression enables the system to verify consistency before restored components again influence safety-relevant physical actions.

Concurrent faults require arbitration because several fallback conditions may be active simultaneously. Communication loss might permit local autonomy, while a simultaneous localization failure could make continued navigation unacceptable. The state machine should apply precedence rules so that the most safety-restrictive relevant condition dominates. Lower-level recovery actions must never override a higher-level requirement for controlled stopping or safe-state entry.

Mission state and safety state should remain logically separated but coordinated. A mission may be Running, Paused, Replanning, Returning, or Aborted while the safety controller independently determines Normal, Degraded, Minimum Risk, or Safe State operation. This separation prevents mission objectives from redefining safety requirements and ensures that productivity cannot override the operational restrictions imposed by fault conditions.

Every transition should generate traceable evidence describing the source state, destination state, trigger, guard evaluation, active faults, system health, authority changes, and actions executed. Transition histories allow engineers to reconstruct why the robot behaved as it did and identify repeated oscillations, unnecessary fallback activations, failed recoveries, or unsafe assumptions. They also provide valuable evidence for verification and validation.

The fallback state machine ultimately converts diverse failures into a bounded and understandable progression of system behavior. Normal autonomy can contract into degraded operation, recovery, Minimum Risk Maneuvers, mission abort, or a safe state according to explicit evidence and verified capability. Through guarded transitions, authority management, hierarchy, hysteresis, timeouts, fault arbitration, staged recovery, and logging, Physical AI can fail progressively rather than unpredictably.

폴백 상태 머신(fallback state machine)은 정상 자율 운용(normal autonomy), 성능 저하 운용(degraded operation), 복구(recovery), 최소 위험 기동(Minimum Risk Maneuver), 안전 상태(safe state), 임무 종료(mission termination) 사이의 전환을 관리하기 위한 공식적인 제어 구조를 제공한다. 개별 서브시스템이 고장에 독립적으로 대응하도록 두는 대신 상태 머신은 시스템 전체의 행동을 조정하여 결함이 발생했을 때 권한, 기능, 움직임 및 안전 제약조건이 예측 가능한 방식으로 변경되도록 한다.

각 상태(state)는 단순한 진단 레이블(diagnostic label)이 아니라 명확하게 정의된 운용 조건(operational condition)을 나타낸다. 정상 운용은 필요한 센싱, 위치추정, 연산, 통신, 전력, 계획 및 제어 기능이 각각의 허용 기준(acceptance criteria)을 충족하고 있음을 전제로 한다. 성능 저하 상태(degraded state)는 축소되었지만 여전히 사용할 수 있는 기능을 나타내며, 복구 상태와 안전 상태는 불확실성 또는 결함의 심각도가 증가함에 따라 더욱 제한적인 행동을 정의한다.

상태 사이의 전환(transition)은 명시적인 증거에 의해 트리거되어야 한다. 센서 상태 지표(sensor-health indicator), 위치추정 신뢰도(localization confidence), 모델 불확실성(model uncertainty), 통신 품질, 연산 지연(compute latency), 온도, 배터리 예비량, 액추에이터 상태, 계획 실패, 안전 모니터 위반 및 인간 명령 등이 전환 결정에 기여할 수 있다. 여러 지표를 결합하면 하나의 잡음성 측정값 때문에 전체 로봇이 불필요하게 제한적인 폴백 모드로 전환되는 것을 방지할 수 있다.

전환 가드(transition guard)는 상태 변경이 허용되기 전에 반드시 충족되어야 하는 조건을 정의한다. 위치추정 고장이 발생하더라도 대체 위치추정 기능이 신뢰할 수 있는 경우에만 성능 저하 내비게이션(degraded navigation)으로 전환할 수 있으며, 주 위치추정과 백업 위치추정을 모두 상실한 경우에는 최소 위험 기동이 필요할 수 있다. 따라서 가드는 진단 증거와 기능 요구사항을 연결하여 전환 대상 상태가 실제로 남아 있는 기능으로 지원될 수 있도록 한다.

상태 머신은 경고(warning), 성능 저하(degraded), 심각(critical), 종결(terminal) 조건을 구분해야 한다. 초기 경고는 임무를 변경하지 않은 상태에서 추가적인 모니터링을 활성화하거나 선택적인 작업 부하를 제거할 수 있다. 성능 저하가 지속되면 속도, 경로, 모델 또는 작업 복잡도를 제한할 수 있다. 심각한 조건에서는 제어된 종료(controlled termination)를 시작할 수 있으며, 복구할 수 없는 결함은 유지보수 또는 승인된 개입이 이루어질 때까지 시스템을 안정적인 안전 상태에 둘 수 있다.

계층형 상태 머신(hierarchical state machine)은 물리 인공지능이 여러 자율성 계층을 포함하기 때문에 유용하다. 상위 수준의 시스템 상태는 정상(Normal), 성능 저하(Degraded), 복구(Recovery) 또는 안전 운용(Safe Operation)을 나타낼 수 있으며, 중첩 상태(nested state)는 인지 폴백(perception fallback), 위치추정 폴백, 통신 손실, 연산 축소, 배터리 비상 또는 인간 인수(human takeover)를 나타낼 수 있다. 이러한 구조는 로컬 폴백 로직이 전체 안전 목표와 충돌하지 않으면서 서브시스템 수준의 세부 정보를 유지하도록 한다.

폴백 상태는 제어 권한(control authority)을 명시적으로 정의해야 한다. 정상 운용에서는 AI 플래너가 검증된 제어 계층을 통해 궤적을 명령할 수 있다. 성능 저하 상태에서는 권한이 경량 모델(lightweight model), 결정론적 플래너(deterministic planner) 또는 제한된 로컬 자율성으로 이동할 수 있다. 심각한 상태에서는 고전 제어기(classical controller), 비상 기능 또는 안전 프로세서(safety processor)가 우선적인 권한을 가질 수 있다. 인간 인수는 온보드 안전 기능과 조정되어야 하는 또 하나의 권한 상태를 도입한다.

상태 진입 동작(state entry action)은 전환 직후 수행되는 행동을 정의한다. 성능 저하 운용에 진입하면 속도를 낮추고, 선택적 모델을 비활성화하며, 안전 여유(safety margin)를 확대하고, 경로를 제한하거나 플릿 인프라(fleet infrastructure)에 상태를 알릴 수 있다. 최소 위험 기동 상태에 진입하면 임무 명령을 취소하고 제어된 감속 또는 안전 구역으로의 이동을 시작할 수 있다. 진입 동작은 느슨하게 조정된 서브시스템 대응에 의존하는 대신 시스템 반응을 결정론적으로 만든다.

상태 종료 조건(state exit condition)도 마찬가지로 중요하다. 결함이 순간적으로 사라졌다는 이유만으로 완전 자율 운용을 즉시 복원해서는 안 된다. 복구에는 안정적인 센서 출력, 허용 가능한 위치추정 신뢰도, 충분한 배터리 예비량, 정상적인 연산 지연, 신뢰할 수 있는 통신, 성공적인 진단 또는 일정 시간 동안 주 시스템과 백업 시스템 사이의 일치가 요구될 수 있다. 이러한 조건은 아직 신뢰 가능한 운용을 입증하지 못한 기능이 조기에 복원되는 것을 방지한다.

히스테리시스 및 지속성 메커니즘(hysteresis and persistence mechanism)은 상태 사이에서 빠르게 진동하는 현상을 방지하는 데 도움을 준다. 예를 들어 온도가 임계값을 반복적으로 넘나들거나 네트워크 연결이 간헐적으로 불안정하면 정상 운용과 성능 저하 운용 사이에서 지속적인 상태 전환이 발생할 수 있다. 서로 다른 진입 및 종료 임계값, 최소 체류 시간(minimum dwell time), 신뢰도 윈도우(confidence window), 안정화 구간(stability interval)을 적용하면 상태 머신이 불안정한 모드 전환을 방지하면서도 명확하게 대응할 수 있다.

타임아웃(timeout)은 전환 상태가 의도한 목적을 완료하지 못하는 경우를 보호한다. 재위치추정(relocalization), 네트워크 재연결, 모델 재시작, 충전 또는 원격 지원을 시도하는 로봇은 임시 상태에 무기한 머물러서는 안 된다. 타임아웃이 만료되면 상태 머신은 남아 있는 기능과 환경 위험에 따라 더욱 제한적인 상태로 에스컬레이션(escalation)하거나, 임무 중단(mission abort)을 시작하거나, 최소 위험 기동을 실행할 수 있다.

복구는 일반적으로 고장 상태에서 완전 자율 운용으로 직접 전환하기보다 제어된 중간 상태(controlled intermediate state)를 통해 진행되어야 한다. 복구된 센서 또는 AI 모델은 먼저 관측 모드(observation mode)나 섀도 모드(shadow mode)에서 작동한 후 제한된 권한으로 참여하고, 검증을 완료한 이후 정상 운용으로 복귀할 수 있다. 이러한 단계적 진행은 복원된 구성요소가 안전 관련 물리적 행동에 다시 영향을 주기 전에 시스템이 일관성을 검증할 수 있도록 한다.

동시 결함(concurrent fault)이 발생하면 여러 폴백 조건이 동시에 활성화될 수 있으므로 중재(arbitration)가 필요하다. 통신 손실 상황에서는 로컬 자율성이 허용될 수 있지만 위치추정 고장이 동시에 발생하면 내비게이션을 계속하는 것이 허용되지 않을 수 있다. 상태 머신은 가장 안전 제한이 강한 관련 조건이 우선하도록 우선순위 규칙(precedence rule)을 적용해야 한다. 하위 수준의 복구 동작이 제어된 정지 또는 안전 상태 진입에 대한 상위 수준의 요구사항을 무시해서는 안 된다.

임무 상태(mission state)와 안전 상태(safety state)는 논리적으로 분리하되 서로 조정되어야 한다. 임무는 실행 중(Running), 일시정지(Paused), 재계획(Replanning), 복귀(Returning) 또는 중단(Aborted) 상태일 수 있으며, 안전 제어기는 독립적으로 정상(Normal), 성능 저하(Degraded), 최소 위험(Minimum Risk) 또는 안전 상태(Safe State) 운용을 결정할 수 있다. 이러한 분리는 임무 목표가 안전 요구사항을 재정의하는 것을 방지하고 생산성이 결함 조건으로 인해 설정된 운용 제한보다 우선하지 않도록 한다.

모든 상태 전환은 출발 상태(source state), 목적 상태(destination state), 트리거(trigger), 가드 평가(guard evaluation), 활성 결함, 시스템 건전성(system health), 권한 변경 및 실행된 동작을 설명하는 추적 가능한 증거(traceable evidence)를 생성해야 한다. 전환 이력을 통해 엔지니어는 로봇이 특정 방식으로 행동한 이유를 재구성하고 반복적인 상태 진동, 불필요한 폴백 활성화, 실패한 복구 또는 안전하지 않은 가정을 식별할 수 있다. 또한 이러한 정보는 검증 및 유효성 확인(verification and validation)을 위한 중요한 증거를 제공한다.

궁극적으로 폴백 상태 머신(fallback state machine)은 다양한 고장을 제한되고 이해 가능한 시스템 행동의 진행 과정으로 변환한다. 정상 자율 운용은 명시적인 증거와 검증된 기능에 따라 성능 저하 운용, 복구, 최소 위험 기동, 임무 중단 또는 안전 상태로 단계적으로 축소될 수 있다. 가드 기반 전환(guarded transition), 권한 관리, 계층 구조, 히스테리시스, 타임아웃, 결함 중재, 단계적 복구 및 로깅을 결합함으로써 물리 인공지능은 예측 불가능하게 실패하는 대신 통제되고 점진적인 방식으로 실패하도록 설계할 수 있다.
