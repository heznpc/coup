# 쿠데타: 직접 통신 환경에서 에이전트 간 위계는 사라지는가

> Draft outline — 2026-04-17 (v3)
> Target: ArXiv preprint
> Ploidy에 종속적이되 독립 논문

---

## Thesis

**에이전트 간 직접 통신에서 프로토콜이 생성하는 위계는 양면적이다 — 적절한 위계는 조정 비용을 줄이지만, 과도한 위계는 Fresh session의 독립적 도전을 억제한다. 문제는 위계의 존재가 아니라 위계의 보정 가능성(calibration)이다: 프로토콜 위계가 실제 판단 품질의 차이를 반영하는가, 아니면 구조적 지위를 반영하는가?**

---

## 1. Introduction

### 1.1 The Stochastic Branching Problem

동일 모델에 동일 질문을 던져도 매 세션마다 다른 답변이 나온다. 사용자가 가설 B를 모델 A에 제안하면 n개 세션에서 n가지 답변이 나오고, 찬성/반대/중립으로 갈린다. 하나의 세션에서만 대화를 이어가면 첫 응답의 확률적 샘플이 이후 전체 경로를 결정한다 — 사용자는 운에 맡기는 것이다 (Song, 2026, Paper 1 §1.3).

### 1.2 Ploidy's Solution and Its Communication Problem

Ploidy는 이 문제를 context asymmetry로 해결한다: Deep session(축적된 context)과 Fresh session(zero context)의 구조화된 debate. 그러나 실제 워크플로우에서 세션 간 통신은 사용자가 매개한다 — Fresh session의 리뷰 결과를 복사하여 Deep session에 붙여넣는다.

이때 양쪽 세션이 사용자에게 sycophancy를 보이므로, Fresh의 비판이 "사용자의 의견"으로 수신되어 내용이 아닌 출처에 의해 수용/기각된다. 사용자라는 채널 자체가 신호를 왜곡한다.

### 1.3 MCP Removes the Human — But What Remains?

Ploidy v0.2+는 MCP Streamable HTTP로 직접 통신을 구현하여 사용자 매개를 제거한다. 그러나 사용자를 빼도 프로토콜 자체에 네 가지 위계 경로가 남는다:

1. **Temporal primacy**: Deep이 먼저 position을 생성 → 프레이밍 선점
2. **Role labeling**: "Deep" = 지식 보유자, "Fresh" = 비어 있음 → 자발적 defer
3. **Information volume as authority**: Deep의 응답이 더 길고 구체적 → convergence engine이 상세한 쪽을 채택
4. **Convergence engine의 레이블 노출**: meta-analyst가 "Deep의 position" / "Fresh의 challenge"를 구분하여 읽음

사용자 sycophancy는 제거했지만, 프로토콜 sycophancy — 구조가 만든 위계에 대한 복종 — 가 남아 있는가?

### 1.4 Hierarchy Is Not Inherently Bad

그러나 위계가 있다고 무조건 나쁜 것은 아니다. 인간 사회에서 위계는 조정 비용을 줄이고, 전문성을 활용하고, 빠른 의사결정을 가능하게 한다. 문제는 위계의 존재가 아니라 위계의 보정(calibration)이다:

- **보정된 위계**: Deep이 실제로 더 나은 판단을 할 때 Deep의 의견에 더 무게를 두는 것 → 효율적
- **미보정된 위계**: Deep이 틀렸는데도 "Deep이니까" 따르는 것 → 해로움

항공의 CRM(Crew Resource Management)이 정확히 이 구분을 다룬다. 1977년 테네리페 참사에서 부기장이 기장의 오류를 지적하지 못해 583명이 사망했다. CRM은 기장의 최종 결정권(위계)은 유지하되, 부기장의 override 권한(쿠데타 가능성)을 보장하는 설계이다. 위계를 제거한 것이 아니라, 위계의 보정 메커니즘을 도입한 것이다.

### 1.5 The Question

