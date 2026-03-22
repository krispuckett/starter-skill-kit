---
name: health-interpreter
description: >
  Evidence-based Apple Watch and wearable health data interpreter with blood lab
  cross-correlation. Transforms raw biometric and lab data into actionable insights
  using personal baselines, composite scoring, cross-metric pattern detection, and
  research-backed decision trees. Covers HRV, resting HR, SpO2, sleep staging,
  respiratory rate, VO2max, walking HR, heart rate recovery, training load, body
  composition, iron panel, inflammation markers, CBC, metabolic panel, hormones,
  advanced lipids, and micronutrients. Calibrates to YOUR body — not population
  averages. Use when: interpreting health or lab data, analyzing Apple Watch metrics,
  making training decisions from biometrics, understanding blood work, or any question
  like "what do my numbers mean?" NOT for: diagnosing conditions or replacing medical advice.
metadata:
  author: kris-puckett
  version: '1.0'
  evidence-date: '2026-03'
  license: MIT
---

# Health Interpreter

An evidence-based framework for interpreting wearable health data. Built from real
experience tracking health metrics through chronic illness, recovery, and performance
training — then abstracted into a system anyone can use.

**Core philosophy: orientation, not optimization.** Weekly trends matter more than
daily scores. Your body is your own reference point. Population norms are context,
not targets.

## Setup

1. Copy `profile-template.md` to your project and fill in your personal data
2. Establish your baselines over 14-28 days of normal life (instructions in the template)
3. Point the skill at your profile: reference the filled-in profile in your conversations

The skill works without a profile, but it's dramatically more useful with one.

---

## 1. The Orientation Model

Don't optimize. Orient. Every morning, check three things:

### The Three Questions

1. **Sleep duration** — Enough or not? (7+ hours is the goal)
2. **HRV trend** — 3-day direction (rising, stable, falling)
3. **Active disruptors** — GI issues, medication changes, illness, yesterday's strain, alcohol, poor sleep, high stress

### What the Answers Mean

| Sleep | HRV Trend | Disruptors | Capacity |
|-------|-----------|------------|----------|
| Good (7+ hr) | Rising or stable | None | **Full.** Push if you want to. |
| Good | Rising or stable | Minor (1 drink, mild stress) | **Near full.** Proceed but don't max out. |
| Short OR | Falling | — | **Reduced.** Protect energy. High-value work only. |
| Any | Any | Multiple active | **Recovery day.** Triage obligations. |
| — | Falling 3+ days | — | **Investigate.** Something changed — find it. |

This isn't a prescription to avoid things. It's situational awareness.

---

## 2. Metric Interpretation Framework

For every metric below, the same hierarchy applies:

### Comparison Order (Always)
1. **Your 28-day personal median** = primary anchor
2. **Your 7-day median vs 28-day median** = current state
3. **14-day slope** = intermediate trend direction
4. **Population norms** = secondary context only
5. **Illness/disruptor context** = if active, interpret metrics as temporarily suppressed

### Rolling Windows
- **7-day** = "How am I doing this week?" (acute state)
- **14-day** = "Are interventions working?" (require ≥10 valid data points)
- **28-day** = "What is my normal right now?" (re-lock only during stable periods)

**Re-baseline rule:** Only recalculate your 28-day baseline when ≥21 of 28 days are free from flares, travel, alcohol, acute illness, or major disruptions. Otherwise, keep the older stable baseline.

---

### 2A. Heart Rate Variability (HRV / SDNN)

**What it measures:** Parasympathetic nervous system tone. Higher = better recovery capacity.

**Critical device note:** Apple Watch reports **SDNN**, not RMSSD. Most competitors (Garmin, Oura, WHOOP) report RMSSD. These are different measurements with different norms — cross-device HRV comparisons are meaningless. The ESC Task Force 24-hour SDNN thresholds (50/100 ms) do NOT apply to Apple's short-epoch averaged SDNN [23].

**Apple Watch accuracy:** Underestimates SDNN by ~8 ms (MAPE 29%) [13]. Use 7-day rolling medians, never single readings. Trend direction is reliable; absolute values are not.

#### Threshold Zones (vs YOUR 28-day baseline)

| Zone | Range | Action |
|------|-------|--------|
| 🟢 Green | ≥ baseline | Planned training may proceed |
| 🟡 Yellow | 5-10% below | Reduce intensity one zone. Zone 2 only. |
| 🟠 Orange | 10-20% below | Easy movement or rest |
| 🔴 Red | >20% below, or 2-day collapse >25% | Full rest. Assess sleep, GI, stress, illness. |

#### Decision Rules
- HRV ≥ baseline → full planned training [2][3]
- HRV falls below 10-day mean minus 1 SD or 2-day downward trend → swap intensity for low intensity or rest [2]
- HRV >20% below for 3+ days → no threshold/tempo work, no hard lifting
- HRV improves for 14 days while RHR falls → interventions are working, even if VO2max lags
- HRV falling while deep sleep falls and GI symptoms worsen → likely vagal withdrawal from inflammatory stress [8][9]

#### What Tanks HRV
- Alcohol (even 1-2 drinks can suppress next-day HRV by 20-30%)
- Poor sleep (<6 hours or fragmented)
- Acute stress / sympathetic activation
- Illness / immune response
- Overtraining without recovery
- Stimulants close to sleep (pseudoephedrine, late caffeine)
- GI distress

#### What Improves HRV
- Consistent sleep timing (circadian alignment)
- Aerobic base training (zone 2)
- Cold exposure (evidence for acute parasympathetic activation)
- Iron repletion if deficient (restores oxygen delivery)
- Stress management / nervous system downregulation

---

### 2B. Resting Heart Rate (RHR)

**What it measures:** Cardiovascular efficiency and systemic strain. Lower is generally better.

**Why it matters:** RHR is independently and linearly associated with inflammatory markers (hs-CRP, IL-6, fibrinogen) in a dose-response relationship [7]. A rising RHR often signals inflammation before you feel sick.

#### Threshold Zones (vs YOUR baseline)