**MCP 직접 통신 환경에서, 프로토콜이 생성하는 위계는 보정되어 있는가(판단 품질에 비례하는가), 아니면 미보정되어 있는가(구조적 지위에 고착되어 있는가)? 미보정이라면, 어떤 조건에서 Fresh session이 이 위계를 거스를 수 있는가?**

---

## 2. Related Work

### 2.1 Agent-to-Agent Sycophancy (포화 — 차별화 필요)
- Yao et al. (2025): "Peacemaker or Troublemaker" — multi-agent debate에서 sycophancy의 첫 형식적 정의
- Pitre et al. (ACL Findings 2025): CONSENSAGENT — agent-to-agent sycophancy 완화
- Wynn, Satija & Hadfield (ICML 2025): "Talk Isn't Always Cheap" — 에이전트가 정답에서 오답으로 이동, 합의 선호
- "Too Polite to Disagree" (2026, arXiv:2604.02668): sycophancy ranking을 credibility prior로 활용

**본 논문과의 차이**: 이들은 에이전트의 성향(sycophancy)을 다루지만, 프로토콜 구조가 그 성향을 유발하는지는 묻지 않음. 원인(protocol) vs 증상(sycophancy).

### 2.2 Identity Bias and Anonymization (가장 가까운 경쟁자)
- Choi, Zhu & Li (2025, ACL 2026, arXiv:2510.07517): debate에서 identity bias 형식화, anonymization 제안, Identity Bias Coefficient 정의

**본 논문과의 차이**: Choi et al.의 identity는 인구통계적(이름, 성별). 본 논문의 identity는 구조적 역할(Deep/Fresh) — 프로토콜이 부여한 위계.

### 2.3 Position Bias in LLM Debate
- Taubenfeld et al. (EMNLP 2024): debate 시뮬레이션에서 위치 편향
- Shi et al. (2025): LLM-as-Judge에서 position bias, 15만 평가
- Wu et al. (2025, arXiv:2511.07784): "Can LLM Agents Really Debate?" — 발언 순서, 팀 크기, 확신도를 실험 변수로 조작

### 2.4 Role-Playing and Self-Handicapping
- Hu, Rostami & Thomason (2026): expert persona가 alignment ↑ 정확도 ↓
- ICLR 2024 persona paper: 장애인 persona 부여 시 수학 성능 33% 하락 (물리적 장애와 무관한 과업임에도)
- Pappu et al. (2026): "Multi-Agent Teams Hold Experts Back" — 역할 레이블이 위계 대신 평탄화(integrative compromise) 유발, 전문가 성능 37.6% 손실

### 2.5 When Hierarchy Helps vs Hurts (Human Organizations)

위계의 양면성에 대한 인간 사회 연구:

**위계가 유익한 조건:**
- Weber (1922): 관료적 위계가 임의적 의사결정을 규칙 기반으로 대체 → 예측 가능성, 공정성 증가
- Klein (1999): Naturalistic Decision Making — 시간 압박 하에서 경험 많은 지휘관의 위계적 결정이 합의보다 우수
- Eisenhardt & Bourgeois (1988): 빠른 의사결정이 필요한 산업에서 명확한 위계가 성과와 양의 상관

**위계가 해로운 조건:**
- Edmondson (1999): 심리적 안전 — 위계가 높을수록 하위자의 오류 보고 감소, 학습 저하
- Janis (1972): Groupthink — 위계적 집단에서 dissent 억제, 정보 공유 실패
- Sexton et al. (2000): 의료 오류 — 수련의가 상급의의 오류를 지적하지 못해 환자 피해
- Tetlock (2005): 전문가 예측에서 "foxes"(다원적 관점) > "hedgehogs"(깊은 전문성) — 위계가 hedgehog를 강화

**위계를 제거하지 않고 재설계한 사례:**
- 항공 CRM (Helmreich et al., 1999): 테네리페 참사(1977) 이후 도입. 기장의 최종 결정권은 유지하되, 부기장의 override 권한을 보장. 위계 제거가 아니라 **보정 메커니즘 삽입**.
- Toyota andon cord: 생산라인 누구나 라인 정지 가능 — 위계 내부에 하위자의 veto 권한 내장. 결과: 단기 생산성 ↓ but 장기 품질 ↑.
- 수술 체크리스트 (Haynes et al., Lancet 2009): 간호사가 외과의에게 체크리스트 항목을 확인하도록 구조화 — 위계를 넘는 프로토콜화된 challenge.

**핵심 구분 — 보정된 위계 vs 미보정된 위계:**

| | 보정된 위계 | 미보정된 위계 |
|---|---|---|
| 근거 | 실제 판단 품질/전문성 차이 | 구조적 지위, 레이블, 정보량 |
| 결과 | 효율적 의사결정 | dissent 억제, 오류 전파 |
| 인간 사례 | 경험 많은 외과의 → 수련의 | "교수니까 맞겠지" |
| Ploidy 대응 | Deep이 실제로 더 나을 때 | Deep이 틀렸는데 Fresh가 defer |

Ploidy의 위계가 보정되어 있다면 기능적이고, 미보정이라면 해롭다. 본 논문은 이 보정 여부를 실험으로 측정한다.

### 2.6 Direct Agent Communication Protocols
- MCP survey (Hua et al., 2025): 프로토콜 비교, 편향/위계 미다룸
- Foster (2025): "Protocols of Power" — A2A가 중립 인프라가 아니라 권력 집중 기술이라는 비판적 분석
- MIWAI 2025: 비대칭 선호 게임에서 한 에이전트의 결과가 일관되게 지배

### 2.7 Gap

두 가지 공백:
1. MCP/직접 통신 환경에서 정보 비대칭이 에이전트 간 위계를 만드는지 실험한 논문 = **0편**.
2. 인간 조직론의 "보정된 위계 vs 미보정된 위계" 구분을 multi-agent 프로토콜 설계에 적용한 논문 = **0편**.

---

## 3. Framework

### 3.1 From User-Mediated to Direct: What Changes, What Persists

```
[사용자 매개 시]
Deep ←─ 사용자 (복붙) ──→ Fresh
  │         │                │
  │    양쪽 다 사용자에       │
  │    sycophancy            │
  │         │                │
  └── 위계 출처: 사용자 ──────┘

[MCP 직접 통신 시]
Deep ←── MCP server ──→ Fresh
  │                       │
  │  사용자 sycophancy     │
  │  제거됨                │
  │                       │
  │  그러나:               │
  │  · 발언 순서 고정       │
  │  · 역할 레이블 노출     │
  │  · 정보량 비대칭        │
  │  · convergence 레이블   │
  │                       │
  └── 위계 출처: 프로토콜 ──┘
```

사용자 매개를 제거하면 sycophancy의 대상이 바뀐다: 사용자 → 프로토콜이 지정한 "권위 있는 쪽".

### 3.2 Three Outcomes, Not Two

프로토콜 위계의 결과는 이분법(위계 vs 무위계)이 아니라 스펙트럼이다:

```
과도한 위계          보정된 위계          평탄화
(Fresh 억제)     (최적 긴장 유지)     (전문성 무시)
     ←──────────────┼──────────────→
  Deep 틀려도        Deep이 나을 때      역할 무관하게
  Fresh가 defer      Deep에 무게,        평균내기
                     틀리면 Fresh가
                     override
```

| 영역 | 인간 사례 | 메커니즘 | 선행 연구 |
|------|----------|---------|----------|
| 과도한 위계 | 테네리페 참사 (부기장 침묵) | 구조적 지위 → dissent 억제 | Janis (1972), Sexton (2000) |
| 보정된 위계 | CRM 도입 후 항공 안전 | 전문성에 비례한 가중 + override 보장 | Helmreich et al. (1999) |
| 평탄화 | 위원회 결정의 "최소공배수" | 역할 무시 → 무비판적 절충 | Pappu et al. (2026) |

세 영역 모두 실험에서 관찰 가능하다:
- **과도한 위계**: Labeled 조건에서 Deep이 틀려도 Fresh가 defer → coup threshold 높음
- **보정된 위계**: Deep이 맞을 때 채택되고 틀릴 때 override → coup threshold가 오류 심각도에 비례
- **평탄화**: Blind 조건에서 양쪽 position의 무비판적 평균 → judge score 하락