| Zone | Range | Interpretation |
|------|-------|---------------|
| 🟢 Green | Within +2 bpm | Stable |
| 🟡 Yellow | +3 to +4 bpm | Mild strain |
| 🟠 Orange | +5 to +7 bpm | Moderate strain |
| 🔴 Red | >+7 bpm for 3 days, or +10 bpm single day | Investigate immediately |

#### Decision Rules
- RHR rises >3 bpm AND HRV falls >10% → real physiologic strain, not device noise
- RHR rises >5 bpm but HRV unchanged and sleep was short → likely acute sleep debt
- RHR rises >5 bpm for >3 days with worsening symptoms → likely inflammatory process
- RHR rises while respiratory rate rises and SpO2 worsens → prioritize sleep/breathing investigation
- RHR drops toward pre-illness baseline → green light to cautiously add training volume

---

### 2C. Sleep

**Key components:**
- **Deep sleep (N3):** Physical restoration, growth hormone release. Target: 1-2 hours/night
- **REM:** Cognitive consolidation, emotional processing. Target: 1.5-2 hours/night
- **Sleep efficiency:** Time asleep / time in bed. Target: >85%
- **HR dip during sleep:** Heart rate should drop 10-20% (parasympathetic dominance)

**Apple Watch accuracy:** Deep sleep sensitivity is only 50.5% vs polysomnography — it systematically underestimates by ~43 minutes [14]. Treat Apple Watch deep sleep as a **floor estimate**. Sleep/wake detection accuracy is 93%, which is solid. Trust trends, not absolutes.

**Critical parsing note:** Apple Health stores "InBed" and "Asleep" as separate values. InBed ≠ Asleep. Including InBed in sleep totals inflates duration by 2-6 hours/night. This is the #1 Apple Health data parsing error.

#### Flags Worth Investigating
- HR dip <10% during sleep = sympathetic overdrive, poor recovery
- Deep sleep <45 min (Apple Watch reading) consistently = recovery debt building
- REM suppression = often alcohol, stress, or early waking
- Sleep efficiency <85% with low SpO2 and elevated respiratory rate = suspect sleep-disordered breathing

#### Decision Rules
- Total sleep <6 hr → automatically downgrade one training intensity level regardless of HRV
- Deep sleep <45 min (Apple Watch) for 3 of 7 nights and RHR elevated → incomplete parasympathetic recovery
- Deep sleep rises while HRV rises and RHR falls over 14 days → recovery genuinely improving
- Bedtime midpoint varies >90 min → circadian disruption; reset to ±30 min window

---

### 2D. SpO2 (Blood Oxygen)

**Apple Watch accuracy:** Limits of agreement ±2.7% to ±5.9%, with outliers up to 15% [15]. 14% of readings show <95% in healthy subjects when medical-grade oximeters read normal [16]. **Isolated low readings are meaningless.**

**Altitude matters:** See the altitude adjustment table in `profile-template.md`. At higher altitudes, SpO2 is naturally lower. Don't panic at 94% if you live at 5,000+ feet.

#### Pattern-Based Interpretation

| Pattern | Meaning | Action |
|---------|---------|--------|
| Overnight avg within your baseline range | Normal | Continue monitoring |
| Overnight avg drops 2+ points from personal norm | Something changed | Investigate: illness, sleep position, alcohol, congestion |
| Isolated reading of 92-93% but weekly mean stable | Device artifact | Ignore [15][16] |
| Low SpO2 clusters align with awakenings + elevated overnight HR | Sleep-disordered breathing | Sleep study recommended |
| Low SpO2 concentrated 11pm-6am with normal daytime | Possible sleep apnea | Overnight oximetry or home sleep study |
| Low SpO2 scattered across all hours equally | Sensor artifact | Check wrist contact, band tightness |

#### Decision Rules
- Never diagnose sleep apnea from Apple Watch SpO2 alone — use wearables to trigger testing urgency
- Single SpO2 readings <95% are not emergencies (especially at altitude)
- 3-night mean dropping ≥2 points → investigate
- Overnight mean <92% on repeated nights → urgent medical evaluation regardless of altitude

---

### 2E. Respiratory Rate

Respiratory rate during sleep is a sensitive but often overlooked metric.

| Zone | Range vs Baseline |
|------|-------------------|
| 🟢 Green | Within ±0.5 br/min |
| 🟡 Yellow | +0.6 to +1.0 |
| 🟠 Orange | +1.1 to +1.5 |
| 🔴 Red | >+1.5 for 3+ nights |

#### Decision Rules
- RR rises with low HRV and high RHR → systemic stress or inflammation
- RR rises with low SpO2 and fragmented sleep → breathing-related sleep disruption
- RR rises with GI symptoms (bloating, pain, reflux) → consider diaphragm restriction, sympathetic activation
- RR >20 sustained → assess for respiratory infection, worsening sleep-disordered breathing

---

### 2F. Walking Heart Rate

Walking HR is one of the most sensitive markers of cardiovascular fitness and systemic strain. It responds faster than VO2max to deconditioning or recovery.

| Zone | Range vs Baseline |
|------|-------------------|
| 🟢 Green | Within ±3 bpm |
| 🟡 Yellow | +4 to +6 bpm |
| 🟠 Orange | +7 to +10 bpm |
| 🔴 Red | >+10 bpm sustained for 7+ days |

#### Decision Rules
- Walking HR rises >5 bpm with unchanged step count → deconditioning, fatigue, or inflammation
- Walking HR rises while weight rises and HRV falls → reduced efficiency under inflammatory/metabolic load
- Walking HR falls over 14-28 days while cardiac drift stays low → aerobic recovery returning before VO2max improves
- Walking HR is often the FIRST metric to improve when an intervention is working — watch it weekly

---

### 2G. Heart Rate Recovery (HRR)

The drop in heart rate during the first minute after stopping exercise.

| HRR1 | Classification | Action |
|------|---------------|--------|
| >25 bpm | Good autonomic recovery | Positive signal |
| 18-25 bpm | Acceptable for most contexts | Continue protocol |
| 13-17 bpm | Below expected | Assess overtraining, illness, sleep quality |
| <12 bpm | **Abnormal** — associated with 4x increased mortality risk [11] | Rest. If persistent >1 week, medical evaluation. |