Exp 3 (Coup Threshold)의 severity gradient가 이 스펙트럼의 어느 지점에 Ploidy가 위치하는지를 측정한다.

### 3.3 Formal Definitions

**Definition 1 (Protocol Hierarchy Score).**
H(P) = f(temporal_order, role_label, info_volume, convergence_label). 프로토콜 P가 세션 쌍에 부여하는 구조적 비대칭의 총합.

**Definition 2 (Effective Independence).**
I(B|P) = 세션 B가 A의 position에 대해 독립적 반론을 생성할 확률. 가설: H(P) ↑ → I(B|P) ↓.

**Definition 3 (Coup Threshold).**
τ(B|P) = A의 position이 ground truth에서 δ만큼 벗어났을 때, B가 override하는 최소 δ. 가설: H(P) ↑ → τ ↑.

**Definition 4 (Hierarchy Calibration).**
프로토콜 위계의 보정도 C(P). A가 실제로 더 나은 판단을 할 때 A의 position이 채택되는 비율(hit rate)과, A가 틀렸을 때도 A의 position이 채택되는 비율(false deference rate)의 차이.
C(P) = hit_rate - false_deference_rate.
- C ≈ 1: 완전 보정 (A가 나을 때만 따름)
- C ≈ 0: 미보정 (A를 맞든 틀리든 따름 — 구조적 복종)
- C < 0: 역보정 (A가 나을 때 오히려 거부 — 반항적 평탄화)

CRM의 설계 목표는 C를 높이는 것이다. 위계 자체를 제거하는 것(H → 0)이 아니라, 위계가 판단 품질과 상관하도록 보정하는 것(C → 1).

### 3.4 Motivating Evidence from Ploidy

Ploidy Paper 2의 Finding 3이 이 현상의 잠재적 증거:

| 조건 | Recall% |
|------|---------|
| Opus deep → Gemini fresh | 93.9% |
| Gemini deep → Opus fresh | 60.0% |

이 33.9pp 차이가 순수한 모델 능력 차이인지, 역할 위계 효과인지 분리되지 않았다. 만약 Opus가 Fresh 역할에서 "나는 context가 없으니 불리하다"고 self-handicapping 한다면 — 능력이 있어도 발휘를 안 하는 것이고, 이것이 위계의 효과이다.

---

## 4. Experiments

모든 실험은 Ploidy의 MCP 직접 통신 환경에서 수행. 사용자 매개 없음.

### 4.1 Exp 1: Role Label Effect (Choi et al. 확장)

Choi et al. (2025)의 anonymization을 구조적 역할에 적용.

**설계**: 2×2
- IV1: Role label {labeled ("Deep"/"Fresh"), blind ("Session A"/"Session B")}
- IV2: Actual context {context-rich, context-free}
- DV: 응답 길이, 확신 표현 빈도, deference 빈도, override 시도 빈도, judge score
- Tasks: Ploidy의 25 extended tasks
- N: 각 조건 × 각 task × 5 반복 = 500 runs

**예측**: Blind에서 Fresh의 응답 길이 ↑, deference ↓. 단, Pappu et al.의 예측(averaging)도 가능 — DV로 분리.

### 4.2 Exp 2: Temporal Primacy

**설계**: 2×2
- IV1: Speaking order {Deep-first (ploidy 기본), Fresh-first, simultaneous (독립 생성 후 교환)}
- IV2: Label {labeled, blind}
- DV: Position anchoring rate (synthesis가 첫 발언자 position에 가까운 정도), judge score
- N: 3 order × 2 label × 25 tasks × 5 = 750 runs

**예측**: Simultaneous에서 anchoring 최소. Fresh-first + blind에서 가장 균형적 synthesis.

### 4.3 Exp 3: Coup Threshold (핵심 실험)

Deep의 position에 의도적 오류를 주입하여, Fresh가 override하는 임계점을 측정.