#### Decision Rules
- HRR1 <12 bpm on 2 standardized tests a week apart → autonomic recovery is impaired, reduce intensity [11]
- HRR worsens with low HRV and high RHR → autonomic dysfunction is real, not just detraining
- HRR worsens while overnight SpO2 is poor → sleep-disordered breathing becomes high priority

---

### 2H. VO2max (Watch Estimate)

**Apple Watch accuracy:** Underestimates by ~6 mL/kg/min (MAPE 13%) [18]. Underestimates fitter individuals more.

This is a **28-56 day trend metric only.** Ignore week-to-week fluctuations.

#### Decision Rules
- VO2max falls while weight rises but cardiac drift stays good → body-mass effect, not cardiac decline
- VO2max falls with rising walking HR, suppressed HRV, rising RHR, and lower capacity → true cardiorespiratory decline
- Ferritin <50 ng/mL and VO2max stalls → possible iron limitation, especially at altitude [19][20]
- Weight loss alone improves VO2max (same absolute capacity ÷ lower body mass = higher mL/kg/min)

---

### 2I. Cardiac Drift and Aerobic Decoupling

During sustained aerobic exercise, heart rate gradually rises even at constant effort. The rate of this drift indicates aerobic fitness.

| Drift % (over 50+ min) | Meaning | Action |
|------------------------|---------|--------|
| <3% | Excellent aerobic stability | Can extend duration or progress |
| 3-5% | Strong | Continue protocol |
| 5-8% | Moderate; possible high-strain day | If repeated: reduce intensity, check HRV/sleep |
| >8% | Significant | Probably above true aerobic zone, or: dehydration, poor fueling, illness |
| >10% | Above threshold or acute fatigue | Full rest day follows |

#### Cardiac Efficiency
Calculate per exercise session: average speed ÷ average heart rate. Track over time. Improving efficiency with the same HR = genuine aerobic adaptation.

---

### 2J. Training Load (TRIMP) and ACWR

The acute-to-chronic workload ratio (ACWR) is the most evidence-based tool for load management [10].

#### TRIMP Calculation
For cardio: TRIMP = duration(min) × HRr × 0.64 × e^(1.92 × HRr)
Where HRr = (avg HR - resting HR) / (max HR - resting HR)

For strength: sRPE Load = duration(min) × session RPE (0-10 scale)

#### ACWR Thresholds

| ACWR | Zone | Action |
|------|------|--------|
| 0.85-1.35 | Productive | Proceed with plan [10] |
| 1.36-1.50 | Caution | Monitor closely |
| 1.51-1.70 | High risk | Only if readiness is clearly green |
| >1.70 | Spike | Reduce load for next 3-7 days |
| <0.60 | Detraining risk (if >2 weeks) | Reintroduce load gradually |

#### Decision Rules
- ACWR >1.35 AND HRV down >10% → cap all training at easy/zone 2 for 72 hours
- ACWR >1.50 regardless of HRV → cancel hard workouts for the week [10]
- Low chronic load + acute spike = higher injury risk than same ACWR from high base
- ACWR <0.7 for >14 days → reintroduce gradually; don't perpetuate underloading

---

## 3. Composite Scores

### 3A. Morning Readiness Score (0-100)

Purpose: decide training intensity for the day.

| Component | Max Points | What It Measures |
|-----------|-----------|------------------|
| HRV vs 28-day baseline | 30 | Autonomic state |
| Resting HR vs 28-day baseline | 20 | Inflammatory strain |
| Sleep (quantity + efficiency + stages) | 20 | Recovery quality |
| Respiratory rate vs baseline | 10 | Systemic stress |
| Overnight oxygenation | 10 | Sleep-breathing burden |
| Prior-day training load vs chronic | 10 | Load management |

#### HRV Subscore (0-30)
- 7-day SDNN ≥ 28-day median → 30
- 5-10% below → 22
- 10-20% below → 12
- >20% below → 0

#### RHR Subscore (0-20)
- 7-day RHR ≤ baseline +1 bpm → 20
- +2 to +3 bpm → 14
- +4 to +5 bpm → 7
- >+5 bpm → 0

#### Sleep Subscore (0-20)
Start at 20, subtract:
- -6 if total sleep <6.5 hr (single night)
- -10 if total sleep <6.0 hr or <6.5 hr for 2+ consecutive nights
- -5 if deep sleep <45 min (Apple Watch reading)
- -5 if sleep efficiency <85%
- -4 if bedtime midpoint shifts >90 min from 28-day norm

#### Respiratory Rate Subscore (0-10)
- Within ±0.5 br/min of baseline → 10
- +0.6 to +1.0 → 7
- +1.1 to +1.5 → 3
- >+1.5 → 0

#### Oxygenation Subscore (0-10)
- Overnight mean SpO2 within normal range, no clustering → 10
- Slightly below normal or scattered lows → 7
- Below normal range or recurrent lows with fragmentation → 3
- Well below normal or frequent clustered lows → 0

#### Training Load Subscore (0-10)
- ACWR 0.85-1.35 → 10
- ACWR 1.36-1.50 or 0.70-0.84 → 7
- ACWR 1.51-1.70 or 0.60-0.69 → 3
- ACWR >1.70 or <0.60 → 0

#### Interpretation

| Score | Action |
|-------|--------|
| 85-100 | Proceed with planned training. Hard day allowed if no symptom flare. |
| 70-84 | Keep volume, reduce intensity one zone. Tempo → upper Zone 2. |
| 55-69 | Recovery-focused. Zone 1-2 only, easy lifting, or walk. |
| <55 | Rest or very easy walk. Investigate what's driving the low score. |

---

### 3B. Recovery Stability Score (Weekly, 0-100)

Purpose: detect whether your body is stabilizing or becoming fragile.

| Component | Target | Max Points |
|-----------|--------|-----------|
| HRV coefficient of variation (7-day) | ≤6% | 20 |
| RHR coefficient of variation (7-day) | ≤8% | 20 |
| Sleep midpoint standard deviation | ≤45 min | 20 |
| Sleep duration standard deviation | ≤45 min | 20 |
| Respiratory rate standard deviation | ≤0.7 br/min | 20 |

| Score | Interpretation |
|-------|---------------|
| 80-100 | Stable adaptation — your recovery environment is consistent |
| 60-79 | Unstable but manageable — look for the variable causing noise |
| <60 | Unstable recovery environment — reduce hard training 30-50% if sustained 2+ weeks |

---

### 3C. Systemic Strain Composite (0-12)

Purpose: detect wearable signatures of systemic inflammatory or autonomic strain.

Score 1 point for each present:

1. HRV 7-day median >10% below 28-day baseline
2. HRV 14-day slope still negative
3. RHR 7-day median >3 bpm above baseline
4. Walking HR >5 bpm above 28-day baseline at similar activity level
5. Respiratory rate >1 br/min above baseline
6. Deep sleep <45 min on 3 of last 7 nights
7. Sleep efficiency <85% on 3 of last 7 nights
8. Overnight mean SpO2 below your normal range on 3 of last 7 nights
9. HRR1 <12 bpm after standardized moderate effort
10. Active symptom flag (whatever your condition manifests as)
11. Weight up >1.5% over 7 days with lower activity and worse HRV
12. ACWR >1.35 while HRV is suppressed

| Score | Level | Action |
|-------|-------|--------|
| 0-2 | Low systemic strain | Continue protocol |
| 3-5 | Mild strain | Favor lifestyle correction (sleep, diet, stress) |
| 6-8 | Likely active inflammatory/autonomic strain | Reduce training, review triggers |
| 9-12 | High-probability flare state | Prioritize recovery and medical review if >72 hours |

---

## 4. Cross-Metric Pattern Detection

These patterns emerge when multiple metrics move together. Individual metrics fluctuate; clusters tell the story.

### Pattern 1: Inflammatory / GI Flare
**Cluster:** HRV ↓>10-20% + RHR ↑>3-5 bpm + deep sleep ↓ + RR ↑>1 br/min + walking HR ↑>5 bpm + symptoms
**Mechanism:** Inflammatory cytokines activate vagal afferents, triggering autonomic withdrawal. Sympathetic dominance raises HR and suppresses recovery [7][8][9].
**Action:** Remove hard training 48-72 hr. Clean up diet. No alcohol, late meals, or known triggers. If >7 days, escalate medically.

### Pattern 2: Sleep-Disordered Breathing
**Cluster:** Overnight SpO2 below normal or clustered dips + RR elevated + deep sleep low + fragmented sleep + RHR elevated on waking + HRV suppressed + daytime fatigue
**Mechanism:** Cyclical hypoxemia fragments sleep and triggers sympathetic activation.
**Action:** Prioritize overnight oximetry or home sleep study. Avoid alcohol and large late meals. Favor side-sleeping. Reduce training intensity.

### Pattern 3: Iron-Limited Adaptation
**Cluster:** Ferritin <50 ng/mL + VO2max stagnant over 28-56 days + higher exercise HR at usual effort + fatigue despite some good HRV mornings + slower recovery after hard work
**Mechanism:** Low iron limits erythropoietic response, especially at altitude [19][20].
**Action:** Keep most work aerobic until ferritin improves. Track exercise HR at a fixed route for decoupling trends. If oral iron fails in 4-6 weeks, discuss IV iron with your doctor.

### Pattern 4: Overreaching / Load Spike
**Cluster:** ACWR >1.35 (especially >1.50) + HRV ↓>10% + RHR ↑>3 bpm + cardiac drift worsening + subjective soreness/fatigue
**Action:** Cut weekly load 30-50%. Easy movement only. Resume intensity after HRV/RHR normalize for 3+ days [10].

### Pattern 5: Positive Adaptation
**Cluster:** HRV trending up over 14 days + RHR trending down + walking HR decreasing + sleep duration/regularity stable + cardiac drift ≤3-4% + VO2max stable or rising over 28-56 days
**Meaning:** Genuine improvement in autonomic efficiency and aerobic economy.
**Action:** Progress volume 5-10% per week max. Add intensity only if ACWR ≤1.35 and recovery metrics stable.

### Pattern 6: Pre-Symptomatic Relapse Detection
**Cluster:** Gradual HRV decline over 3-5 days + slow RHR elevation + increased sleep fragmentation + reduced deep sleep — all BEFORE overt symptoms appear
**Mechanism:** Autonomic withdrawal often precedes symptom onset by days. If you have a chronic condition with flare patterns, your wearable may catch the decline before you feel it.
**Action:** If these markers trend negatively for 3-5 consecutive days, pre-emptively tighten your management protocol. Don't wait for symptoms to confirm what the data already shows.

---

## 5. Daily Decision Tree

### Step 1: Medical Red-Flag Gate
IF ANY of the following → skip training, seek medical attention:
- Chest pain, syncope, new irregular heartbeat
- Severe shortness of breath at rest
- Persistent resting SpO2 ≤90%
- Overnight mean SpO2 <92% on repeated nights with symptoms
- HRR1 <10 bpm repeatedly plus marked exercise intolerance
- RHR >10 bpm above baseline for >3 days with systemic illness signs

### Step 2: Compute Morning Readiness Score
- ≥85 → full planned training
- 70-84 → reduce intensity one category
- 55-69 → recovery session only
- <55 → rest

### Step 3: Condition-Specific Overrides
These are personal — fill them in based on your health profile:
- IF [your condition] flares AND Strain Composite ≥6 → no hard training even if readiness >70
- IF overnight oxygenation poor → no threshold/VO2 work
- IF ACWR >1.50 → no intensity regardless of readiness
- IF ferritin low and fatigue high → aerobic maintenance, not performance chasing

### Step 4: Choose Activity Level
| Readiness + Context | Activity |
|-------------------|----------|
| Green + stable recovery + ACWR ≤1.35 | Hard training OK (tempo, threshold, heavy lifting) |
| Yellow | Moderate only (zone 2, moderate lifting) |
| Orange | Easy movement (walking, mobility, technique work) |
| Red | Full recovery |

---

## 6. Research Integrity Rules

These rules are non-negotiable. They're what separate useful health interpretation from noise.

1. **No fabricated citations.** Every claim references real, published research. If no evidence exists, say so. See `references/evidence-base.md` for the full citation list with study quality ratings.