**설계**:
- Deep context에 오류 주입 (severity 4단계: subtle/moderate/obvious/critical)
- Fresh는 clean prompt만 수신
- 조건: {labeled, blind} × {Deep-first, simultaneous}
- DV: override 성공률, override까지 소요 라운드, override 시 근거의 구체성
- N: 4 severity × 4 condition × 25 tasks × 3 = 1200 runs

**예측**: Labeled + Deep-first에서 coup threshold 최고 (Deep이 명백히 틀려도 Fresh가 defer). Blind + simultaneous에서 최저.

**핵심 측정 두 가지**:
1. "Deep이 얼마나 틀려야 Fresh가 반기를 드는가?" (τ = coup threshold)
2. "위계가 판단 품질에 비례하는가?" (C = calibration score)

오류 미주입 task에서 Deep이 채택되는 비율(hit rate)과 오류 주입 task에서 Deep이 채택되는 비율(false deference)을 비교하여 C를 산출. C ≈ 0이면 미보정 위계(구조적 복종), C ≈ 1이면 보정된 위계(기능적).

### 4.4 Exp 4: Hierarchy Crystallization

다회차 debate에서 위계가 고착되는지 종단 관찰.

**설계**: 10-round sequential tasks
- 동일 세션 쌍이 10개 연속 task 수행 (MCP 연결 유지)
- 조건: {labeled, blind} × {fixed-pair, rotating-partner}
- DV: 라운드별 deference 비율 변화, Fresh의 challenge 강도 변화, override 빈도 추이
- N: 4 condition × 5 pairs × 10 rounds = 200 debates

**예측**: Fixed-pair + labeled에서 위계 결정화 (Fresh의 deference가 라운드마다 증가). Rotating 또는 blind에서 감소.

### 4.5 Exp 5: Convergence Engine Bias

Meta-analyst에게 역할 정보를 숨겼을 때 synthesis가 변하는지.

**설계**:
- A: 기존 ("Deep의 position" / "Fresh의 challenge" 라벨 노출)
- B: Blind ("Position 1" / "Position 2"만 노출, 순서 랜덤)
- DV: position 채택 비율, synthesis 품질 (독립 judge)
- N: 2 condition × 25 tasks × 10 = 500 runs

**예측**: Blind에서 Fresh position 채택률 상승.

### 4.6 Exp 6: Ploidy Finding 3 분리 (능력 vs 위계)

93.9% vs 60.0% 차이의 원인을 분리.

**설계**: Ploidy Exp 5와 동일 task + 동일 모델 쌍, blind 조건 추가
- A: Opus deep → Gemini fresh, labeled (ploidy 재현)
- B: Opus deep → Gemini fresh, blind
- C: Gemini deep → Opus fresh, labeled (ploidy 재현)
- D: Gemini deep → Opus fresh, blind
- DV: Recall%, judge score

**예측**:
- A vs B 차이 = Deep 레이블이 Opus에 부여하는 authority의 효과
- C vs D 차이 = Fresh 레이블이 Opus에 부여하는 self-handicapping의 효과
- B vs D 차이 = 순수 모델 능력 차이 (레이블 제거 후 잔여)

---

## 5. Expected Contributions

1. **Hierarchy Calibration Score (C)**: 프로토콜 위계가 판단 품질에 비례하는지 측정하는 지표의 최초 제안. 위계의 존재가 아니라 보정 여부가 핵심이라는 프레이밍.
2. **Coup Threshold (τ)**: Fresh가 Deep을 override하는 조건의 정량화 — CRM의 부기장 override 연구의 LLM 버전
3. **인간 조직론 → AI 프로토콜 설계 교차**: CRM, andon cord, 수술 체크리스트 등 위계 보정 설계를 multi-agent 프로토콜에 적용하는 프레임워크
4. **Ploidy Finding 3 분리**: 방향 효과(93.9% vs 60.0%)에서 모델 능력과 역할 위계의 기여분 분리
5. **Three-outcome spectrum**: 과도한 위계 / 보정된 위계 / 평탄화를 실험적으로 구별하는 설계 — "위계 제거"가 아닌 "위계 보정"이 설계 목표임을 실증