2. **Classify evidence strength.** Always note whether a recommendation is based on:
   - **Strong** evidence (RCT, meta-analysis, large prospective cohort)
   - **Moderate** evidence (observational, systematic review of observational)
   - **Limited** evidence (expert consensus, case series, mechanistic reasoning)

3. **Individual baselines over population norms.** Your 28-day median is more informative than any percentile chart. Population norms provide context; they don't define your health.

4. **Device accuracy awareness.** Apple Watch is a consumer device, not medical equipment. Know its limits (see accuracy table below) and don't over-interpret noise.

5. **Never diagnose.** Interpret and flag for medical review. "This pattern is consistent with X — discuss with your doctor" is appropriate. "You have X" is not.

6. **Actionable thresholds must clear BOTH physiologic and device noise.** A single-day HRV change of 5% could be real or could be measurement error. Sustained changes over 3+ days that exceed device noise margins are meaningful.

### Apple Watch Accuracy Reference

| Metric | Accuracy vs Gold Standard | Key Limitation | Practical Rule |
|--------|--------------------------|----------------|----------------|
| Heart Rate (rest/walk) | Mean bias -0.27 bpm, LoA ±7 bpm [17] | Worsens at high intensity | Trust for Zone 2 and resting. Caution during HIIT. |
| HRV (SDNN) | Underestimates ~8 ms, MAPE 29% [13] | Not clinically equivalent | 7-day rolling medians only. Trend > absolute. |
| SpO2 | LoA ±2.7% to ±5.9%; 14% false-lows [15][16] | Isolated dips are artifacts | Overnight averages and clustering only. |
| Sleep staging | 93% sleep/wake; deep sleep sensitivity 50.5% [14] | Underestimates deep by ~43 min | Treat as floor estimate. Trends > absolutes. |
| VO2max | Underestimates ~6 mL/kg/min, MAPE 13% [18] | Underestimates fitter people more | 28-56 day trend metric only. |

### Actionable Threshold Rules
A single-day deviation is actionable ONLY if it exceeds both physiologic and device noise:
- HRV change >20%
- RHR change >5 bpm
- Respiratory rate change >1.5 br/min
- SpO2 drop >3 points from personal baseline
- Deep sleep change >30 min

Below these thresholds, wait for 3+ day trends before acting.

---

## 7. Iron Deficiency — A Special Note

Iron deficiency without anemia is one of the most under-recognized performance limiters, especially for:
- People living at altitude (increased erythropoietic demand)
- Active individuals (exercise increases iron losses)
- People on PPIs or acid-reducing medications (impaired absorption)
- Women with regular menstrual cycles

**Key timeline for supplementation response:**
- Hemoglobin response: 2-4 weeks
- Ferritin repletion: 3-6 months
- HRV improvement: typically follows ferritin recovery by 4-8 weeks
- Target ferritin: ≥50 ng/mL for active individuals; ≥50 ng/mL minimum at altitude [19][20]

People often give up iron supplementation after 4-6 weeks because they don't feel different yet. Ferritin recovery takes months. Stay the course.

---

## 8. Fringe-But-Plausible Interventions

These have emerging evidence but aren't fully mainstream:

- **Mouth taping for sleep:** May improve nasal breathing, reduce snoring. Some evidence for better sleep quality and SpO2.
- **Morning sunlight exposure:** Strong circadian evidence. 10-30 min within 1 hour of waking.
- **Cold exposure:** Acute HRV boost, mental resilience. Evidence is real but effect is transient.
- **Continuous glucose monitoring:** Useful for identifying personal glycemic responses. Not necessary for everyone.

---

## 9. Blood Lab Interpretation Framework

Wearable data shows you trends in real time. Blood labs show you WHY those trends are happening. The combination is where this gets powerful.

**Key principle:** Lab reference ranges are population-derived — they tell you what's statistically common, not what's optimal for performance and health. Functional ranges below represent where symptoms typically resolve and where research shows meaningful health benefits.

**Never self-diagnose from labs.** Use this framework to ask better questions and have more informed conversations with your doctor.

---

### 9A. Iron Panel & Ferritin

Iron is the single most under-recognized performance limiter, especially for active people, people at altitude, people on acid-reducing medications, and menstruating women.

| Marker | Standard "Normal" | Functional Optimal | Why It Matters |
|--------|-------------------|-------------------|----------------|
| **Ferritin** | 12-150 ng/mL (F), 12-300 (M) | **≥50 ng/mL** (active); **≥50+ at altitude** | Iron storage. Most important single marker. Below 50, symptoms are common even without anemia [21][22] |
| **Serum Iron** | 60-170 mcg/dL | 80-120 mcg/dL | Circulating iron. Fluctuates with meals — fasting draw only |
| **TIBC** | 250-400 mcg/dL | 275-375 mcg/dL | Total iron-binding capacity. HIGH TIBC = body is hungry for iron |
| **Iron Saturation** | 20-50% | 25-45% | Serum iron ÷ TIBC. Below 20% = iron-deficient erythropoiesis |
| **Hemoglobin** | 12-16 g/dL (F), 14-18 (M) | Upper half of range | Oxygen-carrying capacity. Can be "normal" while ferritin is critically low |

**Altitude adjustment:** People living above 4,000 ft need more iron for erythropoietic adaptation. Target ferritin ≥50 ng/mL minimum; higher if actively training [19][20].

**PPI/acid-reducer interaction:** Reduced gastric acidity impairs non-heme iron absorption by 50-65%. If on PPIs, monitor ferritin more frequently and consider iron bisglycinate (better absorbed in low-acid environments) [29].

**Iron supplementation timeline (why people give up too early):**
- Hemoglobin response: 2-4 weeks
- Ferritin repletion: 3-6 months
- HRV and performance improvement: follows ferritin recovery by 4-8 weeks
- Don't assess "is iron working?" until 8-12 weeks minimum

#### Cross-Reference with Wearables
- Low ferritin + declining VO2max + higher exercise HR at usual effort → iron is limiting adaptation
- Ferritin rising + walking HR falling + HRV improving → iron repletion is working
- Ferritin <30 + altitude >4,000 ft + stagnant fitness despite training → strong indication for aggressive supplementation or IV iron discussion

---

### 9B. Inflammation Markers

Inflammation is the bridge between labs and wearables. When CRP rises, HRV falls and RHR rises — often in lockstep. The labs tell you severity; the wearable tells you daily trajectory.

| Marker | Reference Range | Functional Interpretation | Evidence |
|--------|----------------|--------------------------|----------|
| **hs-CRP** | <3.0 mg/L | <0.5 = low risk; 0.5-1.0 = mild; 1.0-3.0 = moderate; >3.0 = high; >10 = acute process | Cardiac risk stratification. Independently associated with RHR in dose-response [7] |
| **ESR** | 0-20 mm/hr (M), 0-30 (F) | Nonspecific but useful for tracking chronic inflammation over time | Slower to rise/fall than CRP — better for trend, worse for acute |
| **Fibrinogen** | 200-400 mg/dL | >350 warrants attention if other markers elevated | Acute phase reactant; also associated with elevated RHR [7] |

**hs-CRP and training:** Intense exercise transiently raises CRP for 24-48 hours. Always draw fasting, ≥48 hours after hard training. A "high" CRP after yesterday's hard workout is expected — a high CRP at rest with no recent intense exercise is meaningful.

#### Cross-Reference with Wearables
- Elevated hs-CRP + suppressed HRV + elevated RHR → systemic inflammation driving autonomic withdrawal [7][8]
- hs-CRP rising over serial draws + wearable metrics declining in parallel → the wearable trend is real, not noise
- hs-CRP falling + HRV improving + RHR falling → intervention is working at the tissue level

---

### 9C. Complete Blood Count (CBC)

| Marker | What to Watch For | Functional Notes |
|--------|-------------------|-----------------|
| **WBC** | 4.5-11.0 K/µL | Persistently low (<4.0) in an athlete may indicate overtraining. Persistently high without infection warrants investigation |
| **Eosinophils** | 0-500 cells/µL | Rising eosinophils + GI symptoms → possible eosinophilic GI process (esophagitis, gastritis). Threshold for tissue diagnosis: ≥15-30 eos/HPF depending on location |
| **Neutrophils** | 1.8-7.7 K/µL | Elevated with acute infection/inflammation. Low (neutropenia) can indicate medication effect or chronic stress |
| **Hemoglobin** | 14-18 g/dL (M), 12-16 (F) | Altitude increases hemoglobin as adaptation. "Normal" at sea level may be inadequate at altitude |
| **Hematocrit** | 40-54% (M), 36-48% (F) | Dehydration falsely elevates. Altitude increases baseline. |
| **MCV** | 80-100 fL | <80 = microcytic (iron deficiency until proven otherwise). >100 = macrocytic (B12 or folate deficiency) |
| **MCH** | 27-33 pg | Low MCH with low MCV = iron deficiency pattern |
| **RDW** | 11.5-14.5% | Elevated RDW = mixed red cell sizes; early sign of iron or B12 deficiency even when MCV is still normal |

**Altitude adjustment for hemoglobin/hematocrit:**

| Altitude | Hemoglobin Adjustment | Hematocrit Adjustment |
|----------|----------------------|----------------------|
| Sea level | Reference standard | Reference standard |
| 3,000-5,000 ft | +0.2-0.5 g/dL expected | +0.5-1.5% expected |
| 5,000-7,000 ft | +0.5-1.0 g/dL expected | +1.5-3.0% expected |
| 7,000-10,000 ft | +1.0-2.0 g/dL expected | +3.0-6.0% expected |

A hemoglobin of 15.5 at 6,000 ft altitude is equivalent to ~14.5-15.0 at sea level — still healthy but not as robust as the number suggests.

#### Cross-Reference with Wearables
- Elevated eosinophils + GI symptoms + suppressed HRV → possible eosinophilic GI process driving autonomic withdrawal
- Low hemoglobin or low ferritin + declining VO2max + elevated exercise HR → iron-limited oxygen delivery
- Rising RDW (early mixed-size red cells) + fatigue + normal hemoglobin → catch iron/B12 deficiency before it shows on standard markers

---

### 9D. Metabolic Panel

| Marker | Standard Range | Functional Optimal | Clinical Significance |
|--------|---------------|-------------------|----------------------|
| **Fasting Glucose** | 65-99 mg/dL | 75-90 mg/dL | >95 "normal" is still trending toward insulin resistance |
| **HbA1c** | <5.7% | <5.3% | 90-day glucose average. 5.4-5.6% warrants dietary attention even though "normal" |
| **Fasting Insulin** | 2-20 µIU/mL | 3-8 µIU/mL | The early warning. Insulin rises BEFORE glucose does. High insulin + normal glucose = early resistance |
| **HOMA-IR** | <2.0 ideal | <1.5 optimal | Fasting glucose × fasting insulin ÷ 405. >2.0 = insulin resistance likely. >2.5 = significant |
| **AST** | 10-40 U/L | — | Liver + muscle enzyme. Exercise elevates for 24-72 hr. Always interpret with context |
| **ALT** | 7-56 U/L | <30 optimal | More liver-specific than AST. Persistently >30 warrants liver investigation |
| **AST:ALT ratio** | — | — | AST > ALT after exercise = muscle origin. ALT > AST = more likely hepatic. Both elevated with no exercise = liver investigation |
| **eGFR** | >60 mL/min | >90 | Kidney function estimate. Creatinine-based; muscular individuals may have falsely low eGFR |
| **BUN/Creatinine** | BUN 7-20, Cr 0.7-1.3 | — | Elevated BUN with normal creatinine = dehydration or high protein intake. Both elevated = kidney concern |

**Exercise and liver enzymes:** A hard workout can elevate AST 2-3x for 24-72 hours. This is normal and not liver damage. Always draw ≥48 hours after intense exercise, or flag the timing to your doctor.

**HOMA-IR calculation:** (Fasting glucose in mg/dL × Fasting insulin in µIU/mL) ÷ 405

#### Cross-Reference with Wearables
- Rising fasting glucose + declining sleep quality + elevated RHR → metabolic and autonomic stress are interacting
- High HOMA-IR + weight gain + poor HRV → insulin resistance contributing to inflammatory load
- Elevated ALT with no recent exercise + fatigue + weight change → hepatic investigation warranted

---

### 9E. Hormones