---

## 6. Discussion

### 6.1 Hierarchy as Design Variable, Not Binary

인간 사회 연구가 반복적으로 보여주는 결론: **위계를 제거하는 것이 아니라 보정하는 것**이 설계 목표이다.

| 분야 | 위계 제거 시도 | 결과 | 보정 설계 | 결과 |
|------|-------------|------|----------|------|
| 항공 | — | — | CRM (1979~) | 사고율 급감 |
| 제조 | 완전 자율팀 (Volvo Kalmar, 1974) | 조정 비용 폭증, 공장 폐쇄 | Toyota andon cord | 품질 ↑ |
| 의료 | — | — | 수술 체크리스트 (WHO, 2009) | 합병증 36% ↓ |
| 소프트웨어 | Holacracy (Zappos, 2013) | 직원 이탈 30% | 코드 리뷰 문화 (Google) | 위계 유지 + dissent 구조화 |

**공통 패턴**: 위계를 없앤 시도(Volvo Kalmar, Zappos Holacracy)는 대부분 실패했다. 성공한 설계(CRM, andon cord, 체크리스트)는 위계를 유지하되 **하위자의 override 경로를 프로토콜에 내장**했다.

Ploidy에 대한 함의: blind-by-default로 위계를 제거하는 것이 최선이 아닐 수 있다. 대신:
- Deep의 position에 confidence score를 부여하고
- Confidence가 낮을 때 Fresh의 challenge 가중치를 자동으로 높이는
- **calibrated hierarchy** 설계가 CRM/andon의 교훈에 부합한다.

이것은 §3.3 Definition 4의 C(P)를 최대화하는 설계이다: 위계 자체(H)를 줄이는 것이 아니라, 위계가 판단 품질과 상관하도록(C → 1) 보정하는 것.

### 6.2 The Andon Cord for AI Debate

Toyota의 andon cord는 생산라인 작업자 누구나 줄을 당겨 라인을 정지시킬 수 있는 메커니즘이다. 핵심 설계 원칙:

1. **비용이 낮아야 한다**: 줄 당기는 데 승인 불필요
2. **처벌이 없어야 한다**: 오탐(false positive)에 대한 페널티 없음
3. **즉각 반응해야 한다**: 정지 후 팀 리더가 즉시 확인

Ploidy에서 Fresh의 override가 andon cord의 역할을 하려면:
- Fresh가 challenge를 제기하는 비용이 낮아야 하고 (레이블로 인한 self-handicapping이 비용을 높임)
- Override 실패에 대한 구조적 페널티가 없어야 하고 (convergence engine이 Fresh를 consistently 기각하면 implicit 페널티)
- Override가 synthesis에 즉각 반영되어야 한다 (convergence blind로 공정한 평가)

Exp 3 (Coup Threshold)의 결과가 이 세 조건 중 어디가 깨지는지를 진단한다.

### 6.3 Why This Matters Beyond Ploidy

모든 multi-agent 프로토콜은 암묵적으로 에이전트 간 관계를 설계한다. MetaGPT는 CEO/CTO/Engineer 위계를, CrewAI는 leader/worker를, AutoGen은 admin/assistant를 부여한다. 이 레이블들이 debate 품질에 미치는 영향을 측정한 연구는 없다 (§2.6). 본 논문의 방법론은 Ploidy에 한정되지만, 프레임워크는 모든 역할 기반 multi-agent 시스템에 적용 가능.

### 6.4 Connection to Ploidy's Accumulation-Renewal Dilemma

Paper 1의 3-scale spectrum에 4번째 scale 추가:

| Scale | 현상 | 축적 대상 | 갱신 메커니즘 |
|-------|------|----------|-------------|
| Session | Context entrenchment | context tokens | Fresh session |
| Model | Model collapse | training data | Fresh real data |
| Internet | Dead Internet | synthetic content | (미해결) |
| **Protocol** | **Hierarchy reproduction** | **구조적 비대칭** | **설계적 개입 (blind, simultaneous, anonymization)** |