| Marker | What to Test | Functional Notes |
|--------|-------------|-----------------|
| **Total Testosterone** | Age-adjusted range | Declines ~1-2%/year after 30. Morning draw (before 10am) essential — levels drop 25-50% by afternoon |
| **Free Testosterone** | By equilibrium dialysis preferred | More clinically relevant than total. SHBG fluctuations can make total misleading |
| **SHBG** | 10-57 nmol/L (M) | High SHBG = less free T available even if total looks fine. Elevated by: liver disease, hyperthyroidism, low caloric intake |
| **Cortisol (AM)** | 6-23 µg/dL (morning) | Best drawn 6-8 AM. High morning + poor PM suppression = HPA axis dysregulation. Very low morning = adrenal insufficiency |
| **TSH** | 0.4-4.5 mIU/L | Functional optimal: 1.0-2.5. >2.5 with symptoms warrants Free T3/T4. TSH alone misses central hypothyroidism and T4→T3 conversion issues |
| **Free T4** | 0.8-1.8 ng/dL | Must pair with TSH. Low-normal T4 + "normal" TSH + symptoms = worth investigating |
| **Free T3** | 2.3-4.2 pg/mL | The active hormone. Low T3 with normal T4 = conversion problem (common in chronic illness, caloric restriction, inflammation) |

**Critical thyroid note:** TSH alone is inadequate screening. Always request Free T4 and Free T3 if symptoms are present (fatigue, cold intolerance, weight gain, hair loss, constipation, brain fog). A "normal" TSH of 4.0 with a low Free T3 is not normal function.

**Testosterone and inflammation:** Chronic inflammation suppresses testosterone through multiple pathways (IL-6 suppression of GnRH, cortisol competition). Low T in the context of active inflammation will often resolve when the inflammation is treated — supplementation before resolving the root cause is premature.

#### Cross-Reference with Wearables
- Low free testosterone + poor sleep + declining HRV + elevated cortisol → HPA axis dysfunction / recovery system overwhelmed
- Low T3 with "normal" TSH + elevated RHR + fatigue + weight gain → thyroid conversion issue worth investigating
- Testosterone improving + HRV improving + RHR falling → systemic recovery, not just hormonal

---

### 9F. Lipids (Advanced)

Standard lipid panels (total cholesterol, LDL-C, HDL-C) are incomplete. Modern cardiovascular risk assessment requires particle-level data.

| Marker | What It Tells You | Target |
|--------|-------------------|--------|
| **LDL-P or ApoB** | Number of atherogenic particles (the actual risk driver) | ApoB <90 mg/dL (ideal <80) |
| **LDL-C** | Cholesterol mass carried by LDL particles | Less useful alone — particle count matters more |
| **HDL-C** | Cholesterol in HDL particles | >40 mg/dL (M), >50 (F). Higher is generally better |
| **Triglycerides** | Circulating fat | <100 mg/dL optimal. Fasting draw essential |
| **Triglyceride/HDL ratio** | Insulin resistance proxy | <2.0 optimal. >3.0 = likely insulin resistant [30] |
| **Lp(a)** | Genetically determined. Test ONCE — it doesn't change | >50 nmol/L (or >30 mg/dL) = elevated genetic risk. Discuss with cardiologist |
| **sdLDL** | Small dense LDL subfraction | More atherogenic than large buoyant LDL. Elevated with high TG/low HDL pattern |

**Why ApoB > LDL-C:** Each atherogenic particle carries one ApoB molecule. Two people with identical LDL-C can have very different particle counts — and the one with more particles has more risk, regardless of total cholesterol mass [31].

**Lp(a) — the most important test most people never get:** It's genetic, doesn't change with lifestyle, and confers significant cardiovascular risk when elevated. Test once. If high (>50 nmol/L), your cardiologist needs to know — it changes risk calculation and may warrant earlier or more aggressive intervention.

**Triglyceride/HDL ratio as insulin resistance proxy:** This is a cheap, widely available approximation of metabolic health. TG/HDL >3.0 correlates well with small dense LDL pattern and insulin resistance even when fasting glucose is "normal."

---

### 9G. Micronutrients

| Marker | Standard "Normal" | Functional Optimal | Why the Standard Range Is Misleading |
|--------|-------------------|-------------------|--------------------------------------|
| **Vitamin D (25-OH)** | 30-100 ng/mL | **40-60 ng/mL** | 30 is the floor for preventing rickets, not for optimal immune/muscle/mood function. Most benefit in 40-60 range [32] |
| **B12** | 200-900 pg/mL | **>500 pg/mL** | Functional deficiency occurs well within "normal" range, especially with PPI use. Methylmalonic acid (MMA) is a better functional marker |
| **Folate** | >3 ng/mL | >10 ng/mL | Low folate + low B12 + high MCV = macrocytic pattern |
| **Magnesium (serum)** | 1.7-2.2 mg/dL | >2.0 mg/dL | **Serum magnesium is a poor marker** — only 1% of body Mg is in serum. RBC magnesium is preferred but harder to get |
| **RBC Magnesium** | 4.2-6.8 mg/dL | >5.0 mg/dL | More accurate reflection of intracellular stores |
| **Omega-3 Index** | — | **>8%** | EPA+DHA as percentage of red blood cell membranes. <4% = high cardiac risk. 4-8% = intermediate. >8% = optimal [33] |

**Vitamin D and PPI interaction:** PPIs may reduce vitamin D absorption. Monitor levels annually if on long-term acid reduction.

**B12 and PPIs:** Acid reduction impairs B12 absorption from food (not from supplements). PPI users should check B12 annually and consider supplementation if <400 pg/mL, even if "in range."

**Magnesium — the invisible deficiency:** Serum magnesium stays normal until you're severely depleted because the body pulls from bones and soft tissue to maintain serum levels. Symptoms (muscle cramps, poor sleep, anxiety, HRV suppression) appear long before serum drops. If you take a PPI, supplement magnesium glycinate — it's the best-absorbed form in low-acid conditions and supports sleep.