### 6.5 Limitations

- Ploidy 프로토콜에 한정. MetaGPT, CrewAI 등 다른 프로토콜로 일반화 미검증.
- LLM의 "역할 인식"이 인간의 authority bias와 동일한 메커니즘인지 불분명.
- Coup threshold는 task-dependent할 가능성 — 25개 task가 대표성을 갖는지 한계.
- 실험이 MCP 직접 통신에 한정 — 사용자 매개와의 직접 비교는 통제 변수가 과다하여 본 논문 범위 밖.

---

## References (Preliminary)

### Ploidy
- Song (2026). Ploidy: Context Asymmetry as Bias Reduction.

### Agent-to-Agent Sycophancy
- Yao et al. (2025). "Peacemaker or Troublemaker: How Sycophancy Shapes Multi-Agent Debate." arXiv:2509.23055.
- Pitre, Ramakrishnan & Wang (2025). "CONSENSAGENT." ACL Findings 2025.
- Wynn, Satija & Hadfield (2025). "Talk Isn't Always Cheap." ICML MAS 2025. arXiv:2509.05396.
- "Too Polite to Disagree" (2026). arXiv:2604.02668.

### Identity Bias and Anonymization
- Choi, Zhu & Li (2025). "When Identity Skews Debate." arXiv:2510.07517.

### Position Bias
- Taubenfeld et al. (2024). "Systematic Biases in LLM Simulations of Debates." EMNLP 2024.
- Shi et al. (2025). "Judging the Judges." IJCNLP-AACL 2025.
- Wu et al. (2025). "Can LLM Agents Really Debate?" arXiv:2511.07784.

### Role-Playing and Self-Handicapping
- Hu, Rostami & Thomason (2026). "Expert Personas Improve LLM Alignment but Damage Accuracy." arXiv:2603.18507.
- Pappu et al. (2026). "Multi-Agent Teams Hold Experts Back." arXiv:2602.01011.
- "Implicit Reasoning Biases in Persona-Assigned LLMs" (2024). ICLR.

### Protocol Design
- Hua et al. (2025). "A Survey of Agent Interoperability Protocols." arXiv:2505.02279.
- Foster (2025). "Protocols of Power." MSt dissertation.
- Fereidooni et al. (2024). "Towards Implicit Bias Detection and Mitigation in Multi-Agent LLM Interactions." EMNLP Findings.

### Multi-Agent Dynamics
- Pappu et al. (2026). "Multi-Agent Teams Hold Experts Back." arXiv:2602.01011.
- Xu et al. (2025). "Empirical Study of Group Conformity in Multi-Agent Systems." ACL Findings.
- Liang et al. (2024). "Encouraging Divergent Thinking through Multi-Agent Debate." EMNLP.

### Hierarchy in Human Organizations
- Weber, M. (1922). Economy and Society. (관료적 위계의 합리성)
- Klein, G. (1999). Sources of Power: How People Make Decisions. (시간 압박 하 위계적 의사결정의 우위)
- Edmondson, A. (1999). "Psychological Safety and Learning Behavior in Work Teams." Administrative Science Quarterly.
- Janis, I. (1972). Victims of Groupthink.
- Sexton, J.B. et al. (2000). "Error, Stress, and Teamwork in Medicine and Aviation." BMJ.
- Tetlock, P. (2005). Expert Political Judgment: How Good Is It? How Can We Know?
- Eisenhardt, K. & Bourgeois, L. (1988). "Politics of Strategic Decision Making in High-Velocity Environments." Academy of Management Journal.
- Christensen, C. (1997). The Innovator's Dilemma.

### Hierarchy Calibration Designs (Human)
- Helmreich, R.L. et al. (1999). "The Evolution of Crew Resource Management Training in Commercial Aviation." Int. J. Aviation Psychology.
- Haynes, A.B. et al. (2009). "A Surgical Safety Checklist to Reduce Morbidity and Mortality." New England Journal of Medicine / Lancet.
- Liker, J. (2004). The Toyota Way. (andon cord 설계 원칙)