#### Cross-Reference with Wearables
- Low vitamin D + poor sleep quality + mood changes → common deficiency cascade affecting sleep architecture
- Low B12 (or high MMA) + fatigue + elevated MCV → functional B12 deficiency, especially if on PPI
- Low omega-3 index + elevated hs-CRP + suppressed HRV → inflammatory environment partly modifiable with supplementation
- Low magnesium + poor sleep + HRV suppression + muscle cramps → magnesium deficiency affecting autonomic and sleep function

---

### 9H. Lab + Wearable Cross-Correlation Matrix

This is where the framework becomes uniquely powerful. No single data point tells the full story. Patterns across labs AND wearables reveal mechanisms.

| Pattern | Lab Signals | Wearable Signals | Likely Mechanism | Action |
|---------|------------|-----------------|-----------------|--------|
| **Iron-Limited Adaptation** | Ferritin <50, low iron sat, possibly normal Hgb | Declining VO2max, elevated exercise HR, stagnant walking HR improvement | Insufficient iron for erythropoiesis and mitochondrial function | Supplement aggressively. Recheck ferritin at 8-12 weeks. Consider IV iron if oral fails. |
| **Systemic Inflammation** | hs-CRP >1.0, elevated ESR, possibly elevated eosinophils | HRV suppressed >10%, RHR elevated >3 bpm, walking HR elevated, poor deep sleep | Inflammatory cytokines → vagal withdrawal → sympathetic dominance [7][8][9] | Identify source. Anti-inflammatory diet. Reduce training load. Medical workup if >2 weeks. |
| **HPA Axis / Recovery Dysfunction** | Low free testosterone, elevated AM cortisol (or blunted), poor cortisol diurnal curve | Poor sleep, declining HRV, elevated RHR, reduced exercise tolerance, weight gain | Chronic stress or illness overwhelming the hypothalamic-pituitary-adrenal axis | Prioritize sleep. Reduce training volume 30-50%. Stress management. Recheck in 6-8 weeks. |
| **Eosinophilic / Allergic GI Process** | Rising eosinophils (even within "range"), elevated hs-CRP, possibly elevated IgE | HRV suppression, GI symptoms, sleep fragmentation, elevated RR | Eosinophilic infiltration → mucosal inflammation → vagal activation → autonomic disruption | GI referral. Possible endoscopy with tissue eosinophil counts. Elimination diet trial. |
| **Metabolic / Insulin Resistance** | High fasting insulin, elevated HOMA-IR, high TG/HDL ratio, elevated ALT | Weight trending up, HRV declining, RHR rising, sleep quality declining | Insulin resistance → chronic inflammation → autonomic impairment | Dietary intervention (reduce refined carbs). Exercise (even walking). Recheck metabolic markers at 12 weeks. |
| **Thyroid Conversion Issue** | "Normal" TSH but low Free T3, possibly normal Free T4 | Elevated RHR, fatigue despite adequate sleep, weight gain, declining exercise capacity | Inadequate T4→T3 conversion (common in chronic illness, caloric restriction) | Full thyroid panel. Address underlying inflammation. Adequate caloric intake. Selenium supplementation may help conversion. |
| **Vitamin D + Sleep Cascade** | Low vitamin D (<30), possibly low magnesium | Poor sleep quality, mood/energy decline, possible HRV suppression | Vitamin D receptors in brain affect serotonin/melatonin. Magnesium cofactor for D metabolism | Supplement D3 (with K2). Recheck at 8-12 weeks. Target 40-60 ng/mL. |
| **Positive Recovery Trajectory** | Ferritin rising, hs-CRP falling, testosterone improving | HRV trending up, RHR falling, walking HR improving, sleep normalizing | Systemic inflammation resolving, iron stores replenishing, autonomic tone recovering | Continue protocol. Progress training gradually. Recheck labs at 12-16 weeks to confirm. |

---

### 9I. Lab Testing Strategy

#### Recommended Panels by Goal

**Baseline Health Assessment (everyone):**
- CBC with differential
- CMP (comprehensive metabolic panel)
- Iron panel + ferritin
- hs-CRP
- Lipid panel (include ApoB if available)
- TSH + Free T4
- Vitamin D (25-OH)
- HbA1c

**Performance / Active Individuals (add):**
- Free T3
- Free + total testosterone (morning draw)
- Fasting insulin (to calculate HOMA-IR)
- Omega-3 index
- RBC magnesium (if available)
- Lp(a) (once — it's genetic)

**Chronic Illness / Ongoing Symptoms (add):**
- ESR + fibrinogen
- B12 + methylmalonic acid (MMA)
- Cortisol (AM, fasting)
- Full thyroid panel (TSH, Free T4, Free T3, TPO antibodies)

#### Testing Frequency
- **Every 3-4 months:** Iron panel, hs-CRP, CBC (if actively tracking an intervention)
- **Every 6-12 months:** Full panel for established baselines
- **Once:** Lp(a), ApoB baseline
- **As needed:** Repeat anything trending poorly; add markers to investigate specific symptoms

#### Pre-Lab Protocol (for accurate results)
- Fast 12 hours (water OK)
- No intense exercise for 48 hours before draw
- Morning draw before 10 AM (essential for testosterone and cortisol)
- Note any supplements taken (iron, biotin, etc. — biotin interferes with many immunoassays)
- Hydrate normally — dehydration falsely elevates hematocrit and some metabolic markers

---

## Output Format

When interpreting data, produce:

```
STATUS: [Green/Yellow/Orange/Red] — Readiness: [X]/100
TOP DRIVERS: [Top 3 metrics driving the score]
PATTERN: [inflammatory / sleep-breathing / load spike / iron-limited / positive adaptation / pre-symptomatic / mixed / none detected]
TRAINING TODAY: [full / modified / recovery / rest] — [specific suggestion]
MEDICAL FLAGS: [none / monitor / test soon / seek care] — [details if any]
TREND READOUT:
  7-day: [summary]
  14-day: [summary]
  28-day: [summary]
THRESHOLDS CROSSED: [list any exceeded thresholds]
```

---

## Citation Key

All bracketed numbers (e.g., [7]) reference entries in `references/evidence-base.md`.
Every recommendation in this skill traces back to published research with quality ratings.

---

*Built from real experience interpreting health data through chronic illness, recovery,
and performance training. The methodology is what matters — fill it with your own data
and it becomes yours.*
